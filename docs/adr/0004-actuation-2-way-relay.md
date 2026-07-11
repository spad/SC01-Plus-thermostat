# ADR-0004 — Actuation: single 2-way relay

**Status:** accepted

## Context

The heating/cooling system is driven by a pump that the thermostat switches. Only one
actuation output is needed.

## Decision

Use a single **2-way relay** to command the heat/cool pump. This is the only output the
device drives.

## Alternatives rejected

- Multiple outputs / zone control — not needed for this installation.

## Consequences

- Fits the SC01-Plus's limited GPIO (one output is enough).
- The firmware control path is trivial: mode + on/off → relay state.
- Safety interlocks (min on/off times, mode-change guards) to be defined in firmware phase.
