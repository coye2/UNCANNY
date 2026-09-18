# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF16**

- Runtime: `release-alpha.1.elysium-engine45`
- BuildId: `elysium45-hf16`
- ABI: `143`
- Source revision: `6c7ee4675a110fceb3c2c5bdddf82eb4d2745471`
- Published: 2026-09-18
- Latest release: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip
- SHA-256: `fb9a49e68ef11ba8b6e5932e37eee01b4875d7fb782249b92965601dc93e381a`

## HF16

HF16 adds a bounded ELYSIUM runtime recovery path for repeated post-FX/device faults.

- Native Present remains alive during recovery backoff.
- Recovery first reduces Adaptive Realism / Performance Guard cost.
- Continued instability locally cuts Reference Stack, pass depth and optional DLSS 5 cost.
- Saved user settings are not overwritten.
- Higher-cost rendering returns only after a sustained clean run.
- HF15 launcher/library, rollback, Adaptive Realism, Motion Guard/Ghosting Guard, PCSX2 and REVENANT work is preserved.

## Verification

Exact candidate run: https://github.com/coye2/uncanny-dev/actions/runs/35305423361

Static/resource gates, x86/x64 production builds, Windows HLSL compilation, PowerShell parsing, manual Add game persistence, dynamic install/remove rollback, exact ZIP hash verification and Microsoft Defender ZIP/extracted-tree scans all passed with **0 detections**.

Real-game visual/performance acceptance remains title/GPU/driver specific.
