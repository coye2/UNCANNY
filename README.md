# UNCANNY v0.20 ELYSIUM — HF18.11

UNCANNY is a Windows real-time reconstruction/remaster runtime for games and emulators.

**HF18.11 is the current public stabilization release.** It restores a staged direct-D3D11 neural path without removing the universal hard-lock safety floor.

## Start

1. Extract the ZIP completely.
2. Double-click **`UNCANNY.exe`**.
3. Select or manually add a game/emulator.
4. Choose **Install UNCANNY** or **Update UNCANNY**.
5. Launch from UNCANNY and press **HOME** for the Control Deck.

## HF18.11 — direct-D3D11 neural promotion

HF18.9 fixed the Fallout/Stray-class D3D11 hard-lock problem by making the conservative current-frame path universal. Review of the current runtime found that this safety floor was also permanently forcing DLSS5/Feature-18 off on every direct-D3D11 frame.

HF18.11 separates those two concerns:

- The universal direct-D3D11 current-frame/fail-open safety floor remains active.
- Neural promotion requires **240 successful ELYSIUM frames**, an advancing/recent native Present stream, and at least **9 seconds** since the active DXGI transition.
- Neural/shared-resource warmup stays on the maintenance thread; Present never waits behind it.
- Native depth, optical-flow temporal history, and the advanced temporal route remain deferred on the direct safe path even after neural becomes eligible.
- If neural output is unavailable, busy, broken, or still warming, the live source frame is retained.
- Resize, fullscreen, target-mode, and color-space transitions revoke promotion and re-arm stabilization.
- The policy is route-wide with no Fallout 4, Stray, or other executable-name exception.

## Preserved HF18.10 / PCSX2 behavior

- HF18.10's universal direct-D3D12 startup and resize protection is unchanged.
- PCSX2 remains explicitly on **Direct3D 12** with `Renderer=15`.
- Verified `UNCANNY.Launch.exe` sidecar launch remains authoritative; selected target executables keep their original names/bytes.
- OneDrive/Cloud Files-aware PCSX2 configuration, legacy-wrapper migration, installer fast paths, rollback, scanner/library fixes, REVENANT, Motion Guard, Ghosting Guard, and X2.5 clean-motion behavior remain preserved.

## Exact validation

Exact tested candidate: `131560b87608e34fd0ede99dc2e16f9c1472d39e`  
Dev-main merge: `a86bc309ea697b4928493f58c16596ad18ef235d`  
Validation run: https://github.com/coye2/uncanny-dev/actions/runs/35424918011  
Public release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45-hf18.11  
ZIP SHA-256: `7e4d0f990ab33f10abec01a23ff467e487ad45da2b250cd49b6823b321c3d800`

The exact candidate passed the static/regression suite, x86/x64 production and Engine 4.5 builds, Windows HLSL, D3D11 WARP visual-quality matrix, packaged install/update/rollback/scanner/PCSX2 sidecar tests, normal and AllSigned launcher startup, exact ZIP integrity, and Microsoft Defender with 0 detections. The public release pipeline independently re-downloaded, hash-verified, identity-checked, and Defender-scanned the artifact before publication.

CI proves the packaged/runtime contracts above. Current Fallout/Stray D3D11 neural output, PCSX2 gameplay, REVENANT visible use, and Feature-18 rendered output still require real target-machine/GPU evidence.

## Windows trust

UNCANNY is currently unsigned. Windows SmartScreen / Unknown Publisher may appear until trusted Authenticode signing is configured.
