# UNCANNY v0.20 — ELYSIUM Engine 4.5 — Usage

Current public runtime: `release-alpha.1.elysium-engine45` · ABI `143`.

UNCANNY is experimental Windows remastering middleware for PC games and emulators. The public package contains the compiled runtime and support files; the full development source workspace is private.

## Install

1. Download `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip` from the latest GitHub release.
2. Extract the entire ZIP. Do not run UNCANNY from inside the archive.
3. Run **`UNCANNY.exe`** from the package root.
4. Leave **Scan on startup** enabled for automatic discovery, or disable it if you want UNCANNY to open only from cached/manual entries.
5. Use **Scan PC** whenever you want an explicit discovery refresh, or use **Add game** to select the real rendering executable manually. Manual entries persist independently of startup scanning.
6. Select the title and choose **Install UNCANNY**.
7. Launch from UNCANNY or normally from the selected executable.
8. Reach gameplay and press **HOME** to open the Control Deck.

Do not mix DLLs or EXEs from older UNCANNY packages.

Manual library entries use Windows path canonicalization so short-path and long-path aliases for the same executable do not become duplicate games.

## Verify your download

Official Engine 4.5 ZIP:

`UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip`

SHA-256:

`cef5daff98e611e9da27f9365a660f14f82208238ce3d277db3f1088ba1a304e`

The release also includes the `.sha256` file and `MALWARE-VERIFICATION-ENGINE45.json`.

The exact final package passed Microsoft Defender scans of the extracted release and the completed ZIP with **0 detections**. No Defender exclusion, threat restoration, allowlisting or antivirus bypass is required.

See [docs/MALWARE-VERIFICATION.md](docs/MALWARE-VERIFICATION.md).

## Fallout 4 HF17 compatibility

HF17 detects `Fallout4.exe` and uses a conservative D3D11 compatibility route: extended native-Present warmup, no D3D11 neural interop, and current-frame ELYSIUM behavior. Press HOME only after the game reaches a stable visible state; the Control Deck now starts on demand and automatically exposes a desktop fallback if in-frame connection fails.

## HF16 runtime recovery

HF16 adds a bounded recovery path for repeated advanced-rendering/device faults. If post-FX becomes unstable, UNCANNY temporarily backs off while native Present continues. It retries ELYSIUM at safer in-session settings before reducing Reference Stack, pass depth or optional DLSS 5 cost. Saved settings are not overwritten.

For diagnostics, `UNCANNY-STATUS.cmd` now reports `PostFxRecoveryFaults`, `PostFxRecoveryCleanFrames` and `PostFxRecoveryBackoffMs`.

## Adaptive Realism

HOME → the ELYSIUM/UNCANNY image controls expose five Adaptive Realism levels:

`OFF / LOW / BALANCED / HIGH / INSANE`

Adaptive Realism is separate from DLSS 5. It can operate without DLSS 5 and scales its behavior to the scene evidence UNCANNY can safely obtain.

### Capability tiers

- **Tier A** — trustworthy depth + native motion.
- **Tier B** — trustworthy depth + UNCANNY optical flow.
- **Tier C** — trustworthy depth only; conservative spatial lighting and no temporal history.
- **Tier D** — no trustworthy depth; tonal/spatial enhancement only, with no fake depth-aware GI claim.

D3D11 currently has the strongest route because it can use capability-scored discovered depth and UNCANNY optical flow when available. D3D12 and D3D9 use conservative fallbacks when trustworthy scene depth is unavailable.

## What Adaptive Realism changes

Depending on quality level and capability tier, Engine 4.5 can coordinate:

- depth-aware contact occlusion
- bounded screen-space diffuse/specular support
- reconstructed normal/form cues
- scene-adaptive exposure
- highlight recovery
- shadow compression
- local contrast
- clarity / meso-detail
- bounded saturation correction
- motion-confidence/disocclusion history rejection

The runtime deliberately reduces features when the required scene evidence is not trustworthy.

## UNCANNY passes

HOME → **UNCANNY PASSES** controls native ELYSIUM reconstruction depth:

`1 / 1.5 / 2 / 2.5 / 3`

This remains independent from **DLSS 5 PASSES**.

### X2.5 motion behavior

X2.5 intentionally uses substantially less temporal history than the other multi-pass modes. It is the motion-clean mode when minimizing trails/afterimages matters more than retaining maximum still-frame temporal detail.

## ELYSIUM advanced controls

The Control Deck exposes live controls including:

- structural reconstruction
- surface detail
- face reconstruction
- material definition
- depth / form recovery
- source color recovery
- material color separation
- fine edge recovery
- distant detail
- texture relief
- Motion Guard
- Ghosting Guard
- Adaptive Realism quality

Settings persist per executable where supported by the current profile path.

## Motion Guard / Ghosting Guard

Keep Motion Guard and Ghosting Guard enabled for normal testing unless you are deliberately isolating a visual issue.

Engine 4.5 reduces temporal contribution when:

- motion confidence is poor
- current/history structure disagrees
- depth continuity fails
- disocclusion is detected

The goal is to prefer a clean current frame over a detailed frame with visible trails.

## DLSS 5

DLSS 5 is a separate optional neural route. Use the **DLSS 5** page for provider state, enable/disable, DLSS 5 pass depth and provider diagnostics.

**UNCANNY PASSES**, **Adaptive Realism quality** and **DLSS 5 PASSES** are three different controls.

Adaptive Realism itself is vendor-neutral. DLSS 5 remains NVIDIA-specific.

## D3D11 startup / fail-open behavior

The Hotfix 11 D3D11 safety work remains preserved in Engine 4.5:

1. native `Present` / `Present1` is allowed to establish visible output first
2. optional preprocessing/Deck work must not become a prerequisite for the first visible frame
3. DLSS 5 startup waits for a healthy advancing presentation stream where that route applies
4. if optional neural work is not ready, the live source frame remains authoritative

For black-screen reports, run `UNCANNY-STATUS.cmd` and inspect `PresentAttempts`, `Presents`, `PresentAdvancing`, FPS, `AttachmentStage` and Feature-18 create/evaluate counters.

## REVENANT

REVENANT is separate from the live image-processing path. It is an experimental persistent asset-reconstruction system with PCSX2 as its main acceptance target.

Worker/capture success does not by itself prove that a replacement is visibly bound by the running game/emulator. Native-PC-game asset replacement remains experimental.

## Compare / bypass

Use **ENABLE UNCANNY OFF** for the master bypass when doing matched comparisons. It must bypass UNCANNY image processing instead of merely hiding the Control Deck.

Cached REVENANT assets are a separate system and may need to be restored/removed through their own workflow for a complete asset-level before/after comparison.

## Compatibility notes

- D3D11 is the strongest current Adaptive Realism path.
- D3D12 is supported, with reduced Adaptive Realism behavior when trustworthy generic scene depth is unavailable.
- D3D9 is supported as a legacy route, with conservative Adaptive Realism fallback when depth is unavailable.
- D3D10/10.1 remain compatibility routes with capability depending on available evidence.
- Vulkan/OpenGL are not at DirectX parity.
- REVENANT remains experimental.

See [docs/COMPATIBILITY.md](docs/COMPATIBILITY.md).

## Reporting a bug

Include:

1. game/emulator and exact executable
2. graphics API
3. x86/x64
4. GPU + driver
5. exact UNCANNY runtime/revision
6. expected behavior
7. actual behavior
8. `UNCANNY-STATUS.cmd` output where applicable
9. screenshot/video for visual issues
10. whether the issue changes with `ENABLE UNCANNY OFF`, Adaptive Realism OFF, Motion Guard/Ghosting Guard, or a different UNCANNY pass depth

## What CI does and does not prove

The Engine 4.5 release passed the full regression suite, 22 compiled Engine 4.5 checks, x86/x64 Adaptive Realism tests, production builds, public-package integrity checks, install/rollback regression and Defender scanning.

Those checks prove the tested software/package contract. They do **not** replace real-game visual/performance acceptance across every NVIDIA, AMD and Intel GPU/title combination.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA.