# ADR-0006 — Screen orientation & resolution

**Status:** accepted

## Context

The SC01-Plus panel is 480×320 (3.5" IPS). The UI layout depends heavily on orientation.

## Decision

Use the screen in **landscape**: **480×320** (width×height).

## Alternatives rejected

- Portrait (320×480) — rejected by the owner in favor of landscape.

## Consequences

- All Penpot frames and layouts target **480×320 landscape**.
- Landscape is tight vertically (320 px): the LCARS-inspired aesthetic must be
  space-conscious. Typography and touch targets must stay legible at a glance and usable
  with a finger (capacitive touch).
