# HF18.13

HF18.13 is the launch/runtime recovery build for the failures reproduced in the Sept. 19 hardware logs.

## PCSX2 / Direct3D 12

HF18.12 moved heavy D3D12 processor initialization off Present, but that introduced a bad resize interaction.

HF18.13 fixes both sides of it:

- D3D12 Present stays fail-open and nonblocking.
- Once UNCANNY owns swapchain resources, ResizeBuffers gets a bounded transactional handoff instead of immediately returning `DXGI_ERROR_WAS_STILL_DRAWING`.
- While off-Present D3D12 warmup is actively building resources for a swapchain, that same swapchain cannot resize underneath the resource build.
- PCSX2 stays on Direct3D 12 with `Renderer=15`.

That targets the reproduced pattern where PCSX2 reached gameplay for a few seconds and then wedged as the renderer transitioned.

## Cyberpunk / Spider-Man 2 / modern dynamic targets

HF18.13 also hardens launch ownership and deferred attach:

- dynamically-bound non-PCSX2 targets start natively first;
- UNCANNY waits for a stable visible top-level game window before late runtime attach;
- verified stale/headless UNCANNY sessions can be reclaimed on retry/update;
- a visible game is never auto-terminated by stale-session cleanup.

## HOME / Control Deck

The HOME/Deck path itself was not rewritten. The dead HOME key seen during the PCSX2 failure is consistent with the runtime/renderer becoming wedged before the Deck can remain responsive.

## Build

BuildId: `elysium45-hf18.13`  
updateSerial: `1930`  
ABI: `143`

ZIP SHA-256:

`c4faffd66ca5addfd7c200b08d46d279c5aa3274fabdae643280242845fca522`

Exact candidate: `982baa13dd2612e8368921ade4322bc99d6d6578`  
Dev merge: `7d1087276c4eac9b0e4ddfdf64ff8d23d439cd96`  
Validation run: `35459233640`  
Publication run: `35459735287`

The published candidate passed production builds, Windows HLSL/WARP, PCSX2/D3D12 regression, launch/session recovery, packaged PCSX2 + generic sidecar launch, launcher smoke, AllSigned and Microsoft Defender with 0 detections.

Real PCSX2/Cyberpunk/Spider-Man hardware behavior still needs the actual machine retest.
