# v0.20.0-alpha.2 — Final Alpha

Final Alpha freezes the validated `748f80b6a63f64bc811479b185e00dc45d34c373` candidate before the beta line.

## Verified in the exact candidate

- source-bounded detail governor: controlled overshoot fell from 0.0391917 to 0.0129333
- flat-region variance fell from 0.00182544 to 0.000234787 in the controlled fixture
- conservative water response was measurable but subtle; no dramatic-water claim
- restricted rigid D3D11 replacement changed 48 → 120 triangles
- corrected silhouette error against an independent reference fell 4,464 → 3,816 pixels
- normal-only tests changed real normal buffers while preserving depth exactly
- material targeting produced 65,536 pink target pixels, left 65,536 unrelated pixels exact and restored the original exactly
- x86/x64 production builds and the exact-candidate private CI completed successfully

Validation run: `35683346915`.

## Explicitly not claimed

No real games were exercised by this exact candidate. No approved game geometry profile ships as proof. Universal auto-tessellation, native LOD tracking, animated replacement, automatic rock/gravel displacement, dramatic water geometry and universal DLSS 5 are not claimed.

Beta will continue the newer bridge/REVENANT work separately instead of destabilizing this final alpha checkpoint.
