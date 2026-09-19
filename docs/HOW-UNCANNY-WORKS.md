# how UNCANNY works

people keep asking me to show source. i get why. UNCANNY is closed source and if i was looking at a project like this from the outside i'd want to know what is actually happening too.

i'm still not dumping the repo.

what i can do is show real parts of the current code and explain what they do without giving out the whole tree, build system, full shader source, provider work and everything around it.

this is from the current HF18.11 line.

# the basic setup

UNCANNY is split up pretty heavily.

the launcher handles installs, updates, rollback, game detection and saved state.

the sidecar launcher starts the real game exe. it doesn't replace the game exe with an UNCANNY wrapper.

the runtime is the part inside the graphics path. it tracks the active API, swapchain state, Present state, transitions and what parts of the engine are safe to use.

ELYSIUM is the live image engine.

the neural path is optional. ELYSIUM does not depend on it.

Control Deck talks to the live runtime state.

REVENANT handles persistent asset reconstruction and has its own validation before it writes anything.

roughly this:

```text
game
 |
UNCANNY launch
 |
native runtime
 |
active graphics route
 |
stability checks
 |
ELYSIUM
 |
neural path if it is actually ready
 |
Present
```

REVENANT runs beside that. not inside every frame.

# where the magic happens

this is the stuff people actually want to see.

## D3D11 neural promotion

direct D3D11 starts safe first.

after the hard lock problems i did not want neural just turning on because the user clicked a toggle. the route has to prove it is healthy first.

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

that means D3D11 neural does nothing until Present is moving, the route is confirmed as D3D11, ELYSIUM has made it through 240 frames, 9 seconds have passed after the last transition and Present is still recent.

if the game resizes, changes fullscreen state or ownership changes, it has to settle again.

there are no Fallout 4 or Stray exe checks in this logic. i wanted the route itself to decide this. not the name of the game.

## Present does not wait on UNCANNY

this is a big one.

if maintenance is busy with the D3D11 state i do not want Present sitting there blocked.

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

if that lock is busy the frame just keeps going without the extra work.

that's why it uses `try_to_lock`.

dropping UNCANNY for one frame is fine. making the game wait on my maintenance thread is not.

this is also why provider and neural setup are kept off Present when possible.

## what ELYSIUM is actually doing

ELYSIUM is not just one sharpen value getting pushed harder.

a lot of the stronger work gets scaled by what the frame is telling the engine.

this is from Adaptive Realism:

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

the important part is not the numbers.

`arFlowConf` is motion confidence.

`arDisocclusion` catches areas where history stops being trustworthy.

`arDepthSpread` helps decide how much depth response makes sense.

`skinProtect` pulls it back on skin.

`noiseRisk` pulls it back when the source looks unstable.

`sourceAgreement` makes the effect lose strength when the current source does not support it.

so yeah, higher settings make it stronger. but the guards still get the final say.

if the route does not have trustworthy depth, UNCANNY should not act like it does.

same thing with motion. same thing with neural.

## motion and ghosting

this is probably the area i care about the most.

a still screenshot can look insane while the game looks awful as soon as you move.

Motion Guard and Ghosting Guard reduce later reconstruction when flow confidence drops, history stops matching the current frame, disocclusion shows up or edges stop agreeing.

2.5 exists for this reason.

it is not just 3 with a smaller number.

2.5 is biased harder toward clean motion. i would rather lose some tiny still detail than have a face, weapon or car leave a trail behind it.

## ELYSIUM passes

the 1, 1.5, 2, 2.5 and 3 settings are ELYSIUM depth settings.

they are not the neural pass setting and they are not just the exact same shader being called three times.

higher modes allow more of the later reconstruction stack to contribute and give it more room to work.

1 and 1.5 are lighter.

2 is the normal strong path.

2.5 is the clean motion path.

3 is the hardest ELYSIUM can push the current stack.

the route still decides what is actually available. choosing 3 does not suddenly give a game good depth or good motion data.

## REVENANT

REVENANT is way more strict about replacing something because its output can persist.

if ELYSIUM has one bad frame, whatever. next frame is new.

if REVENANT writes a worse asset and keeps swapping between versions, now you have a real problem.

this is part of the current replacement logic:

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

before it even gets here the candidate already went through source identity and quality checks.

the simple version is this:

```text
see source
wait for stable source
reconstruct
verify output
check quality
compare to accepted version
replace only if it clears the gate
```

newer does not automatically win.

## Control Deck

Control Deck is not required for the runtime to boot.

that used to be way too coupled.

current code arms it and waits for HOME:

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

the runtime starts first.

when HOME is pressed it starts the Deck and tries the in frame path.

if that handshake fails it can fall back to the desktop Deck.

the Deck is editing live versioned runtime state. it is not just changing an ini and hoping the renderer catches up later.

## launch system

the current launcher uses a sidecar setup.

the selected game exe stays the selected game exe.

UNCANNY keeps its own launch record and checks the target and launcher state before using it.

if the install does not match what UNCANNY expects anymore, it can be marked stale and repaired.

older wrapper installs can be migrated too.

this also makes rollback and remove cleaner because UNCANNY has a better idea of what it actually owns.

## APIs

D3D11 and D3D12 do not use the exact same path because that would be stupid.

they have different sync and resource rules.

the common part is the policy.

keep the game authoritative. prove the route is healthy. do advanced work only when the state supports it. back off when it does not.

D3D11 has the current frame safety floor and staged neural promotion.

D3D12 has its own startup, resize and resource retirement logic.

PCSX2 is currently kept on D3D12 with `Renderer=15`.

older APIs can still work but they do not magically get the same scene data as the best route.

## when something goes wrong

this is basically how the engine reacts rn:

```text
state lock busy           keep native frame
settings changing         skip that frame
provider missing          keep ELYSIUM
provider fails            keep current result
Present stops             no promotion
device removed            release resources
resize or fullscreen      reset and settle again
bad depth                 reduce depth work
bad motion                reduce temporal work
bad REVENANT candidate    keep accepted asset
Deck fails in frame       open desktop Deck
install state changed     mark stale and repair
```

that is the part people do not see in screenshots but it is half the reason the engine works at all.

## Adaptive Realism

Adaptive Realism is supposed to make the game look more real without forcing the same look on every game.

it works with source cleanup, form, material response, contact response, local contrast, depth backed lighting work when it actually has depth, black level cleanup, highlight shaping, color protection and detail recovery.

higher levels push that stack harder.

they are not supposed to just mean more saturation and more sharpening.

## what i'm keeping private

the full repo is still private.

i am not posting the whole source tree, complete shaders, full runtime files, build graph, provider internals, package tooling or every surrounding function needed to rebuild the project.

that's not what this page is for.

this page is just here because people asked to see how the engine actually works. now there is real code here to look at.

## current build proof

this is based on HF18.11.

the release candidate passed the normal build gate. x86 and x64 production builds, HLSL compile, static regressions, D3D11 WARP testing, install/update/rollback tests, scanner and sidecar tests, PCSX2 sidecar smoke, launcher checks, ZIP integrity and Defender scanning.

that proves the package i released passed those checks.

it does not mean i am claiming every game on every GPU is perfect. real hardware testing is still real hardware testing.

that is pretty much UNCANNY rn.

push the image as hard as i can when the engine has good data. back off when it doesn't.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.
