# Compatibility and Evidence Levels

UNCANNY is under active alpha development. Compatibility claims are separated by evidence level so detection, compilation and real rendered use are not confused.

Current public runtime: `release-alpha.1.elysium-hotfix11` · ABI `141`.

## Evidence terminology

- **Detected** — an API, provider or file was found.
- **Implemented** — source contains the intended route.
- **Compiled** — the relevant Windows component built successfully.
- **Attached** — the UNCANNY runtime connected to the target process.
- **Transport active** — frame/resource transport is operating.
- **Feature created** — the neural provider successfully created the requested feature/context.
- **Evaluated** — a real neural evaluation completed successfully.
- **Returned** — current-frame neural output returned to the game-side runtime.
- **Presented / certified** — the intended output was associated with a successful presentation event in the implemented certification scope.
- **Visible rendered use** — the user or an instrumented render-binding path has established that the intended result is actually visible/used by the running game.

A copied source frame, IPC fixture, provider version, green overlay state, texture worker success or replacement file on disk is not counted as neural/remaster presentation success by itself.

## API matrix

| API / environment | Core runtime | Neural path | Current alpha status |
|---|---|---|---|
| Direct3D 12 x64 | implemented | native neural path | strongest PC path; continued regressions |
| Direct3D 11 x64 | implemented | native/in-process interoperability | active support; Hotfix 11 adds fail-open first-frame startup |
| Direct3D 11 x86 | implemented | x64 helper when required | experimental hardware acceptance |
| Direct3D 10 / 10.1 | implemented compatibility path | helper/interop route | experimental hardware acceptance |
| Direct3D 9 x86 | implemented native image/runtime path | legacy x86→x64 helper route | core runtime works in tested titles; broad Feature-18 proof still in progress |
| PCSX2 | established UNCANNY presentation path | D3D11/D3D12 rendering + REVENANT target | primary emulator acceptance target; Hotfix 11 addresses a D3D11 startup regression |
| Vulkan | partial / roadmap | not at DirectX parity | experimental/deferred |
| OpenGL | partial / roadmap | not at DirectX parity | experimental/deferred |

## Hotfix 11 D3D11 evidence

The triggering tester run was PCSX2 x64 on D3D11. Device and swapchain capture succeeded and the DXGI Present patch was installed, but the report stopped with:

- `PresentAttempts=1`
- `Presents=0`
- `PresentAdvancing=0`
- `BaseFPS=0`
- `PresentedFPS=0`
- `FeatureCreateAttempts=0`
- `FeatureEvaluateAttempts=0`

That means the first hooked frame entered the wrapper but a successful native Present was never observed afterward. Hotfix 11 responds by changing startup order rather than claiming a provider fix.

The same report had `Host64LaunchAttempted=0`. On a native x64 D3D11 route this is not sufficient evidence of a fault because UNCANNY can use the in-process bridge. Separate helper startup is still relevant to routes that actually require an isolated/cross-bitness host.

The tester's REVENANT worker completed 38/38 texture jobs while live D3D11 presentation was stalled. This demonstrates why texture-worker evidence and swapchain presentation evidence are tracked separately.

### Hotfix 11 D3D11 contract

For direct D3D11:

1. native Present is allowed to establish the base game image first
2. initial UNCANNY image processing and Deck composition are deferred for the short warmup
3. Feature-18 initialization waits for an advancing native stream with at least 8 successful, recent Presents
4. if neural startup is not ready, the current source stays visible
5. foreground/Deck state must not become a prerequisite for base presentation

### Hotfix 11 diagnostic stages

- `PRESENT_PREPROCESS` — entered UNCANNY preprocessing
- `PRESENT_NATIVE_CALL` — reached original application Present
- `PRESENT1_PREPROCESS` — entered Present1 preprocessing
- `PRESENT1_NATIVE_CALL` — reached original application Present1
- `PRESENT_SUCCEEDED` — native presentation successfully advanced

These stages make it possible to distinguish a stall ahead of Present from one that occurs on/below the original Present call.

## ELYSIUM pass status

| Mode | Intended behavior | Validation state |
|---|---|---|
| 1 | base native ELYSIUM reconstruction depth | Hotfix 10/11 control routing verified; visual acceptance ongoing |
| 1.5 | intermediate reconstruction depth | routing verified; visual/performance acceptance ongoing |
| 2 | deeper reconstruction | routing verified; visual/performance acceptance ongoing |
| 2.5 | high reconstruction depth with motion safeguards | routing verified; motion/performance acceptance ongoing |
| 3 | maximum exposed native reconstruction depth | routing verified; real-GPU quality/performance acceptance ongoing |

**UNCANNY PASSES** and **DLSS 5 PASSES** are separate controls. Requested pass depth does not by itself prove a specific number of successful Feature-18 evaluations.

## REVENANT status

### PCSX2

Implemented engineering includes game isolation, texture identity, capture/reconstruction worker paths, validation, receipts, backup/restore and reload handling.

A healthy REVENANT worker does not prove that the live Present stream is healthy. Hotfix 11 was triggered by a session where REVENANT completed its worker jobs but D3D11 presentation did not advance.

The remaining headline acceptance gate is representative end-to-end replacement that is visibly used by the emulator, persists when expected and restores exactly.

### Native PC games

Resource capture/replacement experiments exist, especially around Direct3D resource identity, but native-game REVENANT is still experimental and should not be described as universal asset replacement.

## Launcher/package compatibility

Hotfix 11's public user entry point is root-level native `UNCANNY.exe`. The old top-level `UNCANNY.cmd` launcher is not the normal launch path. Maintenance CMD tools remain available where they serve a specific diagnostic/install purpose.

The package preserves the already-published UNCANNY 2.5 Lucid ABI 136 engine bundle by its manifest hashes while ELYSIUM remains the current ABI 141 engine.

## Hotfix 11 build evidence

Before publication the exact Hotfix 11 build passed:

- Hotfix 9 regression
- Hotfix 10 ELYSIUM control-wiring regression
- Hotfix 11 D3D11 fail-open regression
- native launcher regression
- 12 public diagnostic cross-builds
- 16 focused Hotfix 11 acceptance checks
- x86/x64 production compilation
- protected-resource verification
- PE hardening audit across 11 current production/helper binaries
- strict package/ZIP audit

These are build-host and static/portable checks. They do not replace real Windows/GPU/game acceptance.

## Reporting a compatibility result

For useful compatibility data include:

1. Game/title and exact executable.
2. Graphics API.
3. x86 or x64.
4. GPU and driver.
5. UNCANNY revision and ABI.
6. Whether runtime attachment succeeds.
7. `PresentAttempts`, `Presents` and `PresentAdvancing`.
8. `AttachmentStage`.
9. `FeatureCreateAttempts/Success`.
10. `FeatureEvaluateAttempts/Success`.
11. Neural-return/presentation evidence.
12. REVENANT evidence if tested.
13. Saved `UNCANNY-STATUS.cmd` report.

Use the GitHub compatibility-report issue template so results become reproducible and searchable.