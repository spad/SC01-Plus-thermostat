# ADR-0008 — Device ↔ HA entity model

**Status:** accepted (2026-07-11).

## Context

With ESPHome chosen ([ADR-0005](0005-ha-connection-method.md)) and HA as the brain
([ADR-0003](0003-ha-brain-no-on-device-scheduling.md)), we need to decide how the device's
data and controls are represented across the device/HA boundary: current temperature,
humidity, target temperature (setpoint), heat/cool mode, and manual override.

Per the project scope (see `CLAUDE.md`), the device owns **target temperature, mode, and
override**; **current temperature and humidity come from HA sensors** (the device has no
usable local sensor — [ADR-0002](0002-external-temperature-sensor.md)).

## Decision

- **Read-only from HA (display only):** import via the ESPHome `homeassistant` sensor
  platform — `sensor.sensore_ambiente_sala_temperature` (room readout) and
  `sensor.sensore_ambiente_sala_humidity` (toolbar). HA pushes state over the native API.
- **Device-owned, exposed to HA:**
  - **Target temperature** → template `number` (5–35 °C, step 0.5, restored). The on-device
    −/+ buttons and HA can both set it; it drives the target readout and the gauge fill.
  - **Mode (heat/cool)** → template `select` with options `Cool` / `Heat`. The mode button
    cycles it; chosen over a `switch` for clear semantics and future extensibility
    (e.g. Off/Auto).
  - **Override on/off** → template `switch`. The power button toggles it.
- Display widgets and entities are kept **bidirectionally in sync** (entity `on_value` /
  `turn_on/off` actions update the LVGL widgets; button triggers set the entities).

## Alternatives rejected

- **ESPHome `climate` component on the device** — would place thermostat logic on the device,
  contradicting "HA is the brain". Rejected.
- **Setpoint/mode owned by HA** (device mirrors an `input_number` / `climate`) — the scope
  makes these device-owned controls; a device-owned `number`/`select` also works standalone.
- **Mode as a `switch`** (on=heat) — semantically ambiguous; `select` is clearer.

## Consequences

- HA sees three new controllable entities (Target Temperature, HVAC Mode, Override) plus the
  imported climate readings; HA automations/logic act on them.
- The **relay actuation logic** (who closes the relay, and when) is intentionally out of this
  ADR — it is a separate Phase 1 item ([ADR-0004](0004-actuation-2-way-relay.md) covers the
  hardware choice, not the control logic).
- Implementation lives in [`firmware/sc01_thermostat.yaml`](../../firmware/sc01_thermostat.yaml);
  see [`firmware/README`](../../firmware/README.md).
