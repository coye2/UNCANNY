# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.6**

- Runtime revision: `release-alpha.1.elysium-engine45-hf18.6`
- BuildId: `elysium45-hf18.6`
- updateSerial: `1860`
- ABI: `143`
- Source revision: `852e617c003a8672ead6bd7607e24163a99b8fc5`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.6.zip`
- SHA-256: `3f9bbe8eb520918df9e23a84f879bce8079b197f2e194326430b3be4930be111`
- Release: https://github.com/coye2/UNCANNY/releases/latest

HF18.6 focuses on game install/update latency and PCSX2 startup: single-pass verification, unchanged-file pruning, verified same-build no-op updates, verified neural-core reuse, bounded provider discovery, bounded/fail-open REVENANT recovery, and a fast PCSX2 runtime-attach path.

The exact public package passed build/package/Windows/WARP, packaged install/update speed, launcher/logo/cache/scanner, packaged PCSX2 wrapper launch, normal startup, AllSigned startup, exact hash/extraction and Defender gates. Same-build second-pass update measured **3884 ms** with zero file transaction.

HF18.6 remains unsigned, so Windows SmartScreen/Unknown Publisher may still appear until trusted code signing is configured.

## Previous release history

HF18.5 repaired packaged scanning/library/logo behavior; HF18.4 fixed restrictive-policy no-launch; HF18.3 hardened StrictMode/path handling and engine selection; HF18.2 cleaned the public ZIP; HF18.1 addressed install preflight progress; HF18 closed the Universal API Bridge/tester-feedback push.

## Private source/workspace

The engineering source remains private and is not part of the public release.
