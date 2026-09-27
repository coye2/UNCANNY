# changelog

## STRATA preview — cad2556 — 2026-09-27

- moved the public preview onto UNCANNY Engine 5 — STRATA
- kept the newer integrated launcher/library work
- kept the newer neural bridge work for D3D9/D3D11/D3D12
- kept the PCSX2 REVENANT saved-pack path
- native D3D9 REVENANT captured real Deadpool textures and produced five validated neural replacement assets without Retry Worker/Rebuild Assets
- added exact replacement-size cache admission so one native-PC asset cannot push the managed cache past its cap
- REVENANT Pause now blocks new native-PC reconstruction jobs
- D3D9 GPU fixtures passed capture, upload, readback change, OFF restore, stale-update rejection and reset cleanup
- visible D3D9 in-game replacement proof is still open; the real-game performance guard stayed active and I did not weaken it to force a pass

This is a preview checkpoint, not a claim that every STRATA path is finished.

## v0.20.0-alpha.2 — Final Alpha — 2026-09-22

- froze the validated Final Alpha candidate
- cleaner bounded detail/noise control
- conservative water recovery
- restricted rigid D3D11 geometry replacement proof
- normal-only recovery
- isolated material targeting/restoration
- production x86/x64 builds + private validation

Final Alpha remains the current stable public checkpoint while STRATA is being finished.
