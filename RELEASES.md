# Release Status

## Current packaged candidate

**UNCANNY v0.19.0-alpha.1 — Alpha RC2 Hotfix 2**

- Runtime revision: `release-alpha.rc2.hotfix.2`
- ABI: `140`
- Helper protocol: `2`
- Windows package name: `UNCANNY-v0.19.0-alpha.1-ALPHA-RC2-HOTFIX-2-Windows.zip`
- Windows package SHA-256: `bac0da28b86076daa18fbdeafb514043fb93e008c1518df9a17805f740754f86`

### Build-host verification

- 11 production Windows components cross-compiled successfully.
- 77 mixed regression records passed: 50 compile-only and 27 Linux-host execution records.
- 7 ASan/UBSan executions passed.
- 527 shared fields / 1,070 x86/x64 layout values matched.
- 79 static release gates and 50 persisted control routes passed.
- Public package inventory: 117 strictly allowlisted files.
- Public package excludes proprietary C/C++ source, PDBs, objects and nested private archives.

### Release classification

This package is a **public test candidate** while the remaining Windows/NVIDIA/PCSX2 rendered-acceptance gates are completed.

The project intentionally does not translate compilation, transport fixtures or provider-file detection into claims of universal DLSS 5 success.

### Remaining headline acceptance gates

1. Broad legacy D3D9/D3D10 Feature-18 create/evaluate/return/present proof.
2. End-to-end visible neural REVENANT replacement/persistence/restore proof on PCSX2.
3. Real-GPU quality, motion and frametime acceptance for deeper Clean 2/2.5/3 stages.
4. Regression testing of already-working D3D11/D3D12 and PCSX2 paths.

## Private source/workspace

The private source recovery workspace is intentionally **not** a public release artifact. Do not request, mirror or redistribute private recovery packages as public builds.

## Version naming

The product version can remain `v0.19.0-alpha.1` while engineering candidates advance through `RC` and `Hotfix` revisions. The runtime revision and ABI are the authoritative way to identify a specific installed candidate.
