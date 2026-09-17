# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Hotfix 11**

- Runtime: `release-alpha.1.elysium-hotfix11`
- ABI: `141`
- Published: 2026-09-17
- GitHub release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-hotfix11
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-hotfix11/UNCANNY-v0.20.0-alpha.1-ELYSIUM-HOTFIX11.zip
- SHA-256: `a523db2ec0149f139a24c70aba36f68222cba057369b97864615b07c9c356e69`
- Malware verification: https://github.com/coye2/UNCANNY/blob/main/docs/MALWARE-VERIFICATION.md

Hotfix 11 is a tester-derived D3D11 startup-safety repair. Direct D3D11 now establishes native presentation before optional UNCANNY/Control Deck preprocessing can run, Feature-18 startup waits for a healthy advancing Present stream, and diagnostics identify whether a stall occurred before or inside the game's native Present call.

The public entry point is root-level native `UNCANNY.exe`. Hotfix 10 ELYSIUM pass/slider wiring, REVENANT, PCSX2 integration and the preserved Lucid engine bundle remain intact.

## Security packaging correction

The corrected Hotfix 11 release does not ship internal acceptance-test executables. `revenant-commit32.exe`, `revenant-commit64.exe` and the other internal `diagnostics/` EXEs were removed from the user-facing package.

The exact final ZIP was produced behind a Microsoft Defender release gate on a fresh Windows runner. Defender signatures were updated immediately before scanning. The cleaned runtime tree and the completed ZIP both returned **0 detections** using Defender engine `1.1.26080.3`, signature version `1.459.256.0` and product version `4.18.26080.3`.

The ZIP contains `docs/MALWARE-VERIFICATION.md`, and the GitHub release includes the machine-readable `MALWARE-VERIFICATION-HOTFIX11.json` attachment.

The exact public ZIP also passed focused Hotfix 11 regressions, x86/x64 production builds, protected-resource verification, PE hardening checks and the strict package audit. Internal diagnostic/test binaries are CI-only and are not shipped. Real hardware retesting remains required for the original PCSX2/GPU black-screen report.