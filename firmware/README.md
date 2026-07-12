# Firmware — SC01-Plus (ESPHome)

Phase 1 device config. See the [roadmap](../docs/roadmap.md),
[ADR-0005](../docs/adr/0005-ha-connection-method.md) (ESPHome) and
[ADR-0008](../docs/adr/0008-device-ha-entity-model.md) (device↔HA entity model).

## Files

- `sc01_thermostat.yaml` — the device config.
- `secrets.yaml.example` — the keys the config references; real values stay out of the repo.

## Toolchain

**Current:** builds run in the **ESPHome add-on inside Home Assistant** (HA host is
an N100 VM). This repo holds the versioned copy of the YAML; to build/flash, paste
it into the add-on's `/config/esphome/` and run there.

**Optional (set up, not yet adopted):** building locally via the `esphome` CLI on
the Mac (M3 Pro, much faster than the N100). The config already enables ccache
(`IDF_CCACHE_ENABLE`) for that path; needs `brew install esphome` + a local
`firmware/secrets.yaml` whose API key / OTA password match the add-on's.

Secrets (WiFi, API encryption key, OTA password) are referenced via `!secret` and
live in the add-on's `secrets.yaml` (and, for local builds, a gitignored
`firmware/secrets.yaml`). Never committed (repo is public).

## Build model (important for the iteration loop)

ESPHome generates the whole configuration into `main.cpp`; components are compiled
as a library. Consequence, measured on this project:

- **Changing config values** (colors, fonts, text, positions, layout within
  already-used widgets) → only `main.cpp` recompiles → fast (~27 s incl. link + OTA).
- **Enabling a new LVGL feature** (first use of flex, `meter`, `button`, …) or
  changing components / `sdkconfig` → flips a flag in `lv_conf.h` / regenerates
  shared headers → **full LVGL/app rebuild** (~12 min on the N100).
- The scary "recompiles everything" seen early on was the one-time **cold build**.
- ccache helps only cold/feature-enabling builds and never the link step, so it is
  not the main lever here — the fast loop comes from touching only `main.cpp`.

## Board / hardware

WT32-SC01 Plus — ESP32-S3, 16 MB flash, octal PSRAM @ 80 MHz.

- Display: ST7796 on an 8-bit parallel (i80) bus, driven via the `mipi_spi`
  platform with `model: wt32-sc01-plus` (the 8 data pins are an octal SPI bus).
  Rotates in hardware. **Rotation is set in the `lvgl:` block (`rotation: 90`), not
  in `display:`** (required by ESPHome LVGL v9).
- Touch: FT6336U (`ft63x6`) on I²C (SDA 6, SCL 5, INT 7). No `transform` — LVGL
  rotation auto-rotates touch coordinates.
- Backlight: PWM on GPIO45 (`ledc` → `monochromatic` light).

## Fonts

Fetched from Google Fonts at build time (`gfonts://`) — no TTFs in the repo.

- Display / readout: **Antonio** (owner's preference), weights 700/600. Carry the
  `°` glyph explicitly (outside the default ASCII set).
- UI / labels: **Inter Tight** (`font_ui`). Not yet judged on screen; may switch to
  Antonio too.
- Icons: LVGL built-in symbols in `montserrat_*` (by codepoint): wifi `\uF1EB`, tint `\uF043`, plus `\uF067`, minus `\uF068`, power `\uF011`.

## UI — Holo HUD Main screen

Direction & tokens: see [design-notes](../docs/design-notes.md). Palette `color:` ids
are role-based, carrying the Holo HUD token values (dark-only).

Structure (LVGL flex): `root` → vertical flex:
- **toolbar** (row, space-between): wifi + time · humidity + day.
- **main_row** (row, space-between): `col_left` (− button, mode button) ·
  `gauge` · `col_right` (+ button, override button).
- **gauge**: a `meter` — 44 dim ticks over 270° (gap at bottom) — plus an `arc`
  indicator (`gauge_fill`, cyan, updatable) showing fill up to the setpoint, with
  the room-temp and target labels overlaid in the centre.

Verified on device: layout, fonts, colours, centring. **Deferred:** HUD glow/ring
background (needs baked image assets); snowflake/flame mode icons via MDI (currently
text "COOL"/"HEAT").

## HA integration (see ADR-0008)

- **Read from HA** (display only): `sensor.sensore_ambiente_sala_temperature` →
  room readout; `sensor.sensore_ambiente_sala_humidity` → toolbar %.
- **Device-owned, exposed to HA**: `number` Target Temperature (5–35, step 0.5;
  ± buttons; drives readout + gauge fill), `select` HVAC Mode (Cool/Heat; mode
  button cycles; tints accent), `switch` Override (power button toggles).
- Relay actuation logic is **not** here yet (separate roadmap item).

## Known issues / pending verification

- **HA integration + arc gauge fill: implemented but not yet verified on device**
  (last build pending). Verify sensors show real values, ± moves the fill, and the
  3 new HA entities work both ways.
- **OTA fails on this device**: the add-on can't resolve the mDNS name (the browser
  reaches it fine). Likely cause: the underscore in `sc01_thermostat` (hostnames
  disallow `_`); the other 11 ESPHome devices use hyphens. Fix to try: rename node
  to `sc01-thermostat`. Parked — using serial meanwhile.

## Flashing

- **First flash** (over the previous firmware, e.g. Bruce): over **USB** via the
  ESPHome Dashboard in the laptop browser (WebSerial) → *Install → plug into this
  computer*. Fallback: download `.factory.bin`, flash from `web.esphome.io`.
- **After that**: OTA (once the mDNS/name issue above is fixed) — otherwise serial.
