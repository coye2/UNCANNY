# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — Adaptive Realism**

- Runtime revision: `release-alpha.1.elysium-engine45`
- ABI: `143`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip`
- SHA-256: `f8b13f51cacd96b1b375b566c675d17661f66bb4bb2673cd34edf8e7f5859512`
- Release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45
- Latest-release alias: https://github.com/coye2/UNCANNY/releases/latest

### Engine 4.5 — Adaptive Realism

Engine 4.5 adds a new UNCANNY-native scene-adaptive reconstruction/enhancement layer while preserving the existing launcher, installer, rollback, PCSX2, Control Deck, REVENANT and neural-provider paths.

Five runtime quality levels are exposed:

`OFF / LOW / BALANCED / HIGH / INSANE`

Adaptive Realism scales itself to available scene evidence:

- **Tier A** — trustworthy depth + native motion
- **Tier B** — trustworthy depth + UNCANNY optical flow
- **Tier C** — trustworthy depth only; conservative spatial lighting and no temporal history
- **Tier D** — no trustworthy depth; tonal/spatial fallback only

D3D11 currently provides the strongest route because UNCANNY can use capability-scored discovered depth and its optical-flow path where available. D3D12 and D3D9 remain supported, but fall back conservatively where trustworthy scene depth is not available.

### Motion behavior

- Motion Guard and Ghosting Guard remain authoritative.
- Temporal history is reduced/rejected on low motion confidence, source/history disagreement, depth disagreement and disocclusion.
- X2.5 deliberately uses the lowest temporal-history weight.
- `ENABLE UNCANNY OFF` remains the master bypass.
- UNCANNY pass depth remains independent from DLSS 5 pass depth.

### Preserved compatibility work

Engine 4.5 preserves the earlier Hotfix 11/12 work, including:

- D3D11 fail-open first-frame startup
- native root-level `UNCANNY.exe`
- launcher/game scanning
- install/update/rollback
- PCSX2 wrapper/exact-path handling
- Control Deck
- REVENANT
- provider routing
- D3D9 / D3D10 / D3D11 / D3D12 runtime routes

### Verification before publication

The exact Engine 4.5 release passed:

- full Python regression suite
- Engine 4.5 compiled acceptance: **22 checks PASS**
- Adaptive Realism compiled tests: **x86 PASS / x64 PASS**
- x86/x64 production builds
- protected-resource verification
- Hotfix 11/12 compatibility regressions
- strict public package audit
- final ZIP CRC/member-hash verification
- dynamic Windows install + rollback regression
- restricted third-party shader source/package audit
- Microsoft Defender scan of the extracted final package: **PASS / 0 detections**
- Microsoft Defender scan of the completed ZIP: **PASS / 0 detections**

The public package contains no engine source, debug symbols, nested development archives or internal acceptance-test executables.

No paid/restricted Marty McFly / Pascal Gilcher shader source or binaries are bundled.

### Hardware acceptance still required

The release-gate results establish the tested code/package contract. They do not prove identical visual quality or performance on every game, emulator, GPU or driver.

Real gameplay testing is still required across representative NVIDIA, AMD and Intel hardware, especially for:

1. visible Adaptive Realism response across all five quality levels
2. D3D11 depth/flow quality
3. motion cleanliness and X2.5 behavior
4. D3D12/D3D9 fallback quality
5. REVENANT visible replacement/restore behavior
6. performance impact per title/API

## Previous public milestone — Hotfix 11

Hotfix 11 introduced the D3D11 fail-open startup repair after a PCSX2 x64 session reached the Present hook but never completed a successful native Present. That work is preserved in Engine 4.5.

Historical details remain in [docs/HOTFIX11-D3D11.md](docs/HOTFIX11-D3D11.md).

## Private source/workspace

The engineering source is maintained privately and is not part of the public release. Do not redistribute private source/recovery workspaces.