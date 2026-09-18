# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.5**

- Runtime revision: `release-alpha.1.elysium-engine45-hf18.5`
- BuildId: `elysium45-hf18.5`
- updateSerial: `1850`
- ABI: `143`
- Source revision: `8414a99010fff395c117baaadb77d63dbde946bf`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.5.zip`
- SHA-256: `bc9b34e32556e95ef6098c7c57d74340e3bea64cc66f6687f346c6b5e280d3a9`
- Release: https://github.com/coye2/UNCANNY/releases/latest

HF18.5 fixes packaged scanning, cache/manual/scan normalization, authoritative manual-target retention, and the tester-reproduced launcher-logo decode failure.

The exact package passed build/package/Windows/WARP, official-logo decode, cache normalization, packaged scanner execution, normal launcher startup, **AllSigned launcher startup**, hash and Defender gates.

HF18.5 remains unsigned, so Windows SmartScreen/Unknown Publisher may still appear until trusted code signing is configured.

## Previous release history

HF18.4 fixed restrictive-policy no-launch; HF18.3 hardened StrictMode/path handling and engine selection; HF18.2 cleaned the public ZIP; HF18.1 addressed install preflight progress; HF18 closed the Universal API Bridge/tester-feedback push.

## Private source/workspace

The engineering source remains private and is not part of the public release.
