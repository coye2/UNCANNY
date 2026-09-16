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

Current alpha binaries are unsigned and have not received broad antivirus certification. A security product warning should be investigated rather than automatically ignored or suppressed.
