# UNCANNY

UNCANNY is a real-time graphics remastering project for Windows games and emulators.

The goal is pretty simple: make games look cleaner and more modern without turning setup into a project of its own. ELYSIUM handles the live image work, REVENANT handles experimental asset reconstruction, and the launcher takes care of installs, updates, rollback, profiles and diagnostics.

**Current release:** v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.12

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

people kept asking me to show source. i'm not opening the whole repo, but i did post real current code and explain what it is doing.

D3D11 promotion, Present safety, ELYSIUM, Adaptive Realism, REVENANT, the Deck, launch state. the useful stuff.

[how UNCANNY works](docs/HOW-UNCANNY-WORKS.md)

## HF18.12

HF18.12 is aimed at the exact launch/runtime failures from the latest hardware tests.

PCSX2 could reach gameplay, run for a few seconds, then freeze when the D3D12 path left startup protection. First-use D3D12 setup now happens off Present, and resize/resource cleanup no longer waits on UNCANNY from the game thread.

Cyberpunk and Spider-Man 2 were failing earlier in startup and could leave a stale sidecar session behind. Targets with no static graphics API import can now start natively first and attach UNCANNY afterward. A failed optional attach leaves the game running instead of blocking startup.

HF18.11's staged D3D11 neural promotion is still in place, and PCSX2 remains on Direct3D 12 `Renderer=15`.

## Current status

D3D11 and D3D12 are the main active paths. PCSX2 is the main emulator test target. Older DirectX routes exist but get less capability when the game does not expose enough reliable frame data.

Vulkan and OpenGL are not at DirectX parity yet.

REVENANT is still experimental, especially for native PC games.

UNCANNY is alpha software. CI catches a lot, but real game/GPU behavior still has to be tested on real hardware.

## Download

Latest release:
https://github.com/coye2/UNCANNY/releases/latest

HF18.12 ZIP SHA-256:

`9a7e439967af1b7930769aa29b0a1830afee606ce6246291f4035c5a4927dce6`

More:
- [Usage](USAGE.md)
- [How UNCANNY actually works](docs/HOW-UNCANNY-WORKS.md)
- [Compatibility](docs/COMPATIBILITY.md)
- [FAQ](docs/FAQ.md)
- [Release notes](docs/RELEASE-NOTES.md)
- [Security](SECURITY.md)

## Windows note

The current alpha build is unsigned, so Windows may show SmartScreen / Unknown Publisher. The published HF18.12 package was scanned with Microsoft Defender before release. See [malware verification](docs/MALWARE-VERIFICATION.md).

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.
