# UNCANNY

UNCANNY is a real-time graphics remastering project for Windows games and emulators.

The goal is pretty simple: make games look cleaner and more modern without turning setup into a project of its own. ELYSIUM handles the live image work, REVENANT handles experimental asset reconstruction, and the launcher takes care of installs, updates, rollback, profiles and diagnostics.

**Current release:** v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.11

## Quick start

1. Download the latest release ZIP.
2. Extract the whole folder.
3. Run `UNCANNY.exe`.
4. Pick a detected game, or use **Add game**.
5. Click **Install UNCANNY**.
6. Launch the game and press **HOME** for the Control Deck.

If UNCANNY is already installed for that game, use **Update UNCANNY** instead.

## What it does

- ELYSIUM real-time reconstruction and detail recovery
- 1 / 1.5 / 2 / 2.5 / 3 pass modes
- Motion Guard and Ghosting Guard
- Adaptive Realism scene tuning
- optional neural / DLSS 5 integration where the route is available
- REVENANT experimental asset reconstruction
- D3D9, D3D10, D3D11 and D3D12 compatibility work
- per-game settings, diagnostics, rollback and uninstall

The native ELYSIUM path and the optional neural path are separate. A game can be using ELYSIUM correctly even if the neural provider is unavailable.

## How the source actually works

I am not publishing the private source tree, but I did publish a real technical breakdown of the runtime and selected current implementation excerpts.

It covers the frame path, D3D11/D3D12 safety model, ELYSIUM, Adaptive Realism, neural promotion, Motion/Ghosting Guard, REVENANT replacement logic, Control Deck state, sidecar launching and the main failure/fallback rules.

It also has a **Where the Magic Happens** section with real source chunks instead of fake pseudocode.

[Read: How UNCANNY actually works](docs/HOW-UNCANNY-WORKS.md)

## HF18.11

HF18.11 fixes a D3D11 logic bug that kept the neural path disabled forever after the earlier stability work.

Direct D3D11 still starts conservatively so the game gets a healthy native Present stream first. Once the route has been stable long enough, neural resources can warm up and the neural path can become eligible without re-enabling the riskier depth/temporal behavior that caused earlier lockups.

HF18.10's D3D12 startup/resize fix is still in place, and PCSX2 remains on the D3D12 `Renderer=15` route.

## Current status

D3D11 and D3D12 are the main active paths. PCSX2 is the main emulator test target. Older DirectX routes exist but get less capability when the game does not expose enough reliable frame data.

Vulkan and OpenGL are not at DirectX parity yet.

REVENANT is still experimental, especially for native PC games.

UNCANNY is alpha software. CI catches a lot, but real game/GPU behavior still has to be tested on real hardware.

## Download

Latest release:
https://github.com/coye2/UNCANNY/releases/latest

HF18.11 ZIP SHA-256:

`7e4d0f990ab33f10abec01a23ff467e487ad45da2b250cd49b6823b321c3d800`

More:
- [Usage](USAGE.md)
- [How UNCANNY actually works](docs/HOW-UNCANNY-WORKS.md)
- [Compatibility](docs/COMPATIBILITY.md)
- [FAQ](docs/FAQ.md)
- [Release notes](docs/RELEASE-NOTES.md)
- [Security](SECURITY.md)

## Windows note

The current alpha build is unsigned, so Windows may show SmartScreen / Unknown Publisher. The published HF18.11 package was scanned with Microsoft Defender before release. See [malware verification](docs/MALWARE-VERIFICATION.md).

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.
