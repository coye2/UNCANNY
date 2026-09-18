# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF15**

- Runtime: `release-alpha.1.elysium-engine45`
- BuildId: `elysium45-hf15`
- ABI: `143`
- Source revision: `b253880333ce2b8e4036cd5e53a6dcaf3bc69f8d`
- Published: 2026-09-17
- Latest release: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip
- SHA-256: `8ea0f3742fc52595eb1b95597ab3112d50be5867abfa6193fb4d5f5465e6460d`

## HF15

HF15 closes the current ELYSIUM 4.5 flagship build.

- **Scan on startup** is persisted and may be disabled.
- With startup scanning off, UNCANNY loads cached and manually-added entries without discovery.
- **Add game** remains authoritative across reboot and does not require a later scan.
- Windows short/long path aliases are canonicalized before deduplication.
- Adaptive Realism now includes shared scene evidence, split contact/diffuse lighting, bounded emissive bounce, Black Floor Intelligence, asymmetric local contrast, Legacy Cinema Reconstruction v2 and High/Insane Depth Material Sculpt.
- Motion Guard, Ghosting Guard and X2.5 clean-motion behavior remain protected.

## Verification

The exact source revision above passed the release gate in run:
https://github.com/coye2/uncanny-dev/actions/runs/35302273751

Windows manual-add persistence, install/remove rollback, HLSL compilation, PowerShell parsing, x86/x64 production builds, package audits, exact ZIP hash verification and Microsoft Defender ZIP/extracted-tree scans all passed.

Defender engine: `1.1.26080.3`  
Defender signatures: `1.459.263.0`  
Detections: **0**

Real-game visual/performance acceptance remains title/GPU/driver specific.
