# FAQ

## What is UNCANNY?

UNCANNY is experimental real-time remastering middleware for Windows games and emulators. It combines ELYSIUM reconstruction, Adaptive Realism, motion protection, neural-provider integration, REVENANT asset reconstruction, diagnostics and compatibility tooling in one runtime.

## What is the current release?

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — Adaptive Realism**

Runtime: `release-alpha.1.elysium-engine45`  
ABI: `143`

Exact public ZIP SHA-256:

`f8b13f51cacd96b1b375b566c675d17661f66bb4bb2673cd34edf8e7f5859512`

## Where do I download it?

Use https://github.com/coye2/UNCANNY/releases/latest and follow [USAGE.md](../USAGE.md).

## What is Adaptive Realism?

Adaptive Realism is UNCANNY's scene-aware image reconstruction/enhancement layer introduced in ELYSIUM Engine 4.5. It can run independently from DLSS 5 and adjusts its behavior to the scene evidence UNCANNY can safely obtain.

## What are the five Adaptive Realism levels?

`OFF / LOW / BALANCED / HIGH / INSANE`

They are real runtime levels. Higher settings increase supported reconstruction samples/intensity while the performance guard can reduce cost before turning features off.

## What are the Adaptive Realism tiers?

- **Tier A:** trustworthy depth + native motion.
- **Tier B:** trustworthy depth + UNCANNY optical flow.
- **Tier C:** trustworthy depth only; conservative spatial lighting and no temporal history.
- **Tier D:** no trustworthy depth; tonal/spatial enhancement only.

UNCANNY intentionally falls back instead of pretending depth-aware GI is active when trustworthy depth is missing.

## Which API currently gets the strongest Adaptive Realism path?

D3D11. It can use capability-scored discovered depth and UNCANNY optical flow where available.

D3D12 and D3D9 remain supported but currently use conservative fallbacks when trustworthy scene depth is unavailable.

## Is Adaptive Realism the same as DLSS 5?

No. They are separate systems.

Adaptive Realism is UNCANNY-native and vendor-neutral. DLSS 5 is a separate NVIDIA-specific neural-provider route.

## What are UNCANNY PASSES 1 / 1.5 / 2 / 2.5 / 3?

They control native ELYSIUM reconstruction depth. They are separate from Adaptive Realism quality and separate from **DLSS 5 PASSES**.

## Why is X2.5 special?

X2.5 deliberately uses substantially less temporal history. It is intended to be the clean-motion mode when suppressing trails/afterimages matters more than preserving maximum temporal detail.

## What are Motion Guard and Ghosting Guard?

They reduce unstable reconstruction during motion, disocclusion and unreliable temporal history. Engine 4.5 uses them to lower or reject history when motion/depth/current-frame evidence disagrees.

## What ELYSIUM controls are available?

Advanced controls include structural reconstruction, surface detail, face reconstruction, material definition, depth/form recovery, source color recovery, material color separation, fine-edge recovery, distant detail, texture relief, Motion Guard, Ghosting Guard and Adaptive Realism quality.

## What is REVENANT?

REVENANT is UNCANNY's experimental persistent asset-reconstruction system. PCSX2 is currently its main acceptance target.

A successful REVENANT worker job does not automatically prove that the replacement is visibly bound by the game/emulator. Native-PC-game asset replacement remains experimental.

## Does it support D3D9 / D3D10?

The runtime includes D3D9 and D3D10/10.1 compatibility paths. Their Adaptive Realism/neural capabilities depend on the trustworthy scene data and provider path available to that title.

## D3D11 / D3D12?

Both are active PC paths. D3D11 currently has the strongest Adaptive Realism scene-data route. Engine 4.5 also preserves the Hotfix 11 D3D11 fail-open startup behavior.

## Vulkan / OpenGL?

Not at DirectX parity yet.

## Does ENABLE UNCANNY OFF really bypass the engine?

It is intended to remain the master UNCANNY image-processing bypass. REVENANT cached/replaced assets are a separate system and may need to be restored separately for a complete asset-level before/after comparison.

## What happened with the Windows Defender warning from Hotfix 11?

The first Hotfix 11 package mistakenly included internal acceptance-test executables under `diagnostics/`. One of those development harnesses was flagged. It was not a runtime dependency and the public package was corrected.

The current Engine 4.5 package again passed Microsoft Defender scans of both the extracted final package and completed ZIP with **0 detections**. The release includes `MALWARE-VERIFICATION-ENGINE45.json`.

See [MALWARE-VERIFICATION.md](MALWARE-VERIFICATION.md).

## Do I need to disable Defender or whitelist UNCANNY?

No. UNCANNY does not require disabling Defender or adding a broad antivirus exclusion. If a current official package is detected, report the exact file, threat name, release tag and ZIP SHA-256 so it can be investigated.

## Is the source public?

No. The public repository contains documentation, release information and support material. The full development source workspace is private.

## Is it just a ReShade preset?

No. UNCANNY ships native runtime components, controls, diagnostics, installation/rollback tooling, DirectX compatibility components and its own ELYSIUM/Adaptive Realism processing.

## Does UNCANNY bundle paid Marty McFly / Pascal Gilcher shaders?

No. The Engine 4.5 package audit checks for restricted third-party shader source/package leakage. The release does not bundle paid/restricted Marty McFly / Pascal Gilcher shader source or binaries.

## How do I know the runtime actually ran?

Use `UNCANNY-STATUS.cmd` and visible before/after testing. A DLL existing on disk or an overlay saying enabled is not enough evidence by itself.

## Does passing CI prove every game/GPU works?

No. Engine 4.5 passed its regression suite, compiled acceptance tests, production builds, package audit, install/rollback test and Defender scans. Real visual quality, compatibility and performance still require title-by-title hardware testing.

## Is UNCANNY affiliated with NVIDIA?

No. UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.