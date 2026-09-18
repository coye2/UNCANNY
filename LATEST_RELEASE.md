# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — Hotfix 13.1**

- Runtime: `release-alpha.1.elysium-engine45`
- ABI: `143`
- Source revision: `6d9b367bb4ef6506ff33be7023c05634019e78f2`
- Published: 2026-09-17
- Latest release: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip
- SHA-256: `69face793720c1d832afb6d8ea7d69091e5475ce231c7c62f84beef02c96675a`

## Hotfix 13.1

The launcher startup crash from the inline logo XAML `Path.FillRule` member is fixed in the current package.

Hotfix 13.1 fixes the tester-reported remove/restore failures and pushes Adaptive Realism harder.

- Remove restores the complete recorded UNCANNY install stack for the selected target.
- Runtime-generated graphics logs such as `ReShade.log` may change without blocking uninstall.
- Original/user files remain protected from unsafe overwrite.
- The launcher carries the official UNCANNY emblem inline.
- Adaptive Realism is **OFF / LOW / BALANCED / HIGH / INSANE**.
- New installs seed **INSANE + Reference Stack**.
- The reference stack scales with Adaptive Realism; OFF is a true bypass.
- Stronger source/evidence-bounded contact occlusion, diffuse/specular response, scene adaptation, local contrast and meso clarity.

## Verification

Windows HLSL compile, PowerShell parsing, two-layer full-stack rollback, changed-ReShade.log restore, archive integrity and Microsoft Defender all passed. Defender engine `1.1.26080.3`, signatures `1.459.260.0`, 0 detections.

Real-game visual/performance acceptance remains title/GPU/driver specific.
