# using UNCANNY

## install

1. Download the build you want from **Releases**.
2. Extract the whole folder.
3. Open `UNCANNY.exe`.
4. Add a game or use **Scan PC**.
5. Select the real game/emulator executable.
6. Install/update UNCANNY.
7. Launch the game and press **Home** for the Control Deck.

Do not mix files from different UNCANNY builds.

## launcher

Manual games stay in the library. If a game moves, the entry should stay there and show as missing until you locate it again.

Startup scanning is not supposed to crawl the whole PC every launch. Use Scan PC when you actually want a scan.

## Control Deck

The Deck controls STRATA, REVENANT and the neural path.

Some settings need data the game might not expose. If UNCANNY does not have a trustworthy input, it should show that instead of pretending the feature is working.

## REVENANT

PCSX2 has the strongest saved-pack path right now.

Live mode captures supported textures and builds accepted replacements. Saved mode plays a finished captured pack without running reconstruction again.

Native D3D9 REVENANT is farther along than before: real Deadpool textures were captured and rebuilt. The final visible replacement proof from that exact run is still open.

## neural bridge

D3D9, D3D11 and D3D12 have real development evidence for provider creation/evaluation/output use.

Vulkan, OpenGL and AMD are not being called fully proven yet.

## repair / remove

**Repair** fixes UNCANNY-owned files that are missing or damaged.

**Remove UNCANNY** restores recorded originals where possible and leaves unrelated mods, saves and user files alone.

If a managed file changed outside UNCANNY, restore should stop and report the conflict instead of overwriting it.

## bug reports

Send:

- game + version
- exact executable
- API
- x86/x64
- GPU + driver
- UNCANNY build
- what you did
- what happened
- status/log output
- screenshot/video if it is visual

Do not post tokens, private source archives or personal data.
