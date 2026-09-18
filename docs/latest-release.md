# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.3**

- Runtime: `release-alpha.1.elysium-engine45-hf18.3`
- BuildId: `elysium45-hf18.3`
- updateSerial: `1830`
- ABI: `143`
- Source revision: `75e8d346bea6fb30d2a20e50dd8e7e0170b77760`
- Published: 2026-09-18
- Latest release: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45-hf18.3
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.3/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.3.zip
- SHA-256: `4f252c9c21891ecab2f7ecc37f95a0149854f4a2d18f2300402366f515169428`

HF18.3 fixes launcher StrictMode startup/ShowDialog crashes and stale legacy-engine preference migration. Old unmarked Lucid preferences now migrate to Automatic/ELYSIUM; only explicit current user selections preserve Lucid. The launcher uses a native vector ELYSIUM emblem.

Exact validation: https://github.com/coye2/uncanny-dev/actions/runs/35391373976

The exact package passed x86/x64 production builds, HLSL, WARP rendered-quality validation, Windows launcher/install/rollback regressions, stale-Lucid migration, final ZIP checks, packaged launcher survival smoke, and Microsoft Defender scans with 0 detections.
