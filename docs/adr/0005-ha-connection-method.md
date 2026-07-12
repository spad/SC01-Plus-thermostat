# ADR-0005 — HA connection method (ESPHome vs custom firmware)

**Status:** decided — **ESPHome** (2026-07-11).

## Context

The device must integrate with Home Assistant. Two broad approaches exist, with a
trade-off between integration effort and UI freedom.

## Options under consideration

### Option A — ESPHome (with LVGL component)

- Native, first-class HA integration (auto-discovery, entities, OTA).
- Less custom code.
- **Open concern:** can ESPHome's LVGL component render all the sci-fi / hi-tech UI we
  need without excessive `lambda` / custom-component work? ESPHome *does* support LVGL
  (layouts, widgets, custom images/fonts); the question is how far bespoke visuals/animation
  can go before it becomes painful.

### Option B — Custom firmware (full LVGL)

- Full control over the look (raw LVGL on ESP-IDF/Arduino).
- Connects to HA via MQTT or the native/WebSocket API.
- Requires configuration on the HA server side and more firmware work.

## Decision

**Option A — ESPHome (with the LVGL component).**

Rationale, now that the Phase 0 UI is locked (Holo HUD):

- **Architectural fit.** The device is a thin client and HA is the brain
  ([ADR-0003](0003-ha-brain-no-on-device-scheduling.md)). That *is* the ESPHome model:
  the device exposes entities, HA owns the logic. ESPHome is aligned, not merely convenient.
- **Rendering is not a blocker.** The "glow/bloom" of the Holo HUD is baked into pre-rendered
  image assets in either option, so it does not differentiate A from B. ESPHome's LVGL (v9)
  covers the rest. The WT32-SC01 Plus is a first-class target: `mipi_spi` platform with
  `model: wt32-sc01-plus` drives the ST7796 (8-bit parallel bus as octal SPI) with hardware
  rotation; touch via `ft63x6`.
- **Free plumbing.** Native HA API + auto-discovery, OTA, and WiFi provisioning
  (captive portal / Improv) come for free — code we would otherwise hand-write in Option B.

If a bespoke visual later exceeds YAML-LVGL, the escape hatch is raw LVGL via a lambda /
custom component *inside* the ESPHome shell — keeping all the connectivity benefits.

## Consequences

- **No custom WiFi config screen needed** — `captive_portal` handles provisioning. The Phase 0
  "WiFi config screen" deliverable is dropped.
- Firmware config lives in the ESPHome add-on; mirrored in `firmware/` (see its README).
- Phase 1 proceeds on ESPHome: base flashed over the prior firmware, then display/touch, then
  the LVGL Holo HUD build.
