# Releases

## Current

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.13**

- BuildId: `elysium45-hf18.13`
- updateSerial: `1930`
- ABI: `143`
- package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.13.zip`
- SHA-256: `c4faffd66ca5addfd7c200b08d46d279c5aa3274fabdae643280242845fca522`

Download:
https://github.com/coye2/UNCANNY/releases/latest

HF18.13 is the D3D12 freeze + launch/session recovery build. It keeps D3D12 Present nonblocking, restores bounded transactional resize handoff, serializes warmup against resize, and hardens deferred attach/stale-session recovery for modern targets.

## Recent

**HF18.12** — moved first-use D3D12 setup off Present and added deferred startup attach.  
**HF18.11** — staged direct-D3D11 neural promotion.  
**HF18.10** — D3D12 startup/resize stabilization.  
**HF18.9** — universal D3D11 stability floor + PCSX2 D3D12 recovery.  
**HF18.8** — updater state and legacy PCSX2 wrapper repair.  
**HF18.7** — sidecar launch architecture and D3D11 Present hardening.

The full development workspace is private. This repo is the public release/support side of UNCANNY.
