# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.4**

- BuildId: `elysium45-hf18.4`
- updateSerial: `1840`
- Runtime revision: `release-alpha.1.elysium-engine45-hf18.4`
- ABI: `143`
- Source revision: `b865fab000762e7e3015484945d1f1af5d96fe52`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.4/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.4.zip
- SHA-256: `c874239bbd41cfa6c271db10e364f97c241bdc5d5d55c2ff50542d12c6b8f417`

HF18.4 fixes the no-launch regression after HF18.3. The native `UNCANNY.exe` now launches only its child Windows PowerShell bootstrap with process-scoped `ExecutionPolicy Bypass`, so Restricted/AllSigned user policy cannot silently kill startup. Persistent machine/user execution policy is not changed, and Defender/SmartScreen are not disabled.

It preserves the StrictMode-safe installed/cache path fixes, official cropped UNCANNY PNG emblem, stale-Lucid migration, Universal API Bridge, PCSX2, REVENANT, rollback, and HF18 rendering behavior. The updater hotfix parser now maps HF18.3 → 1830 and HF18.4 → 1840 correctly.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35399115389

The exact candidate passed x86/x64 builds, HLSL, WARP rendered-quality validation, Windows launcher/install/rollback regressions, packaged normal startup smoke, packaged **AllSigned startup smoke**, ZIP integrity, and Microsoft Defender with 0 detections.

**Signing note:** HF18.4 is still unsigned. SmartScreen / Unknown Publisher can still appear until UNCANNY is signed with a trusted Authenticode identity.
