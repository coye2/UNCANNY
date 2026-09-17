# UNCANNY v0.20 ELYSIUM Hotfix 10 — Usage

UNCANNY is currently a Windows/NVIDIA RTX public alpha. The compiled runtime is distributed through GitHub Releases; the full development source is private.

## Install

1. Download `UNCANNY-v0.20.0-alpha.1-ELYSIUM-Windows.zip` from the latest GitHub Release.
2. Extract the entire ZIP. Do not run it from inside the archive.
3. Run `UNCANNY.cmd`.
4. Let UNCANNY scan for games/emulators, or use **Add game** and select the real rendering executable.
5. Select the title and choose **Install UNCANNY**.
6. Launch from UNCANNY or normally from the selected executable.
7. Reach gameplay and press **HOME** to open the Control Deck.

Do not mix DLLs or EXEs from older UNCANNY packages.

## UNCANNY passes

HOME → **UNCANNY PASSES** controls the native ELYSIUM image stack live:

`1 / 1.5 / 2 / 2.5 / 3`

This is independent from **DLSS 5 PASSES**. Hotfix 10 specifically repairs this routing so the HOME selector changes `uncanny_pass_depth_x2`, the value consumed by the ELYSIUM renderer.

## ELYSIUM advanced controls

HOME → **Image** → **Show Advanced** exposes:

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

These controls are live and saved per executable. Editing an individual ELYSIUM image control moves the coordinated quality mode to Custom.

## Quality presets

Performance / Balanced / Quality / Photoreal coordinate multiple ELYSIUM controls at once and may change UNCANNY pass depth.

## DLSS 5

DLSS 5 is a separate path. Use the **DLSS 5** page for provider status, enable/disable, **DLSS 5 PASSES**, provider preset and neural diagnostics.

## Motion

Keep Motion Guard and Ghosting Guard enabled for normal testing. They are intended to reduce unstable reconstruction during motion, disocclusion and unreliable temporal history.

## Compare / bypass

Use the runtime bypass control for matched before/after testing. Cached REVENANT replacements are separate from image-processing bypass and may remain present until restored/removed through their own workflow.

## Diagnostics

Run `UNCANNY-STATUS.cmd` after testing. A loaded DLL or enabled overlay is not by itself proof that neural output reached presentation.

For bug reports include the game/emulator, target executable, API, x86/x64, GPU/driver, exact UNCANNY revision, expected behavior, actual behavior, status output and a screenshot/video for visual issues.

## Current limitations

- D3D9/D3D10 neural compatibility remains experimental.
- Vulkan/OpenGL are not at DirectX parity.
- REVENANT rendered-use remains experimental.
- Real-GPU visual/performance acceptance varies by title and hardware.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.
