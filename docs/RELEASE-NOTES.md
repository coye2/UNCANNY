# UNCANNY Engine 5 — STRATA preview cad2556

This is the first STRATA preview from the current Engine 5 line.

The biggest change is that UNCANNY is starting to feel like one program instead of a pile of separate pieces.

## REVENANT

PCSX2 saved packs are working: build accepted captured textures, switch to saved mode and play without keeping reconstruction alive every launch.

Native D3D9 moved forward too. Deadpool produced real captures and five validated neural replacement assets automatically.

The last Deadpool run did **not** finish visible GPU replacement proof because the full graphics stack kept the performance guard high enough to defer uploads. I left the safety guard intact instead of cheating the test.

## STRATA

- newer launcher/library integration
- themes + fullscreen work
- Control Deck profiles/themes
- safer repair/remove/restore paths
- combined renderer + REVENANT + neural integration

## neural bridge

Real provider create/evaluate/output-use evidence already exists on D3D9, D3D11 and D3D12.

Vulkan, OpenGL and AMD are not being called complete in this preview.

## still open

- D3D9 REVENANT visible A/B
- full sky/cubemap seam acceptance
- full water/reflection + motion acceptance
- Radeon hardware acceptance
- Vulkan/OpenGL parity
- full controller/handheld sign-off
- shader/profile archive
- replay + automatic comparison capture

This is a preview. I am not using a new engine name to pretend every single Engine 5 feature is already done.
