# To-do

Actionable backlog. Keep small and concrete. Move items to the roadmap phases as they
grow. Check off or delete when done.

## Done (Phase 0 — UI PoC)

- [x] Sci-fi direction chosen: **Holo HUD** (cold/cyan).
- [x] Penpot token foundation (sets `primitives` + `semantic`).
- [x] Main screen PoC built (radial dot-ring gauge, controls, HUD background).
- [x] `IconButton` reusable component.
- [x] Fonts: display = Chakra Petch, UI = Inter Tight (see font note below).
- [x] Penpot design version saved ("PoC — main screen v3 (Holo HUD)").

## Deferred (only if the project proceeds beyond PoC)

- [ ] **WiFi config screen** (second required screen).
- [ ] Alternative aesthetic variants: LCARS Modern, Phosphor.
- [ ] Active-heating indicator (pulse when relay is actuating).
- [ ] Temperature telemetry mini bar-chart (last hours).
- [ ] Navigation / settings entry point for multi-page (gear icon).
- [ ] Drag-on-arc setpoint control (touch).
- [ ] Revisit fonts — none delighted the owner; consider uploading a custom sci-fi
      font to the Penpot instance if "the one" is found.

## Open questions to resolve later

- [ ] HA connection method — ESPHome vs custom firmware ([ADR-0005](adr/0005-ha-connection-method.md)).
- [ ] Humidity source in HA (shown in UI as 48% placeholder — confirm real sensor).
- [ ] Local sensor on device? (unconfirmed — do not assume.)
