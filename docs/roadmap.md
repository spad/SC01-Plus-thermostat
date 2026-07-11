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
- ☐ **WiFi config screen** — not built yet (deliberately deferred; PoC goal met on Main).

Explicitly parked at PoC level (owner: "otherwise it stops being a PoC and becomes a product"):
alternative aesthetic variants (LCARS Modern, Phosphor), active-heating indicator, temperature
telemetry mini-chart, navigation/settings entry point, drag-on-arc setpoint. All are documented
as options in [design notes](design-notes.md) if the project proceeds.

## Phase 1 — Firmware & HA integration ☐ (project greenlit by PoC)

- ☐ Decide HA connection method (see [ADR-0005](adr/0005-ha-connection-method.md)).
- ☐ Bring up SC01-Plus: display, touch, WiFi.
- ☐ Implement UI on device (LVGL, native or via ESPHome depending on ADR-0005).
- ☐ Relay control (2-way heat/cool) + safety interlocks.
- ☐ HA entities: current temp (from HA sensor), target, mode, override on/off.
- ☐ WiFi provisioning flow.

## Phase 2 — Install & live ☐

- ☐ Enclosure / mounting.
- ☐ Wire relay to the pump; on-site validation.
- ☐ Field tuning.

## Out of scope (permanent)

- On-device weekly scheduling ("crono") — owned by Home Assistant.
