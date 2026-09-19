# how UNCANNY works

people keep asking me to show source, so this is the middle ground.

i'm not dumping the private repo. that would expose the whole project layout, build system, full shaders, provider work, release tooling, etc. i don't think i need to publish all of that just to prove the engine isn't smoke and mirrors.

what i *am* doing here is showing the parts that actually matter: how a frame gets handled, how ELYSIUM decides what it can safely do, how the neural path gets promoted, what happens when something isn't healthy, how REVENANT decides whether to keep or replace an asset, and some real code from the current HF18.11 line.

the snippets are real. i removed file paths and unrelated surrounding code on purpose. i'm showing implementation, not handing out a source-tree map.

## quick version

UNCANNY isn't one giant shader and it isn't just ReShade with a launcher around it.

the current stack is roughly:

```text
launcher / install state
        |
verified sidecar launch
        |
native runtime
        |
active API / swapchain route
        |
startup + transition guards
        |
ELYSIUM current-frame reconstruction
        |
optional neural route if the route is actually healthy
        |
native Present
```

Control Deck sits next to the runtime and edits live shared state.

REVENANT is its own thing. it handles persistent asset reconstruction and doesn't sit in the middle of every Present.

that split matters because i don't want one broken subsystem taking down everything else. ELYSIUM can work without neural. the runtime can work without the Deck being open. REVENANT can be off completely and the live renderer still works.

# where the magic happens

this is the useful part.

### D3D11 doesn't get neural just because the toggle is on

HF18.9 fixed the hard-lock class by giving direct D3D11 a safe current-frame path. the problem was that the safety floor also effectively kept neural dead forever.

HF18.11 changed that. now the route has to prove it's stable first.

real code:

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

so, before direct D3D11 neural can even be considered:

- Present has to actually be advancing
- the route has to really be D3D11
- ELYSIUM needs 240 successful current-frame frames
- the route needs 9 seconds of clean post-transition time
- the last Present has to be recent

resize/fullscreen/ownership changes reset that progress.

there's also no `Fallout4.exe` or `Stray.exe` special-case in there. i stopped wanting title-name hacks for this stuff. if the route is healthy, it earns promotion. if it isn't, it doesn't.

### Present is allowed to skip UNCANNY

this one matters more than half the feature list.

if maintenance/provider setup has the D3D11 state locked, Present does **not** wait for it.

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

    fx_status(L"D3D11 maintenance busy; native Present preserved");
    return false;
}
```

that's intentional.

one unprocessed frame is way better than blocking the game because UNCANNY wanted to finish some background setup.

same reason neural/provider initialization gets pushed off the critical Present path where possible.

### what ELYSIUM is actually looking at

ELYSIUM isn't just "sharpen more when slider goes up."

the stronger stages are gated by evidence from the frame. motion confidence, disocclusion, depth spread, source agreement, noise risk, skin protection, perf budget, etc.

trimmed Adaptive Realism chunk:

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

float3 arDiffuse = clamp(arBounce - oc, -.12, .18);

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

the important part isn't the constants. it's the gates.

if motion gets sketchy, `arStable` drops.

if the source doesn't agree with the reconstruction, `sourceAgreement` cuts it.

if the area looks noisy, the contribution gets pulled back.

if skin protection is high, the contact term gets restrained.

if there isn't trustworthy depth on that route, depth-dependent stuff shouldn't pretend otherwise.

that's how i want the engine to behave. stronger when it has evidence, quieter when it doesn't.

### motion guard / ghosting guard

still screenshots are easy. motion is where bad reconstruction gets exposed instantly.

the later stack gets reduced when flow confidence drops, history disagrees with the current source, disocclusion shows up, or edges stop lining up.

that's also why 2.5 exists separately from 3.

2.5 isn't "almost 3." it's the mode i bias hardest toward clean motion. i'd rather give up a little still-frame detail than leave a trail behind somebody's face or a car.

### pass modes

1 / 1.5 / 2 / 2.5 / 3 are ELYSIUM pass-depth modes, not the DLSS/neural pass count.

higher modes let more of the later reconstruction/detail stack contribute and can spend more budget. they are not literally "run the exact same shader three times."

roughly:

- 1 / 1.5 = lighter
- 2 = normal strong path
- 2.5 = strong path with the clean-motion bias
- 3 = max bounded ELYSIUM depth/detail budget

route capability still wins over the number. 3-pass does not get permission to fake depth or ignore motion guards.

### REVENANT doesn't replace something just because a newer candidate exists

persistent assets need way stricter behavior than live frames.

if ELYSIUM has a bad frame, the next frame can recover. if REVENANT keeps replacing a good asset with worse candidates, now you get flicker and garbage sitting on disk.

this is part of the replacement decision:

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

before that point, the candidate already has to survive source/identity/residual/noise checks.

so the basic idea is:

```text
source shows up
-> wait until it stops changing
-> isolate input
-> reconstruct
-> decode/verify
-> quality checks
-> compare against accepted result
-> only replace if it actually clears the gate
```

newer does not automatically mean better.

### Control Deck is not part of boot

this was another thing i changed because UI failures should not be able to kill a working renderer.

the Deck is lazy-started.

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

runtime comes up first. Deck starts when HOME is requested.

if the in-frame Deck can't establish a healthy handshake, the runtime can fall back to the desktop version instead of leaving the user with a dead hotkey and no clue what happened.

the Deck is editing live versioned runtime state. it isn't just a UI that writes an ini and hopes the renderer notices later.

### launch/install side

the current launch model is sidecar based.

UNCANNY does not need to rename/replace the selected game exe just to launch it.

the install record tracks the selected target and UNCANNY's own launcher/runtime state. target/launcher hashes are used to tell whether an install is still the install we think it is.

if the state doesn't match anymore, it can be marked stale and repaired instead of blindly trusting old files.

old wrapper-style installs can also be recovered/migrated instead of stacking another install on top of a broken one.

that ownership model is also why uninstall/rollback tries to only remove or restore things UNCANNY can prove it owns.

## API stuff

"universal" doesn't mean i'm pretending D3D9, D3D11 and D3D12 are the same API.

the policy is shared. the implementation isn't.

D3D11 has its current-frame floor and staged neural promotion.

D3D12 has different startup/resize/resource-retirement rules.

PCSX2 is intentionally on its D3D12 `Renderer=15` route right now.

older or translated APIs can fall back to reduced capability when they don't expose the same reliable scene data.

that's the difference between *works on the route* and *full feature parity*.

## what happens when something goes wrong

this is basically the rule set i keep coming back to:

```text
UNCANNY lock busy        -> keep native frame
settings mid-update      -> bypass that frame
provider missing         -> ELYSIUM can still run
provider busy/broken     -> keep current source/result
Present stops advancing  -> no advanced promotion
device removed           -> release route resources
resize/fullscreen        -> reset/re-stabilize route
bad depth confidence     -> reduce depth work
bad motion confidence    -> reduce temporal work
bad REVENANT candidate   -> keep accepted/original asset
Deck handshake fails     -> desktop Deck fallback
install identity changed -> mark stale / repair
```

i don't want the engine trying to "win" every frame.

if UNCANNY isn't sure it owns something safely, or the evidence is bad, the right answer is usually to back off.

## Adaptive Realism

Adaptive Realism is supposed to react to the frame, not slap the same grade on every game.

the current stack is doing source cleanup, form/material separation, contact response, bounded indirect-light-like work where the route actually supports it, local contrast, black-floor/veil handling, highlight shaping, color protection and detail recovery.

higher levels mostly let those supported stages work harder.

they are not supposed to mean "more saturation + more sharpen."

## what i'm not posting

i'm still not publishing:

- the full private source tree
- full shader source
- complete runtime translation units
- build/dependency graph
- provider integration internals
- release/package tooling
- generated protected resources
- every surrounding symbol/function needed to reconstruct the repo

that's intentional.

this page is here so people can see real implementation and understand how the engine is put together without me turning the public repo into a source release.

## current proof

this page is based on the HF18.11 line.

the public candidate went through the normal release gate: x86/x64 production builds, HLSL compile, static regressions, D3D11 WARP validation, install/update/rollback tests, scanner/sidecar tests, PCSX2 sidecar smoke, launcher startup checks, ZIP integrity and Defender scanning.

that's build/release proof. it is not me claiming every game/GPU/provider combo is hardware-certified.

real-game acceptance still matters.

that's pretty much the whole idea behind UNCANNY right now: push the image hard when the route gives me good information, and get out of the game's way when it doesn't.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.
