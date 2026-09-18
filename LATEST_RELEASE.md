# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.5**

- BuildId: `elysium45-hf18.5`
- updateSerial: `1850`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18.5`
- ABI: `143`
- Source revision: `8414a99010fff395c117baaadb77d63dbde946bf`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.5/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.5.zip
- SHA-256: `bc9b34e32556e95ef6098c7c57d74340e3bea64cc66f6687f346c6b5e280d3a9`

HF18.5 fixes the tester-reproduced launcher/library break: packaged scanning now resolves runtime dependencies correctly, malformed/legacy cache records are normalized before WPF binding, manual Add Game targets survive later scans, and the launcher asset is a WPF-safe 64×64 RGBA crop from the official Library logo.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35404395219

The exact candidate passed x86/x64 builds, HLSL, WARP rendered-quality validation, Windows launcher/install/rollback regressions, packaged logo/cache validation, packaged scanner execution, normal startup, **AllSigned startup**, ZIP integrity, and Microsoft Defender with 0 detections.

**Signing note:** HF18.5 is still unsigned. SmartScreen / Unknown Publisher can still appear until UNCANNY is signed with a trusted Authenticode identity.
