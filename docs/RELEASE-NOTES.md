# HF18.12

HF18.12 is focused on the current launch/runtime failures from real hardware testing.

## PCSX2

PCSX2 was getting into gameplay, rendering for a few seconds, then hard-freezing when the D3D12 path moved out of startup protection.

First-use D3D12 frame-processor setup now happens off Present. Native Present stays fail-open while UNCANNY prepares the D3D12 resources in maintenance. Resize/resource retirement is also nonblocking instead of waiting behind UNCANNY-owned work on the game thread.

PCSX2 stays on Direct3D 12 with `Renderer=15`.

## Cyberpunk / Spider-Man 2

Some modern targets were failing before a usable game process stayed running and could leave a stale sidecar session behind.

For non-PCSX2 targets with no static graphics API import, UNCANNY can now let native startup happen first and attempt runtime attachment afterward. If that optional attach is not confirmed, the game is left running instead of being blocked by UNCANNY.

A crashed launch also gets a shorter replacement-ownership window, and the launcher can clear a verified dead sidecar monitor and retry once.

## Preserved

HF18.11's staged direct-D3D11 neural promotion is unchanged.

The current sidecar architecture, rollback, scanner/manual add, Motion Guard, Ghosting Guard, Adaptive Realism and REVENANT are preserved.

## Build

BuildId: `elysium45-hf18.12`  
updateSerial: `1920`  
ABI: `143`

ZIP SHA-256:

`8aaa41cb7062ef92ad1ec216ca36a0a2fbddb32632d5746d022e8f5da38c2b41`

Validation run: `35430147608`  
Publication run: `35454243517`

The exact ZIP passed the production build, Windows/package/sidecar/AllSigned gates and Microsoft Defender, then the public publisher downloaded that same artifact, checked the hash/identity again and Defender-scanned it again.

The PCSX2 freeze and Cyberpunk/Spider-Man launch behavior still need the actual machine retest. CI cannot replace that.
