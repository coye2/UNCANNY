# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.3**

- Runtime revision: `release-alpha.1.elysium-engine45-hf18.3`
- BuildId: `elysium45-hf18.3`
- updateSerial: `1830`
- ABI: `143`
- Source revision: `47841050ac5fbb04ffaa90823e2d0adc5c9236da`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.3.zip`
- SHA-256: `9748039fefcbbe941ea3d67cb54b731798d35b7332643677a3a28b4398fbcb21`
- Release: https://github.com/coye2/UNCANNY/releases/latest

HF18.3 fixes launcher StrictMode startup/installed-game path failures, uses the official cropped PNG emblem, removes `-ExecutionPolicy Bypass` from the native EXE bootstrap, and preserves stale legacy-engine preference migration so a successful update cannot silently boot the old Lucid HOME menu unless the user explicitly selected Lucid.

The exact candidate passed full build/package/Windows/WARP/launcher-smoke/hash/Defender gates.

## Previous release history

HF18.2 cleaned the public ZIP and fixed launcher record refresh; HF18.1 addressed install preflight progress; HF18 closed the Universal API Bridge/tester-feedback push.

## Private source/workspace

The engineering source remains private and is not part of the public release.
