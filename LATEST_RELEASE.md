# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.2**

- BuildId: `elysium45-hf18.2`
- updateSerial: `1820`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18.2`
- ABI: `143`
- Source revision: `ba47d93292179fda8e3d83bdb3f8c9347e5cfa65`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.2/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.2.zip
- SHA-256: `2cc50a82e5e30b206e7de2a307f3fb70c31895f088de85edc332dea3fb60b1e4`

HF18.2 fixes launcher post-install/update state refresh, speeds target executable inspection, corrects the ELYSIUM badge crop, and cleans the public ZIP root. PowerShell implementation now lives under `runtime\`, maintenance commands under `Tools\`, and `UNCANNY.exe` remains the normal root entry point.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35387436459

The exact candidate passed static regressions, x86/x64 production builds, HLSL, D3D11 WARP rendered-quality validation, Windows installer/rollback/manual-add regressions, extracted-package clean-root and packaged-PowerShell parsing, ZIP integrity/hash verification, and Microsoft Defender with 0 detections.
