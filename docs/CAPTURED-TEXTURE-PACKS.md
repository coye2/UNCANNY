# captured texture packs

This is the REVENANT saved-pack workflow for PCSX2.

## live mode

Run the game with **Live remaster** when you want REVENANT to collect supported captures and build accepted replacements.

Close PCSX2 before building, switching or restoring packs.

## build a saved pack

1. Select the installed PCSX2 entry in UNCANNY.
2. Open **Captured texture packs**.
3. Pick the captured game serial.
4. Choose **Build / update captured pack**.
5. Let it finish.

Accepted, unsupported and failed captures are counted separately. A failed quality check is not silently turned into a pass.

## play without reconstruction

Choose **Play saved pack**.

PCSX2 texture replacement stays on. Live REVENANT reconstruction stays off.

The point is simple: build the pack once, then play it again without making the neural worker rebuild settled textures every launch.

## verify / export

**Verify pack** checks the saved manifest and hashes.

**Export pack** only exports files listed in the verified manifest.

A verified file is not proof that every game scene used it. File proof and rendered-use proof are different.

## restore

Use **Restore original pack** or switch back to **Live remaster**.

UNCANNY records original bytes before changing files it owns. If one of those files changed later, restore stops instead of overwriting it.

Do not delete recovery records to force a restore.

## one important limit

A captured pack is made from textures the emulator actually captured. It is not a full disc/game extractor.

Packs are game-specific. Do not copy one game's pack into another serial.
