# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.6**

- Runtime revision: `release-alpha.1.elysium-engine45-hf18.6`
- BuildId: `elysium45-hf18.6`
- updateSerial: `1860`
- ABI: `143`
- Source revision: `f14d29b1c321ee3b651511420993deab99af2062`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.6.zip`
- SHA-256: `4cc88f35a53130c464671305cba3b8478f51a90149880fbafb19d86e956a9a13`
- Release: https://github.com/coye2/UNCANNY/releases/latest

HF18.6 focuses on game install/update latency: single-pass release verification, streaming PE checks, unchanged-file pruning, changed-files-only rollback transactions, provider-state reuse, and granular progress.

The exact public package passed build/package/Windows/WARP, packaged install/update speed, launcher/logo/cache/scanner, normal startup, AllSigned startup, exact hash/extraction and Defender gates.

HF18.6 remains unsigned, so Windows SmartScreen/Unknown Publisher may still appear until trusted code signing is configured.

## Previous release history

HF18.5 repaired packaged scanning/library/logo behavior; HF18.4 fixed restrictive-policy no-launch; HF18.3 hardened StrictMode/path handling and engine selection; HF18.2 cleaned the public ZIP; HF18.1 addressed install preflight progress; HF18 closed the Universal API Bridge/tester-feedback push.

## Private source/workspace

The engineering source remains private and is not part of the public release.
