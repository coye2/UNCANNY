# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.1**

- BuildId: `elysium45-hf18.1`
- updateSerial: `1810`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18`
- ABI: `143`
- Source revision: `458dc5820beb9322c7ee115ed98fd07a7b1b0c77`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.1/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.1.zip
- SHA-256: `82257f00d4c323853fef1b5576578d6b0b025b44829c17027c46019ece726777`

HF18.1 fixes the installer/update preflight that could appear stuck at 2%, adds real 3/4/5/6/7% preflight stages, fixes the updater-button text layout, and replaces the monochrome launcher badge with the current full-color ELYSIUM emblem.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35383983512

The exact candidate passed static regressions, x86/x64 production builds, HLSL, D3D11 WARP rendered-quality validation, Windows install/rollback/manual-add regressions, ZIP verification and Microsoft Defender with 0 detections.
