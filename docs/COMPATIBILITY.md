# Compatibility

UNCANNY is still alpha, so this page describes what the runtime currently targets rather than pretending every game is certified.

| Route | Status | Notes |
|---|---|---|
| D3D11 x64 | active | strongest generic ELYSIUM path; HF18.11 adds staged neural promotion |
| D3D11 x86 | experimental | helper path where needed |
| D3D12 x64 | active | HF18.13 fail-open Present + transactional resize/warmup serialization |
| D3D10 / 10.1 | experimental | compatibility route |
| D3D9 | legacy | supported with reduced capability when scene data is limited |
| PCSX2 | active test target | current route uses Direct3D 12 / `Renderer=15` |
| Vulkan | early / partial | not at DirectX parity |
| OpenGL | early / partial | not at DirectX parity |

## What “works” means here

There are a few different milestones that are easy to mix up:

- **attached** — UNCANNY loaded into the target
- **presenting** — the game's frame stream is still advancing
- **ELYSIUM active** — UNCANNY's native image path is actually processing
- **neural active** — the provider created/evaluated work and current output returned
- **visible result** — the intended output is actually on screen

A DLL on disk, a loaded provider, an overlay, or a completed worker job is not enough by itself to prove visible output.

## D3D11

D3D11 starts fail-open. The game gets a stable native Present stream before optional work is allowed to become important.

HF18.11 keeps the conservative safe path but allows neural promotion after a healthy stabilization window. The more aggressive direct-depth/temporal route is still deferred on that safe path.

## D3D12

HF18.10 added the D3D12 startup protection: let the game establish ownership and presentation first, then let UNCANNY take over only when it is safe.

HF18.13 keeps Present fail-open and fixes the later transition. Early resize still passes through natively before UNCANNY owns the swapchain. After ownership, ResizeBuffers gets a bounded transactional handoff instead of immediately failing while maintenance is warming resources, and the same swapchain cannot resize underneath active off-Present warmup.

## PCSX2

PCSX2 is currently kept on Direct3D 12 using `Renderer=15`.

The launcher uses a sidecar instead of replacing `pcsx2-qt.exe`. Existing old wrapper installs are migrated during update.

## Motion and passes

Motion Guard and Ghosting Guard reduce or reject unstable history when motion confidence drops or the current/history frames disagree.

X2.5 intentionally uses less temporal history than the other deep modes and is the clean-motion option.

## Vendors

The native ELYSIUM image path is not NVIDIA-only.

The optional DLSS 5 route depends on NVIDIA/provider support. Running ELYSIUM on AMD or Intel does not imply DLSS 5 availability.

## Anti-cheat / protected titles

UNCANNY is not designed to bypass anti-cheat or protected-process restrictions. If a title does not safely allow the runtime path, optional processing should fail closed/fail open rather than trying to evade the protection.

## Reporting compatibility

Useful reports include the game, executable, API, x86/x64, GPU/driver, UNCANNY version, what you saw, and the session's status/log output.
