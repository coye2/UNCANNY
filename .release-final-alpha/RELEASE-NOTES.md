# UNCANNY v0.20.0-alpha.2 — FINAL ALPHA

last alpha before beta.

## ELYSIUM
- cleaner source-bounded detail reconstruction
- major reduction in crunchy/high-frequency noise
- reduced edge overshoot and haloing
- reduced flat-surface noise
- better color/tone preservation while detail guards are active
- stronger protection against unsupported/invented detail
- expanded controlled motion testing across faces, foliage, thin geometry, specular surfaces and water

## WATER
- new depth/history-gated water recovery
- matched water OFF/ON testing
- temporal/disocclusion/confidence protection
- false-positive protection for non-water surfaces
- automatically backs off when required frame data is not trustworthy

## REVENANT / GEOMETRY
- verified restricted D3D11 rigid-mesh replacement path
- adaptive subdivision on approved rigid geometry
- controlled geometry test: **48 → 120 triangles**
- actual rasterized depth changes verified
- corrected silhouette moved closer to an independent dense reference
- unrelated scene geometry remained unchanged
- smooth-normal recovery
- normal-only enhancement can preserve original depth exactly
- hard-edge / UV-boundary protection

## MATERIALS
- content-identified material targeting
- replacement through the actual D3D11 binding path
- **65,536 target pixels changed**
- **65,536 unrelated pixels remained exact**
- exact original restoration verified

## RUNTIME / COMPATIBILITY
- continued D3D11 runtime/attachment stabilization
- D3D12 compatibility work preserved
- PCSX2 recovery work preserved
- legacy/API bridge regression coverage
- provider lifecycle regression coverage
- safer fail-open behavior when advanced processing cannot be trusted
- protected-resource regression checks
- Control Deck regression coverage

## VALIDATION
- production x86 + x64 builds passed
- WARP + NVIDIA GPU testing
- x86 + x64 geometry/material testing
- expanded static, Windows, provider, geometry and Control Deck suites
- lossless image/depth evidence + SHA256 manifests
- 1080p GPU timing instrumentation
- exact-candidate private CI passed
- public package boundary audit passed
- Microsoft Defender publication gate passed

## IMPORTANT
this is the stable checkpoint before beta. controlled geometry/material tests are not being passed off as real-game certification.

the newer DLSS5 bridge work was intentionally kept out of Final Alpha because it is not finished/certified yet.

## NEXT: BETA
- finish + optimize the universal DLSS5 bridge
- reduce neural performance cost
- real-game proof across DX12 / DX11 / PCSX2 / legacy routes
- deeper REVENANT geometry
- better rock / concrete / gravel reconstruction
- stronger water
- push geometry beyond the current restricted rigid path

Exact private candidate: `748f80b6a63f64bc811479b185e00dc45d34c373`  
Validation run: `35683346915`

**ZIP SHA-256:**  
`673fa1a7ee9dbee10f67d656da24f0c4a53df2e5f384cc6f3026f1145263dc8a`

