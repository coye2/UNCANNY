# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Hotfix 11**

- Runtime: `release-alpha.1.elysium-hotfix11`
- ABI: `141`
- Published: 2026-09-17
- GitHub release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-hotfix11
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-hotfix11/UNCANNY-v0.20.0-alpha.1-ELYSIUM-HOTFIX11.zip
- SHA-256: `14e28fad9a016a096e58167eebc53d8b96ead41687b1b366fbb34c92427c7bd7`

Hotfix 11 is a tester-derived D3D11 startup-safety repair. Direct D3D11 now establishes native presentation before optional UNCANNY/Control Deck preprocessing can run, Feature-18 startup waits for a healthy advancing Present stream, and diagnostics identify whether a stall occurred before or inside the game's native Present call.

The public entry point is now root-level native `UNCANNY.exe` rather than the old top-level `UNCANNY.cmd` launcher. Hotfix 10 ELYSIUM pass/slider wiring, REVENANT, PCSX2 integration and the preserved Lucid engine bundle remain intact.

The exact public ZIP passed focused Hotfix 11 regressions, x86/x64 production builds, 12 public diagnostic builds, protected-resource verification, PE hardening checks and the strict package audit. Real hardware retesting remains required for the original PCSX2/GPU black-screen report.