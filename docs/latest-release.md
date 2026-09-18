# Latest UNCANNY public release

**UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.1**

- Runtime: `release-alpha.1.elysium-engine45-hf18`
- BuildId: `elysium45-hf18.1`
- updateSerial: `1810`
- ABI: `143`
- Source revision: `458dc5820beb9322c7ee115ed98fd07a7b1b0c77`
- Published: 2026-09-18
- Latest release: https://github.com/coye2/UNCANNY/releases/latest
- Tagged release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45-hf18.1
- Windows ZIP: https://github.com/coye2/UNCANNY/releases/download/v0.20.0-alpha.1-elysium-engine45-hf18.1/UNCANNY-v0.20.0-alpha.1-ELYSIUM-ENGINE45-HF18.1.zip
- SHA-256: `82257f00d4c323853fef1b5576578d6b0b025b44829c17027c46019ece726777`

## HF18.1

- fixes install/update preflight that could appear stuck at 2%
- replaces repeated full WMI process enumeration with bounded local target-folder process inspection
- adds visible 3/4/5/6/7% preflight progress
- fixes updater status-button clipping
- uses the current full-color ELYSIUM launcher emblem
- preserves HF18 rendering and Universal API Bridge behavior

Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35383983512

The exact package passed x86/x64 production builds, HLSL compilation, D3D11 WARP rendered-quality validation, Windows installer/rollback/manual-add regressions, ZIP integrity/hash verification and Microsoft Defender scans with 0 detections.
