# DLSS 5 integration

UNCANNY is not just a DLSS feeder. The optional neural route is one part of a larger remaster runtime.

The three main controls are separate:

- **UNCANNY Passes** — ELYSIUM reconstruction depth
- **Adaptive Realism** — scene-aware native processing
- **DLSS 5 Passes** — optional provider-backed neural work

That separation matters because ELYSIUM can run without the neural provider.

## How the neural route is treated

UNCANNY only counts the path as healthy when the frame makes it through the useful parts of the chain:

`attach → frame transport → provider → evaluate → return → compose → present`

Loading a provider DLL or showing an overlay is not treated as proof that the final frame used neural output.

## HF18.11 and D3D11

Earlier D3D11 stability work was too conservative: it protected Present, but it also kept neural execution disabled forever.

HF18.11 keeps the safe startup behavior and adds staged promotion after the D3D11 route has been stable long enough.

Native depth/temporal behavior stays conservative on that safe route, so the fix does not simply turn every old feature back on at once.

## Other projects

UNCANNY can overlap with tools such as RenoDX, OptiScaler, DLSS feeders, DFC and RTX Remix, but it is not trying to be a drop-in clone of any of them.

The project is built around one integrated runtime: live reconstruction, motion protection, compatibility routing, optional neural work, REVENANT, controls, diagnostics and rollback.

UNCANNY is independent and is not affiliated with NVIDIA or those projects.
