# STRATA preview status

Build line: **UNCANNY Engine 5 — STRATA**  
Checkpoint: **cad2556**

## what is solid right now

- launcher/library integration is much farther along
- PCSX2 REVENANT saved packs can be built, verified, played without live reconstruction and restored
- native D3D9 REVENANT can capture real game textures and rebuild accepted assets
- D3D9/D3D11/D3D12 neural provider work has real-game execution evidence
- install/repair/remove logic is more defensive about files UNCANNY does not own

## native D3D9 REVENANT

The latest Deadpool test reached:

`capture -> reconstruct -> validate`

Five fresh neural outputs and five validated replacement assets were produced automatically.

The test did **not** reach:

`GPU upload -> replacement draw -> visible A/B`

The performance guard stayed active and the upload path correctly backed off.

That is why I am calling it progress, not a finished D3D9 REVENANT pass.

## open work

- finish visible D3D9 replacement proof
- broader PCSX2 game acceptance
- Vulkan/OpenGL parity
- real AMD hardware acceptance
- more motion/HUD/transparency acceptance
- connected sky/mip seam proof
- water/reflection acceptance
- controller/handheld sign-off
- shader/profile archive
- replay/comparison capture

Anything not proven stays listed here instead of being hidden in release hype.
