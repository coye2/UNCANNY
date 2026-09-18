# Changelog

## v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.3

- Fixed launcher startup/ShowDialog crashes caused by missing legacy discovery properties under StrictMode.
- Hardened startup/selection/action event callbacks so malformed cached/discovery entries are skipped and logged.
- Replaced the synthetic vector-style launcher badge with the official tightly cropped silver UNCANNY U emblem PNG.
- Added explicit engine-choice tracking via `UserSelected=1`.
- Migrated stale unmarked `release-fix.5` preferences to Automatic/ELYSIUM during install and launch.
- Prevents a successful current update from silently restoring the old Lucid HOME menu unless Lucid was explicitly selected.
- Hardened cached/manual/installed-game path normalization so missing `.Path`/schema properties cannot crash the launcher.
- Removed `-ExecutionPolicy Bypass` from the native desktop EXE bootstrap; launch remains hidden/non-interactive.
- Added Windows stale-Lucid migration regression and final packaged-launcher startup survival smoke test.
- Preserved HF18.2 clean package layout and HF18 rendering/Universal API Bridge behavior.
- Validation: https://github.com/coye2/uncanny-dev/actions/runs/35393751767
- Source: `47841050ac5fbb04ffaa90823e2d0adc5c9236da`
- SHA-256: `9748039fefcbbe941ea3d67cb54b731798d35b7332643677a3a28b4398fbcb21`
- Defender final ZIP + extracted tree: **PASS / 0 detections**

---

## v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.1

- Fixed install/update preflight that could appear stuck at 2%.
- Replaced repeated full WMI process enumeration with bounded local target-folder process inspection.
- Added granular 3/4/5/6/7% preflight progress.
- Fixed updater status-button clipping with a wider compact control and shorter status labels.
- Replaced launcher monochrome badge with the current full-color ELYSIUM emblem.
- Preserved HF18 rendering and Universal API Bridge behavior.
- Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35383983512
- x86/x64 production builds: **PASS**
- HLSL + WARP rendered-quality gate: **PASS**
- Windows installer/rollback/manual-add: **PASS**
- ZIP integrity/hash: **PASS**
- Microsoft Defender ZIP + extracted tree: **PASS / 0 detections**
- Source revision: `458dc5820beb9322c7ee115ed98fd07a7b1b0c77`
- SHA-256: `82257f00d4c323853fef1b5576578d6b0b025b44829c17027c46019ece726777`

---

## v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18

- Generalized D3D11 native-Present startup stabilization to require 120 successful native Presents before optional preprocessing joins a new swapchain.
- Expanded the Universal API Bridge with deterministic capability, ownership, route-group, processing-source and fail-open handling across legacy and modern graphics routes.
- Added creation-captured D3D12 queue/backbuffer/state evidence; ambiguous ownership is never guessed.
- Preserved conservative Vulkan/OpenGL/legacy presentation and lifecycle observation without claiming unsupported full ELYSIUM/neural parity.
- Added visible Control Deck info/help metadata for live image controls.
- Strengthened source-backed facial reconstruction, source-hue/color recovery, material definition, edge recovery and Microtexture response.
- Fixed Motion Protection Strength being masked by Ghosting Guard; both now remain independently effective.
- Added clean-room local exposure fusion, source-radiance recovery, depth-proven relighting/contact shaping, contrast-adaptive clarity/sharpening and source-directed subpixel edge resolve.
- Improved installer verification diagnostics, updater release-name matching and ownership-safe uninstall cleanup.
- Added D3D11 WARP rendered visual-quality acceptance: all 42 exposed floating image controls must change rendered output above the meaningful response floor, with targeted face/color/denoise/edge/reference-quality checks.
- Exact candidate run: https://github.com/coye2/uncanny-dev/actions/runs/35377702421
- x86/x64 production + legacy + acceptance builds: **PASS**.
- Windows HLSL compile: **PASS**.
- WARP rendered visual-quality gate: **PASS**.
- Manual Add / installer / rollback regressions: **PASS**.
- ZIP integrity/hash verification: **PASS**.
- Microsoft Defender final ZIP + extracted tree: **PASS / 0 detections**.
- Source revision: `0c5de983a400dd77d85992c6a5c1d37bcc3139eb`.
- Runtime revision: `release-alpha.1.elysium-engine45-hf18`.
- BuildId: `elysium45-hf18`; updateSerial: `1800`.
- ZIP SHA-256: `21f654c3260a3c258f7121574edef56c44a718449c16f51aa20d7695bc925489`.

Real-game visual, motion and performance acceptance remains title/GPU/driver specific. No proprietary restricted shader implementation is bundled.

---


## v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF16

- Added bounded post-FX fault backoff that preserves native Present during repeated rendering/device instability.
- Added staged session-local ELYSIUM recovery: safer Adaptive Realism/Performance Guard first, then reduced Reference Stack/pass depth/optional DLSS 5 cost if instability persists.
- Saved user settings are not overwritten by recovery.
- Added sustained-clean-frame requirement before restoring higher-cost rendering to prevent oscillation.
- Added diagnostics: `PostFxRecoveryFaults`, `PostFxRecoveryCleanFrames`, `PostFxRecoveryBackoffMs`.
- Preserved all HF15 launcher/library/rollback/Adaptive Realism/Motion Guard/PCSX2/REVENANT work.
- Exact candidate run: https://github.com/coye2/uncanny-dev/actions/runs/35305423361
- x86/x64 production + acceptance builds: **PASS**.
- Windows HLSL compile: **PASS**.
- Manual Add game persistence: **PASS**.
- Dynamic install/remove rollback: **PASS**.
- ZIP integrity/hash verification: **PASS**.
- Microsoft Defender final ZIP + extracted tree: **PASS / 0 detections**.
- Source revision: `6c7ee4675a110fceb3c2c5bdddf82eb4d2745471`.
- ZIP SHA-256: `fb9a49e68ef11ba8b6e5932e37eee01b4875d7fb782249b92965601dc93e381a`.

---

## v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF15

- Added persisted **Scan on startup** control; disabling it prevents discovery at boot while preserving cached/manual entries.
- Fixed **Add game** persistence so manual entries survive reboot independently of scanning.
- Canonicalized Windows short/long path aliases before manual-library deduplication.
- Added a Windows manual-library preflight to fail release validation before expensive build/package work.
- Preserved per-target BuildId update detection, full-stack Remove, rollback, PCSX2, REVENANT and DLSS 5 routing.
- Expanded Adaptive Realism with Shared Scene Evidence Bus, split contact/diffuse lighting, Emissive Bounce Guard, Black Floor Intelligence, asymmetric local contrast, Legacy Cinema Reconstruction v2 and High/Insane Depth Material Sculpt.
- Motion Guard, Ghosting Guard and X2.5 clean-motion behavior remain protected.
- Exact candidate run: https://github.com/coye2/uncanny-dev/actions/runs/35302273751
- Windows manual Add game persistence: **PASS**.
- Windows install/remove rollback: **PASS**.
- x86/x64 production builds and Engine 4.5 compiled acceptance: **PASS**.
- HLSL compilation and PowerShell parse: **PASS**.
- Package/restricted-shader audits and ZIP integrity/hash verification: **PASS**.
- Microsoft Defender final ZIP + extracted tree: **PASS / 0 detections**.
- Source revision: `b253880333ce2b8e4036cd5e53a6dcaf3bc69f8d`.
- ZIP SHA-256: `8ea0f3742fc52595eb1b95597ab3112d50be5867abfa6193fb4d5f5465e6460d`.

---

## v0.20.0-alpha.1 — ELYSIUM Engine 4.5 Hotfix 13

- Remove now unwinds every recorded UNCANNY install layer for the exact selected target.
- Generated ReShade/OptiScaler/dlss5-feed logs no longer block restore.
- Original/user-file conflict protection remains strict.
- Restored the UNCANNY launcher emblem as an inline vector.
- Adaptive Realism now exposes OFF / LOW / BALANCED / HIGH / INSANE in the live Control Deck.
- New installs seed INSANE + Reference Stack.
- Strengthened source/evidence-bounded AO, indirect diffuse/specular response, exposure adaptation, local contrast and meso clarity.
- Regenerated protected shader resources and passed authentication/tamper checks.
- Windows dynamic two-layer rollback and changed-ReShade.log regressions: PASS.
- Windows HLSL compile: PASS.
- Microsoft Defender: PASS / 0 detections.
- Source revision: `16ee9cb8ef9cdb9f038577884bb023909743d1e1`.
- ZIP SHA-256: `843e8a37b32b81c58035cd2d6c70c7288489a5fc1e221527ca7b36767d1e0811`.

---

All notable public UNCANNY alpha changes are documented here.

## v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — Adaptive Realism

Runtime revision: `release-alpha.1.elysium-engine45`  
ABI: `143`

### Adaptive Realism

- Added five live quality levels: **OFF / LOW / BALANCED / HIGH / INSANE**.
- Added capability-tiered scene handling instead of assuming identical data on every API.
- Tier A uses trustworthy depth + native motion.
- Tier B uses trustworthy depth + UNCANNY optical flow.
- Tier C uses trustworthy depth with conservative spatial lighting and no temporal history.
- Tier D uses tonal/spatial enhancement only when trustworthy scene depth is unavailable.
- Added scene-adaptive exposure, highlight/shadow response, local contrast, clarity and bounded saturation correction.
- Added depth-aware contact occlusion and bounded screen-space diffuse/specular support where the scene evidence is trustworthy.
- Added performance-guard degradation that reduces samples/intensity before disabling the feature.

### Motion / temporal behavior

- Motion Guard and Ghosting Guard remain authoritative.
- Temporal history is reduced/rejected when motion confidence is low, depth disagrees, source/history structure disagrees or disocclusion is detected.
- X2.5 now deliberately carries the lowest temporal-history weight for the cleanest motion behavior.
- `ENABLE UNCANNY OFF` remains the master bypass.
- UNCANNY pass depth remains separate from DLSS 5 pass depth.

### API behavior

- D3D11 can use capability-scored discovered depth plus UNCANNY optical flow and is the strongest current Adaptive Realism route.
- D3D12 preserves runtime support but does not claim generic trustworthy scene depth where the route cannot establish it; Adaptive Realism falls back accordingly.
- D3D9 preserves the legacy runtime path and uses conservative fallback when trustworthy depth is unavailable.
- D3D10/10.1 remain compatibility paths with behavior determined by available evidence.

### Preserved

- Hotfix 11 D3D11 fail-open startup behavior.
- native root-level `UNCANNY.exe` launcher.
- launcher/game scanning and exact-path handling.
- install/update/rollback.
- PCSX2 integration.
- Control Deck.
- REVENANT.
- provider handling and DLSS 5 cooperation.
- protected runtime/package model.

### Release checks

- Full Python regression suite: PASS.
- Engine 4.5 compiled acceptance: **22 checks PASS**.
- Adaptive Realism compiled tests: **x86 PASS / x64 PASS**.
- x86/x64 production builds: PASS.
- protected-resource verification: PASS.
- Hotfix 11/12 regressions: PASS.
- dynamic Windows install + rollback regression: PASS.
- strict public-package audit: PASS.
- final ZIP CRC/member-hash verification: PASS.
- restricted third-party shader source/package audit: PASS.
- Microsoft Defender extracted-package scan: **0 detections**.
- Microsoft Defender completed-ZIP scan: **0 detections**.

Release ZIP SHA-256: `f8b13f51cacd96b1b375b566c675d17661f66bb4bb2673cd34edf8e7f5859512`

No paid/restricted Marty McFly / Pascal Gilcher shader source or binaries are bundled. Real-game visual/performance acceptance remains a hardware/title-specific test requirement.

---

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
- Removed `revenant-commit32.exe` and `revenant-commit64.exe` from public distribution. These are internal acceptance-test harnesses, not runtime requirements.
- Internal diagnostic/test binaries remain available to CI but are no longer part of the user-facing release ZIP.
- Added a Microsoft Defender release gate on a fresh GitHub-hosted Windows runner.
- Cleaned runtime tree scan: **PASS / 0 detections**.
- Final completed ZIP scan: **PASS / 0 detections**.

### Launcher / package

- Added native root-level **`UNCANNY.exe`** as the normal public launcher.
- Removed the old top-level `UNCANNY.cmd` from the normal user launch path.
- Preserved the already-published UNCANNY 2.5 Lucid ABI 136 engine bundle by its existing manifest hashes.

---

## v0.20.0-alpha.1 — ELYSIUM Hotfix 10

Runtime revision: `release-alpha.1.elysium-hotfix10`  
ABI: `141`

### Fixed

- HOME-page **UNCANNY PASSES** now controls the native ELYSIUM reconstruction stack instead of accidentally writing the DLSS 5 pass-depth control.
- **DLSS 5 PASSES** remains independent on the DLSS 5 page.
- ELYSIUM structural, surface, face, material, depth/form, color, edge, distant-detail and texture-relief controls are exposed through the live Control Deck and persisted control registry.
- Generated and protected shader-control layouts are synchronized to the current ELYSIUM layout.

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