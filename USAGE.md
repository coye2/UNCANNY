# UNCANNY Usage

UNCANNY is currently a Windows/NVIDIA RTX public alpha. The compiled runtime is distributed through **GitHub Releases**; the repository itself is not a complete source distribution.

## Install

1. Download the latest public `UNCANNY-...-Windows.zip` from **Releases**.
2. Extract the entire ZIP. Do not run it from inside the archive.
3. Find the actual game or emulator `.exe` that renders the game.
4. Drag that `.exe` onto `INSTALL-NATIVE.cmd`.
5. Let the installer create its backup and install the appropriate runtime.
6. Launch the game or emulator normally.

Do not use a package marked `PRIVATE-WORKSPACE-RECOVERY`.

## First run

1. Reach gameplay.
2. Press **Home** to open the UNCANNY Control Deck.
3. Turn **ENABLE UNCANNY** on.
4. Start with **Clean 1** and leave Motion Guard/Ghosting Guard enabled.
5. Compare the same scene with UNCANNY off and on.
6. If the title is stable, try deeper Clean modes.

If Home causes an exclusive-fullscreen title to minimize, try borderless/windowed mode and report the behavior.

## Clean modes

`1 / 1.5 / 2 / 2.5 / 3` represent increasing reconstruction depth. They are not intended to be repeated sharpening presets or blindly repeated identical neural passes. Higher modes can cost more GPU time and remain under real-hardware validation.

## DLSS / neural verification

A loaded DLL or working overlay does not prove neural rendering is contributing. Run `UNCANNY-STATUS.cmd` after testing and check whether feature creation/evaluation succeeds and whether neural output reaches presentation.

D3D9/D3D10 neural execution remains experimental. D3D11/D3D12 and PCSX2 are currently the primary test paths.

## REVENANT

REVENANT is experimental persistent asset reconstruction. PCSX2 is its primary acceptance target. Capturing or generating an asset does not by itself prove that the replacement was rendered; rendered-use/persistence is still being validated.

## If something breaks

First test the game without other graphics injectors stacked on top of UNCANNY. Use the included rollback/uninstall path to restore the target if necessary.

For a useful bug report, include:

- game/emulator + version
- target executable
- D3D9/10/11/12
- x86/x64
- GPU + NVIDIA driver
- UNCANNY version
- what you expected and what happened
- `UNCANNY-STATUS.cmd` output
- screenshot/video when the problem is visual

## Current limitations

- D3D9/D3D10 neural compatibility is still being validated.
- Vulkan/OpenGL are not at DirectX parity.
- REVENANT rendered-use is experimental.
- Clean 2/2.5/3 quality and performance are still undergoing broader GPU testing.
- Some fullscreen titles may have overlay/focus issues.

## More

- [README](README.md)
- [Releases](RELEASES.md)
- [Compatibility](docs/COMPATIBILITY.md)
- [FAQ](docs/FAQ.md)
- [Contributing / testing](CONTRIBUTING.md)
- [Security](SECURITY.md)

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.
