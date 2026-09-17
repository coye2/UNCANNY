# Changelog

All notable public UNCANNY alpha changes are documented here.

## v0.20.0-alpha.1 — ELYSIUM Hotfix 11

Runtime revision: `release-alpha.1.elysium-hotfix11`  
ABI: `141`

### Tester-derived D3D11 repair

- Fixed a PCSX2 x64 / D3D11 first-frame black-screen failure class where `PRESENT_PATCH_OK` was followed by one Present attempt, zero successful Presents, no advancing Present stream and 0 FPS.
- Direct D3D11 startup now fails open: native `Present` / `Present1` receives the initial presentation opportunities before optional UNCANNY image processing or in-frame Control Deck composition can run.
- D3D11 Feature-18 / DLSS 5 interop now waits for a healthy Present stream instead of becoming part of first-frame startup.
- While neural startup is deferred, the current live source frame remains authoritative; stale neural output is not substituted.
- Added `PRESENT_PREPROCESS`, `PRESENT_NATIVE_CALL`, `PRESENT1_PREPROCESS`, `PRESENT1_NATIVE_CALL` and `PRESENT_SUCCEEDED` diagnostic stages.
- Corrected the interpretation of `Host64LaunchAttempted=0` for the normal native x64 D3D11 route: a separate helper process is not required for every x64 session.
- Preserved the independent REVENANT path; the triggering tester report completed 38/38 texture jobs while the swapchain presentation path was stalled.

### Security / packaging correction

- Removed the public `diagnostics/` executable payload.
- Removed `revenant-commit32.exe` and `revenant-commit64.exe` from public distribution. These are internal acceptance-test harnesses built from the REVENANT test suite, not runtime requirements.
- Internal diagnostic/test binaries remain available to CI but are no longer part of the user-facing release ZIP.
- Added a Microsoft Defender release gate on a fresh GitHub-hosted Windows runner.
- Defender signatures are updated immediately before release scanning.
- Cleaned runtime tree scan: **PASS / 0 detections**.
- Final completed ZIP scan: **PASS / 0 detections**.
- Defender engine: `1.1.26080.3`; signatures: `1.459.256.0`; product: `4.18.26080.3`.
- Added `docs/MALWARE-VERIFICATION.md` inside the ZIP and `MALWARE-VERIFICATION-HOTFIX11.json` as a GitHub release attachment.
- No Defender exclusions, threat restoration, allowlisting or antivirus bypass were used for the verified release.

### Launcher / package

- Added native root-level **`UNCANNY.exe`** as the normal public launcher.
- Removed the old top-level `UNCANNY.cmd` from the normal user launch path.
- Native launcher uses the Windows GUI subsystem, starts the bundled launcher without a console flash, prevents duplicate launcher instances and records native startup failures.
- Preserved the already-published UNCANNY 2.5 Lucid ABI 136 engine bundle by its existing manifest hashes so ELYSIUM/Lucid selection remains available.

### Preserved

- Hotfix 10 **UNCANNY PASSES** wiring.
- Separate **DLSS 5 PASSES** control.
- ELYSIUM structural/surface/face/material/depth/color/edge/distant-detail/texture-relief controls.
- PCSX2 wrapper behavior.
- REVENANT runtime functionality.
- install/update/rollback flow.
- provider policy.
- D3D9, D3D10 and D3D12 paths outside this targeted D3D11 startup change.

### Release checks

- Hotfix 9 ELYSIUM regression: PASS.
- Hotfix 10 control-wiring regression: PASS.
- Hotfix 11 D3D11 fail-open regression: PASS.
- native `UNCANNY.exe` regression: PASS.
- internal Windows diagnostic/test binaries compiled in CI and excluded from the public package.
- 16 focused Hotfix 11 acceptance checks: PASS.
- x86/x64 production binaries compiled successfully.
- protected shader authentication/roundtrip verification: PASS.
- PE hardening audit: PASS across all 11 current production/helper binaries.
- strict public package audit and final ZIP integrity: PASS.
- Microsoft Defender cleaned-tree scan: PASS / 0 detections.
- Microsoft Defender final-ZIP scan: PASS / 0 detections.

Release ZIP SHA-256: `a523db2ec0149f139a24c70aba36f68222cba057369b97864615b07c9c356e69`

Real hardware retesting remains required for the original PCSX2/GPU configuration.

---

## v0.20.0-alpha.1 — ELYSIUM Hotfix 10

Runtime revision: `release-alpha.1.elysium-hotfix10`  
ABI: `141`

### Fixed

- HOME-page **UNCANNY PASSES** now controls the native ELYSIUM reconstruction stack instead of accidentally writing the DLSS 5 pass-depth control.
- **DLSS 5 PASSES** remains independent on the DLSS 5 page.
- ELYSIUM structural, surface, face, material, depth/form, color, edge, distant-detail and texture-relief controls are exposed through the live Control Deck and persisted control registry.
- Generated and protected shader-control layouts are synchronized to the current 56-float / 14-register ELYSIUM layout.

### Preserved

- Existing v0.20 launcher UI and game scanning.
- Install/update/rollback flow.
- PCSX2 wrapper behavior.
- REVENANT behavior and provider routing.
- Engine selection and source-protection model.

---

## v0.19.0-alpha.1 — RC2 Hotfix 2

- Improved legacy DLSS 5/Feature-18 helper startup evidence and monitoring.
- Improved D3D9 reset/device-loss behavior.
- Preserved deeper reconstruction scheduling, Motion Guard/Ghosting Guard and REVENANT compatibility work.