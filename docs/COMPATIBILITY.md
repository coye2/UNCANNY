# Compatibility and Evidence Levels

UNCANNY is under active alpha development. Compatibility claims are separated by evidence level so detection, compilation and real rendered use are not confused.

Current public runtime: `release-alpha.1.elysium-engine45` · ABI `143`.

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
- **Visible rendered use** — the user or an instrumented render-binding path established that the intended result is actually visible/used by the running game.

A copied frame, provider version, green overlay state, texture-worker success or replacement file on disk is not counted as visible remaster success by itself.

## Engine 4.5 API matrix

| API / environment | Core runtime | Adaptive Realism | Neural/DLSS 5 | Current alpha status |
|---|---|---|---|---|
| Direct3D 11 x64 | implemented | strongest current route; scored depth + native motion/flow where available | native/in-process interoperability | active primary test path |
| Direct3D 11 x86 | implemented | capability-tiered | x64 helper where required | experimental hardware acceptance |
| Direct3D 12 x64 | implemented | supported; conservative fallback when trustworthy scene depth is unavailable | native neural path | active PC path |
| Direct3D 10 / 10.1 | compatibility path | capability depends on available scene evidence | helper/interop route | experimental hardware acceptance |
| Direct3D 9 x86 | implemented legacy runtime | tonal/spatial fallback when trustworthy depth is unavailable | legacy x86→x64 helper route | supported legacy path; broad neural proof still in progress |
| PCSX2 | established UNCANNY presentation path | strongest through its D3D11/D3D12 renderer routes as evidence allows | provider path depends on renderer/runtime | primary emulator acceptance target |
| Vulkan | partial / roadmap | not at DirectX parity | not at DirectX parity | experimental/deferred |
| OpenGL | partial / roadmap | not at DirectX parity | not at DirectX parity | experimental/deferred |

## Adaptive Realism capability tiers

Engine 4.5 does not assume every API/game exposes trustworthy depth or motion.

### Tier A — trustworthy depth + native motion

Highest available confidence path. Depth-aware work and temporal behavior can use native motion evidence.

### Tier B — trustworthy depth + UNCANNY optical flow

Depth-aware path with UNCANNY-reconstructed motion. Temporal confidence remains guarded by Motion Guard/Ghosting Guard and disocclusion checks.

### Tier C — trustworthy depth only

Conservative spatial lighting/detail behavior. Temporal history is disabled rather than fabricated.

### Tier D — no trustworthy scene depth

Adaptive exposure, tonal reconstruction, local contrast, clarity, color and other spatial enhancements can still run. Depth-aware GI/occlusion is disabled rather than faked.

## D3D11 depth evidence

D3D11 can score depth candidates using evidence such as:

- full-resolution matching
- draw-use evidence
- precision
- stable resource identity
- multisample state

A candidate that does not meet the confidence threshold is not treated as trustworthy depth.

## Motion / temporal acceptance

Motion Guard and Ghosting Guard remain authoritative in Engine 4.5.

Temporal history is reduced or rejected when:

- motion confidence drops
- depth continuity fails
- current/history structure disagrees
- disocclusion is detected

X2.5 deliberately uses the lowest temporal-history weight and is intended to be the clean-motion mode.

## ELYSIUM pass status

| Mode | Intended behavior | Validation state |
|---|---|---|
| 1 | base native ELYSIUM reconstruction depth | routing/build validation complete; visual acceptance ongoing |
| 1.5 | intermediate reconstruction depth | routing/build validation complete; visual/performance acceptance ongoing |
| 2 | deeper reconstruction | routing/build validation complete; visual/performance acceptance ongoing |
| 2.5 | motion-clean deep reconstruction with reduced history | compiled behavior verified; real-GPU motion/performance acceptance ongoing |
| 3 | maximum exposed native reconstruction depth | routing/build validation complete; real-GPU quality/performance acceptance ongoing |

**UNCANNY PASSES**, **Adaptive Realism quality** and **DLSS 5 PASSES** are separate controls.

## D3D11 fail-open startup

The Hotfix 11 startup-safety contract remains preserved in Engine 4.5:

1. native Present is allowed to establish the base game image first
2. initial optional UNCANNY/Deck work must not block the first visible frame
3. DLSS 5 initialization waits for a healthy advancing Present stream where that route applies
4. if optional neural startup is not ready, the current source remains visible
5. foreground/Deck state must not become a prerequisite for base presentation

Historical details: [HOTFIX11-D3D11.md](HOTFIX11-D3D11.md).

## REVENANT status

### PCSX2

Implemented engineering includes game isolation, texture identity, capture/reconstruction worker paths, validation, receipts, backup/restore and reload handling.

A healthy REVENANT worker does not prove that the replacement is visibly bound or that the live Present stream is healthy. Visible replacement, persistence and exact restore remain the important acceptance gates.

### Native PC games

Resource capture/replacement experiments exist, but native-game REVENANT remains experimental and should not be described as universal asset replacement.

## Vendor notes

Adaptive Realism is vendor-neutral and does not require DLSS 5.

DLSS 5 is a separate NVIDIA-specific provider route. An AMD/Intel system may still use UNCANNY-native Adaptive Realism behavior where the DirectX/runtime path is supported, but that does not imply DLSS 5 availability.

## Engine 4.5 build evidence

Before publication the exact Engine 4.5 package passed:

- full Python regression suite
- 22 compiled Engine 4.5 acceptance checks
- Adaptive Realism compiled tests on x86 and x64
- x86/x64 production compilation
- protected-resource verification
- Hotfix 11/12 compatibility regressions
- strict package/ZIP audit
- dynamic Windows install + rollback regression
- restricted third-party shader source/package audit
- Microsoft Defender scan of extracted final package: 0 detections
- Microsoft Defender scan of completed ZIP: 0 detections

These are build-host/package checks. They do not replace real Windows/GPU/game visual and performance acceptance.

## Reporting a compatibility result

For useful compatibility data include:

1. game/title and exact executable
2. graphics API
3. x86 or x64
4. GPU and driver
5. UNCANNY runtime/revision and ABI
6. whether runtime attachment succeeds
7. `PresentAttempts`, `Presents` and `PresentAdvancing`
8. `AttachmentStage`
9. Feature-18 create/evaluate counters if testing DLSS 5
10. Adaptive Realism quality level and UNCANNY pass depth
11. visible before/after evidence
12. REVENANT evidence if tested
13. saved `UNCANNY-STATUS.cmd` report

Use the GitHub compatibility-report issue template so results become reproducible and searchable.