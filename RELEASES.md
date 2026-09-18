# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.3**

- Runtime revision: `release-alpha.1.elysium-engine45-hf18.3`
- BuildId: `elysium45-hf18.3`
- updateSerial: `1830`
- ABI: `143`
- Source revision: `75e8d346bea6fb30d2a20e50dd8e7e0170b77760`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.3.zip`
- SHA-256: `4f252c9c21891ecab2f7ecc37f95a0149854f4a2d18f2300402366f515169428`
- Release: https://github.com/coye2/UNCANNY/releases/latest

HF18.3 fixes launcher StrictMode startup failures and stale legacy-engine preference migration so a successful update cannot silently boot the old Lucid HOME menu unless the user explicitly selected Lucid.

The exact candidate passed full build/package/Windows/WARP/launcher-smoke/hash/Defender gates.

## Previous release history

HF18.2 cleaned the public ZIP and fixed launcher record refresh; HF18.1 addressed install preflight progress; HF18 closed the Universal API Bridge/tester-feedback push.

## Private source/workspace

The engineering source remains private and is not part of the public release.
