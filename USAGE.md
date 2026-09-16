# UNCANNY Usage Guide

This guide walks through installing, launching, testing and troubleshooting **UNCANNY — Universal DLSS 5 Neural Remaster Engine**.

> **Alpha warning:** UNCANNY is still in active public-alpha testing. Compatibility varies by game, graphics API, architecture, GPU/driver and emulator. Direct3D 11/12 and PCSX2 are currently the most mature paths. D3D9/D3D10 neural execution and REVENANT rendered-use are still active validation areas.

## Before you start

UNCANNY currently targets:

- Windows
- NVIDIA RTX GPUs
- Direct3D 9, 10, 11 and 12
- PC games and selected emulators, with PCSX2 as a primary emulator target

Before installing:

1. Update your NVIDIA driver.
2. Close the game or emulator you want to install UNCANNY into.
3. Back up any important mods or custom graphics files you want to keep.
4. Check [RELEASES.md](RELEASES.md) for the exact current build name, runtime revision, ABI and SHA-256.
5. Use the package that matches the public candidate listed there. Do not mix files from different UNCANNY builds.

## 1. Download and verify the package

Download the current public Windows package listed in [RELEASES.md](RELEASES.md).

Always extract the entire archive to its own folder before running anything. Do **not** run UNCANNY directly from inside the ZIP.

To verify the package in PowerShell:

```powershell
Get-FileHash .\UNCANNY-*.zip -Algorithm SHA256
```

Compare the result with the SHA-256 published in [RELEASES.md](RELEASES.md).

If the hashes do not match, do not install that copy.

## 2. Install UNCANNY into a game or emulator

1. Open the extracted UNCANNY package.
2. Run the included UNCANNY installer/setup entry point.
3. Select the **real game or emulator executable** when prompted.
4. Let the installer inspect the target folder, create its backup/rollback state and prepare the correct runtime path.
5. If UNCANNY reports conflicting graphics injectors, ReShade files or incompatible remnants, review the warning before allowing cleanup.
6. When installation finishes, close the installer.

UNCANNY is designed so that, after a successful install, you launch the game or emulator from its normal executable or normal launcher. A separate UNCANNY launch script should not be required for ordinary use on a correctly supported target.

### Picking the correct executable

Choose the executable that actually creates the game window and graphics device.

Examples:

- Steam game: the game's main `.exe`, not `steam.exe`
- PCSX2: the PCSX2 executable you normally launch
- Standalone game: the executable that directly starts the game

If a launcher starts a second executable, UNCANNY normally needs to be installed against the executable that renders the game.

## 3. Launch the game normally

Start the game or emulator the same way you normally would.

When UNCANNY attaches correctly, its runtime should load with the target. You should not need to manually start an external feeder every time.

For first-time testing, use windowed or borderless mode if exclusive fullscreen makes overlays difficult to access.

## 4. Open the UNCANNY Control Deck

Press the configured UNCANNY overlay key. Current builds use **Home** as the standard control-panel key unless the build/package notes say otherwise.

The Control Deck is the user-facing control surface for UNCANNY. Internal compatibility components are not intended to be the normal user interface.

If pressing Home minimizes the game or exits exclusive fullscreen, try borderless/windowed mode for testing and include that behavior in your compatibility report.

## 5. First test: prove UNCANNY itself is working

Do this before turning every feature up at once.

1. Launch a scene you can reproduce easily.
2. Open the Control Deck.
3. Set **ENABLE UNCANNY** to **ON**.
4. Start with **Clean 1**.
5. Leave **Motion Guard** and **Ghosting Guard** enabled for the first test.
6. Close the panel and move the camera around normally.
7. Toggle UNCANNY **OFF**, observe the same scene, then turn it **ON** again.
8. Compare image reconstruction, edge stability, fine detail, fogginess/softness and motion behavior.

Do not judge a build from a single still frame. UNCANNY is designed around both reconstruction quality and motion stability.

## 6. Understanding Clean modes

UNCANNY's Clean levels are reconstruction-depth budgets, not simple sharpening presets.

### Clean 1

Lowest-latency primary reconstruction path. Use this as the baseline when testing a new title.

### Clean 1.5

Adds additional reconstruction budget while remaining relatively conservative.

### Clean 2

Allows deeper reconstruction when the runtime has enough confidence and frame budget.

### Clean 2.5

Targets a stronger quality/motion balance. It is intended to preserve clean motion rather than forcing extra detail into unstable frames.

### Clean 3

Highest requested reconstruction depth. This does **not** mean UNCANNY blindly runs three identical neural evaluations. Later work can be reduced or bypassed when it would be redundant, too expensive or unsafe for motion quality.

Start with Clean 1. Move upward only after the title is stable and you have checked performance and motion.

## 7. Motion Guard and Ghosting Guard

These systems protect moving content and temporal stability.

Watch for:

- character outlines
- weapon edges
- vehicles
- foliage
- fences and thin geometry
- particles
- HUD/UI elements
- camera cuts
- newly revealed/disoccluded areas

If higher Clean modes increase trailing, doubled edges, smearing or unstable detail, keep Motion Guard/Ghosting Guard enabled and reduce reconstruction depth while testing.

## 8. DLSS 5 / Feature-18 verification

Seeing a DLL on disk or seeing a provider listed is **not** enough to prove neural rendering is actually contributing.

Use the included `UNCANNY-STATUS.cmd` diagnostic after testing a title.

Useful evidence includes:

- UNCANNY runtime attached to the intended process
- correct graphics API and x86/x64 architecture
- Feature-18 creation attempts
- successful feature creation
- evaluation attempts
- successful evaluations
- returned neural output
- evidence that returned output reached presentation/rendered use

For legacy D3D9/D3D10 games, the core UNCANNY runtime may attach even when the neural path has not yet completed a successful Feature-18 create/evaluate/return/present chain. Report that distinction instead of treating attachment as full DLSS 5 success.

## 9. PCSX2 walkthrough

PCSX2 is one of UNCANNY's primary test environments.

Recommended first test:

1. Install UNCANNY against the PCSX2 executable you actually use.
2. Launch PCSX2 normally.
3. Start a game and reach a repeatable in-game scene.
4. Open the UNCANNY Control Deck with Home.
5. Enable UNCANNY.
6. Start with Clean 1 and motion protection enabled.
7. Compare UNCANNY OFF versus ON.
8. Only after the base runtime is stable, begin testing deeper Clean modes or REVENANT.
9. Run `UNCANNY-STATUS.cmd` after the session and keep the report if you are submitting compatibility results.

### REVENANT on PCSX2

REVENANT is UNCANNY's persistent asset-reconstruction system. Its intended path is:

`capture → identify → infer → validate → replace → reload/bind → rendered-use proof → persistence → exact restore`

REVENANT is still experimental. A captured asset, generated file or successful inference is not by itself proof that the emulator rendered the replacement.

When testing REVENANT, report whether you can prove:

- an asset was captured
- real reconstruction/inference ran
- a replacement was produced
- PCSX2 loaded/bound the replacement
- the replacement was visibly/renderably used
- the result persisted across a relaunch when expected
- rollback restored the original state

## 10. Testing a new PC game

For a game that has never been tested with UNCANNY:

1. Install UNCANNY against the real rendering executable.
2. Start with all optional/deeper features conservative.
3. Confirm the game reaches gameplay without crashing.
4. Confirm the Control Deck opens.
5. Confirm ENABLE UNCANNY can be toggled without closing or freezing the game.
6. Test Clean 1 first.
7. Check motion, UI and camera cuts.
8. Run the status diagnostic.
9. Only then test Clean 1.5/2/2.5/3, REVENANT or more aggressive settings.

This makes it much easier to identify which layer caused a problem.

## 11. Troubleshooting

### The game launches but I see no visual difference

Check the following:

- Is `ENABLE UNCANNY` actually ON?
- Does the status report show the correct process and graphics API?
- Does Feature-18 creation succeed?
- Are evaluations succeeding?
- Is neural output actually returned and used for presentation?
- Are you testing a legacy path that is still experimental?

A working overlay does not automatically mean the neural backend is contributing.

### The Control Deck does not open

- Try Home again after the game reaches actual gameplay.
- Test windowed or borderless mode.
- Make sure another application has not captured/remapped the Home key.
- Confirm UNCANNY attached to the correct executable.
- Include the behavior in a compatibility report if it is repeatable.

### Pressing Home minimizes the game

Some games/emulators or fullscreen modes may intercept the key or react badly to overlay focus. Test borderless/windowed mode and report the exact title, display mode and API.

### The game crashes or freezes after installation

1. Do not keep stacking additional injectors or graphics mods on top while diagnosing.
2. Use UNCANNY's rollback/uninstall path to restore the target.
3. Confirm the game works again without UNCANNY.
4. Reinstall UNCANNY by itself.
5. Test the lowest-depth configuration first.
6. Save the status/diagnostic output and submit a report.

### D3D9 or D3D10 attaches but DLSS 5 does not run

This is a known alpha validation area. Report the exact API, x86/x64 architecture and the Feature-18 create/evaluate counters from the status output. Do not report the title as full neural success unless returned output reaches rendered presentation.

## 12. Rollback / uninstall

Use the rollback or uninstall entry point included with the same UNCANNY build that performed the installation.

After rollback:

1. Confirm UNCANNY runtime files are no longer active for the target.
2. Launch the game/emulator normally.
3. Confirm the original game still works.
4. Restore any third-party mods you intentionally removed before installing UNCANNY.

Do not manually delete random DLLs from the game directory unless you know exactly which project installed them.

## 13. How to make a useful compatibility report

When reporting a game or emulator, include:

- game/emulator name and version
- executable used
- graphics API
- x86 or x64
- GPU
- NVIDIA driver version
- UNCANNY product version
- UNCANNY runtime revision / ABI
- whether the runtime attached
- whether the Control Deck opened
- whether ENABLE UNCANNY toggled safely
- requested Clean level
- Feature-18 create/evaluate success
- whether neural output returned and reached presentation
- motion/ghosting observations
- REVENANT evidence when applicable
- `UNCANNY-STATUS.cmd` output

Use the repository's compatibility-report issue template so results stay searchable and reproducible.

## Recommended first-session checklist

If you only want the short version:

1. Verify the package hash.
2. Extract the full ZIP.
3. Install UNCANNY against the game's real executable.
4. Launch the game normally.
5. Press Home to open the Control Deck.
6. Turn ENABLE UNCANNY ON.
7. Start with Clean 1 + Motion Guard/Ghosting Guard.
8. Compare OFF versus ON in the same scene.
9. Run `UNCANNY-STATUS.cmd`.
10. Move to deeper Clean modes only after the baseline is stable.
11. Report problems with the status output attached.

## More information

- [README](README.md)
- [Release status](RELEASES.md)
- [Compatibility and evidence levels](docs/COMPATIBILITY.md)
- [FAQ](docs/FAQ.md)
- [Contributing / testing](CONTRIBUTING.md)
- [Security](SECURITY.md)

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.
