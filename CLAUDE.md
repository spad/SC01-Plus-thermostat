# CLAUDE.md — SC01-Plus Thermostat

> Project description + working conventions + index of the documentation.
> This file and everything under `/docs` are the **inter-session source of truth (SoT)**:
> a fresh session must be able to resume from these documents alone.

## What this project is

A DIY replacement for an old home thermostat (cronotermostato), built to integrate
natively with **Home Assistant (HA)**.

The old unit is being replaced because:

- It is not IoT-connectable (the home already runs HA).
- Its temperature sensor is embedded in the wall-mounted body, right next to the
  heating pipes — so the reading is meaningless as a room temperature.

The new device is intentionally a **thin client**: HA is the brain (logic, scheduling,
history); the device provides a screen, one relay output, and a polished UI.

### Hardware

- Board: **SC01-Plus** — ESP32-S3 + 3.5" capacitive touch screen.
- Display: **480×320, landscape** (IPS, ST7796 driver, FT6336U touch).
- Output: a single **2-way relay** driving the heat/cool pump.

### Scope split

- **In scope (device):** UI, real room-temperature display (from HA sensors),
  target temperature, heat/cool mode, WiFi config, manual **override** on/off.
- **Out of scope (device):** weekly scheduling ("crono"). HA owns all scheduling.
  In daily use the owner **always uses override**, never on-device scheduling.

### The real challenge

The **UI**. It must have the polish of a commercial product — no DIY look — because it
stays in the home long-term. Target aesthetic: **sci-fi / hi-tech** (LCARS-inspired but
space-conscious, since landscape 480×320 is tight). The firmware/relay side is trivial
for the owner (experienced MCU/FW/DIY engineer).

### Current phase

**Phase 0 — UI concept (gate).** Produce a couple of screens in Penpot to decide
whether the result is good enough to commit to the full project. UI outcome drives go/no-go.

## Working conventions

- **One step at a time.** No batched changes. Finish a step, then agree the next.
- **Docs are the SoT.** Keep `/docs` always up to date and coherent; a new session
  resumes from docs alone.
- **Artifacts in English** (code, docs, comments, commits). Chat in Italian.
- **ADR per scope.** One decision = one file under `docs/adr/`. Lightweight format.
- **Ask before acting** when anything is unclear.

## Penpot workflow

- Target MCP server: **`mcp__penpot__`** (Mediacross self-hosted, created via Claude Code).
  Do **not** use the removed `claude.ai` connector.
- Before any Penpot work: read `~/.penpot-ai-kit/AGENTS.md`, run `high_level_overview`,
  route via `penpot-router`. Tokens-first; never one-shot; Suggest → Apply-with-review.

## Documentation index

- [Roadmap](docs/roadmap.md) — phases, done / to do.
- [To-do](docs/todo.md) — actionable backlog.
- [Priorities](docs/priorities.md) — current focus and ordering.
- [Glossary](docs/glossary.md) — domain terms.
- [ADR index](docs/adr/README.md) — architectural decisions.
  - [0001 — Hardware: SC01-Plus](docs/adr/0001-hardware-sc01-plus.md)
  - [0002 — External temperature sensing](docs/adr/0002-external-temperature-sensor.md)
  - [0003 — HA as brain, no on-device scheduling](docs/adr/0003-ha-brain-no-on-device-scheduling.md)
  - [0004 — Actuation: 2-way relay](docs/adr/0004-actuation-2-way-relay.md)
  - [0005 — HA connection method](docs/adr/0005-ha-connection-method.md) — **open**
  - [0006 — Screen orientation & resolution](docs/adr/0006-orientation-and-resolution.md)
