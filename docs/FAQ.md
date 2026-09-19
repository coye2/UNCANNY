# FAQ

## What is UNCANNY?

A Windows real-time graphics remastering runtime for games and emulators.

It combines ELYSIUM live reconstruction, motion protection, optional neural processing, compatibility work and the experimental REVENANT asset system.

## What is the current release?

HF18.13.

BuildId: `elysium45-hf18.13`  
updateSerial: `1930`  
ABI: `143`

Download:
https://github.com/coye2/UNCANNY/releases/latest

## Is it a ReShade preset?

No. UNCANNY uses native runtime components, its own controls, install/rollback tooling and graphics-API hooks.

## Is ELYSIUM the same thing as DLSS 5?

No.

ELYSIUM is UNCANNY's native image-processing path. DLSS 5 is a separate optional provider route.

## What are 1 / 1.5 / 2 / 2.5 / 3?

Those are ELYSIUM pass depths.

X2.5 intentionally uses less temporal history and is meant to favor cleaner motion.

## What do Motion Guard and Ghosting Guard do?

They reduce unstable history when motion, disocclusion or current/history disagreement makes temporal reconstruction unsafe.

## What is Adaptive Realism?

A scene-aware layer that adjusts supported ELYSIUM processing based on the frame data UNCANNY can actually trust.

If reliable depth or motion data is missing, it falls back instead of pretending those features are available.

## What is REVENANT?

UNCANNY's experimental asset-reconstruction system.

PCSX2 is the main test target. Native PC-game asset replacement is still experimental.

## Does it support PCSX2?

Yes. It is one of the main test targets. The current route uses Direct3D 12 with `Renderer=15`.

## D3D11 and D3D12?

Both are active routes.

HF18.11 provides staged neural promotion on D3D11. HF18.13 fixes the D3D12 warmup/resize transition regression while keeping Present fail-open and preserving the D3D12 startup protections.

## D3D9 / D3D10?

There are legacy/compatibility routes, but capability depends on the game and what frame data is available.

## Vulkan / OpenGL?

Not at DirectX parity yet.

## Do I need to disable Defender?

No.

If Defender flags an official current release, check the release hash and report the exact detection instead of blindly whitelisting it.

## Why does Windows say Unknown Publisher?

The current alpha binaries are unsigned.

## Is the source public?

The full development workspace is private. This repository is the public release/support repo.

## Does CI prove every game works?

No. CI proves the code/package checks it actually runs. Game and GPU behavior still needs real hardware testing.

## Is UNCANNY affiliated with NVIDIA?

No.
