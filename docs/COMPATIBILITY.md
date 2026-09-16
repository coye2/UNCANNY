# Compatibility and Evidence Levels

UNCANNY is under active alpha development. Compatibility claims are separated by evidence level so detection, compilation and real rendered use are not confused.

## Evidence terminology

- **Detected** — an API, provider or file was found.
- **Implemented** — source contains the intended route.
- **Compiled** — the relevant Windows component built successfully.
- **Attached** — the UNCANNY runtime connected to the target process.
- **Transport active** — frame/resource transport is operating.
- **Feature created** — the neural provider successfully created the requested feature/context.
- **Evaluated** — a real neural evaluation completed successfully.
- **Returned** — current-frame neural output returned to the game-side runtime.
- **Presented / certified** — the neural output was composed into a frame associated with a successful presentation event in the implemented certification scope.
- **Visible rendered use** — the user or an instrumented render-binding path has established that the intended result is actually visible/used by the running game.

A copied source frame, IPC fixture, provider version, green overlay state or replacement file on disk is not counted as neural/remaster success by itself.

## API matrix

| API / environment | Core runtime | Neural path | Current alpha status |
|---|---|---|---|
| Direct3D 12 x64 | implemented | native neural path | strongest PC path; continued regressions |
| Direct3D 11 x64 | implemented | native/interoperability work | active support, title-specific validation |
| Direct3D 11 x86 | implemented | x64 helper when required | experimental hardware acceptance |
| Direct3D 10 / 10.1 | implemented compatibility path | helper/interop route | experimental hardware acceptance |
| Direct3D 9 x86 | implemented native image/runtime path | legacy x86→x64 helper route | core runtime works in tested titles; broad Feature-18 proof still in progress |
| PCSX2 | established UNCANNY presentation path | neural rendering + REVENANT target | primary emulator acceptance target |
| Vulkan | partial / roadmap | not at DirectX parity | experimental/deferred |
| OpenGL | partial / roadmap | not at DirectX parity | experimental/deferred |

## Deep Clean status

| Mode | Intended behavior | Validation state |
|---|---|---|
| Clean 1 | primary neural reconstruction | implemented baseline |
| Clean 1.5 | primary + conditional lower-contribution refinement | implemented scheduler; GPU acceptance ongoing |
| Clean 2 | up to two meaningful neural stages | implemented scheduler; GPU acceptance ongoing |
| Clean 2.5 | two strong stages + optional selective third-stage refinement | implemented scheduler; motion/performance acceptance ongoing |
| Clean 3 | maximum-quality depth up to three meaningful stages | implemented scheduler; real-GPU quality/performance acceptance ongoing |

UNCANNY reports actual evaluations separately from the requested Clean mode. If the scheduler rejects later work, a Clean 3 frame can honestly report one evaluation.

## REVENANT status

### PCSX2
Implemented engineering includes game isolation, texture identity, capture/reconstruction worker paths, validation, receipts, backup/restore and reload handling.

The remaining headline acceptance gate is a representative end-to-end neural replacement that is visibly used by the emulator, persists when expected and restores exactly.

### Native PC games
Resource capture/replacement experiments exist, especially around Direct3D resource identity, but native-game REVENANT is still experimental and should not be described as universal asset replacement.

## Reporting a compatibility result

For useful compatibility data include:

1. Game/title and exact executable.
2. Graphics API.
3. x86 or x64.
4. GPU and driver.
5. UNCANNY revision and ABI.
6. Whether runtime attachment succeeds.
7. `FeatureCreateAttempts/Success`.
8. `FeatureEvaluateAttempts/Success`.
9. Neural-return and presentation evidence.
10. REVENANT evidence if tested.
11. Saved `UNCANNY-STATUS.cmd` report.

Use the GitHub compatibility-report issue template so results become reproducible and searchable.
