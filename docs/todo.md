# To-do

Actionable backlog. Keep small and concrete. Move items to the roadmap phases as they
grow. Check off or delete when done.

## Now (Phase 0 — UI)

- [ ] Confirm sci-fi / hi-tech direction with reference examples before designing.
- [ ] Create Penpot design foundation (tokens: color, typography, spacing, radius).
- [ ] Design Main screen (see requirements below).
- [ ] Design WiFi config screen.
- [ ] Visual self-review + present for go/no-go.

## Main screen — required elements

- [ ] Detected (room) temperature — source: HA sensors.
- [ ] Target temperature.
- [ ] Mode: heat / cool (aka summer / winter).
- [ ] Toolbar: WiFi connection status, time, day.
- [ ] Override action (turn heating/cooling on/off manually — the primary interaction).

## WiFi config screen — required elements

- [ ] Network selection / SSID entry.
- [ ] Password entry (on-screen keyboard, capacitive touch).
- [ ] Connection status / feedback.

## Open questions to resolve later

- [ ] HA connection method — ESPHome vs custom firmware ([ADR-0005](adr/0005-ha-connection-method.md)).
- [ ] Additional screens / data not yet remembered by the owner ("andiamo per ordine").
- [ ] Humidity? secondary sensors? (unconfirmed — do not assume.)
