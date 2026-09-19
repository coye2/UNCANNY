# UNCANNY v0.20 ELYSIUM — HF18.6

UNCANNY is a Windows real-time reconstruction/remaster runtime for games and emulators.

**HF18.6 is the installer/update performance + PCSX2 launch hotfix.** It addresses the tester-reproduced stalls around 7%, 24–48% staging, 70% rollback planning, and the case where PCSX2 finished installing but would not visibly open.

## Start

1. Extract the ZIP completely.
2. Double-click **`UNCANNY.exe`**.
3. Select a game/emulator.
4. Choose **Install UNCANNY** or **Update UNCANNY**.
5. Launch normally and press **HOME** for the Control Deck.

## HF18.6 installer/update changes

- Release binaries are verified once for the selected architecture instead of repeating the same full verification.
- PE architecture checks use bounded streaming header/import reads instead of loading entire binaries into memory.
- 32-bit game installs validate only the required x64 neural helper/bridge route instead of re-validating the entire x64 runtime set.
- The verified original-game digest is carried forward so the same large EXE is not repeatedly hashed.
- Byte-identical installed files are skipped instead of being backed up and rewritten.
- Healthy same-build updates take a **verified no-op fast path**. The packaged gate measured the second pass at **3.884 seconds with zero file transaction**.
- A verified existing neural asset core is reused instead of unpacking/re-hashing the same package again.
- Provider discovery uses a bounded installed-target fast path and stops once the required roles are found.
- Changed files still receive verified backup, staged-temp verification, current-destination verification, atomic replacement, and committed-destination verification.
- Progress from 24–95% reports real work instead of sitting on one opaque percentage.

## PCSX2 launch repair

- Normal ELYSIUM installs no longer run an unnecessary engine-switch transaction before PCSX2 opens.
- Optional REVENANT proof recovery is bounded and fail-open; it cannot block PCSX2 startup.
- PCSX2 runtime attachment uses a shorter bounded startup budget instead of holding the emulator suspended for a long pre-window wait.
- If optional attachment/engine preparation is unconfirmed, the emulator is allowed to resume.
- The exact packaged acceptance gate verified the wrapper spawned the verified original executable, loaded the UNCANNY runtime, acknowledged runtime initialization, resumed the child, and exited cleanly.

## Verification

Exact validated source: `852e617c003a8672ead6bd7607e24163a99b8fc5`  
Exact validation run: https://github.com/coye2/uncanny-dev/actions/runs/35412014280  
ZIP SHA-256: `3f9bbe8eb520918df9e23a84f879bce8079b197f2e194326430b3be4930be111`

HF18.5's Scan PC/runtime-root fix, cache/manual/scan normalization, authoritative Add Game retention and official Library logo remain intact. HF18 rendering, Universal API Bridge, rollback, Motion Guard/Ghosting Guard and startup-policy recovery remain preserved.

## Windows trust

UNCANNY is still unsigned. Windows SmartScreen / Unknown Publisher may appear until trusted Authenticode signing is configured.
