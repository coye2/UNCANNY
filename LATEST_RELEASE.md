# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.3**

- BuildId: `elysium45-hf18.3`
- updateSerial: `1830`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18.3`
- ABI: `143`
- Source revision: `75e8d346bea6fb30d2a20e50dd8e7e0170b77760`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.3/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.3.zip
- SHA-256: `4f252c9c21891ecab2f7ecc37f95a0149854f4a2d18f2300402366f515169428`

HF18.3 fixes the launcher StrictMode `Path` crash, hardens WPF event recovery, uses a native vector ELYSIUM badge, and prevents stale unmarked Lucid preferences from silently swapping freshly installed ELYSIUM binaries back to the legacy HOME menu. Explicit current user engine choices remain honored.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35391373976

The exact candidate passed x86/x64 builds, HLSL, WARP rendered-quality validation, Windows launcher/install/rollback regressions, stale-Lucid migration, extracted-package checks, packaged `UNCANNY.exe` → WPF `ShowDialog()` survival smoke, ZIP integrity, and Microsoft Defender with 0 detections.
