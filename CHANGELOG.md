# v0.20.0-alpha.1 ELYSIUM Engine 4.5 — HF18.6 — 2026-09-18

`release-alpha.1.elysium-engine45-hf18.6`, ABI 143, BuildId `elysium45-hf18.6`, updateSerial `1860`.

- Removes duplicate full release verification from game install/update.
- Uses streaming PE checks for release-binary architecture validation.
- Validates only the required x64 helper/bridge route for 32-bit titles.
- Carries forward the verified original-game digest instead of repeatedly hashing a large EXE.
- Skips byte-identical installed files before rollback backup/commit.
- Healthy same-build updates use a verified no-op fast path; packaged second pass measured 3884 ms with zero file transaction.
- Reuses a verified existing neural asset core instead of unpacking/re-hashing it again.
- Bounds provider discovery and stops once required provider roles are found.
- Removes unnecessary normal-ELYSIUM engine switching before PCSX2 startup.
- Makes optional REVENANT proof recovery bounded/fail-open for PCSX2.
- Gives PCSX2 a shorter bounded runtime-attach startup budget and allows fail-open resume.
- Adds packaged PCSX2 wrapper acceptance proving verified-original spawn, runtime load, initialization acknowledgement and clean child exit.
- Adds granular 24–95% installer progress to expose real work instead of apparent stalls.
- Preserves HF18.5 scanner/library/logo fixes and all HF18 rendering/runtime behavior.

Exact validated source: `852e617c003a8672ead6bd7607e24163a99b8fc5`  
Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35412014280  
ZIP SHA-256: `3f9bbe8eb520918df9e23a84f879bce8079b197f2e194326430b3be4930be111`

# v0.20.0-alpha.1 ELYSIUM Engine 4.5 — HF18.5 — 2026-09-18

`release-alpha.1.elysium-engine45-hf18.5`, ABI 143, BuildId `elysium45-hf18.5`, updateSerial `1850`.

- Fixes packaged scanner dependency resolution after PowerShell moved under `runtime\`.
- Canonicalizes heterogeneous cache/manual/scan records before WPF binding.
- Removes remaining brittle `Resolve-Path(...).Path` provider-object reads from library discovery helpers.
- Re-encodes the official UNCANNY PNG through 32-bit ARGB before WPF display.
- Adds stack + invocation-position diagnostics for recovered launcher failures.
- Adds exact packaged cache/render/logo and packaged scan execution gates.
- Preserves HF18.4 startup-policy recovery and all HF18 rendering/runtime behavior.

Exact build/package/Windows/cache-render/scan/WARP/hash/Defender validation is required before publication.

# v0.20.0-alpha.1 ELYSIUM Engine 4.5 — HF18.4 — 2026-09-18

`release-alpha.1.elysium-engine45-hf18.4`, ABI 143, BuildId `elysium45-hf18.4`, updateSerial `1840`.

- Fixes launcher startup crashes caused by StrictMode property access on malformed/legacy discovery records.
- Adds guarded WPF startup/selection/action callbacks so malformed records are logged/recovered instead of tearing down `ShowDialog()`.
- Fixes the HF18.3 no-launch regression under Restricted/AllSigned PowerShell policy using a process-scoped policy-independent bootstrap that does not change persistent system/user policy.
- Fixes updater hotfix serial ordering so HF18.4 is discoverable over HF18.3.
- Replaces the raster/poster launcher badge path with a official cropped silver UNCANNY U PNG.
- Adds explicit engine-choice tracking (`UserSelected=1`) to new Control Deck selections.
- Migrates stale/unmarked Lucid preferences to Automatic/ELYSIUM at install and launch time.
- Prevents updated PCSX2 installs from silently booting the preserved Lucid 2.5 Control Deck unless Lucid was explicitly selected by the user.
- Preserves HF18.2 clean public package layout and all HF18 rendering/runtime work.

Exact build/package/Windows/WARP/hash/Defender validation is required before publication.

# v0.20.0-alpha.1 ELYSIUM Engine 4.5 — HF18.2 — 2026-09-18

`release-alpha.1.elysium-engine45-hf18.2`, ABI 143, BuildId `elysium45-hf18.2`, updateSerial `1820`.

- Fixes launcher post-install/update state refresh when a record does not already contain `InstalledBuildId`.
- Normalizes cached, manually-added and newly-scanned game records to one launcher schema.
- Adds direct PE-table target inspection so install/update no longer reads an entire large game executable into memory just to discover architecture/API imports.
- Corrects ELYSIUM launcher emblem crop and centering.
- Cleans the public package root: PowerShell implementation moves to `runtime\`; maintenance CMDs move to `Tools\`; `UNCANNY.exe` stays at root.
- Adds package gates that reject root-level maintenance scripts and parse every shipped runtime PowerShell file after ZIP extraction.
- Preserves HF18 rendering and Universal API Bridge behavior.

Exact build/package/Windows/WARP/hash/Defender validation is required before publication.

# v0.20.0-alpha.1 ELYSIUM Engine 4.5 — HF18.1 — 2026-09-18

`release-alpha.1.elysium-engine45-hf18`, ABI 143, BuildId `elysium45-hf18.1`, updateSerial `1810`.

- Fixes installer/update preflight that could appear stuck at 2% while repeatedly enumerating Windows processes.
- Replaces those repeated full WMI walks with bounded local process inspection for the selected target folder.
- Adds visible 3/4/5/6% preflight progress stages before release-binary verification.
- Fixes launcher update-button text clipping with a wider compact status control and shorter status labels.
- Replaces the monochrome launcher badge with the current full-color ELYSIUM emblem.
- Preserves the HF18 rendering pipeline and Universal API Bridge behavior.

Final package still requires the exact build/package/Windows/WARP/hash/Defender gate before publication.

# v0.20.0-alpha.1 ELYSIUM Engine 4.5 — Adaptive Realism — 2026-09-17

`release-alpha.1.elysium-engine45`, ABI 143.

- Adds original UNCANNY **Adaptive Realism** with OFF / LOW / BALANCED / HIGH / INSANE levels.
- Adaptive Realism is vendor-neutral and does not require DLSS 5, CUDA or Tensor Cores.
- D3D11 can use capability-scored discovered depth plus UNCANNY optical flow for depth-aware contact occlusion and bounded screen-space indirect lighting.
- When trustworthy depth is unavailable, the engine fails safely to spatial/tonal adaptation instead of claiming full GI. D3D9/D3D10/D3D12 currently use reduced capability where scene depth is not trustworthy.
- Scene adaptation derives bounded exposure, highlight/shadow recovery, local contrast, clarity and saturation shaping from the current scene rather than hardcoding the Eternights grade.
- Motion Guard/Ghosting Guard remain authoritative. Flow confidence loss, source disagreement and disocclusion reduce/reject history; X2.5 deliberately uses the lowest temporal-history weight.
- ENABLE UNCANNY OFF remains a true master bypass. The UNCANNY pass stack remains separate from DLSS 5 pass depth.
- Preserves current launcher, clean package structure, PCSX2 scanner/install fixes, rollback, REVENANT, provider handling, DirectX adapters and Hotfix 11/12 safety work.
- CI cross-built production binaries and passed compiled Engine 4.5 acceptance, Python regressions, protected-shader verification and restricted-shader source auditing. Real game/GPU visual acceptance is still required.
- No paid/restricted Marty McFly / Pascal Gilcher shader source or binaries are bundled. The supplied preset was used only as a behavioral calibration reference.

# v0.20.0-alpha.1 ELYSIUM Hotfix 11 - 2026-09-17

`release-alpha.1.elysium-hotfix11`, ABI 141. Tester-derived D3D11 first-frame safety hotfix.

- Fixes a PCSX2 x64 / D3D11 black-screen case where `PRESENT_PATCH_OK` was followed by one Present attempt, zero successful Presents, no advancing presentation stream and 0 FPS.
- Makes direct D3D11 startup fail open: native `Present` / `Present1` gets the first three presentation opportunities before UNCANNY image processing or in-frame HOME composition can run.
- Defers D3D11 Feature-18/DLSS5 initialization until at least 8 successful recent native Presents are advancing.
- Keeps the live source visible while neural startup is deferred; no stale neural result is reused.
- Adds exact Present-stage diagnostics: `PRESENT_PREPROCESS`, `PRESENT_NATIVE_CALL`, `PRESENT1_PREPROCESS`, `PRESENT1_NATIVE_CALL`, and `PRESENT_SUCCEEDED`.
- Correctly treats `Host64LaunchAttempted=0` as normal for the native x64 in-process D3D11 route instead of assuming the helper failed.
- Preserves the tester's working REVENANT path; the triggering report completed 38/38 texture jobs independently of the Present failure.
- Replaces the public top-level `UNCANNY.cmd` entry point with native **`UNCANNY.exe`**. Maintenance CMD tools remain only for install/diagnostics where appropriate.
- Preserves Hotfix 10 ELYSIUM pass/slider wiring, PCSX2 wrapper behavior, engine switching, provider policy, updater/install/rollback and protected shader resources.

The same PCSX2/GPU setup still requires final hardware retest after the exact release binaries are built.

# v0.20.0-alpha.1 ELYSIUM - 2026-09-17

- UNCANNY 4 ELYSIUM promoted to the current ABI 140 engine.
- Final launcher/install/manual-add/PCSX2 discovery polish.
- ELYSIUM/Lucid engine selector fixed to the current ABI and made per-game/transactional.
- Release branding, Control Deck diagnostics and public package identity unified.
- Existing working rendering, REVENANT, provider and rollback paths preserved.

# Alpha RC2 Hotfix 2 — 2026-09-16

`release-alpha.rc2.hotfix.2`, ABI 140, helper protocol 2. No new compatibility certification.

- Acknowledge helper entry/IPC before explicit System32 DXGI/D3D12 loading; remove those graphics DLLs from the helper's loader import table.
- Write a capped helper bootstrap journal for failures before shared-state initialization; decode early exit/loader errors without reusing the parent's starting message as child evidence.
- Monitor helper wall-clock startup/request deadlines outside Present, using existing ownership locks; retain explicit closed-session evidence and trace ages.
- Latch D3D9 lost-device cleanup once per device and clear it after successful Reset/Present, instead of repeated teardown on every lost-device Present.
- Add CPU-only startup fixtures for 32-/64-bit parents with exact helper IPC and invalid-header/parent rejection. No provider counters may increase in this test.
- Independently query reported helper PID/image/parent in saved diagnostics and include the matching bootstrap journal where available.
- Preserve HF1 shared-resource ownership fallback, protected shaders, provider policy, REVENANT safety/inference evidence, deep-neural processing and historical engine bytes.
- Windows/GPU execution remains NOT RUN. The supplied RE4 report still has zero actual Feature-18 and asset inference success; no finished official release is claimed.

# Alpha RC2 Hotfix 1 — 2026-09-15

`release-alpha.rc2.hotfix.1`, ABI 140. Targeted hardware-derived legacy neural startup repair.

- Preserves the D3D12-owned D3D11 interop route when accepted.
- If `OpenSharedResource1` rejects that transport, reverses only transport ownership: D3D11 creates an NT-shared RT/SRV texture and D3D12 opens it on the same adapter.
- Keeps neural output work on a private D3D12 UAV; rejected/failed neural work never overwrites the last accepted shared output.
- Adds a focused `RUN-LEGACY-SHARING-CHECK.cmd` transport-only hardware fixture.
- Preserves RC2 bounded host diagnostics, REVENANT repair path and honest 1–3 neural-stage accounting.
- Windows/NVIDIA legacy Feature-18 success and PCSX2 visible REVENANT use remain hardware acceptance gates.

# Alpha RC2 — 2026-09-15

`release-alpha.rc2`, ABI 140. Continues the verified RC1 private/public pair.

- Replaced masked legacy waiting status with actual process/provider/resource/fence transitions, numeric failures, request receipts and bounded timeouts. Added compatible SDR format cases; no claim of universal legacy success.
- Repaired PCSX2 growing/fragmented-log identity handling and pending reload retention. Preserved actual inference errors and independently hashed source/input/raw output/commit evidence. Checker confirmation no longer certifies neural reconstruction.
- Added original independent full-frame source-detail and source-tone neural refinements, real per-stage GPU query recording and an adaptive motion/cost/VRAM policy. Extra-stage execution and quality remain unverified on GPU.
- Updated one-click saved diagnostics, current acceptance entry points, ABI/provenance/public-private packaging. Preserved prior protection and historical engine bytes.

## Historical Alpha RC1 notes

# Alpha RC1 — 2026-09-15

`release-alpha.rc1`, ABI 139. Continues Repair 8 Hotfix 1; real historical Lucid remains ABI 136.

Added native D3D9 fallback and D3D10/10.1 Feeder/image routes, D3D10 Home compositor, same-adapter x64-helper isolation, current-frame/timeout policy and explicit transfer telemetry. Preserved working native D3D11/12 processing and first-choice On12 behavior.

Added PCSX2 worker supervision and startup errors, pending-request recovery, current-session paired game identity, captured-original cyan proof and journaled exact-absence recovery. Fixed AI-core repair so a failed rollback cannot delete its backup; verified all pinned engine/model hashes before promotion and bounded download time.

Refreshed current Control Deck status/layout and listed existing hotkeys. Added authenticated shader-resource encryption, protected release flags and local Windows decryption/proof fixtures. No screenshot/clip/updater extras. Hardware acceptance remains required; no exact-revision game certification is claimed.

---

## Preserved historical notes

## Repair 8 Hotfix 1

Provider-setup trailing-backslash argument fix; helper stage diagnostics; focus-aware panel fallback and in-game retry. No hardware certification.

# Changelog

## Repair 8 — release-repair.8 — ABI 138

Test candidate, not official. Continues the saved Repair 8 source checkpoint and Repair 7 runtime, not a baseline rewrite.

### Asset safety and recovery
- Fixed WIC encoder pixel-format negotiation; convert into the actual negotiated format and verify exact decoded BGRA/alpha before atomically publishing PNG output.
- Added stable-source settling and isolated inference input snapshots.
- Reject significant source identity/alpha disagreement and unsupported micro-pattern variance before commit. These are conservative heuristics, not semantic correctness guarantees.
- Audit previous receipt-owned replacements during processing; quarantine rejected files after verified backup.
- Added confirmed, receipt-scoped restoration of original PCSX2 textures. Generation pauses; unknown/user-edited/busy files are retained.
- Batch automatic reload input and defer it while the panel is visible.

### Rendering and controls
- Select a GPU-completed D3D12 recording slot independently of current swap-chain buffer index; fence safety remains mandatory. Keep a safe bypass if every slot is busy.
- Return the actual submission fence through D3D9On12.
- Try another available D3D11 neural recording slot rather than unnecessarily skipping a frame.
- Added an integrated Home engine selector for actual current/Lucid builds; full runtime switch remains next-launch.
- Preserve cursor, scrolling/drag/resize, provider-discovery, x64-helper and Ghosting Guard work from Repair 7.

### Evidence
- Windows production binaries rebuilt from the current source with recorded hashes.
- Portable safety/slot tests executed on the build host; WIC/owned-restore regression compiled for Windows.
- Windows gameplay, GPU inference, fullscreen quality, performance and external compatibility have not been executed here.

Not included: universal scene/PBR remodeling, generic D3D12 REVENANT, native inputs across all games, all named historical generations, or instantaneous whole-runtime engine swapping.

## Prior releases

Preserved private history and the Lucid bundle remain unchanged. Old reports are historical evidence, not certification of Repair 8.
