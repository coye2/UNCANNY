# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Hotfix 11**

- Runtime: `release-alpha.1.elysium-hotfix11`
- ABI: `141`
- GitHub release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-hotfix11
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-hotfix11/UNCANNY-v0.20.0-alpha.1-ELYSIUM-HOTFIX11.zip
- SHA-256: `14e28fad9a016a096e58167eebc53d8b96ead41687b1b366fbb34c92427c7bd7`

Hotfix 11 repairs a PCSX2 x64 / D3D11 first-frame black-screen failure class by making native Present fail open before optional UNCANNY/Deck preprocessing, delaying Feature-18 initialization until presentation is healthy, and adding exact Present-stage diagnostics.

The user-facing launcher is now native root-level `UNCANNY.exe`. Hotfix 10 ELYSIUM pass/slider wiring and the existing REVENANT/Lucid paths are preserved.