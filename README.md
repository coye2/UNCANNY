# UNCANNY

Real-time neural remastering middleware for Windows PC games and emulators.

**Public alpha · NVIDIA RTX · D3D9/10/11/12 · PCSX2**

**[Download](https://github.com/coye2/UNCANNY/releases) · [Join the Discord](https://discord.gg/zMveJN2kDa)**

> The compiled runtime is distributed through **Releases**. This repository contains public documentation and release information; the full development source workspace is private.

## Latest build

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Hotfix 11**  
Runtime: `release-alpha.1.elysium-hotfix11` · ABI `141`

Release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-hotfix11

SHA-256: `a523db2ec0149f139a24c70aba36f68222cba057369b97864615b07c9c356e69`

Hotfix 11 is a targeted D3D11 startup-safety repair based directly on a PCSX2 x64 tester report. The affected session successfully captured the D3D11 device/swapchain and installed the Present hook, but then stopped with one Present attempt, zero successful Presents, no advancing presentation stream and 0 FPS.

Hotfix 11 changes that ordering so optional UNCANNY processing cannot become a prerequisite for the first visible game frame.

### D3D11 fail-open startup

- The first direct-D3D11 presentation opportunities prioritize the game's original `Present` / `Present1`.
- UNCANNY image preprocessing and in-frame Control Deck composition are deferred during the short native warmup.
- Feature-18 / DLSS 5 initialization waits for a healthy, advancing native Present stream before starting D3D11 neural interop.
- While neural startup is deferred, the current live source remains authoritative; UNCANNY does not substitute a stale neural result.
- New diagnostic stages identify whether a future stall occurred before or inside the game's native Present call: `PRESENT_PREPROCESS`, `PRESENT_NATIVE_CALL`, `PRESENT1_PREPROCESS`, `PRESENT1_NATIVE_CALL`, and `PRESENT_SUCCEEDED`.

The tester also reported 38/38 successful REVENANT texture jobs while presentation was stalled, so Hotfix 11 deliberately leaves that independent path intact.

`Host64LaunchAttempted=0` is not automatically a failure on an x64 D3D11 target. The normal native x64 route can use the in-process bridge; a separate x64 helper is not required for every D3D11 session.

## Security packaging correction

The Hotfix 11 public ZIP was repackaged after Windows Defender flagged `diagnostics/revenant-commit32.exe`. That executable is an internal REVENANT acceptance-test harness, not a runtime dependency, and should not have been present in the public package.

The current release:

- ships **no internal test/diagnostic executables**
- ships no `revenant-commit32.exe` or `revenant-commit64.exe`
- passed a Microsoft Defender scan of the cleaned runtime tree with updated signatures
- passed a second Microsoft Defender scan of the completed release ZIP
- recorded **0 detections** in both release-gate scans
- includes `docs/MALWARE-VERIFICATION.md` inside the ZIP
- includes `MALWARE-VERIFICATION-HOTFIX11.json` beside the ZIP on the GitHub release

Defender release gate: engine `1.1.26080.3`, signatures `1.459.256.0`, product `4.18.26080.3`.

Full verification record: [docs/MALWARE-VERIFICATION.md](docs/MALWARE-VERIFICATION.md)

## Install

1. Download `UNCANNY-v0.20.0-alpha.1-ELYSIUM-HOTFIX11.zip` from the Hotfix 11 release.
2. Extract the ZIP completely.
3. Double-click **`UNCANNY.exe`** at the root of the extracted folder.
4. Let the launcher scan, or add the real game/emulator executable manually.
5. Choose **Install UNCANNY**, then launch the game.
6. Press **HOME** for the Control Deck.

`UNCANNY.exe` is now the normal public launcher. The old top-level `UNCANNY.cmd` entry point is not shipped as the user-facing launcher. Maintenance CMD tools remain where they are useful for diagnostics/install tasks.

Full walkthrough: [USAGE.md](USAGE.md)

## ELYSIUM controls

Hotfix 11 preserves the Hotfix 10 control-wiring repair:

- **UNCANNY PASSES: 1 / 1.5 / 2 / 2.5 / 3** — native ELYSIUM reconstruction depth.
- **DLSS 5 PASSES** — separate neural-route pass control on the DLSS 5 page.
- Structural reconstruction
- Surface detail
- Face reconstruction
- Material definition
- Depth / form recovery
- Source color recovery
- Material color separation
- Fine edge recovery
- Distant detail
- Texture relief
- Motion Guard / Ghosting Guard

## Verification

The exact Hotfix 11 public build passed:

- Hotfix 9 ELYSIUM regression
- Hotfix 10 control-wiring regression
- Hotfix 11 D3D11 fail-open regression
- native `UNCANNY.exe` regression
- internal Windows test binaries compiled in CI but excluded from the public runtime package
- 16 focused Hotfix 11 acceptance checks
- x86 + x64 production builds
- protected shader verification
- PE hardening checks across all 11 current production/helper binaries
- strict public-package audit and ZIP integrity check
- Microsoft Defender scan of the cleaned runtime tree: **PASS / 0 detections**
- Microsoft Defender scan of the final ZIP: **PASS / 0 detections**

These build/host checks do not replace the final hardware retest. The original PCSX2/GPU setup should be rerun to establish that the black-screen regression is gone in real use.

## Current state

| Path | Status |
|---|---|
| D3D12 | Primary PC test path |
| D3D11 | Active support; Hotfix 11 adds first-frame fail-open startup |
| PCSX2 | Primary emulator test path; Hotfix 11 tester regression target |
| D3D9 / D3D10 neural path | Experimental |
| REVENANT | Experimental; separate from the Hotfix 11 Present fix |
| Vulkan / OpenGL | Not at DirectX parity |

## Community & feedback

**[Join the UNCANNY Discord](https://discord.gg/zMveJN2kDa)** for testing, screenshots, compatibility discussion, bug help and development talk.

For D3D11/PCSX2 reports, include `PresentAttempts`, `Presents`, `PresentAdvancing`, FPS, `AttachmentStage`, Feature-18 create/evaluate counters, game/emulator, API, x86/x64, GPU/driver, exact revision and the full `UNCANNY-STATUS.cmd` output when possible.

## Docs

[Usage](USAGE.md) · [Release status](RELEASES.md) · [Malware verification](docs/MALWARE-VERIFICATION.md) · [Hotfix 11 D3D11 report](docs/HOTFIX11-D3D11.md) · [Compatibility](docs/COMPATIBILITY.md) · [FAQ](docs/FAQ.md) · [Contributing](CONTRIBUTING.md) · [Security](SECURITY.md)

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.