# ADR-0005 — HA connection method (ESPHome vs custom firmware)

**Status:** open (decide later — does not block Phase 0 UI)

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

**Not yet decided.** Deferred until after the Phase 0 UI concept, because the chosen visual
design informs how demanding the rendering requirements are — which is the deciding factor
between A and B.

## Consequences (of deferring)

- Phase 0 UI mockups in Penpot are designed to be valid for **either** option.
- Decision to be revisited once the UI direction is locked.
