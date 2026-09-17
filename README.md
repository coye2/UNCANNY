# UNCANNY

Real-time neural remastering middleware for Windows PC games and emulators.

**Public alpha · NVIDIA RTX · D3D9/10/11/12 · PCSX2**

**[Download](https://github.com/coye2/UNCANNY/releases) · [Join the Discord](https://discord.gg/zMveJN2kDa)**

> The compiled runtime is distributed through **Releases**. This repository contains public documentation and release information; the full development source workspace is private.

## Latest build

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Hotfix 10**  
Runtime: `release-alpha.1.elysium-hotfix10` · ABI `141`

Hotfix 10 fixes the native **UNCANNY PASSES** selector and completes the live ELYSIUM slider wiring. The UNCANNY reconstruction stack and DLSS 5 pass selector are now separate controls.

## Install

1. Download `UNCANNY-v0.20.0-alpha.1-ELYSIUM-HOTFIX10-Windows.zip` from **Releases**.
2. Extract the ZIP completely.
3. Run `UNCANNY.cmd`.
4. Let the launcher scan, or add the real game/emulator executable manually.
5. Choose **Install UNCANNY**, then launch the game.
6. Press **HOME** for the Control Deck.

Full walkthrough: [USAGE.md](USAGE.md)

## ELYSIUM controls

- **UNCANNY PASSES: 1 / 1.5 / 2 / 2.5 / 3** — native ELYSIUM reconstruction depth.
- **DLSS 5 PASSES** — separate neural-route pass control on the DLSS 5 page.
- **Structural reconstruction**
- **Surface detail**
- **Face reconstruction**
- **Material definition**
- **Depth / form recovery**
- **Source color recovery**
- **Material color separation**
- **Fine edge recovery**
- **Distant detail**
- **Texture relief**
- **Motion Guard / Ghosting Guard**

The Hotfix 10 Windows binaries were rebuilt for x86 and x64 and passed the project’s static ELYSIUM wiring and protected-resource checks. Real-GPU visual behavior remains hardware/game dependent and should still be tested with `UNCANNY-STATUS.cmd` evidence.

## Current state

| Path | Status |
|---|---|
| D3D12 | Primary PC test path |
| D3D11 | Active testing |
| PCSX2 | Primary emulator test path |
| D3D9 / D3D10 neural path | Experimental |
| REVENANT | Experimental |
| Vulkan / OpenGL | Not at DirectX parity |

## Community & feedback

**[Join the UNCANNY Discord](https://discord.gg/zMveJN2kDa)** for testing, screenshots, compatibility discussion, bug help and development talk.

For bug reports include the game/emulator, API, x86/x64, GPU/driver, exact UNCANNY revision and `UNCANNY-STATUS.cmd` output when possible.

## Docs

[Usage](USAGE.md) · [Release status](RELEASES.md) · [Compatibility](docs/COMPATIBILITY.md) · [FAQ](docs/FAQ.md) · [Contributing](CONTRIBUTING.md) · [Security](SECURITY.md)

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.
