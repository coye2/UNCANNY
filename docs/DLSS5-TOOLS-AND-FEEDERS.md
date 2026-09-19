# DLSS 5 integration

UNCANNY is not just a DLSS feeder. The neural route is one part of the engine.

Three things are separate in the Control Deck:

- **UNCANNY Passes** — ELYSIUM reconstruction depth
- **Adaptive Realism** — scene-aware native processing
- **DLSS 5 Passes** — optional provider-backed neural work

That separation matters because ELYSIUM can work without the neural provider.

## What counts as a working neural path

UNCANNY does not count a loaded DLL or an enabled overlay as proof by itself.

The useful path is:

`attach → frame transport → provider → evaluate → return → compose → present`

If it breaks anywhere in that chain, the game should keep the live source frame instead of hanging on stale output.

## HF18.11

The earlier D3D11 stability fix went too far and kept neural execution disabled forever.

HF18.11 keeps the protected startup behavior, but lets neural resources warm up after the route has stayed healthy long enough. The riskier direct depth/temporal path is still held back on the safe route.

## Where UNCANNY fits

UNCANNY overlaps with projects such as RenoDX, OptiScaler, DLSS feeders, DFC and RTX Remix, but it is not trying to be a clone of any one of them.

The project is built around one runtime: live reconstruction, motion protection, compatibility routing, optional neural work, REVENANT, controls, diagnostics and rollback.

UNCANNY is independent and is not affiliated with NVIDIA or those projects.
