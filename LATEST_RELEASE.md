# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18**

- BuildId: `elysium45-hf18`
- updateSerial: `1800`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18`
- ABI: `143`
- Source revision: `0c5de983a400dd77d85992c6a5c1d37bcc3139eb`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.zip
- SHA-256: `21f654c3260a3c258f7121574edef56c44a718449c16f51aa20d7695bc925489`

HF18 closes the current Universal API Bridge and tester-feedback push. D3D11 startup now uses a universal native-Present stabilization floor before optional preprocessing, API routing/ownership evidence fails open instead of guessing, Control Deck controls expose visible help, and the ELYSIUM perceptual path receives stronger source-backed face, color, edge and microtexture reconstruction.

Motion Protection Strength and Ghosting Guard are independently effective. The package also includes clean-room local exposure fusion, source-radiance recovery, depth-proven relighting/contact shaping, adaptive clarity/sharpening and source-directed subpixel edge resolve.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35377702421

The exact HF18 candidate passed static/generated-resource regressions, x86/x64 production and legacy builds, Windows HLSL compilation, a real D3D11 WARP rendered visual-quality matrix across all 42 exposed floating image controls, installer/rollback/manual-add regressions, exact ZIP verification and Microsoft Defender scans with 0 detections.

Real-game visual, motion and performance acceptance remains title/GPU/driver specific.
