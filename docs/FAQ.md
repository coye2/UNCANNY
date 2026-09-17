# FAQ

## What is UNCANNY?

UNCANNY is experimental real-time remastering middleware for Windows games and emulators. It combines reconstruction, motion protection, neural-rendering integration, diagnostics and compatibility tooling in one runtime.

## What is the current release?

`v0.20.0-alpha.1 — ELYSIUM Hotfix 11`, runtime `release-alpha.1.elysium-hotfix11`, ABI 141.

Exact public ZIP SHA-256: `a523db2ec0149f139a24c70aba36f68222cba057369b97864615b07c9c356e69`.

## Where do I download it?

Use the Hotfix 11 public Windows ZIP under **GitHub Releases** and follow [USAGE.md](../USAGE.md).

## What happened with the Windows Defender warning?

The first Hotfix 11 package mistakenly shipped internal acceptance-test executables under `diagnostics/`. Defender flagged `revenant-commit32.exe`. That executable is a REVENANT development test harness, not a runtime dependency.

The corrected public package removes the complete internal diagnostic executable set. Microsoft Defender signatures were updated and the cleaned runtime tree plus the completed final ZIP were both scanned on a fresh GitHub-hosted Windows runner: **0 detections**. No Defender exclusions, allowlisting or bypass were used.

See [MALWARE-VERIFICATION.md](MALWARE-VERIFICATION.md) for the exact verification record.

## Do I need to disable Defender or whitelist UNCANNY?

No. UNCANNY does not require disabling Defender or adding a broad antivirus exclusion. If a current official package is detected, report the exact file, threat name, release tag and ZIP SHA-256 so it can be investigated.

## Is the source public?

No. The public repository contains documentation, release information and support material. The full development source workspace is private.

## Is it just a ReShade preset?

No. UNCANNY ships native runtime components, controls, diagnostics, installation/rollback tooling and compatibility components.

## What are UNCANNY PASSES 1 / 1.5 / 2 / 2.5 / 3?

They control increasing native ELYSIUM reconstruction depth. Hotfix 10 fixed the Control Deck so this selector drives the actual UNCANNY renderer field; Hotfix 11 preserves that repair.

## Is that the same as DLSS 5 PASSES?

No. They are separate controls. **UNCANNY PASSES** controls the ELYSIUM image stack; **DLSS 5 PASSES** controls the separate DLSS 5/neural route.

## What ELYSIUM controls are available?

Advanced Image controls include structural reconstruction, surface detail, face reconstruction, material definition, depth/form recovery, source color recovery, material color separation, fine-edge recovery, distant detail and texture relief.

## What are Motion Guard and Ghosting Guard?

Controls intended to reduce unstable reconstruction during motion, disocclusion and unreliable temporal history.

## What is REVENANT?

An experimental persistent asset-reconstruction system. PCSX2 is currently its main acceptance target.

## Does it support D3D9 / D3D10?

The runtime contains legacy compatibility work, but the neural path on D3D9/D3D10 remains experimental.

## D3D11 / D3D12?

These are the primary PC test paths. Hotfix 11 specifically changes D3D11 first-frame startup so native presentation is established before optional neural/Deck preprocessing.

## Vulkan / OpenGL?

Not at DirectX parity yet.

## How do I know the runtime actually ran?

Use `UNCANNY-STATUS.cmd`. A DLL being present or an overlay saying enabled is not enough evidence by itself.

## Is UNCANNY affiliated with NVIDIA?

No. UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.