# Changelog

All notable public UNCANNY alpha changes are documented here.

## v0.20.0-alpha.1 — ELYSIUM Hotfix 10

Runtime revision: `release-alpha.1.elysium-hotfix10`  
ABI: `141`

### Fixed

- HOME-page **UNCANNY PASSES** now controls the native ELYSIUM reconstruction stack instead of accidentally writing the DLSS 5 pass-depth control.
- **DLSS 5 PASSES** remains independent on the DLSS 5 page.
- ELYSIUM structural, surface, face, material, depth/form, color, edge, distant-detail and texture-relief controls are exposed through the live Control Deck and persisted control registry.
- Generated and protected shader-control layouts are synchronized to the current 56-float / 14-register ELYSIUM layout.
- Public validation scripts/docs now identify Hotfix 10 / ABI 141 consistently.

### Preserved

- Existing v0.20 launcher UI and game scanning.
- Install/update/rollback flow.
- PCSX2 wrapper behavior.
- REVENANT behavior and provider routing.
- Engine selection and source-protection model.

### Release checks

- x86/x64 Windows production binaries compiled successfully.
- Hotfix 9 static regression: PASS.
- Hotfix 10 control-wiring regression: PASS.
- Protected shader-resource verification: PASS.
- Final ZIP CRC/hash/source-leak audit: PASS.

Real-GPU visual acceptance remains hardware/game specific.

---

## v0.19.0-alpha.1 — RC2 Hotfix 2

- Improved legacy DLSS 5/Feature-18 helper startup evidence and monitoring.
- Improved D3D9 reset/device-loss behavior.
- Preserved deeper reconstruction scheduling, Motion Guard/Ghosting Guard and REVENANT compatibility work.
