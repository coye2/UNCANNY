# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — Adaptive Realism**

- Runtime: `release-alpha.1.elysium-engine45`
- ABI: `143`
- Published: 2026-09-17
- Latest release: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip
- SHA-256: `f8b13f51cacd96b1b375b566c675d17661f66bb4bb2673cd34edf8e7f5859512`
- Source revision used for the release build: `8f021aafef138784d042d81e2c7287e934d5cf3b`
- Malware verification attachment: `MALWARE-VERIFICATION-ENGINE45.json`

## What changed

Engine 4.5 adds UNCANNY **Adaptive Realism**, a scene-aware remastering layer that is independent from the DLSS 5 provider path.

Five live levels are exposed:

`OFF / LOW / BALANCED / HIGH / INSANE`

The pipeline adapts to available scene evidence instead of pretending every API provides the same data:

- **Tier A:** trustworthy depth + native motion
- **Tier B:** trustworthy depth + UNCANNY optical flow
- **Tier C:** trustworthy depth only; conservative spatial lighting
- **Tier D:** no trustworthy depth; tonal/spatial fallback only

D3D11 currently has the strongest Adaptive Realism path. D3D12 and D3D9 use conservative fallbacks when trustworthy generic scene depth is unavailable.

Motion Guard and Ghosting Guard remain integrated with temporal history rejection. X2.5 intentionally uses the lowest history weight for cleaner motion. `ENABLE UNCANNY OFF` remains the master bypass, and UNCANNY pass depth remains separate from DLSS 5 pass depth.

## Preserved from Hotfix 11/12

- D3D11 fail-open startup
- native root-level `UNCANNY.exe`
- launcher/game scan flow
- install/update/rollback
- PCSX2 handling
- Control Deck
- REVENANT
- provider handling
- D3D9/D3D10/D3D11/D3D12 routes

## Verification

The exact Engine 4.5 release passed:

- full Python regression suite
- Engine 4.5 compiled acceptance: **22 checks PASS**
- Adaptive Realism compiled tests: **x86 PASS / x64 PASS**
- x86/x64 production compilation
- protected-resource checks
- strict public-package audit
- ZIP CRC/member-hash verification
- dynamic Windows install + rollback regression
- restricted third-party shader source/package audit
- Microsoft Defender scan of extracted final package: **0 detections**
- Microsoft Defender scan of completed ZIP: **0 detections**

The public ZIP contains no engine source, debug symbols, nested development archives or internal acceptance-test executables.

No paid/restricted Marty McFly / Pascal Gilcher shader source or binaries are bundled. Reference material was used only for behavioral calibration.

## Remaining acceptance work

CI/build validation does not replace real rendered gameplay testing. Visual quality, compatibility and performance still require title-by-title testing on target NVIDIA, AMD and Intel hardware.