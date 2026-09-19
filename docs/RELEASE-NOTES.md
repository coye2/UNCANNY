# UNCANNY HF18.9 Release Notes

Release: **UNCANNY v0.20.0-alpha.1 — ELYSIUM Engine 4.5 — HF18.9**  
BuildId: `elysium45-hf18.9`  
Update serial: `1890`  
ABI: `143`

## What HF18.9 fixes

### Universal direct-D3D11 stability

HF18.9 generalizes the compatibility behavior that kept Fallout 4 stable after tester-reproduced hard locks.

Direct D3D11 titles now use a universal current-frame safe floor instead of executable-name exceptions. Native Present remains authoritative and UNCANNY defers the riskier depth, temporal-history, optical-flow-dependent, and D3D11 neural stages on that floor. Stray reproduced the same failure class, which is why the fix was moved from title-specific policy to the D3D11 route itself.

This is a stability policy, not a claim that every D3D11 title has completed hardware acceptance.

### PCSX2 D3D12 / Feature-18 route recovery

PCSX2 follows a different path. UNCANNY had previously worked with PCSX2 using Direct3D 12 and Feature-18, so HF18.9 restores that route instead of forcing the emulator through the D3D11 safe floor.

UNCANNY now:

- writes PCSX2 `EmuCore/GS Renderer=15`, the PCSX2 Direct3D 12 renderer value;
- applies the setting to the main configuration plus existing per-game overrides managed by UNCANNY;
- records the intended PCSX2 renderer in the launch record;
- treats renderer drift away from DX12 as stale so Update UNCANNY repairs it;
- keeps REVENANT texture replacement settings transactional;
- preserves the verified sidecar launch architecture and the original `pcsx2-qt.exe` filename.

## Preserved HF18.7 / HF18.8 repairs

HF18.9 retains:

- verified `UNCANNY.Launch.exe` sidecar launch;
- target and sidecar SHA-256 validation;
- transactional recovery from old wrapper-in-place PCSX2 installs;
- Windows CRLF sidecar state handling;
- OneDrive/Cloud Files PCSX2 profile support while blocking real symlink/junction redirects;
- bounded/fail-open D3D11 Present behavior;
- same-build no-op updates;
- verified neural-core reuse;
- scanner/manual-library fixes;
- rollback, Control Deck, Motion Guard, Ghosting Guard, and X2.5 behavior.

## DLSS 5 / Feature-18 note

ELYSIUM and DLSS 5 are separate runtime paths. A visibly active ELYSIUM frame does not by itself prove a current DLSS 5 result was produced.

Tester hardware confirmed ELYSIUM running in Fallout 4. DLSS 5 current-output on that title still requires hardware confirmation. PCSX2 HF18.9 restores the D3D12 route that previously supported Feature-18, but the current physical-machine retest remains the final acceptance step.

## Exact release evidence

- Candidate source: `b168d748d241851d8faf13c83ff64aab10cd19b2`
- Dev-main merge: `cff224e353348df35d912d706b11061e0d56aba3`
- Validation run: https://github.com/coye2/uncanny-dev/actions/runs/35420827416
- Release: https://github.com/coye2/UNCANNY/releases/tag/v0.20.0-alpha.1-elysium-engine45-hf18.9
- ZIP SHA-256: `7c469cc508b7fa999b1598c80156cbf4af6201925d3455b27f980c4acf9d4c37`

The exact candidate passed static/regression tests, x86/x64 production builds, Engine 4.5 acceptance, PowerShell parsing, installer/update/rollback gates, PCSX2 DX12 configuration regression, packaged sidecar launch, HLSL compile, D3D11 WARP visual-quality validation, normal and AllSigned launcher startup, package/hash audits, and Microsoft Defender scanning with zero detections.

Real-game GPU/provider acceptance is intentionally kept separate from CI validation.
