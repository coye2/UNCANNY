# Historical note: Hotfix 11 D3D11 startup fix

Hotfix 11 was the first major D3D11 fail-open repair.

A PCSX2 test had shown UNCANNY reaching the Present hook but never completing a successful Present. The game stayed black even though the hook itself was installed.

The important change was simple: optional UNCANNY work could not be allowed to become a requirement for the game's first visible frame.

Hotfix 11 moved the D3D11 path toward this order:

1. let native Present establish a real frame stream
2. keep HOME/overlay work out of the way during startup
3. delay neural setup until presentation is healthy
4. keep the source frame visible if optional work is not ready

That design became the base for the later HF18 D3D11 work.

HF18.11 is the current version of that idea. It keeps the fail-open startup behavior, but fixes the opposite problem: the safety floor had become so conservative that neural promotion could never happen.

For current behavior, see [Compatibility](COMPATIBILITY.md) and [HF18.11 release notes](RELEASE-NOTES.md).
