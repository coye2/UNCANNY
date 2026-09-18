# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF17**

- BuildId: `elysium45-hf17`
- ABI: `143`
- Source revision: `192d0c652b2ef3dee8dcb542a93ed816cc6cea9f`
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip
- SHA-256: `cef5daff98e611e9da27f9365a660f14f82208238ce3d277db3f1088ba1a304e`

HF17 fixes the post-install/update launcher crash caused by legacy or malformed library/cache entries, adds fail-open post-install UI refresh, adds a Fallout 4 D3D11 safe startup route, and changes the Control Deck to HOME-only lazy startup with automatic visible fallback.

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35308356045

The exact candidate passed Windows library regressions, x86/x64 production builds, shipped HLSL compilation, PowerShell parsing, install/remove rollback, exact ZIP verification and Microsoft Defender scans with 0 detections.

Fallout 4 still requires real-machine retesting on the affected PC.
