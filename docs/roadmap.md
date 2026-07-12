# Roadmap

Status legend: ☐ to do · ◐ in progress · ☑ done

## Phase 0 — UI concept (gate) ◐ — direction approved (PoC)

Goal: decide go/no-go by seeing how good the UI can look on a 480×320 landscape screen.

- ☑ Define the two screens (Main + WiFi config) — requirements captured.
- ☑ Penpot token foundation with a sci-fi / hi-tech direction — **Holo HUD** chosen
  (cold/cyan). Sets `primitives` + `semantic` created (see [design notes](design-notes.md)).
- ☑ Design **Main screen** (PoC, "v3"): toolbar (wifi/time/day/humidity), radial dot-ring
  gauge with big room temp + target, −/+ target control, heat/cool mode, override on/off,
  HUD background. Reusable `IconButton` component. Penpot version saved:
  *"PoC — main screen v3 (Holo HUD)"*.
- ☑ **Go decision**: owner approved the direction as a PoC. UI is achievable and looks good.
- ~~WiFi config screen~~ — **dropped**: ESPHome's `captive_portal` handles WiFi provisioning
  (see [ADR-0005](adr/0005-ha-connection-method.md)), so a custom config screen is unnecessary.

Explicitly parked at PoC level (owner: "otherwise it stops being a PoC and becomes a product"):
alternative aesthetic variants (LCARS Modern, Phosphor), active-heating indicator, temperature
telemetry mini-chart, navigation/settings entry point, drag-on-arc setpoint. All are documented
as options in [design notes](design-notes.md) if the project proceeds.

## Phase 1 — Firmware & HA integration ◐ (project greenlit by PoC)

- ☑ Decide HA connection method: **ESPHome** ([ADR-0005](adr/0005-ha-connection-method.md)).
- ☑ Bring up SC01-Plus: ESPHome flashed over prior firmware (Bruce) via USB; WiFi + API
  online in HA; display (`mipi_spi` / `wt32-sc01-plus`) + touch (`ft63x6`) working. Config
  in [`firmware/`](../firmware/). *(OTA still failing on this node — see known issues.)*
- ◐ Implement UI on device: LVGL **Holo HUD Main** built and verified — toolbar, `meter`
  gauge (44-tick ring + cyan `arc` fill) with room/target readout, and −/+/mode/override
  controls. **Deferred:** HUD glow/ring background (needs image assets); mode icons (MDI).
- ◐ HA entities ([ADR-0008](adr/0008-device-ha-entity-model.md)): temp + humidity imported
  from HA for display; device-owned `number` (target), `select` (mode), `switch` (override)
  exposed to HA and wired to the buttons. **Implemented, pending on-device verification.**
- ☐ Relay control (2-way heat/cool) + safety interlocks — actuation logic not started.
- ☑ WiFi provisioning flow — handled by ESPHome `captive_portal` (no custom screen).

Known issues: OTA fails on this node (add-on can't resolve mDNS; browser can). Likely the
underscore in `sc01_thermostat` — try renaming to `sc01-thermostat`. See
[`firmware/README`](../firmware/README.md).

## Phase 2 — Install & live ☐

- ☐ Enclosure / mounting.
- ☐ Wire relay to the pump; on-site validation.
- ☐ Field tuning.

## Out of scope (permanent)

- On-device weekly scheduling ("crono") — owned by Home Assistant.
