# UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18

HF18 closes the current Universal API Bridge and tester-feedback push.

## Compatibility / startup

- D3D11 now uses a universal native-Present stabilization floor: optional UNCANNY preprocessing waits for 120 successful native Presents on a new swapchain before joining the path.
- Native Present remains the fail-open baseline when capability, provider, ownership or processing-source evidence is incomplete.
- Universal API Bridge routing separates presentation ownership from processing-source evidence and keeps deterministic route-group correlation.
- D3D12 queue/backbuffer/state evidence is captured from creation/lifecycle events instead of guessed.
- Legacy DirectX routes are normalized through the bridge.
- Vulkan/OpenGL lifecycle and presentation compatibility observation is preserved, but HF18 does not claim full ELYSIUM/neural-processing parity there.
- Protected/anti-cheat-sensitive routes remain conservative; UNCANNY does not attempt to evade protection systems.

## ELYSIUM visual pipeline

- Stronger source-backed facial reconstruction and complexion/structure recovery.
- Stronger source-hue and chroma recovery across shadows, midtones and highlights.
- Stronger material, edge, distant-detail and texture-relief response.
- Motion Protection Strength and Ghosting Guard are independently effective; Ghosting Guard no longer masks Motion Strength.
- Microtexture now has a dedicated source-backed response instead of disappearing inside generic sharpening.
- Added clean-room local exposure fusion, source-radiance recovery, depth-proven relighting/contact shaping, contrast-adaptive clarity/sharpening and source-directed subpixel edge resolve.
- No proprietary iMMERSE/Marty McFly/Pascal Gilcher shader implementation, binary, LUT or texture is bundled.

## Control Deck / launcher / install

- Live image controls expose visible info/help text.
- Installer verification reports exact failure reasons without telling users to disable security software.
- Updater recognizes the current Engine 4.5 release naming convention.
- Full uninstall removes UNCANNY-owned residue only after recorded install layers restore safely.
- Manual Add Game, optional Scan on startup, PCSX2 support, rollback and REVENANT are preserved.

## Rendered-quality validation

HF18 adds a real D3D11 WARP pixel-rendering matrix instead of relying only on static wiring checks.

- All 42 exposed floating image controls must change rendered output above a meaningful response floor.
- Targeted checks cover face reconstruction, source-color recovery, denoise, edge recovery, finite output and clipping.
- On the controlled degraded-reference scene, balanced ELYSIUM reduced RGB RMSE from about 0.08236 to 0.06618.
- Source-color chroma error dropped from about 0.04582 to 0.02207.
- Motion Strength endpoint delta measured about 0.06887 after the masking fix.
- Face Reconstruction endpoint delta measured about 0.04491.
- Color Recovery endpoint delta measured about 0.25015.

These are controlled CI measurements, not claims about every real game.

## Exact release verification

- Source revision: `0c5de983a400dd77d85992c6a5c1d37bcc3139eb`
- BuildId: `elysium45-hf18`
- updateSerial: `1800`
- ABI: `143`
- Validation run: https://github.com/coye2/uncanny-dev/actions/runs/35377702421
- x86/x64 production + legacy + acceptance builds: **PASS**
- Windows HLSL compilation: **PASS**
- D3D11 WARP rendered visual-quality gate: **PASS**
- Installer / rollback / manual-add regressions: **PASS**
- Exact ZIP integrity/hash: **PASS**
- Microsoft Defender final ZIP + extracted tree: **PASS / 0 detections**

Package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.zip`

SHA-256:

`21f654c3260a3c258f7121574edef56c44a718449c16f51aa20d7695bc925489`

Real-game visual quality, motion, compatibility and performance remain title/GPU/driver specific. AMD and Intel share vendor-neutral ELYSIUM image-processing logic where supported, but the WARP gate is not an AMD or Intel hardware test.

UNCANNY is independent and is not affiliated with or endorsed by NVIDIA. NVIDIA and DLSS are trademarks of NVIDIA Corporation.
