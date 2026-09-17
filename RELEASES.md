# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Hotfix 11**

- Runtime revision: `release-alpha.1.elysium-hotfix11`
- ABI: `141`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-HOTFIX11.zip`
- SHA-256: `14e28fad9a016a096e58167eebc53d8b96ead41687b1b366fbb34c92427c7bd7`
- Release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-hotfix11

### Why Hotfix 11 exists

A real PCSX2 x64 / D3D11 tester session reached `PRESENT_PATCH_OK`, but the game remained black. The status/trace showed one hooked Present attempt and zero completed native Presents:

- `PresentAttempts=1`
- `Presents=0`
- `PresentAdvancing=0`
- `BaseFPS=0`
- `PresentedFPS=0`
- `FeatureCreateAttempts=0`
- `FeatureEvaluateAttempts=0`
- `DeckConnected=1`
- `DeckSurfacePublished=0`
- `DeckVisible=0`
- `GameForeground=0`

The independent REVENANT texture path completed 38/38 jobs during the same report. That separated the working texture worker from the stalled live swapchain path.

The report also showed `Host64LaunchAttempted=0`. On an x64 D3D11 target this is not automatically a failure: the normal native route can use the in-process bridge. Hotfix 11 therefore addresses presentation ordering instead of treating the missing helper launch as the root cause.

### Hotfix 11

- Direct D3D11 startup is fail-open. The first native presentation opportunities prioritize the game's original `Present` / `Present1` before UNCANNY image preprocessing or in-frame HOME/Deck composition.
- Feature-18 / DLSS 5 D3D11 interop waits until the native presentation stream is advancing, at least 8 successful Presents have completed and the most recent Present is current.
- A delayed neural route leaves the live source frame in place instead of substituting stale output.
- New stages — `PRESENT_PREPROCESS`, `PRESENT_NATIVE_CALL`, `PRESENT1_PREPROCESS`, `PRESENT1_NATIVE_CALL` and `PRESENT_SUCCEEDED` — make future reports much more precise.
- Hotfix 10 ELYSIUM pass/slider wiring remains intact.
- REVENANT remains intact.
- PCSX2 wrapper behavior, updater/install/rollback flow, provider policy and non-D3D11 routes are not redesigned by this hotfix.
- The existing UNCANNY 2.5 Lucid ABI 136 bundle is preserved by its already-published manifest hashes.

### Launcher change

The normal public entry point is now **`UNCANNY.exe`** at the root of the extracted package.

- native Windows GUI executable
- no top-level `UNCANNY.cmd` user launcher
- starts the bundled launcher without exposing a console window
- duplicate-instance guard
- native startup error handling/logging

Maintenance `.cmd` files still exist for specific diagnostics/install tasks where appropriate.

### Verification before publication

The exact public Hotfix 11 ZIP passed:

- Hotfix 9 ELYSIUM static regression: PASS
- Hotfix 10 pass/slider wiring regression: PASS
- Hotfix 11 D3D11 native-Present fail-open regression: PASS
- native `UNCANNY.exe` regression: PASS
- 12 public Windows diagnostic binaries: COMPILED
- 16 focused Hotfix 11 acceptance checks: PASS
- x86 + x64 production runtime/launcher/REVENANT/Control Deck/bridge builds: PASS
- x64 Neural Host build: PASS
- protected shader roundtrip/authentication checks: PASS
- production PE hardening audit: PASS across all 11 current production/helper binaries
- strict public package audit: PASS
- final ZIP integrity: PASS

### Hardware acceptance still required

The build-host evidence proves the code/package contract, not that every GPU/title is fixed. The original PCSX2 D3D11 setup should confirm:

1. the game image appears immediately
2. `Presents` advances continuously
3. `PresentAdvancing=1`
4. FPS becomes non-zero
5. `AttachmentStage` reaches `PRESENT_SUCCEEDED`
6. neural attempts begin only after native presentation is healthy
7. HOME opens without requiring Alt-Tab or stopping presentation
8. REVENANT remains functional
9. PCSX2 exits cleanly

## Previous v0.20 hotfix

Hotfix 10 repaired **UNCANNY PASSES** and the ELYSIUM reconstruction-slider wiring and separated UNCANNY passes from DLSS 5 passes. Those changes are preserved in Hotfix 11.

## Private source/workspace

The engineering source is maintained privately and is not part of the public release. Do not redistribute private recovery/source packages.