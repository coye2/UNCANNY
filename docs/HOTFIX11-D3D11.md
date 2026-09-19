# Historical note: Hotfix 11 D3D11 startup fix

Hotfix 11 was the first big D3D11 fail-open repair.

A PCSX2 test showed UNCANNY reaching the Present hook but never completing a successful Present. The game stayed black even though the hook itself was installed.

The fix was straightforward: optional UNCANNY work could not be allowed to become a requirement for the game's first visible frame.

Hotfix 11 moved the D3D11 path toward this order:

1. let native Present establish a real frame stream
2. keep HOME/overlay work out of startup
3. delay neural setup until presentation is healthy
4. keep the source frame visible if optional work is not ready

That design became the base for the later HF18 D3D11 stability work.

HF18.11 was the release that fixed the opposite problem: the safety floor had become so conservative that neural promotion could never happen.

HF18.12 keeps that staged D3D11 promotion behavior and adds the newer D3D12/runtime startup recovery work.

For current behavior, see [Compatibility](COMPATIBILITY.md) and the [current release notes](RELEASE-NOTES.md).
