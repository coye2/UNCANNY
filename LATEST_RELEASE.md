# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.6**

- BuildId: `elysium45-hf18.6`
- updateSerial: `1860`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18.6`
- ABI: `143`
- Source revision: `852e617c003a8672ead6bd7607e24163a99b8fc5`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.6/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.6.zip
- SHA-256: `3f9bbe8eb520918df9e23a84f879bce8079b197f2e194326430b3be4930be111`

HF18.6 fixes installer/update latency and the PCSX2 post-install no-open path. Healthy same-build updates now use a verified no-op fast path; the packaged gate measured **3884 ms** with zero file transaction. PCSX2 startup is bounded/fail-open and no longer performs unnecessary engine work before the emulator can open.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35412014280

The exact candidate passed x86/x64 builds, HLSL, WARP, installer/rollback regressions, packaged install/update speed, logo/cache, scanner, packaged PCSX2 wrapper → verified original/runtime launch, normal startup, AllSigned startup, ZIP integrity and Microsoft Defender with 0 detections.

**Signing note:** HF18.6 is still unsigned. SmartScreen / Unknown Publisher can still appear until UNCANNY is signed with a trusted Authenticode identity.
