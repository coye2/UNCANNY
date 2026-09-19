# How UNCANNY actually works

If somebody wants to know what UNCANNY is doing under the hood without me dumping the entire source tree, this is the page.

I am **not** open-sourcing the private repo just because people want to inspect it. That would expose the full layout, build graph, internal provider work, shader set, tooling and a bunch of stuff that has nothing to do with proving the engine is real.

What I *can* show is the important part:

- how the runtime is split up
- what happens from launch to Present
- how ELYSIUM actually changes a frame
- how the neural route is allowed or denied
- how motion/depth evidence is used
- how REVENANT decides whether an asset is safe to replace
- how the Control Deck talks to the runtime
- how failure paths are handled
- real source chunks from the current code

The source below is from the current HF18.11 lineage. It is not mock code written for the README.

I intentionally removed repo paths and unrelated surrounding code. You can see how the systems work without getting a map of the private source tree.

---

## First: what UNCANNY actually is

UNCANNY is not one shader.

It is a bunch of separate systems that have to agree with each other:

**Launcher / installer**  
Finds games, stores per-game state, installs the runtime, updates it, removes it, rolls it back and keeps diagnostics.

**Verified sidecar launcher**  
Starts the original game/emulator executable without replacing that executable with an UNCANNY wrapper.

**Native runtime**  
Attaches to the actual graphics route, watches device/swapchain state, owns the live runtime state and decides what is safe to run on the current frame.

**ELYSIUM**  
The real-time remastering engine. This is the part doing the normal live image reconstruction even when the optional neural route is unavailable.

**Neural / Feature-18 route**  
Optional. It only gets to run when the route, provider and runtime state say it is actually safe and available.

**Control Deck**  
The UI. It edits live runtime state, reads status back from the runtime and stays separate enough that the graphics runtime does not have to die if the UI has a problem.

**REVENANT**  
The experimental persistent asset-reconstruction side. It has its own validation and replacement rules because writing an asset to disk is a completely different risk than changing one live frame.

That separation is important.

A game can be running ELYSIUM correctly with no neural provider.  
REVENANT can be disabled while the live runtime works normally.  
The Control Deck can fail and the game should still be able to run.

---

## The basic frame path

This is the simplified version:

```text
Game / Emulator
      |
      v
UNCANNY verified launch
      |
      v
Native graphics runtime
      |
      v
Detect/own active graphics route
      |
      v
Startup + transition safety
      |
      v
ELYSIUM current-frame work
      |
      +----------------------+
      |                      |
      v                      v
Neural eligible?            No
      |                      |
     Yes                     |
      |                      |
      v                      |
Neural warm/evaluate         |
      |                      |
      +----------+-----------+
                 |
                 v
           Native Present
```

REVENANT is off to the side of this. It is not sitting in the middle of every live Present.

---

# Where the Magic Happens

This is the part people usually mean when they say "show source."

So here are real chunks that actually matter.

Not random boilerplate. Not a settings parser. Not 500 lines of launcher UI.

Actual runtime decisions.

---

## 1. D3D11 has to prove it is stable before neural promotion

One of the biggest recent changes was getting rid of the dumb choice between:

- keep neural disabled forever for safety
- or turn the whole advanced path back on and risk another hard lock

The current D3D11 path makes the route prove itself first.

Real source:

```cpp
static bool direct_d3d11_neural_promotion_ready(IDXGISwapChain* sc){
    if(!sc || !g_state || !g_state->present_advancing)
        return false;

    auto route = g_swapRoutes.find(sc);
    if(route == g_swapRoutes.end() || route->second.api != 11)
        return false;

    constexpr unsigned d3d11NeuralPromotionFrames = 240u;

    if(route->second.d3d11PostfxFrames < d3d11NeuralPromotionFrames ||
       !route->second.transitionMs)
        return false;

    const ULONGLONG now = GetTickCount64();

    if(now < route->second.transitionMs ||
       now - route->second.transitionMs < 9000)
        return false;

    return g_state->last_present_ms &&
           now >= g_state->last_present_ms &&
           now - g_state->last_present_ms < 1000;
}
```

What that actually means:

- native Present has to be moving
- the active route has to really be D3D11
- ELYSIUM has to survive **240 current-frame frames**
- the route has to stay stable for at least **9 seconds after transition**
- there has to be a recent successful Present

If the swapchain goes through a resize/fullscreen/ownership transition, that progress gets reset and the route has to settle again.

I would rather make the advanced path wait a few seconds than hard-lock the entire game.

Also notice what is *not* there: no Fallout4.exe check, no Stray.exe check, no title-specific "if this game then do this" garbage.

The route proves whether it is healthy.

---

## 2. Present is fail-open

This is probably one of the most important rules in the runtime.

If UNCANNY's maintenance/provider thread is busy, the game's Present should not sit there waiting forever for UNCANNY.

Real source:

```cpp
std::unique_lock<std::mutex> lock(
    g_fx11Mutex,
    std::try_to_lock
);

if(!lock.owns_lock()){
    ++g_state->frames_bypassed;

    g_state->postfx_active = 0;
    g_state->dlss5_active = 0;

    g_state->flags &=
        ~(UNCY_FLAG_POSTFX_ACTIVE |
          UNCY_FLAG_DLSS5_ACTIVE);

    fx_status(
        L"D3D11 maintenance busy; native Present preserved"
    );

    return false;
}
```

That `try_to_lock` is very intentional.

If another UNCANNY thread owns the reconstruction state, this frame gets skipped.

The game does **not** wait for us.

That is the kind of thing that matters way more than saying "supports D3D11" in a feature list.

Missing one enhanced frame is fine.

Freezing the user's PC because my graphics mod wanted a mutex is not.

The same thinking is why neural/provider warmup is kept away from the critical Present path.

---

## 3. ELYSIUM is not just a sharpen pass

A lot of graphics mods boil down to "sample around the pixel, add contrast, sharpen it."

ELYSIUM does use spatial evidence, obviously, but stronger parts of the stack are gated by whether the current frame actually supports what they are trying to do.

Here is a real trimmed section from Adaptive Realism:

```hlsl
float arStable =
    lerp(.48, 1.0, arFlowConf) *
    (1.0 - arDisocclusion * .86);

float arAo =
    arContact *
    lerp(.085, .36, arQ) *
    arTierScale *
    arPerf *
    arStable;

arAo *=
    lerp(.55, 1.0, saturate(arDepthSpread * 52.0)) *
    lerp(1.0, .55, warmMidCue * saturate(skinProtect));

p *= 1.0 - saturate(arAo);

float3 arDiffuse =
    clamp(arBounce - oc, -.12, .18);

float arDiffuseGate =
    saturate(.35 + directionalSupport * .65) *
    (1.0 - noiseRisk) *
    sourceAgreement;

p += arDiffuse *
     arDiffuseGate *
     lerp(.060, .30, arQ) *
     arTierScale *
     arPerf *
     arStable;
```

This is the kind of logic that makes Adaptive Realism different from blindly throwing AO/clarity on the frame.

The result is being scaled by stuff like:

- motion/flow confidence
- disocclusion
- depth spread
- skin protection
- noise risk
- source agreement
- quality level
- performance budget

So when evidence gets worse, the effect gets weaker.

That is the correct behavior.

If the engine cannot prove the information is trustworthy, it should not pretend it knows more than it does.

---

## 4. ELYSIUM's job is to spend strength where the frame supports it

The current image stack has separate controls/stages for things like:

- structural detail
- surface detail
- face reconstruction
- material definition
- depth/form
- color recovery
- color separation
- edge recovery
- distant detail
- texture relief
- local contrast
- denoise
- anti-halo
- skin protection
- line-art / flat-color protection
- motion rejection
- temporal history

Those are not all equal on every route.

If reliable native depth exists, depth-dependent work can do more.

If it does not exist, UNCANNY is supposed to fall back instead of lying and pretending full depth-aware reconstruction is active.

Same with motion.

Same with neural.

This is also why D3D9/D3D10/translated routes can work without having feature parity with the strongest D3D11/D3D12 path.

"Compatible" and "full capability" are not the same thing.

---

## 5. Motion Guard / Ghosting Guard are there because still screenshots are easy

A graphics effect can look incredible in a screenshot and then look awful once the camera moves.

That is one of the main things I care about with UNCANNY.

The later stages of the pipeline are supposed to lose authority when:

- flow confidence drops
- source/history disagree
- disocclusion is detected
- depth confidence gets bad
- the object edge does not line up with history

That is why X2.5 exists as a separate pass behavior instead of just being "almost 3."

X2.5 is meant to be the clean-motion option.

I would rather lose a little still-frame detail than have a character leave a trail behind their head.

---

## 6. REVENANT will keep the old result if the new one is worse

Persistent asset work needs a completely different attitude than live image work.

If ELYSIUM has one weird frame, the next frame can recover.

If REVENANT writes a bad replacement and keeps swapping it around, now you have flicker, broken assets and a mess on disk.

So an accepted replacement keeps ownership until a new one clears the gate.

Real source:

```cpp
struct ReplacementDecision {
    bool replace = false;
    const char* reason = "keep original";
};

inline ReplacementDecision ChooseReplacement(
    bool hasAccepted,
    double acceptedConfidence,
    double candidateConfidence,
    double temporalAgreement,
    const AssetQuality& q)
{
    if(!q.accepted)
        return {false, q.reason};

    acceptedConfidence =
        std::clamp(acceptedConfidence, 0.0, 1.0);

    candidateConfidence =
        std::clamp(candidateConfidence, 0.0, 1.0);

    temporalAgreement =
        std::clamp(temporalAgreement, 0.0, 1.0);

    if(!hasAccepted)
        return {true, "first quality-gated candidate"};

    if(candidateConfidence + 0.07 < acceptedConfidence &&
       temporalAgreement < 0.92)
        return {
            false,
            "accepted reconstruction retained: candidate confidence regressed"
        };

    if(temporalAgreement < 0.45 &&
       candidateConfidence < 0.84)
        return {
            false,
            "accepted reconstruction retained: temporal identity unstable"
        };

    return {
        true,
        "candidate cleared replacement hysteresis"
    };
}
```

That little bit of hysteresis is important.

Without it, the newest candidate wins just because it is new.

That is not reconstruction. That is churn.

---

## 7. REVENANT also validates before replacement

Before a candidate even gets to that replacement decision, the asset path already has validation around source identity, residual error and unstable/noisy patterns.

The general flow is:

```text
observe source
    |
wait until source is stable
    |
take isolated reconstruction input
    |
build candidate
    |
decode / verify output
    |
source identity + residual checks
    |
noise / instability rejection
    |
compare against accepted version
    |
replacement hysteresis
    |
publish owned replacement
```

If a candidate fails, the safe result is normally:

**keep the known-good asset**

not:

**the model returned something so I guess ship it**

REVENANT is still experimental, but this is the direction the system is built around.

---

## 8. The Control Deck is not allowed to become a boot dependency

I do not want the entire graphics runtime depending on whether the UI process started perfectly.

So the Deck is lazy-started.

Real source:

```cpp
deck_surface_create();

trace_log(
    L"DECK_LAZY_START_ARMED",
    S_OK,
    L"Control Deck process starts on HOME only"
);

HANDLE maintenance = CreateThread(
    nullptr,
    0,
    MaintenanceThread,
    nullptr,
    0,
    nullptr
);
```

The runtime starts.

The game starts.

The Deck process does **not** have to launch just to make UNCANNY exist.

When HOME is pressed, the runtime requests the Deck.

If the in-frame version cannot establish a healthy handshake in its bounded grace period, UNCANNY can fall back to a normal desktop Deck instead of leaving the UI invisible forever.

That separation has fixed a bunch of stupid "runtime is fine but UI killed the experience" problems.

---

## 9. The Deck is editing live runtime state, not a fake mirror

The Control Deck is not supposed to be a pretty settings app that writes values somewhere and hopes the runtime notices.

The runtime and Deck use versioned shared state.

The runtime reads a settings snapshot for the current frame.

If the state is being updated in the middle of the read, that frame can be bypassed instead of applying half-old / half-new values.

That is also why control ABI matters.

If the UI and runtime disagree about what a field means, that is a build mismatch, not something to "just make work."

The master UNCANNY switch is a real runtime bypass.

The compare toggle is a real runtime bypass/reset path.

UNCANNY pass depth and neural pass depth are separate because they control different parts of the engine.

---

## 10. Launching the game without replacing its EXE

Older UNCANNY builds used more invasive launch behavior.

The current model uses a verified sidecar.

The selected game/emulator EXE stays where it is, with its real name and real bytes.

UNCANNY stores launch/install state around it.

The important bits are:

- selected target stays untouched
- launch record binds the expected target
- target hash is checked
- UNCANNY launcher hash/state is checked
- changed state can be marked stale
- old wrapper-style installs can be migrated/recovered
- argv / working-directory behavior is preserved for the real target

That is a much cleaner ownership model.

It also means Remove can focus on UNCANNY-owned files instead of pretending it owns the game's executable.

---

## 11. Why transitions matter so much

Fullscreen changes, resize, swapchain recreation, color-space changes and device ownership changes are not cosmetic events.

They can invalidate:

- backbuffer references
- depth references
- shared resources
- history
- provider resources
- route ownership assumptions

So UNCANNY treats transitions as an actual runtime state.

Advanced promotion gets revoked.

History can get cleared.

The route stabilizes again.

Then features can come back.

Trying to keep every advanced resource alive across every transition is how you get random black screens and "works until I alt-tab" bugs.

---

## 12. D3D11 and D3D12 do not get the exact same rules

The goal is universal compatibility.

That does **not** mean pretending every graphics API has the same synchronization model.

D3D11 currently has a conservative current-frame safety floor and staged neural promotion.

D3D12 has its own startup/resize behavior and bounded resource-retirement rules.

PCSX2 is currently intentionally kept on its Direct3D 12 renderer route.

Older APIs use their own reduced paths where needed.

The abstraction is at the policy level:

> keep the native application authoritative, prove ownership/state before advanced work, and fail open when UNCANNY cannot safely proceed.

The implementation under that policy is API-specific because it has to be.

---

## 13. What happens when UNCANNY cannot safely do something

This is probably the easiest way to understand the engine philosophy.

**Runtime state lock busy**  
Keep the native frame.

**Settings snapshot changing**  
Bypass that update/frame.

**Provider missing**  
ELYSIUM can still run.

**Provider busy/broken**  
Keep the current source/ELYSIUM result.

**Native Present stops advancing**  
Do not promote advanced work.

**Device removed**  
Release route resources.

**Resize / fullscreen / ownership transition**  
Revoke advanced state and stabilize again.

**Depth confidence bad**  
Reduce depth-dependent work.

**Motion confidence bad**  
Reduce/reject temporal work.

**REVENANT candidate fails validation**  
Keep the current accepted version/original.

**Control Deck in-frame path fails**  
Use the desktop fallback.

**Install identity changed**  
Mark it stale and repair/update it.

That is a lot less exciting than saying "AI remastering engine" but this is the stuff that decides whether the project is actually usable.

---

## 14. Why there are 1 / 1.5 / 2 / 2.5 / 3 pass modes

These are ELYSIUM reconstruction-depth modes.

They are not just:

```text
run same shader
run same shader again
run same shader again
```

Higher modes allow more of the later reconstruction/detail stack to contribute and can raise the search/detail budget.

X2.5 is intentionally its own thing because it keeps the motion side more conservative.

So the intended tradeoff is roughly:

**1 / 1.5**  
lighter, safer, cheaper

**2**  
normal strong path

**2.5**  
strong reconstruction with the cleanest motion bias

**3**  
maximum bounded reconstruction/detail budget

The exact result still depends on route capability and scene evidence.

A higher pass mode is not permission to ignore guards.

---

## 15. Adaptive Realism is supposed to react to the scene, not recolor every game the same way

The point of Adaptive Realism is not "apply my favorite contrast preset to every game."

The current stack is built around things like:

- source recovery
- form/material separation
- contact response
- bounded indirect-light-like response where evidence exists
- local contrast
- black-floor / veil handling
- filmic highlight control
- source-hue protection
- edge/detail recovery
- motion rejection

The stronger levels mainly increase how hard those supported stages are allowed to work.

The engine should not turn every game teal/orange, crush the blacks and call it realism.

---

## 16. What I intentionally am not publishing here

This page is transparency, not a source release.

I am intentionally **not** publishing:

- the private source tree
- full file layout
- build scripts and dependency graph
- complete native runtime translation units
- complete shader source
- generated/protected shader resources
- provider integration internals
- private packaging/release machinery
- every symbol/function around the excerpts
- internal recovery/audit tooling
- anything that turns this page into a reconstruction guide for the private repo

That is the line.

People can inspect meaningful implementation and understand the design without me handing over the entire project.

---

## 17. What the current build has actually been validated for

Current public release at the time this page was written:

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.11**

The exact release candidate went through:

- static/regression checks
- x86/x64 production builds
- Windows HLSL compilation
- D3D11 WARP visual-quality validation
- packaged install/update/rollback tests
- scanner/sidecar tests
- PCSX2 sidecar smoke
- normal launcher startup
- AllSigned launcher startup
- ZIP integrity checks
- Microsoft Defender scanning

That does **not** mean every game/GPU/provider combination is certified.

Real-game GPU behavior still needs real hardware testing.

I try to keep that line pretty clear because "CI passed" and "this exact game is proven perfect on your PC" are not the same statement.

---

## 18. Source / license reality

UNCANNY is currently closed-source.

That does not mean the executable is magic or impossible to inspect. Anything that runs on a user's PC can be analyzed to some degree.

It means I am not publishing the complete editable source and internal project structure.

The public repo is for releases, usage, compatibility, documentation, hashes, security notes, changelogs and selected implementation transparency like this page.

That is the current model.

---

## 19. The actual engineering goal

The goal is not to win a screenshot contest.

It is:

> make the game look noticeably better, keep motion clean, keep the original game in control, and fail safely when UNCANNY does not have enough evidence or enough ownership to do something correctly.

That is why so much work goes into routing, state, synchronization, fallback behavior and validation.

The flashy part is the image.

The part that makes it a real engine is everything around it.

---

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.
