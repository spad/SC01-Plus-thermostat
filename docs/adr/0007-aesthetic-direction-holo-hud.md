# ADR-0007 — Aesthetic direction: Holo HUD

**Status:** accepted (for the PoC)

## Context

The UI must look like a commercial product, not DIY, and the owner wants a sci-fi / hi-tech feel
(LCARS-liked but space-conscious on a 480×320 landscape screen). Three directions were mocked as
options: Holo HUD (cold/cyan), LCARS Modern (warm amber), Phosphor (retro terminal green).

## Decision

Adopt **Holo HUD**: near-black background, cyan chrome, thin lines and faint glow, large
glanceable readout, radial dot-ring gauge. Functional mode accents stay constant: heat = amber,
cool = cyan.

## Alternatives rejected (for now)

- **LCARS Modern** — warm, rounded "elbow" panels; too space-hungry for 320px height.
- **Phosphor** — retro terminal; less modern than desired.

Both remain available as variants if the project proceeds and wants to compare.

## Consequences

- Token palette and the main-screen PoC are built around this direction
  (see [design notes](../design-notes.md)).
- Fonts: Chakra Petch (display) + Inter Tight (UI) — a "least-worst" pick, open to revisit.
- Decision is scoped to the PoC; a full product pass could refine or switch direction.
