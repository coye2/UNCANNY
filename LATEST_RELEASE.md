# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.3**

- BuildId: `elysium45-hf18.3`
- updateSerial: `1830`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18.3`
- ABI: `143`
- Source revision: `47841050ac5fbb04ffaa90823e2d0adc5c9236da`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.3/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.3.zip
- SHA-256: `9748039fefcbbe941ea3d67cb54b731798d35b7332643677a3a28b4398fbcb21`

HF18.3 fixes the launcher StrictMode `Path` crash, hardens WPF event recovery and installed-game path normalization, uses the official cropped UNCANNY PNG emblem, removes `-ExecutionPolicy Bypass` from the native EXE bootstrap, and prevents stale unmarked Lucid preferences from silently swapping freshly installed ELYSIUM binaries back to the legacy HOME menu. Explicit current user engine choices remain honored.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35393751767

The exact candidate passed x86/x64 builds, HLSL, WARP rendered-quality validation, Windows launcher/install/rollback regressions, stale-Lucid migration, extracted-package checks, packaged `UNCANNY.exe` → WPF `ShowDialog()` survival smoke, ZIP integrity, and Microsoft Defender with 0 detections.
