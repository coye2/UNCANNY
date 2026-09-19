# UNCANNY v0.20 ELYSIUM — HF18.9

UNCANNY is a Windows real-time reconstruction/remaster runtime for games and emulators.

**HF18.9 is the current stabilization release.** It focuses on the two failure classes reproduced during HF18.7/HF18.8 testing: direct-D3D11 games that could hard-freeze when UNCANNY advanced beyond native startup, and PCSX2 drifting away from the previously working Direct3D 12 / Feature-18 route.

## Start

1. Extract the ZIP completely.
2. Double-click **`UNCANNY.exe`**.
3. Select a game or emulator.
4. Choose **Install UNCANNY** or **Update UNCANNY**.
5. Launch from UNCANNY or normally through the installed sidecar route.
6. Press **HOME** for the Control Deck.

## HF18.9 — universal D3D11 stability floor

The Fallout-class D3D11 hard-lock repair is no longer a title-specific exception.

- Every **direct D3D11** route starts from the proven current-frame compatibility floor.
- Native presentation remains authoritative and fail-open.
- Native depth capture, temporal history, optical-flow-dependent stages, and D3D11 neural interop are deferred on the safe floor.
- The safe floor uses conservative current-frame ELYSIUM processing rather than risking a game hard lock.
- This change is intended to cover the same failure class reproduced in Fallout 4 and Stray without maintaining executable-name allowlists.
- External compatibility/feed surfaces keep their separately synchronized path.

## HF18.9 — PCSX2 restores the known-good Direct3D 12 route

PCSX2 is **not** forced through the D3D11 safe floor.

- UNCANNY pins PCSX2's GS renderer to **Direct3D 12** using PCSX2's current `Renderer=15` mapping.
- The setting is applied transactionally to the main PCSX2 GS configuration and existing per-game overrides that UNCANNY already manages.
- Same-build verification treats renderer drift away from DX12 as stale, so **Update UNCANNY** repairs the route instead of silently accepting it.
- The verified `UNCANNY.Launch.exe` sidecar remains the launch path; the selected `pcsx2-qt.exe` is kept at its real filename.
- REVENANT texture replacement configuration, OneDrive/Cloud Files profile handling, and rollback remain transactional.
- The purpose is to recover the previously working PCSX2 **D3D12 + Feature-18** path, not redesign it around D3D11.

## Preserved HF18.7 / HF18.8 fixes

- Universal sidecar launch no longer replaces or renames the selected game/emulator executable.
- Legacy wrapper-in-place PCSX2 installs can be recovered transactionally back to the real `pcsx2-qt.exe`.
- Valid Windows CRLF sidecar records no longer get marked stale immediately after installation.
- PCSX2 profiles under OneDrive/Cloud Files are accepted when the reparse point is a normal cloud placeholder; true symlinks/junctions remain blocked.
- Same-build verified no-op update, neural-core reuse, scanner/library fixes, manual Add Game persistence, rollback, Motion Guard, Ghosting Guard, and X2.5 clean-motion behavior remain preserved.

## DLSS 5 / Feature-18 status

DLSS 5 is a **separate optional NVIDIA/provider path**. ELYSIUM can run without it.

The current runtime reports neural output separately from ordinary UNCANNY image processing. A working ELYSIUM frame does **not** prove DLSS 5 is producing current output. Tester hardware has confirmed the ELYSIUM path running in Fallout 4, while DLSS 5 current-output on that title still requires further hardware validation.

## Validation

Exact tested HF18.9 candidate: `b168d748d241851d8faf13c83ff64aab10cd19b2`  
Dev-main merge: `cff224e353348df35d912d706b11061e0d56aba3`  
Validation run: https://github.com/coye2/uncanny-dev/actions/runs/35420827416  
Public release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45-hf18.9  
ZIP SHA-256: `7c469cc508b7fa999b1598c80156cbf4af6201925d3455b27f980c4acf9d4c37`

The exact candidate passed:

- static/regression contracts
- x86/x64 production and Engine 4.5 acceptance builds
- PowerShell parse, install, update, rollback, and PCSX2 migration regressions
- dedicated PCSX2 Direct3D 12 configuration regression
- packaged same-build install/update regression
- packaged untouched PCSX2 + generic sidecar launch
- Windows HLSL compilation
- D3D11 WARP rendered visual-quality gate
- launcher startup and AllSigned startup
- Microsoft Defender ZIP + extracted-tree scan with 0 detections

CI proves the packaged/runtime contracts above. Real-game visual, motion, performance, and provider behavior remain GPU/driver/title specific and require hardware testing.

## Windows trust

UNCANNY is currently unsigned. Windows SmartScreen / Unknown Publisher may appear until trusted Authenticode signing is configured.
