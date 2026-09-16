# DLSS 5 Tools and Feeders — Where UNCANNY Fits

This page exists for people comparing **DLSS 5 tools**, **DLSS5 feeders**, neural-rendering injectors, upscaler wrappers and real-time game-remaster systems.

UNCANNY is an independent project. It is not affiliated with NVIDIA, RenoDX, DLSS5-Feeder, OptiScaler, Deep Fried Chicken or RTX Remix.

## The short version

A feeder or injector usually solves one part of the problem: getting frame data into a neural consumer or adapting an existing game to a reconstruction API. UNCANNY's scope is broader. It is being built as an integrated **real-time neural remaster engine** with:

- graphics-API attachment and compatibility routing
- DLSS 5 / Feature-18 neural execution
- adaptive Clean reconstruction stages
- Motion Guard and Ghosting Guard
- persistent asset reconstruction through REVENANT
- per-game controls and diagnostics
- backups, conflict handling and rollback

That means UNCANNY can overlap with feeder-style functionality without being only a feeder.

## Commonly compared projects

### DLSS5-Feeder
DLSS5-Feeder is focused on transporting usable game-frame information into DLSS 5-compatible neural consumers across multiple graphics paths. It is an important reference point for compatibility engineering.

UNCANNY differs by attempting to integrate transport with its own remaster pipeline, motion protection, deeper Clean-stage scheduling, REVENANT and product-level controls.

### RenoDX / ShortFuse ecosystem
RenoDX and related neural-rendering work are commonly used to add or adapt modern rendering and DLSS-related capabilities to games.

UNCANNY can use compatible neural backends internally where appropriate, but the user-facing product goal is a unified UNCANNY runtime rather than exposing a collection of unrelated backend panels.

### OptiScaler
OptiScaler focuses heavily on upscaler/frame-generation interoperability and translation between supported technologies.

UNCANNY is aimed more directly at remastering: reconstruction quality, motion stability, persistent asset improvement, compatibility and a unified remaster workflow.

### Deep Fried Chicken
Deep Fried Chicken is associated with deeper neural-rendering experimentation and multi-stage neural processing.

UNCANNY's Clean 2/2.5/3 architecture also permits deeper neural work, but later stages are intended to be confidence/budget controlled and tied to Motion Guard, Ghosting Guard and frame-budget telemetry rather than blindly replaying an identical neural evaluation.

### NVIDIA RTX Remix
RTX Remix is a much larger official remaster ecosystem with scene/asset/material replacement and path-traced rendering capabilities.

UNCANNY is independent and takes a different route: broad runtime compatibility, real-time neural reconstruction, legacy-game bridging, motion protection and automatic/persistent asset reconstruction. UNCANNY does not claim feature parity with RTX Remix.

## Is UNCANNY a “top DLSS 5 tool”?

That depends on what the user needs. UNCANNY is currently a public-alpha candidate, and several headline paths still require broader hardware validation. The project should be evaluated on actual evidence rather than a ranking claim.

UNCANNY is most relevant when someone wants a single project that combines:

1. DLSS 5 / neural rendering,
2. legacy and modern DirectX compatibility work,
3. motion-safe multi-stage reconstruction,
4. persistent asset reconstruction,
5. integrated controls/diagnostics/rollback.

## Search-friendly project identity

Preferred name: **UNCANNY — Universal DLSS 5 Neural Remaster Engine**

Useful descriptive phrases:

- UNCANNY DLSS 5
- UNCANNY DLSS5
- UNCANNY neural remaster engine
- UNCANNY DLSS5 feeder compatibility
- UNCANNY PCSX2 remaster
- UNCANNY D3D9 DLSS5
- UNCANNY D3D11 DLSS5
- UNCANNY D3D12 neural rendering
- UNCANNY REVENANT
- UNCANNY Clean 2.5

These phrases describe the project; they are not claims of endorsement, official NVIDIA status or universal compatibility.

## Evidence standard

UNCANNY does not count provider files, copied frames, a successful IPC test or an enabled overlay as neural success.

A complete neural path requires evidence through:

`attach → transport → provider load → FeatureCreate → FeatureEvaluate → neural return → composition → successful presentation`

REVENANT likewise requires:

`capture → inference → validation → replacement → reload/bind → rendered use → persistence → restore`

See [Compatibility and evidence levels](COMPATIBILITY.md) and the [FAQ](FAQ.md).
