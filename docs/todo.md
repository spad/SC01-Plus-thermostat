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

## Phase 1 — in progress

Done:
- [x] HA connection method decided: **ESPHome** ([ADR-0005](adr/0005-ha-connection-method.md)).
- [x] Base flash over Bruce; WiFi + API online in HA; backlight; display + touch working.
- [x] LVGL Holo HUD **Main** built & verified: toolbar, `meter` gauge (ticks + `arc` fill),
      room/target readout, −/+/mode/override buttons.
- [x] Fonts via `gfonts://`: Antonio (display) + Inter Tight (UI).
- [x] HA sensors + controls wired ([ADR-0008](adr/0008-device-ha-entity-model.md)):
      temp/humidity import, `number` target, `select` mode, `switch` override.

Next (resume here):
- [ ] **Verify HA integration on device**: temp/humidity show real values; ± moves the gauge
      fill; the 3 new HA entities (Target Temperature / HVAC Mode / Override) work both ways.
- [ ] **Fix OTA**: add-on can't resolve mDNS name — try renaming node `sc01_thermostat` →
      `sc01-thermostat` (underscore is likely the cause). Unblocks the fast OTA loop.
- [ ] Mode icons: replace text "COOL"/"HEAT" with snowflake/flame (MDI, verified codepoints).
- [ ] HUD glow/ring/bracket background (baked image assets).
- [ ] Decide `font_ui`: keep Inter Tight or switch labels to Antonio (judge on screen).
- [ ] Relay actuation logic (2-way heat/cool) + safety interlocks.

## Deferred (only if the project proceeds beyond PoC)

- [x] ~~WiFi config screen~~ — dropped: ESPHome `captive_portal` handles provisioning.
- [ ] Alternative aesthetic variants: LCARS Modern, Phosphor.
- [ ] Active-heating indicator (pulse when relay is actuating).
- [ ] Temperature telemetry mini bar-chart (last hours).
- [ ] Navigation / settings entry point for multi-page (gear icon).
- [ ] Drag-on-arc setpoint control (touch).
- [ ] Revisit fonts — none delighted the owner; consider uploading a custom sci-fi
      font to the Penpot instance if "the one" is found.

## Open questions to resolve later

- [ ] Humidity source in HA (shown in UI as 48% placeholder — confirm real sensor).
- [ ] Local sensor on device? (unconfirmed — do not assume.)
