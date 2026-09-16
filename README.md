# UNCANNY

## Universal DLSS 5 Neural Remaster Engine for PC Games and Emulators

**UNCANNY** is an independent Windows real-time remastering middleware project built around **DLSS 5 / Feature-18 neural rendering**, adaptive multi-stage reconstruction, motion protection, and persistent asset reconstruction.

> **Current public build:** `v0.19.0-alpha.1` — `release-alpha.rc2.hotfix.2`  
> **Status:** public alpha / active development  
> **Platform focus:** Windows + NVIDIA RTX  
> **API focus:** Direct3D 9, 10, 11 and 12; PCSX2 is a primary emulator target

## Download and install

**The files in the main repository are currently the public documentation, testing information and release metadata. The full development/source workspace is not published here. The usable compiled UNCANNY runtime is distributed through GitHub Releases.**

1. Open **Releases** on this repository.
2. Download the latest `UNCANNY-...-Windows.zip` public package.
3. Extract the ZIP somewhere outside the game folder.
4. Drag the target game's `.exe` onto `INSTALL-NATIVE.cmd`.
5. Follow the installer output, then launch the game normally.

Do not download packages marked `PRIVATE-WORKSPACE-RECOVERY`; those are not public runtime distributions.

UNCANNY is free to test. The current public GitHub repository should **not** be interpreted as a complete source distribution or a build-from-source repository.

---

## What UNCANNY is

UNCANNY is **not simply a ReShade preset or a single graphics add-on**. The current stack contains native runtime components, x86/x64 interoperability, an x64 neural helper for legacy processes, a standalone Control Deck, REVENANT workers, diagnostics, installer/rollback logic and protected runtime resources. Some compatibility paths can interoperate with third-party graphics components internally where appropriate.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.

### DLSS 5 neural rendering
UNCANNY integrates a neural-rendering path and tracks provider creation, evaluation, returned output and presentation evidence instead of treating file presence or a status indicator as proof of execution.

### Clean 1 / 1.5 / 2 / 2.5 / 3
Clean stages are reconstruction-depth budgets rather than repeated sharpening. Deeper stages are being developed to add refinement while respecting motion confidence, VRAM and frame budget.

### Motion Guard + Ghosting Guard
Later reconstruction work can be reduced or bypassed when temporal confidence is poor, with the goal of protecting moving characters, weapon silhouettes, foliage, particles, disocclusions, HUD elements and camera cuts.

### REVENANT
REVENANT is UNCANNY's experimental persistent asset-reconstruction system. Its target pipeline is:

`capture → identify → infer → validate → replace → reload/bind → rendered-use proof → persistence → exact restore`

PCSX2 is the primary REVENANT acceptance target. End-to-end neural rendered-use proof is still under active development.

### Legacy compatibility
UNCANNY contains explicit work for legacy Direct3D paths, including 32-bit game support and an x64 neural-helper route. D3D9/D3D10 neural compatibility remains an active hardware-validation area and is not claimed as universally proven.

### Control Deck, diagnostics and rollback
The runtime includes an external Control Deck, per-game state, runtime diagnostics, installer conflict handling, backups and rollback tooling.

---

## Current compatibility status

| Area | Current state |
|---|---|
| D3D12 x64 | strongest native PC path; regression testing continues |
| D3D11 x64/x86 | implemented; game-specific acceptance continues |
| D3D10 | compatibility path implemented; hardware acceptance required |
| D3D9 / legacy x86 | core runtime compatibility work exists; neural helper path remains experimental |
| PCSX2 | primary emulator target; REVENANT neural rendered-use acceptance is still in progress |
| Vulkan / OpenGL | not at DirectX parity yet |
| REVENANT native PC | experimental |
| Clean 2 / 2.5 / 3 | deeper scheduler exists; real-GPU quality/performance validation ongoing |

See **[Compatibility](docs/COMPATIBILITY.md)** for more detail.

---

## Latest packaged candidate

**UNCANNY v0.19.0-alpha.1 — Alpha RC2 Hotfix 2**

- Runtime revision: `release-alpha.rc2.hotfix.2`
- ABI: `140`
- Helper protocol: `2`
- Public Windows package: `UNCANNY-v0.19.0-alpha.1-ALPHA-RC2-HOTFIX-2-Windows.zip`
- Public SHA-256: `bac0da28b86076daa18fbdeafb514043fb93e008c1518df9a17805f740754f86`

This is an **alpha test candidate**, not a claim of universal compatibility.

Read **[CHANGELOG.md](CHANGELOG.md)** and **[Release status](RELEASES.md)**.

---

## Testing and feedback

Testing on different GPUs, games, APIs and architectures is welcome. Useful reports include the game/executable, graphics API, x86/x64, GPU + driver, UNCANNY revision, what worked, what failed, and the output from `UNCANNY-STATUS.cmd` when available.

Bug reports, compatibility findings and implementation feedback are welcome through GitHub issues.

New users should start with the **[Usage / installation walkthrough](USAGE.md)**.

---

## Documentation

- [Usage / installation walkthrough](USAGE.md)
- [DLSS 5 tools and feeders — where UNCANNY fits](docs/DLSS5-TOOLS-AND-FEEDERS.md)
- [Compatibility and evidence levels](docs/COMPATIBILITY.md)
- [UNCANNY FAQ](docs/FAQ.md)
- [Changelog](CHANGELOG.md)
- [Release status](RELEASES.md)
- [Contributing / testing](CONTRIBUTING.md)
- [Security](SECURITY.md)

---

Canonical repository: `github.com/coye2/UNCANNY`
