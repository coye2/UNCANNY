# UNCANNY

## Universal DLSS 5 Neural Remaster Engine for PC Games and Emulators

**UNCANNY** is an independent Windows real-time remastering middleware project built around **DLSS 5 / Feature-18 neural rendering**, adaptive multi-stage reconstruction, motion protection, and persistent asset reconstruction.

UNCANNY is designed to put the pieces of a modern neural-remaster stack into one product: graphics-API attachment, neural transport, Clean reconstruction stages, Motion Guard, Ghosting Guard, REVENANT asset reconstruction, a Control Deck, rollback, diagnostics, and compatibility tooling.

> **Current public test candidate:** `v0.19.0-alpha.1` — `release-alpha.rc2.hotfix.2`  
> **ABI:** 140  
> **Status:** public-alpha candidate / real-hardware validation in progress  
> **Platform focus:** Windows + NVIDIA RTX  
> **API focus:** Direct3D 9, 10, 11 and 12; PCSX2 is a primary emulator target

UNCANNY is **not simply a ReShade preset or a single graphics add-on**. The current stack contains native runtime components, x86/x64 interoperability, an x64 neural helper for legacy processes, a standalone Control Deck, REVENANT workers, diagnostics, installer/rollback logic and protected runtime resources. Some compatibility paths can interoperate with third-party graphics components internally where appropriate.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.

---

## What UNCANNY does

### DLSS 5 neural rendering
UNCANNY integrates a real neural-rendering path and tracks actual provider creation, evaluation, returned output and presentation evidence instead of treating file presence or a green status indicator as proof of DLSS 5 execution.

### Clean 1 / 1.5 / 2 / 2.5 / 3
Clean stages are reconstruction-depth budgets, not labels for repeated sharpening. The current development runtime can schedule additional neural refinement stages when motion confidence, queue pressure, VRAM and frame budget permit them. Requested stage and actual neural-evaluation count are reported separately.

### Motion Guard + Ghosting Guard
Later reconstruction work is reduced or bypassed when temporal confidence is poor. The system is built to protect moving characters, weapon silhouettes, foliage, fences, particles, disocclusions, HUD elements and camera cuts instead of maximizing still-frame detail at any cost.

### REVENANT
REVENANT is UNCANNY's persistent asset-reconstruction system. Its target pipeline is:

`capture → identify → infer → validate → replace → reload/bind → rendered-use proof → persistence → exact restore`

PCSX2 is the primary REVENANT acceptance target because it exposes a practical texture replacement path. Native-game resource substitution is also under active development.

### Legacy game compatibility
UNCANNY contains explicit work for legacy Direct3D paths, including 32-bit game support and an x64 neural-helper route. D3D9/D3D10 legacy neural compatibility remains an active hardware-validation area; it is not represented here as universally proven.

### Control Deck, diagnostics and rollback
UNCANNY ships as a product stack rather than a loose collection of effects. The runtime includes an integrated Control Deck, per-game state, hardware/runtime evidence, installer conflict handling, backups and rollback.

---

## Where UNCANNY fits in the DLSS 5 ecosystem

People comparing **DLSS 5 tools, DLSS5 feeders, neural-rendering injectors, real-time remaster tools and game-remaster middleware** will often encounter projects such as DLSS5-Feeder, RenoDX/ShortFuse, OptiScaler, Deep Fried Chicken and NVIDIA RTX Remix.

UNCANNY occupies a different scope: it is trying to combine **neural rendering + motion-safe reconstruction + persistent asset reconstruction + compatibility + product-level control/rollback** in one independent remaster runtime.

Read: **[DLSS 5 tools and feeders — where UNCANNY fits](docs/DLSS5-TOOLS-AND-FEEDERS.md)**.

---

## Current compatibility status

| Area | Current state |
|---|---|
| D3D12 x64 | strongest native PC path; regression testing continues |
| D3D11 x64/x86 | implemented; game-specific acceptance continues |
| D3D10 | compatibility path implemented; hardware acceptance required |
| D3D9 / legacy x86 | UNCANNY runtime works in tested legacy titles; neural helper path remains experimental until Feature-18 return/present is proven broadly |
| PCSX2 | primary emulator target; core UNCANNY pipeline is established, REVENANT neural rendered-use acceptance is still in progress |
| Vulkan / OpenGL | not at DirectX parity yet |
| REVENANT native PC | experimental |
| Clean 2 / 2.5 / 3 | deeper neural scheduler implemented; real-GPU quality/performance validation ongoing |

See **[Compatibility](docs/COMPATIBILITY.md)** for the evidence standard and reporting terminology.

---

## Latest packaged candidate

**UNCANNY v0.19.0-alpha.1 — Alpha RC2 Hotfix 2**

- Runtime revision: `release-alpha.rc2.hotfix.2`
- ABI: `140`
- Helper protocol: `2`
- Public Windows package: `UNCANNY-v0.19.0-alpha.1-ALPHA-RC2-HOTFIX-2-Windows.zip`
- Public SHA-256: `bac0da28b86076daa18fbdeafb514043fb93e008c1518df9a17805f740754f86`
- Build-host verification: 11 production Windows components compiled; 77 mixed regression records passed; 7 sanitizer executions passed; 527 ABI fields / 1,070 layout comparisons matched.

The current candidate is intentionally described as a **test candidate**, not a universally verified release. Windows/NVIDIA/PCSX2 rendered acceptance remains required for the remaining headline gates.

Read **[CHANGELOG.md](CHANGELOG.md)** and **[Release status](RELEASES.md)**.

---

## Frequently asked questions

- **What is UNCANNY?** A universal real-time neural remaster engine in development for Windows games and emulators.
- **Is UNCANNY a DLSS5 feeder?** It includes feeder/transport-style compatibility work, but its scope is broader: neural rendering, Clean reconstruction, motion protection, REVENANT asset rebuilding, controls, diagnostics and rollback.
- **Does UNCANNY work with old DirectX games?** The core runtime has D3D9/D3D10 work, while legacy DLSS 5 Feature-18 execution is still being validated title by title.
- **Does UNCANNY work with PCSX2?** PCSX2 is a primary target and one of the most-developed UNCANNY environments; REVENANT's final neural asset rendered-use proof is still an active acceptance gate.
- **Is UNCANNY RTX Remix?** No. UNCANNY is an independent project with a different architecture and compatibility goal.

More: **[FAQ](docs/FAQ.md)**.

---

## Testing UNCANNY

Alpha testers are especially useful on different GPUs, APIs, architectures and games. A good report includes:

- game and executable
- graphics API
- x86 or x64
- GPU + driver
- UNCANNY revision / ABI
- whether the core runtime attaches
- whether Feature-18 create/evaluate succeeds
- whether neural output returns and reaches presentation
- REVENANT capture/inference/replacement evidence when applicable
- `UNCANNY-STATUS.cmd` report

Use the repository's **compatibility report** issue template so results can become searchable, reproducible compatibility evidence.

---

## Documentation

- [DLSS 5 tools and feeders — where UNCANNY fits](docs/DLSS5-TOOLS-AND-FEEDERS.md)
- [Compatibility and evidence levels](docs/COMPATIBILITY.md)
- [UNCANNY FAQ](docs/FAQ.md)
- [Changelog](CHANGELOG.md)
- [Release status](RELEASES.md)
- [Contributing / testing](CONTRIBUTING.md)
- [Security](SECURITY.md)

---

## Project name and canonical link

The preferred project name is **UNCANNY — Universal DLSS 5 Neural Remaster Engine**. Using the full name on first reference helps distinguish this project from unrelated uses of the ordinary word “uncanny”.

Canonical repository: `github.com/coye2/UNCANNY`
