# UNCANNY

UNCANNY is a real-time graphics remastering project for Windows games and emulators.

The goal is pretty simple: make games look cleaner and more modern without turning setup into a project of its own. ELYSIUM handles the live image work, REVENANT handles experimental asset reconstruction, and the launcher takes care of installs, updates, rollback, profiles and diagnostics.

**Current release:** v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.13

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

## HF18.13

HF18.13 is the launch/runtime recovery build for the failures from the Sept. 19 hardware logs.

HF18.12 moved D3D12 setup off Present, but the new maintenance warmup could race a real renderer resize. HF18.13 keeps Present fail-open, restores a bounded transactional handoff for owned D3D12 resize, and serializes off-Present warmup against that exact swapchain transition.

PCSX2 stays on Direct3D 12 `Renderer=15`.

Modern dynamically-bound games also get the hardened startup path: native startup first, a stable visible top-level window before late attach, and verified stale/headless session recovery without auto-killing a visible game.

HF18.11's staged D3D11 neural promotion is still in place.

## Current status

D3D11 and D3D12 are the main active paths. PCSX2 is the main emulator test target. Older DirectX routes exist but get less capability when the game does not expose enough reliable frame data.

Vulkan and OpenGL are not at DirectX parity yet.

REVENANT is still experimental, especially for native PC games.

UNCANNY is alpha software. CI catches a lot, but real game/GPU behavior still has to be tested on real hardware.

## Download

Latest release:
https://github.com/coye2/UNCANNY/releases/latest

HF18.13 ZIP SHA-256:

`c4faffd66ca5addfd7c200b08d46d279c5aa3274fabdae643280242845fca522`

More:
- [Usage](USAGE.md)
- [How UNCANNY actually works](docs/HOW-UNCANNY-WORKS.md)
- [Compatibility](docs/COMPATIBILITY.md)
- [FAQ](docs/FAQ.md)
- [Release notes](docs/RELEASE-NOTES.md)
- [Security](SECURITY.md)

## Windows note

The current alpha build is unsigned, so Windows may show SmartScreen / Unknown Publisher. The published HF18.13 package was scanned with Microsoft Defender before release. See [malware verification](docs/MALWARE-VERIFICATION.md).

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.
