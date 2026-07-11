# Roadmap

Status legend: ☐ to do · ◐ in progress · ☑ done

## Phase 0 — UI concept (gate) ◐

Goal: decide go/no-go by seeing how good the UI can look on a 480×320 landscape screen.

- ◐ Define the two screens (Main + WiFi config) — requirements captured.
- ☐ Establish a Penpot design foundation (tokens: colors, type, spacing, radius) with a
  sci-fi / hi-tech direction.
- ☐ Design **Main screen**: detected temp, target temp, mode (heat/cool), toolbar
  (WiFi status, time, day), override action.
- ☐ Design **WiFi config screen**.
- ☐ Review polish against "commercial product" bar → **go/no-go decision**.

## Phase 1 — Firmware & HA integration ☐ (only if Phase 0 passes)

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
