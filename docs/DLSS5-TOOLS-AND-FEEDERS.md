# neural bridge / DLSS route

UNCANNY's neural bridge is one part of the engine. It is not the whole renderer and it is not REVENANT.

## what counts as working

I do not count a DLL being present as proof.

The useful chain is:

`attach -> get the frame -> create provider feature -> evaluate -> return output -> compose -> present`

If the chain breaks, the game should keep the real source frame instead of hanging on stale output.

## current proof

Development testing has real provider create/evaluate/output-use evidence in:

- D3D9 — Deadpool
- D3D11 — Fallout 4
- D3D12 — Subnautica 2

Those tests are real progress, but they do not make Vulkan/OpenGL/AMD magically complete.

## D3D9

The current D3D9 neural route uses the compatibility/helper path. That is different from REVENANT's D3D9 asset-replacement path.

Do not mix the two when reporting a bug.

## controls

STRATA/Control Deck keeps normal reconstruction controls separate from provider-backed neural work. If a control does not have a real runtime path, it should not be presented as doing something.

## vendor naming

UNCANNY does not call FSR or another provider “DLSS”.

NVIDIA and DLSS are NVIDIA trademarks. UNCANNY is independent and is not endorsed by NVIDIA.
