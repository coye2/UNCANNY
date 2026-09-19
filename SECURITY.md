# Security

UNCANNY installs low-level runtime components into game folders, so treat alpha builds like any other graphics injection/modding tool: use official packages, keep backups and do not mix files between releases.

## Official builds

Use releases from:
https://github.com/coye2/UNCANNY/releases

The full development workspace is private and is not a redistributable release package.

## Antivirus

HF18.13 was scanned with Microsoft Defender as part of its validated release/publication flow. The published release reports 0 detections.

That result applies to the exact published package/hash. It is not a promise that antivirus signatures will never change.

UNCANNY does not require users to disable Defender or add broad exclusions.

See [docs/MALWARE-VERIFICATION.md](docs/MALWARE-VERIFICATION.md).

## Reporting a security problem

Do not post exploit details, private source, secrets or sensitive diagnostic data in a public issue.

Contact the project owner through the GitHub account/repository first with the minimum information needed to reproduce the problem.

## Signing

The current alpha binaries are unsigned, so SmartScreen / Unknown Publisher warnings are expected until code signing is set up.
