# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18**

- Runtime: `release-alpha.1.elysium-engine45-hf18`
- BuildId: `elysium45-hf18`
- updateSerial: `1800`
- ABI: `143`
- Source revision: `0c5de983a400dd77d85992c6a5c1d37bcc3139eb`
- Published: 2026-09-18
- Latest release: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45-hf18
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.zip
- SHA-256: `21f654c3260a3c258f7121574edef56c44a718449c16f51aa20d7695bc925489`

## HF18

HF18 closes the current compatibility and perceptual-quality push:

- universal D3D11 native-Present startup stabilization before optional preprocessing
- deterministic Universal API Bridge ownership/capability/source evidence with fail-open behavior
- stronger source-backed face reconstruction and source-hue/color recovery
- clean-room local exposure fusion, source-radiance recovery, relighting/contact shaping and adaptive clarity
- source-directed subpixel edge resolve
- independent Motion Protection Strength and Ghosting Guard behavior
- stronger dedicated Microtexture response
- visible Control Deck info icons and hover help
- exact installer verification diagnostics, safer owned-residue cleanup and current release-name updater support
- all 42 exposed floating image controls rendered through the D3D11 WARP quality matrix

## Verification

Exact candidate run: https://github.com/coye2/uncanny-dev/actions/runs/35377702421

Static/generated-resource regressions, x86/x64 production/legacy builds, Windows HLSL, WARP rendered visual-quality gates, PowerShell installer/rollback/manual-add, exact ZIP integrity/hash and Microsoft Defender all passed. Defender reported 0 detections on the exact final ZIP and extracted tree.

Real-game visual/performance acceptance remains title/GPU/driver specific.
