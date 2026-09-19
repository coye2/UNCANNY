# FAQ

## What is UNCANNY?

A Windows real-time remastering runtime for games and emulators. It combines ELYSIUM live reconstruction, motion protection, optional neural processing, compatibility work and the experimental REVENANT asset system.

## What is the current release?

HF18.11.

BuildId: `elysium45-hf18.11`  
updateSerial: `1910`  
ABI: `143`

Download:
https://github.com/coye2/UNCANNY/releases/latest

## Is it a ReShade preset?

No. UNCANNY uses native runtime components, its own controls, install/rollback tooling and graphics-API hooks.

## Is ELYSIUM the same thing as DLSS 5?

No.

ELYSIUM is UNCANNY's native image-processing path. The DLSS 5 route is optional and provider-specific.

## What are 1 / 1.5 / 2 / 2.5 / 3?

Those are ELYSIUM pass depths.

X2.5 is intentionally tuned to use less temporal history and favor cleaner motion.

## What are Motion Guard and Ghosting Guard?

They reduce unstable history when motion, disocclusion or current/history disagreement makes temporal reconstruction unsafe.

## What is Adaptive Realism?

A scene-aware layer that adjusts supported ELYSIUM processing based on the frame data UNCANNY can actually trust.

If reliable depth/motion data is missing, it falls back instead of pretending those features are available.

## What is REVENANT?

UNCANNY's experimental asset-reconstruction system.

PCSX2 is the main test target. Native PC-game asset replacement is still experimental.

## Does it support PCSX2?

Yes, it is one of the main targets. The current route uses Direct3D 12 / `Renderer=15`.

## D3D11 and D3D12?

Both are active routes.

HF18.11 fixes staged neural promotion on D3D11. HF18.10 handles D3D12 startup/resize stabilization.

## D3D9 / D3D10?

There are legacy/compatibility routes, but they can have reduced capability depending on the game and available frame data.

## Vulkan / OpenGL?

Not at DirectX parity yet.

## Do I need to disable Defender?

No.

If Defender flags an official current release, do not blindly whitelist it. Check the release hash and report the exact detection.

## Why does Windows say Unknown Publisher?

The current alpha binaries are unsigned.

## Is the source public?

The full development workspace is private. This repository is the public release/support repo.

## Does CI prove every game works?

No. CI proves the code/package gates it actually runs. Game/GPU behavior still needs real hardware testing.

## Is UNCANNY affiliated with NVIDIA?

No.
