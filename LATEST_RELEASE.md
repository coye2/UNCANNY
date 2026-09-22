# Latest release candidate

## UNCANNY v0.20.0-alpha.2 — Final Alpha — ELYSIUM Engine 4.5

Exact private candidate: `748f80b6a63f64bc811479b185e00dc45d34c373`  
Validation run: `35683346915`

This is the final alpha checkpoint before beta.

Verified controlled evidence includes the detail/noise governor, conservative water recovery, restricted rigid D3D11 geometry replacement, normal-only recovery, isolated material replacement/restoration, motion fixtures and production x86/x64 builds.

Material proof: 65,536 target pixels pink; 65,536 unrelated pixels byte-identical; exact restoration.

Geometry proof: 48 → 120 triangles; independent silhouette-reference error 4,464 → 3,816 pixels; unrelated visible component preserved.

No real-game run was part of this exact candidate. Synthetic evidence is not presented as real-game certification.

The public package is intentionally stripped of private source, internal test executables, CI evidence and developer tooling.
