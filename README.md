# UNCANNY

Real-time remastering middleware for Windows PC games and emulators.

**Public alpha · ELYSIUM Engine 4.5 · D3D9/10/11/12 · PCSX2 · Adaptive Realism · REVENANT**

**[Download latest](https://github.com/coye2/UNCANNY/releases/latest) · [Join the Discord](https://discord.gg/zMveJN2kDa)**

> The compiled runtime is distributed through **GitHub Releases**. This public repository contains release information, documentation and support material; the full development workspace is private.

## Latest release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF17**  
Runtime: `release-alpha.1.elysium-engine45` · ABI `143`

Release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45  
Package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip`  
SHA-256: `cef5daff98e611e9da27f9365a660f14f82208238ce3d277db3f1088ba1a304e`

HF17 is the emergency ELYSIUM 4.5 runtime-resilience update. It preserves HF15 and adds a bounded recovery circuit breaker so repeated post-FX/device faults back off and degrade safely instead of hammering the failing path every Present.

## HF17

- Fixed launcher crashes after a successful game install/update when cached library entries were malformed or legacy-shaped.
- Post-install UI/cache refresh is fail-open after install verification.
- Added a title-scoped Fallout 4 D3D11 safe path with extended native-Present stabilization and D3D11 neural interop disabled.
- Control Deck now starts only on HOME and falls back visibly if in-frame handshake fails.

- Added bounded **post-FX recovery backoff** so repeated advanced-rendering/device faults preserve native Present instead of repeatedly retrying the failing path.
- Recovery first retries ELYSIUM at safer Adaptive Realism / Performance Guard settings.
- Continued instability locally reduces Reference Stack, pass depth and optional DLSS 5 cost.
- Recovery is session-local and does **not** overwrite the user's saved settings.
- Higher-cost rendering returns only after a sustained clean run to avoid fallback/retry oscillation.
- New diagnostics expose `PostFxRecoveryFaults`, `PostFxRecoveryCleanFrames` and `PostFxRecoveryBackoffMs`.
- HF15 startup-scan, manual-game, rollback, Adaptive Realism, Motion Guard/Ghosting Guard, PCSX2 and REVENANT work is preserved.
- Exact HF17 candidate passed static gates, x86/x64 production builds, Windows HLSL, manual Add game persistence, dynamic install/remove rollback, exact ZIP hash verification and Microsoft Defender scans.

Source revision: `192d0c652b2ef3dee8dcb542a93ed816cc6cea9f`.  
BuildId: `elysium45-hf17`.

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

1. Download `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip` from the latest release.
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
| Vulkan / OpenGL | not at DirectX parity |

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

`MALWARE-VERIFICATION-ENGINE45.json`

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