# Hotfix 11 — PCSX2 D3D11 first-frame fail-open repair

Hotfix 11 exists because of a real tester result, not a synthetic compatibility guess.

## Triggering tester result

Target: PCSX2 x64 using D3D11.

UNCANNY successfully captured the D3D11 device/swapchain and installed the Present patch, but the game remained black. The saved status/trace showed:

- `PRESENT_PATCH_OK`
- `PresentAttempts=1`
- `Presents=0`
- `PresentAdvancing=0`
- `BaseFPS=0`
- `PresentedFPS=0`
- `Host64LaunchAttempted=0`
- `Host64Alive=0`
- `ProviderLoaded=0`
- `FeatureCreateAttempts=0`
- `FeatureEvaluateAttempts=0`
- `SharedResourcesCreatedMask=0`
- `FenceCreatedMask=0`
- `DeckConnected=1`
- `DeckSurfacePublished=0`
- `DeckVisible=0`
- `GameForeground=0`
- separate REVENANT texture path: 38/38 jobs completed

The central evidence is that the hook was installed and entered, but zero successful native Presents were observed afterward. That localizes the first-frame failure to work performed ahead of the original D3D11 `Present` / `Present1` completing.

## Why Host64 was not treated as the root cause

`Host64LaunchAttempted=0` is not automatically a failure on an x64 D3D11 target. UNCANNY's normal native x64 route can use the in-process bridge. A separate helper remains important for routes that explicitly require an isolated/cross-bitness transport, but this tester report did not prove a helper-launch failure.

Hotfix 11 therefore fixes presentation ordering instead of simply forcing `UNCANNY.NeuralHost64.exe` to launch earlier.

## Root failure class

Before Hotfix 11, direct D3D11 UNCANNY preprocessing could begin immediately after the Present hook was installed. That work can include image resources, shader setup, temporal preparation, Control Deck composition and D3D11↔D3D12 neural interoperability preparation.

If a title/driver/emulator stalls during that first-use work, the very first hooked Present can become trapped before the game's original Present establishes visible output.

For compatibility, that ordering is unsafe. An optional visual enhancement layer must not become a prerequisite for the base game to show a frame.

## Hotfix 11 behavior

### 1. Native D3D11 presentation comes first

For a direct D3D11 swapchain, the first presentation opportunities are native warmup frames. UNCANNY image preprocessing and in-frame Control Deck composition are deferred so the game's original `Present` / `Present1` gets priority.

### 2. Feature-18 waits for a proven Present stream

D3D11 Feature-18 / DLSS 5 interoperability is delayed until diagnostics establish:

- `PresentAdvancing=1`
- at least 8 successful native Presents
- a recent successful Present timestamp

Until then, the current source frame remains authoritative. UNCANNY does not reuse a stale neural result because neural initialization is late.

### 3. HOME/Deck state cannot block the first game frames

During the short D3D11 warmup, frame composition for the Control Deck is deferred with the rest of optional UNCANNY preprocessing.

`GameForeground=0`, `DeckSurfacePublished=0` or `DeckVisible=0` can be diagnostically useful, but those states must not become permission to suppress native presentation.

### 4. Present-stage telemetry is explicit

Hotfix 11 exposes:

- `PRESENT_PREPROCESS`
- `PRESENT_NATIVE_CALL`
- `PRESENT1_PREPROCESS`
- `PRESENT1_NATIVE_CALL`
- `PRESENT_SUCCEEDED`

Interpretation:

- stops at `PRESENT_PREPROCESS` → the stall remains in work ahead of original Present
- reaches `PRESENT_NATIVE_CALL` but not `PRESENT_SUCCEEDED` → UNCANNY reached the application's original Present; investigate that game/driver/native call boundary
- reaches `PRESENT_SUCCEEDED` repeatedly → the base presentation stream is advancing

## REVENANT was deliberately preserved

The triggering tester session completed 38/38 independent REVENANT texture jobs while the live D3D11 presentation path was stalled.

That is useful evidence that these are separate subsystems. Hotfix 11 does not rewrite the working texture path to repair a swapchain ordering failure.

## Launcher/package change included with Hotfix 11

The public user-facing entry point is native **`UNCANNY.exe`** at the root of the extracted package.

- Windows GUI executable
- no normal top-level `UNCANNY.cmd` launch step
- starts the bundled launcher without showing a command window
- guards against duplicate launcher instances
- native startup failure dialog/logging

Maintenance CMD utilities remain where they serve specific diagnostics or install workflows.

The already-public UNCANNY 2.5 Lucid ABI 136 engine bundle is preserved by its existing manifest hashes so engine selection remains available alongside ELYSIUM ABI 141.

## Security packaging correction

The first Hotfix 11 package accidentally included internal acceptance-test executables under `diagnostics/`. Windows Defender flagged `revenant-commit32.exe`. That executable is a development REVENANT commit/recovery test harness and is not required by the runtime.

The corrected public package removes the complete internal diagnostic executable set. Microsoft Defender signatures were updated before scanning, and both the cleaned runtime tree and final ZIP returned **0 detections**. No Defender exclusions, restoration or allowlisting were used.

See [MALWARE-VERIFICATION.md](MALWARE-VERIFICATION.md) for the exact release-gate record.

## What was not redesigned

Hotfix 11 intentionally preserves:

- Hotfix 10 ELYSIUM pass/slider wiring
- REVENANT
- PCSX2 wrapper/launch behavior
- D3D9/D3D10/D3D12 routes outside this targeted D3D11 startup change
- provider selection policy
- install/update/rollback transactions
- protected shader resources
- per-game ELYSIUM/Lucid engine selection

## Publication verification

The exact corrected public Hotfix 11 build passed:

- Hotfix 9 ELYSIUM regression
- Hotfix 10 control wiring regression
- Hotfix 11 D3D11 fail-open regression
- native `UNCANNY.exe` regression
- internal Windows diagnostic/test builds in CI; those executables are **not shipped**
- 16 focused Hotfix 11 acceptance checks
- x86/x64 production compilation
- protected shader authentication/roundtrip checks
- PE hardening checks across all 11 current production/helper binaries
- strict public-package audit
- final ZIP integrity verification
- Microsoft Defender cleaned-runtime scan: **PASS / 0 detections**
- Microsoft Defender final-ZIP scan: **PASS / 0 detections**

Release ZIP SHA-256:

`a523db2ec0149f139a24c70aba36f68222cba057369b97864615b07c9c356e69`

## Same-machine retest gate

The original PCSX2 D3D11 setup is considered repaired in practice only if the tester observes all of the following:

1. the game image appears instead of remaining black
2. `PresentAttempts` continuously increases
3. `Presents` becomes non-zero and keeps increasing
4. `PresentAdvancing=1`
5. `BaseFPS` / `PresentedFPS` become non-zero
6. `AttachmentStage` reaches `PRESENT_SUCCEEDED`
7. UNCANNY processing begins only after native warmup
8. Feature-18 work starts only after base presentation is healthy
9. HOME opens without requiring Alt-Tab, minimizing PCSX2, stealing focus or stopping Presents
10. REVENANT remains functional
11. PCSX2 exits cleanly

Build-host verification is required before publication, but it does not replace this final hardware acceptance step.