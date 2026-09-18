# Release Status

## Current public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.4**

- Runtime revision: `release-alpha.1.elysium-engine45-hf18.4`
- BuildId: `elysium45-hf18.4`
- updateSerial: `1840`
- ABI: `143`
- Source revision: `b865fab000762e7e3015484945d1f1af5d96fe52`
- Windows package: `UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.4.zip`
- SHA-256: `c874239bbd41cfa6c271db10e364f97c241bdc5d5d55c2ff50542d12c6b8f417`
- Release: https://github.com/coye2/UNCANNY/releases/latest

HF18.4 fixes the HF18.3 no-launch regression under restrictive PowerShell execution policy, preserves the installed-game/cache path fixes and official PNG branding, and corrects updater hotfix ordering.

The exact package passed build/package/Windows/WARP, normal launcher startup, **AllSigned launcher startup**, hash and Defender gates.

HF18.4 remains unsigned, so Windows SmartScreen/Unknown Publisher may still appear until trusted code signing is configured.

## Previous release history

HF18.3 fixed launcher StrictMode/path failures and stale engine selection; HF18.2 cleaned the public ZIP; HF18.1 addressed install preflight progress; HF18 closed the Universal API Bridge/tester-feedback push.

## Private source/workspace

The engineering source remains private and is not part of the public release.
