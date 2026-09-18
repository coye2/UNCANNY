# UNCANNY

Real-time remastering middleware for Windows PC games and emulators.

**Public alpha · ELYSIUM Engine 4.5 · D3D9/10/11/12 · PCSX2 · Adaptive Realism · REVENANT**

**[Download latest](https://github.com/coye2/UNCANNY/releases/latest) · [Join the Discord](https://discord.gg/zMveJN2kDa)**

> The compiled runtime is distributed through **GitHub Releases**. This public repository contains release information, documentation and support material; the full development workspace is private.

## Latest release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.3**  
Runtime: `release-alpha.1.elysium-engine45-hf18.3` · BuildId `elysium45-hf18.3` · updateSerial `1830` · ABI `143`

Release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45-hf18.3  
Package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.3.zip`  
SHA-256: `9748039fefcbbe941ea3d67cb54b731798d35b7332643677a3a28b4398fbcb21`

## HF18.3

- Fixes the launcher startup crash caused by missing legacy/discovery object properties under PowerShell StrictMode.
- Startup, selection and action callbacks recover/log malformed records instead of tearing down WPF `ShowDialog()`.
- Replaces the synthetic vector-style badge with the official cropped silver UNCANNY U emblem PNG.
- Migrates stale unmarked Lucid engine preferences back to Automatic/ELYSIUM.
- Only explicit current `UserSelected=1` Lucid choices may preserve the legacy engine.
- Adds a packaged-launcher survival smoke test against the final ZIP.
- Hardens installed-game/cache path handling so missing `.Path`/schema fields cannot crash the launcher.
- Removes `-ExecutionPolicy Bypass` from the native EXE bootstrap while keeping the launch hidden/non-interactive.
- Preserves the HF18.2 clean `runtime\` / `Tools\` package layout and HF18 rendering stack.

Validation run: https://github.com/coye2/uncanny-dev/actions/runs/35393751767

## Adaptive Realism

Adaptive Realism is UNCANNY's scene-aware image reconstruction and enhancement layer. It is separate from the DLSS 5 provider path and can operate without DLSS 5.

### Five real levels

`OFF / LOW / BALANCED / HIGH / INSANE`

These levels change actual runtime tuning rather than only changing a label. Higher levels increase reconstruction samples and the strength of supported lighting/detail work while the performance guard can reduce cost before disabling the effect.

### Capability tiers

UNCANNY does not pretend every API exposes the same scene data:

| Tier | Available evidence | Behavior |
|---|---|---|
| A | trustworthy depth + native motion | strongest depth-aware/temporal path |
| B | trustworthy depth + UNCANNY optical flow | depth-aware path with reconstructed motion |
| C | trustworthy depth only | conservative spatial lighting; no temporal history |
| D | no trustworthy scene depth | tonal/spatial enhancement only; no fake GI claim |

D3D11 currently has the strongest Adaptive Realism path because it can use scored discovered depth plus UNCANNY optical flow when available. D3D12 and D3D9 fall back conservatively when trustworthy scene depth is not available.

### Motion-first behavior

- **Motion Guard** and **Ghosting Guard** remain authoritative.
- Temporal history is reduced when motion confidence drops, depth disagrees, or disocclusion is detected.
- **X2.5** deliberately uses the lowest history weight and remains the clean-motion mode.
- `ENABLE UNCANNY OFF` remains the master bypass.
- **UNCANNY PASSES** and **DLSS 5 PASSES** remain separate controls.

## ELYSIUM controls

The Control Deck keeps the live ELYSIUM controls for:

- UNCANNY passes: `1 / 1.5 / 2 / 2.5 / 3`
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
- Motion Guard / Ghosting Guard
- Adaptive Realism quality

## DLSS 5

DLSS 5 remains a separate optional neural route. Provider availability, neural feature creation/evaluation and **DLSS 5 PASSES** live on the DLSS 5 side of the runtime and are not the same thing as UNCANNY's native ELYSIUM pass depth or Adaptive Realism quality.

Adaptive Realism itself is vendor-neutral; DLSS 5 remains NVIDIA-specific.

## REVENANT

REVENANT is UNCANNY's experimental persistent asset-reconstruction system. PCSX2 remains its main acceptance target. REVENANT worker success is tracked separately from live swapchain/presentation health, and native-PC-game asset replacement is still experimental rather than claimed as universal.

## Install

1. Download `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.3.zip` from the latest release.
2. Extract the ZIP completely.
3. Run **`UNCANNY.exe`** from the root of the extracted folder.
4. Let UNCANNY scan, or add the real game/emulator executable manually.
5. Choose **Install UNCANNY**.
6. Launch the title and press **HOME** for the Control Deck.

Do not mix DLLs or EXEs from older packages.

Full walkthrough: [USAGE.md](USAGE.md)

## Compatibility snapshot

| Path | Engine 4.5 status |
|---|---|
| D3D11 | strongest current Adaptive Realism route; depth + flow where trustworthy |
| D3D12 | supported runtime; Adaptive Realism uses conservative fallback when scene depth is unavailable |
| D3D9 | supported legacy runtime; Adaptive Realism falls back when trustworthy depth is unavailable |
| D3D10 / 10.1 | compatibility path; capability depends on available scene data |
| PCSX2 | primary emulator acceptance target |
| REVENANT | experimental persistent asset reconstruction |
| Vulkan / OpenGL | lifecycle/presentation compatibility observation; full ELYSIUM/neural parity is not claimed |

See [docs/COMPATIBILITY.md](docs/COMPATIBILITY.md) for evidence levels and exact limitations.

## Release verification

The exact Engine 4.5 public package passed:

- full Python regression suite
- **22** compiled Engine 4.5 acceptance checks
- Adaptive Realism compiled tests on **x86 and x64**
- x86/x64 production builds
- protected-resource verification
- Hotfix 11/12 compatibility regressions
- dynamic Windows install + rollback regression
- strict public-package audit
- ZIP CRC/member-hash verification
- restricted third-party shader source/package audit
- Microsoft Defender scan of the extracted final package: **0 detections**
- Microsoft Defender scan of the completed release ZIP: **0 detections**

The public ZIP contains no engine source, debug symbols, nested development archives or internal test executables. No paid/restricted Marty McFly / Pascal Gilcher shader source or binaries are bundled.

Build/CI success is not the same as broad real-game GPU acceptance. Visual quality and performance still need title-by-title testing across NVIDIA, AMD and Intel hardware.

## Security

The current package has a machine-readable verification attachment on the release:

`MALWARE-VERIFICATION-ENGINE45-HF18.3.json`

See [docs/MALWARE-VERIFICATION.md](docs/MALWARE-VERIFICATION.md). UNCANNY does not require users to disable Defender or create broad antivirus exclusions.

## Automated readers / Cammy

Bots and release monitors do not need to scrape the README. The current release is published in simple public machine-readable surfaces:

- `CURRENT_RELEASE.json` — canonical release/version/package/hash/feature manifest
- `llms.txt` — plain-text current release summary
- `docs/llms.txt` — lightweight docs-site summary
- `https://github.com/coye2/UNCANNY/releases/latest` — canonical GitHub latest-release endpoint

Raw manifest: https://raw.githubusercontent.com/coye2/UNCANNY/main/CURRENT_RELEASE.json  
Raw text summary: https://raw.githubusercontent.com/coye2/UNCANNY/main/llms.txt

## Community & feedback

**[Join the UNCANNY Discord](https://discord.gg/zMveJN2kDa)** for testing, screenshots, compatibility reports, bug help and development discussion.

For useful reports include the game/emulator, real executable, API, x86/x64, GPU/driver, exact UNCANNY revision, status output and screenshots/video for visual issues.

## Docs

[Usage](USAGE.md) · [Latest release](LATEST_RELEASE.md) · [Release history](RELEASES.md) · [Changelog](CHANGELOG.md) · [Compatibility](docs/COMPATIBILITY.md) · [FAQ](docs/FAQ.md) · [Malware verification](docs/MALWARE-VERIFICATION.md) · [Hotfix 11 D3D11 history](docs/HOTFIX11-D3D11.md) · [Contributing](CONTRIBUTING.md) · [Security](SECURITY.md)

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.