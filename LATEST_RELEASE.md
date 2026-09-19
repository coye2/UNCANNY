# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.6**

- BuildId: `elysium45-hf18.6`
- updateSerial: `1860`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18.6`
- ABI: `143`
- Source revision: `f14d29b1c321ee3b651511420993deab99af2062`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.6/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.6.zip
- SHA-256: `4cc88f35a53130c464671305cba3b8478f51a90149880fbafb19d86e956a9a13`

HF18.6 is the installer/update performance hotfix. It removes duplicate verification work, skips byte-identical installed files before rollback/commit, reuses prior provider state on updates, and adds real progress through the formerly opaque install stages.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35409019931

The exact candidate passed x86/x64 builds, HLSL, WARP rendered-quality validation, installer/rollback regressions, packaged install/update speed, official-logo/cache validation, scanner execution, normal startup, AllSigned startup, ZIP integrity and Microsoft Defender with 0 detections.

**Signing note:** HF18.6 is still unsigned. SmartScreen / Unknown Publisher can still appear until UNCANNY is signed with a trusted Authenticode identity.
