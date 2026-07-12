# Design Notes — Penpot UI

Resume point for the Penpot design work. The design itself lives in the Penpot file
(self-hosted, `mcp__penpot__` = `https://penpot.mediacross.it`); this file is the human-readable
record of what exists, how, and the gotchas learned.

## Direction

**Holo HUD** — cold/holographic sci-fi: near-black background, cyan chrome, thin lines,
faint glow, big glanceable readout. LCARS-inspired but space-conscious (480×320 landscape).
Mode accents are functional and constant: **heat = amber**, **cool = cyan**.
(See [ADR-0007](adr/0007-aesthetic-direction-holo-hud.md).)

## Token foundation (Penpot sets, both active)

Tier model: `primitives` → `semantic` (shapes bind to semantic). Single dark-only theme
(no light/dark split — fixed embedded display).

- **primitives (42)**: colors `color.ink.{950..700}`, `color.slate.{400,200}`,
  `color.frost.{50,0}`, `color.cyan.{400,600}`, `color.amber.{400,300}`,
  `color.green.400`, `color.yellow.400`, `color.red.400`; `spacing.{1..12}` (4px grid);
  `radius.{sm,md,lg,xl,pill}`; `font.family.{display,ui}`; `font.size.{100,200,300,500,700,1000}`;
  `font.weight.{regular,medium,semibold,bold}`.
- **semantic (35)**: `color.bg.{base,surface,raised}`, `color.border.{subtle,accent}`,
  `color.text.{primary,muted,inverse}`, `color.accent.{default,dim}`,
  `color.mode.{heat,cool}`, `color.status.{ok,warn,danger}`,
  `color.control.{on.bg,on.text,off.bg,off.text}`, `spacing.inset.*`, `spacing.gap.*`,
  `radius.{control,panel,full}`, `font.size.{caption,label,body,title,target,hero}`.

Key palette: bg `#060A0F`, surface `#0E141C`, raised `#16202B`, border `#22303F`,
text `#DCEAF7` / muted `#6E8299`, cyan accent `#33E1FF`, amber heat `#FF8A3D`.

## Fonts

- Display / readout: **Chakra Petch** (`gfont-chakra-petch`). Chosen as "least-worst" —
  none delighted; revisit possible (can upload a custom font to the instance).
- UI / labels: **Inter Tight**.
- The instance has ~1911 fonts available.
- **Firmware note:** on the device (ESPHome LVGL) the display font is **Antonio**
  (owner's preference, chosen while building the real screen), not Chakra Petch — so the
  Penpot PoC and the firmware diverge on the readout typeface. UI labels stay Inter Tight.
  Firmware UI specifics (LVGL structure, gauge, fonts, build model) live in
  [`firmware/README`](../firmware/README.md).

## Main screen structure (board `main-thermostat`, 480×320)

- **background** (absolute, behind): blurred cyan radial glow + 2 concentric ring strokes
  + 8 corner-bracket rects (HUD frame).
- **toolbar** (flex row): left = signal-bars icon + `14:32`; right = humidity drop + `48%` · `MON`.
- **main-row** (flex row): `col-left` [− , mode(snowflake)] · `gauge` · `col-right` [+ , override].
  - **gauge**: 44-dot radial ring (270° arc, active dots up to target ~62%, white target dot),
    subtle dark center disc, big room temp `21.4°`, cyan target `22.0°`.
  - `col-left`/`col-right`/`main-row` have `clipContent = false` so the override glow isn't cut.
- **IconButton** component (round chrome), instanced for −, +, mode, override; icon = a `Path`
  child, per-instance `content`/color override. Main instance parked off-canvas at (520, 420).

## Penpot MCP gotchas learned (important for resuming)

- **Fonts**: `Font.applyToText()` sets a wrong internal `fontId` → text shows "missing font"
  and falls back. **Set properties directly**: `t.fontId = penpot.fonts.findByName(name).fontId`
  (`gfont-<slug>`), plus `fontFamily`/`fontVariantId`/`fontWeight`.
- **Token names are hierarchical paths**: can't have both a leaf and its prefix
  (`color.accent` + `color.accent.dim` fails → use `color.accent.default`). A semantic token
  must not reference a primitive of the *same* name (`radius.pill` → `{radius.pill}` self-ref;
  renamed semantic to `radius.full`).
- **Flex**: `justifyContent` uses `start|center|end|space-between|space-around` (NOT `flex-end`).
- **Icons**: build via `penpot.createPath()` + `path.content = "<svg d>"`; `resize()` scales
  (uniform-scale to avoid distortion). Injecting children into an existing component *instance*
  does not render — put the icon in the component and override the child instead.
- **`execute_code` calls are atomic**: a mid-script throw leaves partial shapes. Prefer small
  steps, guard risky ops with try/catch, keep it idempotent (check-before-create).
- `borderRadius`/`rotation` on some shapes rejected non-integer / direct-set values — dot-ring
  uses ellipses (no rotation) to avoid this.

## Versioning

Penpot has native version history (`File.saveVersion(label)` / `findVersions()` / restore in
History panel). Milestone saved: **"PoC — main screen v3 (Holo HUD)"**. This complements git,
which versions the docs/decisions (not the Penpot file).
