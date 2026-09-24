# UNCANNY

UNCANNY is a real-time graphics remastering project for Windows games and emulators.

**Current release candidate:** v0.20.0-alpha.2 — Final Alpha — ELYSIUM Engine 4.5

This is the final alpha checkpoint before beta. It is based on the exact private candidate `748f80b6a63f64bc811479b185e00dc45d34c373`, whose full private CI run passed.

## Verified additions

- source-bounded detail/noise governor
- conservative depth/history-gated water recovery
- restricted D3D11 rigid-geometry replacement evidence
- normal-only rigid-mesh recovery
- content-identified material targeting with exact restoration
- matched synthetic motion/water evidence and GPU timing
- x86/x64 production builds and full private validation

The controlled material fixture changed 65,536 target pixels to unmistakable pink, kept 65,536 pixels from the unrelated material byte-identical, and restored the original exactly.

The corrected rigid silhouette fixture changed 48 to 120 triangles and reduced independent-reference coverage error from 4,464 to 3,816 pixels while preserving the unrelated scene component.

## Boundaries

This release does **not** claim universal auto-tessellation, animated mesh replacement, automatic rock/gravel displacement, dramatic water geometry, universal DLSS 5, or real-game certification from synthetic fixtures.

REVENANT remains experimental. The optional neural/DLSS route is separate from ELYSIUM.

## Install

1. Download the Final Alpha ZIP from the release.
2. Extract the whole folder.
3. Run `UNCANNY.exe`.
4. Pick a detected game or use **Add game**.
5. Install/update UNCANNY.
6. Press **HOME** in-game for Control Deck.

## Support UNCANNY

UNCANNY is built independently and released to the community. If you like what I'm building and want to help keep development moving, you can support the project on [Ko-fi](https://ko-fi.com/coye2).

Support helps with development, testing, infrastructure, code signing, and keeping UNCANNY moving toward beta.

## Source and security

UNCANNY is closed source. The public repository contains release/support material, not the private development tree. No private source, CI evidence bundle, developer harness, or internal build tooling is part of the public package.

The binaries remain unsigned, so Windows may show Unknown Publisher. Do not disable Defender or add broad exclusions.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.
