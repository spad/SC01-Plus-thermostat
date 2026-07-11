# ADR-0002 — External temperature sensing (via HA)

**Status:** accepted

## Context

The old thermostat's core flaw: its temperature sensor is embedded in the wall-mounted
body next to the heating pipes, so it never reflects the real room temperature.

## Decision

The device does **not** rely on a sensor embedded in its body for control. The **detected
(room) temperature comes from Home Assistant sensors**, which can be placed where they
actually measure the room.

## Alternatives rejected

- Embedded sensor in the device body — rejected: this is exactly the flaw being replaced,
  and the device may sit in a thermally biased location.

## Consequences

- The device displays and acts on a temperature value provided by HA.
- Removes any hard constraint on where the device itself is mounted.
- Sensor selection/placement is an HA-side concern, not a device concern.

## Open follow-ups

- Whether the device also has a local sensor (for display or fallback) is not decided —
  do not assume.
