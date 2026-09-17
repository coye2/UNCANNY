# Security

UNCANNY is experimental graphics middleware that installs runtime components into game directories. Treat alpha builds like any other low-level modding/injection software: preserve backups, use complete packages, and do not mix DLLs from unrelated revisions.

## Public vs private packages

Only public Windows packages are intended for redistribution.

Private workspace-recovery archives contain proprietary source, development material and internal recovery data. They are not public release artifacts and should not be mirrored or redistributed.

## Reporting a security issue

Do not publish exploit details, private source material, secrets, personal paths or sensitive diagnostic data in a public GitHub issue.

Contact the project owner through the GitHub account/repository first and share only the minimum information needed to establish the problem. A sanitized public issue can be created later when disclosure is appropriate.

## Runtime hardening

Current public candidates use compiled-code hardening and authenticated encrypted runtime resources. This is tamper resistance and source protection, not a claim that client-side software is impossible to reverse engineer.

## Antivirus / signing

Current alpha binaries are unsigned. Public packaging now treats a Microsoft Defender detection as a release blocker, and internal CI/test executables are not part of the public runtime payload.

The AV-clean Hotfix 11 package was scanned on a GitHub-hosted Windows Server 2025 runner after Microsoft Defender signatures were updated. Both the cleaned runtime tree and the completed ZIP returned **0 detections**.

- Microsoft Defender engine: `1.1.26080.3`
- Defender signatures: `1.459.256.0`
- Defender product: `4.18.26080.3`
- Defender exclusions used: **none**
- Defender disabled/bypassed: **no**
- Threat restoration/allowlisting used: **none**
- Release ZIP SHA-256: `a523db2ec0149f139a24c70aba36f68222cba057369b97864615b07c9c356e69`

The exact verification record is published in [docs/MALWARE-VERIFICATION.md](docs/MALWARE-VERIFICATION.md), is included inside the release ZIP, and is attached to the Hotfix 11 GitHub release as `MALWARE-VERIFICATION-HOTFIX11.json`.

A clean scan is evidence for that exact build and Defender signature snapshot, not a permanent guarantee against future antivirus signature changes. Any future warning should still be investigated rather than automatically ignored or suppressed.
