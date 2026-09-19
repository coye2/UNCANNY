# Changelog

## HF18.12 — 2026-09-19

- Moved first-use D3D12 frame-processor setup off Present so native frames keep advancing while UNCANNY prepares resources.
- Made owned D3D12 resize/resource retirement nonblocking/fail-fast instead of waiting on UNCANNY from the game thread.
- Kept PCSX2 on Direct3D 12 `Renderer=15` while targeting the reproduced "gameplay for a few seconds, then hard-freeze" transition.
- Added deferred startup attach for non-PCSX2 targets with no static graphics API import.
- Added bounded stale sidecar recovery so a crashed launch does not keep returning `SESSION_ALREADY_TRACKED PID=0`.
- Preserved HF18.11 staged direct-D3D11 neural promotion.

BuildId: `elysium45-hf18.12`  
updateSerial: `1920`  
ZIP SHA-256: `8aaa41cb7062ef92ad1ec216ca36a0a2fbddb32632d5746d022e8f5da38c2b41`

## HF18.11 — 2026-09-19

- Fixed direct-D3D11 neural promotion being permanently blocked by the stability floor.
- D3D11 now gets a protected native-only startup period, then allows neural warmup/promotion after the route stays healthy.
- Kept direct-depth, optical-flow history and the riskier temporal route disabled on the D3D11 safe path.
- Kept neural/resource warmup off Present.
- Preserved the HF18.10 D3D12 startup/resize fix and PCSX2 `Renderer=15` route.

BuildId: `elysium45-hf18.11`  
updateSerial: `1910`  
ZIP SHA-256: `7e4d0f990ab33f10abec01a23ff467e487ad45da2b250cd49b6823b321c3d800`

## HF18.10 — 2026-09-19

- Added a longer native-only startup/transition floor for direct D3D12.
- Let early D3D12 resize calls pass through before UNCANNY owns swapchain resources.
- Added bounded resource retirement for later resize events.

## HF18.9 — 2026-09-19

- Replaced title-specific Fallout/Stray D3D11 handling with one route-wide stability policy.
- Restored PCSX2 to Direct3D 12 and `Renderer=15`.
- Made renderer drift repairable through a normal update.

## HF18.8 — 2026-09-19

- Fixed the install/update loop caused by CRLF sidecar state parsing.
- Added recovery for old PCSX2 installs where the original executable had been replaced by a wrapper.

## HF18.7 — 2026-09-19

- Moved launches to the verified `UNCANNY.Launch.exe` sidecar model.
- Kept selected game/emulator executables untouched.
- Added PCSX2 Cloud Files support.
- Moved D3D11 provider/neural setup out of Present.

## HF18.6 and earlier

HF18.6 focused on install/update speed and PCSX2 startup. Earlier ELYSIUM builds introduced the current launcher, Adaptive Realism, pass controls, Motion/Ghosting Guard, REVENANT work and the Universal API Bridge.

Older detail is still available in Git history and the GitHub release history.
