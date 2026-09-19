# HF18.11

HF18.11 fixes a D3D11 bug left behind by the earlier hard-lock work.

The D3D11 safe floor was doing its job — keeping risky work out of Present — but it was also forcing the neural path off forever. That is why a title could show normal ELYSIUM processing while the neural route never came online.

## What changed

Direct D3D11 now has two stages:

1. start on the conservative native/current-frame path
2. after the route stays healthy long enough, allow neural resources to warm up and neural processing to become eligible

The promotion window currently requires 240 processed frames and at least 9 seconds since the last relevant DXGI transition.

The riskier direct-depth/temporal path is still not re-enabled on the safe route. Resize, fullscreen and similar transitions reset the promotion window.

## Also included

HF18.10's D3D12 startup/resize protection is unchanged.

PCSX2 stays on Direct3D 12 with `Renderer=15`.

The current sidecar launcher, legacy PCSX2 migration, scanner/manual-add fixes, rollback, REVENANT, Motion Guard and Ghosting Guard are all preserved.

## Build

BuildId: `elysium45-hf18.11`  
updateSerial: `1910`  
ABI: `143`

ZIP SHA-256:
`7e4d0f990ab33f10abec01a23ff467e487ad45da2b250cd49b6823b321c3d800`

The release passed the normal build, regression, package, Windows, WARP and Defender gates before publication.

That does not replace real game testing. Fallout/Stray neural output and PCSX2 Feature-18 gameplay still need to be judged from actual hardware sessions.
