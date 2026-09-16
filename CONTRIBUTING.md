# Contributing and Alpha Testing

UNCANNY's highest-value contributions during alpha are **reproducible compatibility reports** from different games, APIs, architectures and GPUs.

## What makes a useful report

Please include:

- game/title
- exact executable name/path (you may redact personal folder names)
- graphics API
- x86 or x64
- GPU model and driver
- UNCANNY product version, runtime revision and ABI
- whether UNCANNY attaches
- whether Home / Control Deck works
- whether Feature-18 create/evaluate succeeds
- whether neural output returns and reaches presentation
- whether REVENANT was tested
- saved `UNCANNY-STATUS.cmd` report
- reproduction steps

Use the **Compatibility report** issue template whenever possible.

## Evidence over assumptions

Please do not report a path as working solely because:

- the provider DLL exists
- an overlay says enabled
- an IPC fixture passed
- a source frame was copied
- an output file appeared on disk

For neural rendering, the useful chain is:

`FeatureCreate → FeatureEvaluate → neural return → composition → presentation`

For REVENANT, the useful chain is:

`capture → inference → validated replacement → reload/bind → visible rendered use → persistence/restore`

## Private material

Do not upload private source-recovery archives, development encryption material, private build workspaces or proprietary source to public issues.

## Security reports

See [SECURITY.md](SECURITY.md). Avoid posting exploit details or sensitive local paths in a public issue.
