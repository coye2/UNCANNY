# FAQ

## What is UNCANNY?

UNCANNY is experimental real-time remastering middleware for Windows games and emulators. It combines reconstruction, motion protection, neural-rendering integration, diagnostics and compatibility tooling in one runtime.

## Where do I download it?

Use the latest public Windows ZIP under **GitHub Releases**. Extract it, then follow [USAGE.md](../USAGE.md).

## Is the source public?

No. The public repository contains documentation, release information and support material. The full development source workspace is private.

## Is it just a ReShade preset?

No. UNCANNY ships native runtime components, controls, diagnostics, installation/rollback tooling and compatibility components. Some paths may interoperate with third-party graphics software.

## What are Clean 1 / 1.5 / 2 / 2.5 / 3?

Increasing reconstruction-depth modes. Higher modes are intended to add useful refinement rather than blindly repeat identical processing. Quality and performance of the deeper modes are still being tested across GPUs and games.

## What are Motion Guard and Ghosting Guard?

Controls intended to reduce unstable reconstruction during motion, disocclusion and unreliable temporal history.

## What is REVENANT?

An experimental asset-reconstruction system. PCSX2 is currently its main acceptance target. End-to-end rendered replacement and persistence are still under development.

## Does it support D3D9 / D3D10?

The runtime contains legacy compatibility work, but the neural path on D3D9/D3D10 remains experimental. Do not treat successful runtime attachment as proof that neural output reached the frame.

## D3D11 / D3D12?

These are the primary PC test paths, with D3D12 currently the strongest.

## Vulkan / OpenGL?

Not at DirectX parity yet.

## PCSX2?

PCSX2 is the primary emulator test environment. The base UNCANNY pipeline is substantially further along there than REVENANT's experimental rendered-use path.

## How do I know neural rendering actually ran?

Use `UNCANNY-STATUS.cmd`. A DLL being present or an overlay saying enabled is not enough evidence by itself.

## Is UNCANNY affiliated with NVIDIA?

No. UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.

## How do I report a bug?

Open an issue and include the game/emulator, graphics API, x86/x64, GPU/driver, UNCANNY version, reproduction steps and `UNCANNY-STATUS.cmd` output when possible.
