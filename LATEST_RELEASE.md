# Latest release

## UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.11

BuildId: `elysium45-hf18.11`  
updateSerial: `1910`  
ABI: `143`

Download:
https://github.com/coye2/UNCANNY/releases/latest

Package:
`UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.11.zip`

SHA-256:
`7e4d0f990ab33f10abec01a23ff467e487ad45da2b250cd49b6823b321c3d800`

HF18.11 fixes the D3D11 safe path accidentally keeping neural promotion disabled forever. The conservative startup behavior stays in place; neural resources can now warm up after the route has been stable long enough.

HF18.10's D3D12 startup/resize fix and PCSX2's D3D12 `Renderer=15` route are unchanged.

The release passed the project's build, package, Windows launcher/install, WARP, regression and Defender gates. Real-game GPU behavior is still tested separately.
