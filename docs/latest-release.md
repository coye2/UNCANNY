# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.6**

- Runtime: `release-alpha.1.elysium-engine45-hf18.6`
- BuildId: `elysium45-hf18.6`
- updateSerial: `1860`
- ABI: `143`
- Source revision: `f14d29b1c321ee3b651511420993deab99af2062`
- Published: 2026-09-18
- Latest release: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45-hf18.6
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.6/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.6.zip
- SHA-256: `4cc88f35a53130c464671305cba3b8478f51a90149880fbafb19d86e956a9a13`

## HF18.6

- removes duplicate installer verification work
- uses streaming PE architecture/import checks
- reuses the verified original-game digest
- skips byte-identical installed files before rollback/commit
- backs up and writes only files that actually change
- reuses prior negative provider discovery state during routine updates
- adds visible progress through the old 24–95% stall range
- preserves HF18.5 scanner/library/logo fixes and HF18 rendering/runtime behavior

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35409019931

The exact package passed x86/x64 production builds, HLSL compilation, D3D11 WARP rendered-quality validation, Windows launcher/install/rollback regressions, packaged install/update speed, logo/cache/scanner checks, normal startup, AllSigned startup, ZIP integrity/hash verification and Microsoft Defender scans with 0 detections.
