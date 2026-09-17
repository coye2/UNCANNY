# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Hotfix 11**

- Runtime: `release-alpha.1.elysium-hotfix11`
- ABI: `141`
- GitHub release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-hotfix11
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-hotfix11/UNCANNY-v0.20.0-alpha.1-ELYSIUM-HOTFIX11.zip
- SHA-256: `a523db2ec0149f139a24c70aba36f68222cba057369b97864615b07c9c356e69`
- Malware verification: [MALWARE-VERIFICATION.md](MALWARE-VERIFICATION.md)

Hotfix 11 repairs a PCSX2 x64 / D3D11 first-frame black-screen failure class by making native Present fail open before optional UNCANNY/Deck preprocessing, delaying Feature-18 initialization until presentation is healthy, and adding exact Present-stage diagnostics.

The user-facing launcher is native root-level `UNCANNY.exe`. Hotfix 10 ELYSIUM pass/slider wiring and the existing REVENANT/Lucid paths are preserved.

The corrected public package does not ship internal acceptance-test executables. `revenant-commit32.exe`, `revenant-commit64.exe` and the rest of the internal diagnostics EXEs are CI-only.

The cleaned runtime tree and the completed release ZIP were both scanned with Microsoft Defender Antivirus after signature update and returned **0 detections**. Defender engine `1.1.26080.3`, signatures `1.459.256.0`, product `4.18.26080.3`.