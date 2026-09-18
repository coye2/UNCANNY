# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF16**

- Runtime revision: `release-alpha.1.elysium-engine45`
- BuildId: `elysium45-hf16`
- updateSerial: `1600`
- ABI: `143`
- Source revision: `6c7ee4675a110fceb3c2c5bdddf82eb4d2745471`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45.zip`
- SHA-256: `fb9a49e68ef11ba8b6e5932e37eee01b4875d7fb782249b92965601dc93e381a`
- Release: https://github.com/coye2/UNCANNY/releases/latest

HF16 is the emergency runtime-resilience update. Repeated post-FX/device faults now back off and retry at safer in-session settings while native Present remains available, instead of repeatedly hammering the failing stage.

The exact candidate passed the full build/package/Windows/hash/Defender gate.

## Previous release history

HF15 introduced persistent optional startup scanning, authoritative manual game persistence, Windows path canonicalization and the flagship ELYSIUM 4.5 Adaptive Realism expansion.

Earlier ELYSIUM Hotfix 13/13.1, Hotfix 11 and v0.19 alpha releases remain available in GitHub Releases for historical testing.

## Private source/workspace

The engineering source is maintained privately and is not part of the public release. Do not redistribute private source/recovery workspaces.
