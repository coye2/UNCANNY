# security

UNCANNY installs low-level graphics/runtime files into game folders, so use the official packages and keep your backups.

## Defender / SmartScreen

UNCANNY does **not** require you to disable Defender or add a giant exclusion.

The current binaries are unsigned, so Windows can show Unknown Publisher / SmartScreen warnings.

If Windows actually detects something, do not blindly restore it. Send the exact detection name, file hash and build so it can be checked.

## closed source

The development repo is private.

Public packages must not contain private C++/shader source, internal CI evidence, developer harnesses, credentials or private build tooling.

## third-party files

Provider/model files keep their own licenses. UNCANNY does not claim ownership of NVIDIA/AMD/provider binaries or model weights.

## reporting

For a security issue, send the minimum reproduction details needed. Do not post secrets, private source or personal diagnostic data in a public issue.
