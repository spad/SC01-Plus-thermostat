# ADR-0003 — HA as brain; no on-device scheduling

**Status:** accepted

## Context

The home runs Home Assistant. Weekly temperature scheduling ("crono") is a classic
thermostat feature, but the owner never uses on-device scheduling — in practice they
always use manual override.

## Decision

**Home Assistant is the brain**: it owns logic, scheduling, and history. The device is a
**thin client** — it displays state and sends commands. **No weekly scheduling on-device.**
The primary on-device interaction is **manual override** (force heating/cooling on/off) plus
setting the target temperature.

## Alternatives rejected

- Full-featured on-device chrono-thermostat — rejected: unused by the owner, duplicates
  logic better kept in HA, and adds UI/firmware complexity.

## Consequences

- Simpler firmware and UI: no schedule editor.
- The device must stay in sync with HA (state reflects HA; commands go to HA).
- If HA is unavailable, override behavior / fallback needs definition (follow-up).
