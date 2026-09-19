# Using UNCANNY

## Install

1. Download the latest ZIP from https://github.com/coye2/UNCANNY/releases/latest
2. Extract it somewhere permanent. Do not run it from inside the ZIP.
3. Open `UNCANNY.exe`.
4. Let the launcher scan, or turn **Scan on startup** off and add games manually.
5. Select the real game/emulator executable.
6. Click **Install UNCANNY**.
7. Launch from UNCANNY or from the game normally.
8. Press **HOME** in-game to open the Control Deck.

Manual entries stay in the library even if automatic scanning is disabled.

Do not mix files from different UNCANNY releases.

## Updating

If a game already has UNCANNY installed, the launcher will show **Update UNCANNY** when the installed runtime is out of date or needs repair.

Same-build updates are designed to avoid rewriting files that are already correct.

## Control Deck

The main controls are:

- **Enable UNCANNY** — master image-processing bypass
- **UNCANNY Passes** — 1 / 1.5 / 2 / 2.5 / 3
- **Adaptive Realism** — Off / Low / Balanced / High / Insane
- **Motion Guard** — reduces unstable reconstruction during motion
- **Ghosting Guard** — targets trailing and afterimages
- image controls for structure, faces, materials, edges, color and surface detail
- separate neural / DLSS 5 controls when that route is available

X2.5 uses less temporal history than the other deep modes and is meant to favor cleaner motion.

## PCSX2

PCSX2 currently uses the Direct3D 12 route. UNCANNY writes `Renderer=15` and keeps the original `pcsx2-qt.exe` intact.

HF18.12 specifically changes the D3D12 handoff that could let PCSX2 reach gameplay and then hard-freeze a few seconds later. First-use D3D12 setup now warms off Present and resize/resource retirement is nonblocking.

If an older UNCANNY build replaced or wrapped PCSX2 incorrectly, running **Update UNCANNY** should migrate it back to the current sidecar layout.

Cloud/OneDrive PCSX2 profile folders are supported, but real symlinks/junctions are handled conservatively.

## Modern startup failures

HF18.12 can use deferred startup attach for non-PCSX2 targets with no static graphics API import. Native process startup happens first, then UNCANNY attempts attachment.

If that optional attach cannot be confirmed, the game should remain running rather than being terminated by UNCANNY.

## REVENANT

REVENANT is the asset-reconstruction side of UNCANNY.

It is separate from ELYSIUM's live frame processing. A completed REVENANT job does not automatically mean the running game is visibly using that replacement yet.

PCSX2 is the main REVENANT test target. Native PC-game replacement is still experimental.

## Before/after testing

For a clean live-image comparison, turn **Enable UNCANNY** off.

REVENANT replacements are persistent files, so they may need to be restored separately if you want a complete asset-level before/after comparison.

## If something breaks

Start with:

- update UNCANNY for that game
- confirm you selected the actual rendering executable
- reach a stable in-game scene before opening HOME
- try **Enable UNCANNY OFF** to see whether the runtime is actually involved
- run `Tools/UNCANNY-STATUS.cmd`
- keep the launcher/runtime logs from that session

For a useful bug report, include the game, executable, graphics API, x86/x64, GPU/driver, UNCANNY version, what happened, and the relevant log/status output.

## Current package

Release: **HF18.12**  
BuildId: `elysium45-hf18.12`  
updateSerial: `1920`  
ABI: `143`

ZIP:
`UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.12.zip`

SHA-256:
`9a7e439967af1b7930769aa29b0a1830afee606ce6246291f4035c5a4927dce6`
