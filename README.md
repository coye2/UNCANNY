# UNCANNY v0.20 ELYSIUM — HF18.5

UNCANNY is a Windows real-time reconstruction/remaster runtime for games and emulators. **HF18.5** is a launcher/library repair release driven by a real tester log: the launcher opened, but its official logo failed WPF decoding and cached/scanned games never reached the UI.

## Start

1. Extract the ZIP completely.
2. Double-click **`UNCANNY.exe`**.
3. Let the launcher load cached/manual games immediately, or use **Scan PC**.
4. Use **Add game** for any title/emulator discovery misses.
5. Select the real game/emulator EXE and choose **Install UNCANNY** or **Update UNCANNY**.
6. Launch normally and press **HOME** for the Control Deck.

## HF18.5

- Fixes packaged **Scan PC** using the wrong root. Public PowerShell lives under `runtime\`; the scanner now resolves `UNCANNY-InstallCommon.ps1` and `UNCANNY-Library.ps1` beside itself instead of looking in the clean ZIP root.
- Cache/manual/scan records are canonicalized through guarded property access before WPF binding. Legacy records with `Path`, `Exe`, missing optional fields, or stale schemas can no longer blank the library.
- The official silver UNCANNY U PNG is still the real asset. The launcher re-encodes it through a **32-bit ARGB** surface before WPF loads it, fixing the tester-reproduced “image format is unrecognized” failure.
- Recovered launcher failures now log the PowerShell stack and invocation position instead of only the exception name.
- HF18.4’s process-scoped startup recovery is preserved. UNCANNY does not change persistent machine/user execution policy and does not disable Defender or SmartScreen.
- Installed-game path hardening, updater ordering, stale-Lucid migration, PCSX2, REVENANT, rollback, Universal API Bridge, Motion Guard/Ghosting Guard and the HF18 rendering stack are preserved.

The release gate now executes the **packaged** launcher with malformed/legacy cache records, verifies the logo actually loads, invokes the **packaged scanner**, checks the library render log, then runs normal startup, AllSigned startup, WARP, ZIP/hash and Defender gates.

## Status

This is public alpha software. Build/package validation does not replace real-game GPU/driver/title acceptance. The executable remains unsigned, so SmartScreen/Unknown Publisher may still appear until trusted Authenticode signing is configured.
