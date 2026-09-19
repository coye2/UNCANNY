# UNCANNY v0.20 ELYSIUM — HF18.6

UNCANNY is a Windows real-time reconstruction/remaster runtime for games and emulators.

**HF18.6 is an installer/update performance hotfix.** It focuses on the tester-reproduced stalls at 7%, the opaque 24–48% staging phase, and the 70% verified rollback backup phase.

## Start

1. Extract the ZIP completely.
2. Double-click **`UNCANNY.exe`**.
3. Select a game/emulator.
4. Choose **Install UNCANNY** or **Update UNCANNY**.
5. Launch normally and press **HOME** for the Control Deck.

## HF18.6 installer/update changes

- Release binaries are verified once for the selected architecture instead of repeating the same full verification.
- PE architecture checks use bounded streaming header/import reads instead of loading entire binaries into memory.
- 32-bit game installs validate the required x64 neural helper/bridge route directly instead of re-validating the entire x64 runtime set.
- The verified original-game digest is carried forward through the transaction so the same large EXE is not repeatedly hashed.
- Update planning compares installed bytes against the new package and **skips byte-identical files completely** instead of backing them up, rewriting them and flushing them again.
- Only files that actually change enter the rollback transaction.
- The changed files still receive verified backup, staged-temp integrity, current-destination verification and committed-destination verification.
- Progress from 24–95% now reports real sub-stages instead of appearing frozen at one percentage.

## Preserved

HF18.5's Scan PC/runtime-root fix, cache/manual/scan normalization, authoritative Add Game retention and official Library logo remain intact. HF18 rendering, Universal API Bridge, PCSX2, REVENANT, rollback, Motion Guard/Ghosting Guard and startup-policy recovery are unchanged.

## Windows trust

UNCANNY is still unsigned. Windows SmartScreen / Unknown Publisher may appear until trusted Authenticode signing is configured.
