# DLSS 5 Tools and Feeders — Where UNCANNY Fits

This page is for people comparing **DLSS 5 tools**, **DLSS5 feeders**, neural-rendering injectors, upscaler wrappers and real-time game-remaster systems.

UNCANNY is an independent project. It is not affiliated with NVIDIA, RenoDX, DLSS5-Feeder, OptiScaler, Deep Fried Chicken or RTX Remix.

Current public engine: **ELYSIUM Engine 4.5 — Adaptive Realism** (`release-alpha.1.elysium-engine45`, ABI 143).

## The short version

A feeder or injector usually solves one part of the problem: getting frame data into a neural consumer or adapting an existing game to a reconstruction API. UNCANNY's scope is broader. It is being built as an integrated **real-time remaster engine** with:

- graphics-API attachment and compatibility routing
- UNCANNY-native ELYSIUM reconstruction
- Adaptive Realism with capability-aware fallbacks
- optional DLSS 5 / Feature-18 neural execution
- Motion Guard and Ghosting Guard
- persistent asset reconstruction through REVENANT
- per-game controls and diagnostics
- backups, conflict handling and rollback

Adaptive Realism itself is separate from DLSS 5 and does not require the DLSS 5 route. That means UNCANNY can overlap with feeder-style functionality without being only a feeder or only a DLSS wrapper.

## Engine 4.5 separation of concerns

Three controls should not be conflated:

1. **UNCANNY PASSES** — ELYSIUM native reconstruction depth (`1 / 1.5 / 2 / 2.5 / 3`).
2. **Adaptive Realism quality** — `OFF / LOW / BALANCED / HIGH / INSANE`.
3. **DLSS 5 PASSES** — separate optional neural-provider pass control.

D3D11 currently has the strongest generic Adaptive Realism route because UNCANNY can use capability-scored depth and optical flow where available. Other DirectX paths reduce capability rather than pretending unavailable scene data exists.

## Commonly compared projects

### DLSS5-Feeder
DLSS5-Feeder is focused on transporting usable game-frame information into DLSS 5-compatible neural consumers across multiple graphics paths. It is an important reference point for compatibility engineering.

UNCANNY differs by attempting to integrate transport with its own remaster pipeline, Adaptive Realism, motion protection, multi-pass scheduling, REVENANT and product-level controls.

### RenoDX / ShortFuse ecosystem
RenoDX and related neural-rendering work are commonly used to add or adapt modern rendering and DLSS-related capabilities to games.

UNCANNY can use compatible neural backends internally where appropriate, but the user-facing product goal is a unified UNCANNY runtime rather than exposing a collection of unrelated backend panels.

### OptiScaler
OptiScaler focuses heavily on upscaler/frame-generation interoperability and translation between supported technologies.

UNCANNY is aimed more directly at remastering: reconstruction quality, scene-adaptive enhancement, motion stability, persistent asset improvement, compatibility and a unified remaster workflow.

### Deep Fried Chicken
Deep Fried Chicken is associated with deeper neural-rendering experimentation and multi-stage neural processing.

UNCANNY's 2/2.5/3 architecture also permits deeper processing, but later stages are intended to be confidence/budget controlled and tied to Motion Guard, Ghosting Guard and frame-budget telemetry rather than blindly replaying an identical evaluation.

### NVIDIA RTX Remix
RTX Remix is a much larger official remaster ecosystem with scene/asset/material replacement and path-traced rendering capabilities.

UNCANNY is independent and takes a different route: broad runtime compatibility, real-time reconstruction, legacy-game bridging, motion protection and experimental automatic/persistent asset reconstruction. UNCANNY does not claim feature parity with RTX Remix.

## Is UNCANNY a “top DLSS 5 tool”?

That depends on what the user needs. UNCANNY is a public alpha, and several headline paths still require broader hardware validation. The project should be evaluated on actual evidence rather than a ranking claim.

UNCANNY is most relevant when someone wants one project combining:

1. UNCANNY-native ELYSIUM reconstruction,
2. Adaptive Realism that can work independently of DLSS 5,
3. optional DLSS 5 / neural rendering,
4. legacy and modern DirectX compatibility work,
5. motion-safe multi-stage reconstruction,
6. experimental persistent asset reconstruction,
7. integrated controls, diagnostics and rollback.

## Project identity

The canonical project name is **UNCANNY**. The current public engine is **ELYSIUM Engine 4.5**. In discussions UNCANNY may also be described as a neural remaster engine, PCSX2 remaster stack, Adaptive Realism engine or REVENANT project. Those descriptions help distinguish the project from the ordinary word “uncanny”; they are not claims of NVIDIA endorsement or universal compatibility.

Canonical repository: `github.com/coye2/UNCANNY`

## Evidence standard

UNCANNY does not count provider files, copied frames, a successful IPC test or an enabled overlay as neural success.

A complete neural path requires evidence through:

`attach → transport → provider load → FeatureCreate → FeatureEvaluate → neural return → composition → successful presentation`

Adaptive Realism acceptance requires visible scene response appropriate to the active capability tier without claiming unavailable depth/motion evidence.

REVENANT likewise requires:

`capture → inference → validation → replacement → reload/bind → rendered use → persistence → restore`

See [Compatibility and evidence levels](COMPATIBILITY.md) and the [FAQ](FAQ.md).
