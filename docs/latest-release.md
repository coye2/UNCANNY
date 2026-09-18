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

## HF18.3

- fixes launcher startup/ShowDialog crashes caused by malformed legacy discovery/cache object properties under StrictMode
- adds guarded WPF startup/selection/action recovery
- replaces the fragile raster badge path with a native vector purple/green ELYSIUM emblem
- migrates stale unmarked Lucid preferences to Automatic/ELYSIUM
- preserves Lucid only when a current explicit user choice carries `UserSelected=1`
- prevents a current PCSX2 update from silently booting the legacy HOME menu through an old engine preference
- preserves the clean `runtime\` / `Tools\` public package layout

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35391373976

The exact package passed x86/x64 production builds, HLSL compilation, D3D11 WARP rendered-quality validation, Windows launcher/install/rollback regressions, stale-Lucid migration, clean-package checks, packaged launcher startup/ShowDialog smoke, ZIP integrity/hash verification and Microsoft Defender scans with 0 detections.
