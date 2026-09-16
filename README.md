# UNCANNY

Real-time neural remastering middleware for Windows PC games and emulators.

**Public alpha · NVIDIA RTX · D3D9/10/11/12 · PCSX2**

> The compiled runtime is distributed through **Releases**. This repository contains public documentation and release information; the full development source workspace is not public.

## Install

1. Download the latest `UNCANNY-...-Windows.zip` from **Releases**.
2. Extract it.
3. Drag the game/emulator `.exe` onto `INSTALL-NATIVE.cmd`.
4. Launch normally.
5. Press **Home** for the Control Deck.

Full walkthrough: [USAGE.md](USAGE.md)

## What it does

- **Clean 1 / 1.5 / 2 / 2.5 / 3** — adaptive reconstruction-depth modes.
- **Motion Guard / Ghosting Guard** — reduces aggressive reconstruction when temporal confidence is poor.
- **DLSS 5 / Feature-18 integration** — neural rendering with runtime evidence/diagnostics.
- **REVENANT** — experimental persistent asset reconstruction, currently focused on PCSX2.
- **Legacy compatibility** — x86/x64 and D3D9/10/11/12 runtime work.
- **Control Deck + rollback** — per-game controls, diagnostics, backups and restoration.

## Current state

| Path | Status |
|---|---|
| D3D12 | Primary PC test path |
| D3D11 | Active testing |
| PCSX2 | Primary emulator test path |
| D3D9 / D3D10 neural path | Experimental |
| REVENANT | Experimental |
| Vulkan / OpenGL | Not at DirectX parity |

UNCANNY is an alpha. Working runtime attachment does not automatically prove neural output is reaching presentation; use `UNCANNY-STATUS.cmd` when testing.

## Latest build

**v0.19.0-alpha.1 — Alpha RC2 Hotfix 2**  
Runtime: `release-alpha.rc2.hotfix.2` · ABI `140`

See [Releases](RELEASES.md) and [CHANGELOG.md](CHANGELOG.md).

## Feedback

Different GPUs, games and APIs are useful right now. For bugs, include the game, API, x86/x64, GPU/driver, what happened and `UNCANNY-STATUS.cmd` output when possible.

## Docs

[Usage](USAGE.md) · [Compatibility](docs/COMPATIBILITY.md) · [FAQ](docs/FAQ.md) · [Contributing](CONTRIBUTING.md) · [Security](SECURITY.md)

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.
