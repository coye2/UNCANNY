# UNCANNY FAQ

## What is UNCANNY?

UNCANNY is an independent **universal DLSS 5 neural remaster engine** in active alpha development for Windows games and emulators. It combines neural rendering, adaptive reconstruction stages, motion protection, persistent asset reconstruction, compatibility tooling, controls, diagnostics and rollback.

## Is UNCANNY a DLSS5 feeder?

UNCANNY includes feeder/transport-style compatibility work, including legacy x86→x64 neural transport, but its scope is broader than a feeder. The project is intended to be the complete user-facing remaster runtime rather than only a frame-transport layer.

## Is UNCANNY just a ReShade add-on?

No. UNCANNY is not simply a ReShade preset or one add-on. The current stack includes native runtime components, cross-bitness neural transport, a Control Deck, REVENANT workers, installer/rollback logic, diagnostics and protected runtime resources. Some compatibility paths may use or interoperate with third-party graphics components internally.

## Does UNCANNY use DLSS 5 / Feature 18?

Yes, the neural-rendering architecture targets DLSS 5 / Feature-18 execution. UNCANNY deliberately separates provider detection from real inference evidence. A provider DLL existing on disk is not counted as a successful neural frame.

## Does UNCANNY support DirectX 9 games?

UNCANNY has a D3D9 runtime and legacy/x86 neural-helper architecture. The core runtime is already operating in tested D3D9 titles, but broad D3D9 Feature-18 execution and rendered-use certification are still an active alpha acceptance area.

## Does UNCANNY support DirectX 10?

A D3D10/10.1 compatibility path exists. It remains hardware-acceptance territory rather than a universal-support claim.

## Does UNCANNY support DirectX 11 and DirectX 12?

Yes, D3D11 and D3D12 are major UNCANNY targets. D3D12 is currently the strongest native PC path; D3D11 supports both current native work and legacy interop responsibilities. Game-specific validation still matters.

## Does UNCANNY support Vulkan or OpenGL?

Not at DirectX parity yet. They are part of the broader compatibility roadmap.

## Does UNCANNY work with PCSX2?

PCSX2 is one of UNCANNY's primary targets and one of its most-developed emulator environments. The core UNCANNY presentation pipeline is established there. REVENANT's final neural asset rendered-use/persistence acceptance is still being completed.

## What is REVENANT?

REVENANT is UNCANNY's persistent asset-reconstruction system. The goal is to capture safe assets, run real reconstruction/inference, validate the output, publish the correct replacement, prove that the game/emulator actually uses it, remember the verified improvement, and support exact rollback.

## What are Clean 1, 1.5, 2, 2.5 and 3?

They are reconstruction-depth modes. Clean 1 targets the lowest-latency primary neural reconstruction. Higher modes can schedule additional meaningful neural work when frame budget, motion confidence, VRAM and queue pressure allow it.

The displayed stage is not automatically the number of evaluations that actually ran; UNCANNY records requested depth and actual neural evaluations separately.

## Is Clean 3 just three identical DLSS calls?

That is explicitly not the design goal. Later neural stages must have a distinct reconstruction purpose or they are bypassed. The scheduler is intended to reject redundant work.

## What are Motion Guard and Ghosting Guard?

They control how aggressively later reconstruction can contribute when motion or temporal history is unreliable. They are intended to reduce trailing, double edges, foliage shimmer, weapon ghosts, HUD echoes and disocclusion smearing.

## Is UNCANNY the same thing as RTX Remix?

No. RTX Remix is an NVIDIA remaster platform. UNCANNY is an independent project with a different architecture and compatibility goal.

## Is UNCANNY affiliated with NVIDIA?

No. UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.

## Is UNCANNY open source?

The public repository is the product/discovery/support home. Proprietary development source and private recovery workspaces are not part of the public release package.

## What is the latest public candidate?

`UNCANNY v0.19.0-alpha.1 — Alpha RC2 Hotfix 2`

Runtime revision: `release-alpha.rc2.hotfix.2`  
ABI: `140`  
Public Windows package SHA-256: `bac0da28b86076daa18fbdeafb514043fb93e008c1518df9a17805f740754f86`

It is a test candidate while remaining Windows/NVIDIA/PCSX2 rendered-acceptance gates are completed.

## How should I report a game?

Use the repository compatibility-report issue template and include the game, API, x86/x64 architecture, GPU, driver, UNCANNY revision, attachment status and `UNCANNY-STATUS.cmd` report.

## What should I search for if I am trying to find this project again?

The clearest unique phrase is:

**UNCANNY — Universal DLSS 5 Neural Remaster Engine**

Repository: `github.com/coye2/UNCANNY`
