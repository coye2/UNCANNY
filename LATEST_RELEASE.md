# Latest release

## UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.12

BuildId: `elysium45-hf18.12`  
updateSerial: `1920`  
ABI: `143`

Download:
https://github.com/coye2/UNCANNY/releases/latest

Package:
`UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.12.zip`

SHA-256:
`9a7e439967af1b7930769aa29b0a1830afee606ce6246291f4035c5a4927dce6`

HF18.12 targets the current D3D12/runtime launch failures: PCSX2 freezing a few seconds into gameplay, plus Cyberpunk / Spider-Man 2 startup failures and stale sidecar ownership.

D3D12 first-use setup now warms off Present and owned resize/resource retirement is nonblocking. PCSX2 stays on Direct3D 12 `Renderer=15`. Dynamically-bound non-PCSX2 targets can use deferred startup attach.

HF18.11's staged direct-D3D11 neural promotion is preserved.

The final clean repack passed the project's production build, package, Windows launcher/install, WARP, sidecar, AllSigned and Defender gates. Real-game GPU behavior is still tested separately.
