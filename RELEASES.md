# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Hotfix 10**

- Runtime revision: `release-alpha.1.elysium-hotfix10`
- ABI: `141`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-Windows.zip`
- SHA-256: `521b00a5236046ca7de7feb06df1942d3bbde12eb1eb3e1a2b63a2bd20535f4b`

### Hotfix 10

- Fixed HOME-page **UNCANNY PASSES** so 1 / 1.5 / 2 / 2.5 / 3 drives the native ELYSIUM reconstruction depth instead of the separate DLSS 5 pass field.
- Added a separate **DLSS 5 PASSES** selector on the DLSS 5 page.
- Exposed/wired ELYSIUM structural reconstruction, surface detail, face reconstruction, material definition, depth/form, color recovery/separation, fine-edge recovery, distant detail and texture-relief controls.
- Synchronized the generated shader header with the current 56-float / 14-register ELYSIUM shader-control layout.
- Preserved launcher, game scanning, install/update flow, PCSX2 wrapper behavior, REVENANT and engine switching.

### Verification before packaging

- x86 and x64 Windows runtime/launcher/REVENANT/Control Deck/DLSS bridge targets cross-compiled successfully, plus the x64 Neural Host.
- Hotfix 9 static ELYSIUM regression: PASS.
- Hotfix 10 pass/slider wiring regression: PASS.
- Protected-resource roundtrip/authentication checks: PASS.
- Final ZIP CRC: PASS.
- Final compiled-binary hashes: PASS.
- Public-package source leak audit: 0 source files found.

Real-GPU rendered appearance and game-specific behavior still require hardware testing; build-host checks are not a substitute for that.

## Private source/workspace

The engineering source is maintained privately and is not part of the public release. Do not redistribute private recovery/source packages.
