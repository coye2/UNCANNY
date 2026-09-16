# Changelog

All notable public UNCANNY test-candidate changes are documented here. UNCANNY is under active alpha development; a packaged candidate is not treated as fully verified until its hardware-specific acceptance gates pass.

## v0.19.0-alpha.1 — RC2 Hotfix 2

Runtime revision: `release-alpha.rc2.hotfix.2`  
ABI: `140`  
Helper protocol: `2`

### Legacy DLSS 5 / Feature-18 startup

- Moved neural-helper entry and startup journaling ahead of explicit graphics initialization so early helper failures can be observed instead of disappearing behind a permanent `HOST_LAUNCH` state.
- Removed DXGI/D3D12 from the helper's PE loader-time import table; Windows graphics modules are loaded explicitly after session/parent validation.
- Added explicit startup evidence for mapping, header validation, parent identity, process exit, graphics-module loading and provider initialization boundaries.
- Moved helper monitoring out of the usable-Present dependency so startup/request deadlines can progress during focus loss or a temporarily unusable swap chain.
- Added bounded wall-clock deadlines and retained historical closed/reset-session evidence instead of silently leaving stale startup state current.
- Improved D3D9 device-loss lifecycle so repeated failed Presents do not repeatedly tear down the same state before the application's successful Reset/Present.
- Added `RUN-NEURAL-STARTUP-CHECK.cmd`, a CPU-only exact-helper validation path for 32-bit and 64-bit parent processes. It does not count as neural inference proof.

### Preserved RC2 / Hotfix 1 work

- D3D9/D3D10 compatibility transport and the x86→x64 neural-helper architecture remain intact.
- Shared-texture transport now has a conservative same-adapter ownership fallback for systems that reject the preferred D3D12→D3D11 shared-resource import path.
- Feature-18 create/evaluate/return/present counters remain separate from file detection and transport-only counters.
- Deep Clean stages can schedule up to three meaningful neural contexts when confidence and budget permit; requested depth and actual evaluations are reported separately.
- Motion Guard and Ghosting Guard remain part of later-stage scheduling.
- REVENANT's incremental PCSX2 identity tracking, inference-chain hashes, receipt ownership, backup/restore safeguards and worker liveness reporting remain intact.

### Verification completed on the build host

- 11 production Windows components cross-compiled successfully.
- 77 mixed regression records passed: 50 compile-only and 27 Linux-host execution records.
- 7 ASan/UBSan test executions passed.
- 527 fields / 1,070 compiler-evaluated layout values matched across eight x86/x64 shared structures.
- 79 static release gates and 50 persisted control routes passed.
- 41 PowerShell scripts passed structural audit; the Windows PowerShell runtime was not executed on the Linux build host.
- Public package contains 117 strictly allowlisted files and excludes proprietary C/C++ source, PDBs, object files and nested private archives.

### Still experimental / not yet universal-proof claims

- Broad legacy D3D9/D3D10 Feature-18 inference and rendered-use certification.
- Visible neural REVENANT replacement/persistence/restore proof in stock PCSX2 across representative games.
- Real-GPU quality/performance acceptance for Clean 2/2.5/3.
- Vulkan/OpenGL parity with the current DirectX paths.
- Native-game REVENANT beyond the experimental resource-replacement subset.

Public Windows package SHA-256:

`bac0da28b86076daa18fbdeafb514043fb93e008c1518df9a17805f740754f86`

---

## v0.19.0-alpha.1 — RC2

- Added more precise legacy neural startup diagnostics and one-click runtime evidence capture.
- Expanded legacy-format handling and helper/provider evidence.
- Improved incremental PCSX2 game identity and REVENANT inference receipts.
- Removed the hard one-neural-evaluation ceiling and introduced budgeted deeper Clean-stage scheduling.

## v0.19.0-alpha.1 — RC1

- Added native D3D9 fallback and D3D10/10.1 compatibility work.
- Added x64 neural-helper support for legacy/x86 routes.
- Repaired REVENANT worker startup, pending-request handling and diagnostic checker restore safety.
- Added protected runtime shader resources and public/private package separation.
