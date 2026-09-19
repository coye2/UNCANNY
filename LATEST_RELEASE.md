# Latest release

## UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.13

BuildId: `elysium45-hf18.13`  
updateSerial: `1930`  
ABI: `143`

Download:
https://github.com/coye2/UNCANNY/releases/latest

Package:
`UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.13.zip`

SHA-256:
`c4faffd66ca5addfd7c200b08d46d279c5aa3274fabdae643280242845fca522`

HF18.13 fixes the D3D12 transition regression reproduced by PCSX2 after a few seconds of gameplay. Present stays fail-open. Owned D3D12 resize gets a bounded transactional handoff, and off-Present warmup is serialized against resize for the same swapchain.

It also hardens modern-game launch ownership: native startup first, stable visible-window proof before late attach, and verified stale/headless sidecar recovery without killing a visible target.

PCSX2 remains on Direct3D 12 `Renderer=15`. HF18.11's staged direct-D3D11 neural promotion is preserved.

Exact candidate `982baa13dd2612e8368921ade4322bc99d6d6578` passed the full validation run `35459233640`. Public publication run `35459735287` published the verified package and Defender scan with 0 detections.

Real-game GPU behavior still needs the actual target machine test.
