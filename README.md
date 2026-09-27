# UNCANNY

UNCANNY is my real-time remastering project for Windows games and emulators.

## latest preview release

### UNCANNY Engine 5 — STRATA Preview cad2556

**STRATA is live now.**

[**Download STRATA Preview cad2556**](https://github.com/coye2/UNCANNY/releases/tag/strata-preview-cad2556)

Direct ZIP:

[UNCANNY-STRATA-PUBLIC-PREVIEW-cad2556-POLISHED.zip](https://github.com/coye2/UNCANNY/releases/download/strata-preview-cad2556/UNCANNY-STRATA-PUBLIC-PREVIEW-cad2556-POLISHED.zip)

SHA-256:

`d41be8a9794cbe0426cfb9a1840b00c509b946bd1056a869e8ad80dd3fe408ac`

This is the newest public build. It is marked **Pre-release** because some STRATA paths are still being finished.

**Stable build:** v0.20.0-alpha.2 — Final Alpha

## what STRATA is

STRATA is the next engine line. The goal is simple: make UNCANNY feel like one actual program instead of a launcher, graphics runtime, REVENANT worker and a bunch of separate tools.

The current preview already brings those pieces much closer together.

## what's working in the STRATA preview

- rebuilt launcher with a saved game library, manual add, scanning, search, themes and fullscreen mode
- Control Deck profiles, themes and live controls
- REVENANT captured-texture packs for PCSX2
- saved REVENANT packs can play without running the reconstruction worker again
- backup/restore around managed texture packs
- native-PC REVENANT capture + reconstruction work on D3D9
- real neural provider create/evaluate/output-use evidence on D3D9, D3D11 and D3D12 test games
- safer repair/remove paths that protect files UNCANNY does not own

## what is not finished yet

I am not going to call unfinished stuff finished just because a harness passed.

- native D3D9 REVENANT has real capture + reconstruction proof, but the latest Deadpool run did not finish visible replacement A/B proof
- Vulkan/OpenGL are not at DirectX parity yet
- AMD hardware proof is still missing
- full controller/handheld acceptance is still open
- sky seams, water/reflections and some motion cases are still being pushed
- the full shader/profile archive and replay/comparison capture system are not done

## install

1. Download the STRATA preview above or another build from **Releases**.
2. Extract the whole ZIP somewhere permanent.
3. Run `UNCANNY.exe`.
4. Add a game manually or use **Scan PC**.
5. Select the game and install/update UNCANNY.
6. Launch it and press **Home** for the Control Deck.

Do not run UNCANNY from inside the ZIP and do not mix files from different builds.

## REVENANT

REVENANT is the asset side of UNCANNY. It can capture supported assets, rebuild accepted ones and feed replacements back into supported games/emulators.

PCSX2 currently has the strongest saved-pack workflow. Build a captured pack once, switch to saved mode, then play it without keeping the reconstruction worker alive.

See [Captured texture packs](docs/CAPTURED-TEXTURE-PACKS.md).

## neural rendering

The neural bridge is separate from REVENANT. Current development has real provider execution evidence on D3D9, D3D11 and D3D12. That does not mean every API, GPU or game is certified.

UNCANNY does not rename another vendor's technology and call it DLSS.

## support UNCANNY

If you like what I'm building and want to help me keep pushing it, you can support UNCANNY on [Ko-fi](https://ko-fi.com/coye2).

## source / security

UNCANNY is closed source. The public repo is for releases, docs and support material.

The binaries are currently unsigned, so Windows can show Unknown Publisher. Do not disable Defender or add broad exclusions for UNCANNY.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA, AMD, PCSX2 or the games it supports.
