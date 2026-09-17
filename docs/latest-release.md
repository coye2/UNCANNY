# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — Adaptive Realism**

- Runtime: `release-alpha.1.elysium-engine45`
- ABI: `143`
- Latest: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip
- SHA-256: `f8b13f51cacd96b1b375b566c675d17661f66bb4bb2673cd34edf8e7f5859512`
- Malware verification: [MALWARE-VERIFICATION.md](MALWARE-VERIFICATION.md)

Engine 4.5 adds **Adaptive Realism** with five live levels — OFF / LOW / BALANCED / HIGH / INSANE — and capability tiers that scale from depth + motion reconstruction down to honest tonal/spatial fallback when trustworthy depth is unavailable.

D3D11 is the strongest current Adaptive Realism path because it can use capability-scored scene depth and UNCANNY optical flow. D3D12 and D3D9 remain supported with conservative fallbacks where scene depth cannot be trusted.

Motion Guard and Ghosting Guard remain authoritative, X2.5 uses the lowest temporal-history weight, `ENABLE UNCANNY OFF` remains the master bypass, and UNCANNY pass depth stays separate from DLSS 5 pass depth.

The release preserves Hotfix 11/12 compatibility work, PCSX2, REVENANT, launcher/install/rollback, Control Deck and provider handling.

The exact public package passed the full regression suite, 22 compiled Engine 4.5 checks, x86/x64 Adaptive Realism tests, production builds, strict package/integrity audits, install/rollback regression and Microsoft Defender scans of both the extracted package and final ZIP with **0 detections**.

Real-game visual/performance acceptance across specific NVIDIA, AMD and Intel hardware remains title-specific testing work.