# UNCANNY v0.20 ELYSIUM Hotfix 11 — Usage

UNCANNY is currently a Windows/NVIDIA RTX public alpha. The compiled runtime is distributed through GitHub Releases; the full development source is private.

## Install

1. Download `UNCANNY-v0.20.0-alpha.1-ELYSIUM-HOTFIX11.zip` from the latest GitHub Release.
2. Extract the entire ZIP. Do not run it from inside the archive.
3. Double-click **`UNCANNY.exe`** at the root of the extracted package.
4. Let UNCANNY scan for games/emulators, or use **Add game** and select the real rendering executable.
5. Select the title and choose **Install UNCANNY**.
6. Launch from the UNCANNY launcher or normally from the selected executable.
7. Reach gameplay and press **HOME** to open the Control Deck.

`UNCANNY.exe` is the normal public launcher in Hotfix 11. It is a native Windows GUI executable and starts the bundled launcher without exposing a command window. If launcher startup itself fails, its native entry point records `%LOCALAPPDATA%\UNCANNY\launcher-exe.log` and can display a normal Windows error dialog.

Do not mix DLLs or EXEs from older UNCANNY packages.

## Verify your download

The corrected official Hotfix 11 ZIP has this SHA-256:

`a523db2ec0149f139a24c70aba36f68222cba057369b97864615b07c9c356e69`

The GitHub release also includes a `.sha256` file and `MALWARE-VERIFICATION-HOTFIX11.json`.

The current public ZIP does **not** ship the internal `diagnostics/` test executables that were accidentally included in the first Hotfix 11 package. `revenant-commit32.exe` and `revenant-commit64.exe` are development acceptance-test harnesses and are not runtime dependencies.

Before publication, Microsoft Defender signatures were updated on a fresh GitHub-hosted Windows runner. The cleaned runtime tree and the completed release ZIP were both scanned and returned **0 detections**. No Defender exclusions, threat restoration, allowlisting or antivirus bypass were used.

You do not need to disable Defender or whitelist UNCANNY. If a current official build triggers a warning, report the exact file, threat name, release tag and ZIP SHA-256 so it can be investigated.

Verification record: [docs/MALWARE-VERIFICATION.md](docs/MALWARE-VERIFICATION.md)

## D3D11 startup behavior in Hotfix 11

Hotfix 11 changes the startup order for direct D3D11 targets after a PCSX2 x64 tester reached `PRESENT_PATCH_OK` but then stayed at `PresentAttempts=1`, `Presents=0`, `PresentAdvancing=0` and 0 FPS.

For direct D3D11:

1. The first native frames are fail-open warmup frames.
2. The game's original `Present` / `Present1` is allowed to establish visible output before UNCANNY image processing and HOME composition run.
3. Feature-18 / DLSS 5 startup waits until native presentation is advancing, at least 8 successful Presents have completed, and the last successful Present is recent.
4. While that neural route is waiting, the live source frame remains authoritative.
5. Losing foreground focus or having HOME/Deck not yet published must not be treated as permission to block the game's native frame.

This is intentionally a compatibility-first startup policy: optional remaster processing should fail open rather than turn a provider/interoperability startup issue into a permanent black screen.

## Reading a D3D11 black-screen report

Run `UNCANNY-STATUS.cmd` from the installed game folder and inspect these fields first:

- `PresentAttempts`
- `Presents`
- `PresentAdvancing`
- `BaseFPS`
- `PresentedFPS`
- `AttachmentStage`
- `Feature18CreateAttempts/Success`
- `Feature18EvaluateAttempts/Success`

Hotfix 11 adds exact presentation stages:

- `PRESENT_PREPROCESS` — the hooked frame entered UNCANNY-side preprocessing.
- `PRESENT_NATIVE_CALL` — UNCANNY reached the application's original `Present` call.
- `PRESENT1_PREPROCESS` / `PRESENT1_NATIVE_CALL` — the equivalent Present1 route.
- `PRESENT_SUCCEEDED` — native presentation successfully advanced.

If a report stops at `PRESENT_PREPROCESS`, the stall is still ahead of the original Present call. If it reaches `PRESENT_NATIVE_CALL` but never `PRESENT_SUCCEEDED`, the original game/driver Present was entered and the remaining fault is on or below that call.

Do not treat `Host64LaunchAttempted=0` by itself as a failure on an x64 D3D11 target. The normal x64 route can use the in-process bridge.

## UNCANNY passes

HOME → **UNCANNY PASSES** controls the native ELYSIUM image stack live:

`1 / 1.5 / 2 / 2.5 / 3`

This remains independent from **DLSS 5 PASSES**. Hotfix 10 repaired the routing and Hotfix 11 preserves it.

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

On direct D3D11 Hotfix 11, seeing Feature-18 remain waiting during the first native frames is expected. Neural initialization is deliberately delayed until base presentation is proven healthy.

## REVENANT

REVENANT is independent from the live D3D11 Present path. The tester report that triggered Hotfix 11 completed 38/38 texture jobs even though native presentation had stopped. Hotfix 11 therefore preserves REVENANT rather than using it as a proxy for Present health.

Cached REVENANT replacements are also separate from the live image-processing bypass and may remain present until restored/removed through their own workflow.

## Engine selection

ELYSIUM remains the current ABI 141 engine. The already-published UNCANNY 2.5 Lucid ABI 136 bundle is preserved in the Hotfix 11 package by its existing manifest hashes so the per-game engine-selection workflow remains available.

## Motion

Keep Motion Guard and Ghosting Guard enabled for normal testing. They are intended to reduce unstable reconstruction during motion, disocclusion and unreliable temporal history.

## Compare / bypass

Use the runtime bypass control for matched before/after testing. The native game presentation path should remain usable regardless of whether optional UNCANNY neural work is ready.

## Reporting the Hotfix 11 retest

For the original PCSX2 D3D11 failure, a useful retest should establish:

1. The game image appears instead of remaining black.
2. `PresentAttempts` keeps increasing.
3. `Presents` becomes non-zero and keeps increasing.
4. `PresentAdvancing=1`.
5. FPS becomes non-zero.
6. `AttachmentStage` reaches `PRESENT_SUCCEEDED`.
7. Feature-18 work starts only after native presentation is healthy.
8. HOME opens without requiring Alt-Tab, minimizing the emulator, stealing focus or stopping Presents.
9. REVENANT remains functional.
10. PCSX2 closes cleanly.

For all bug reports include the game/emulator, target executable, API, x86/x64, GPU/driver, exact UNCANNY revision, expected behavior, actual behavior, status output and a screenshot/video for visual issues.

## Current limitations

- D3D9/D3D10 neural compatibility remains experimental.
- Vulkan/OpenGL are not at DirectX parity.
- REVENANT rendered-use remains experimental.
- Successful compilation/static tests do not certify a hardware-specific issue until it is reproduced/retested on the affected machine.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.