# Glossary

Domain terms used across the docs. Keep definitions short and canonical.

- **Override** — manually forcing heating/cooling on (or off), bypassing any schedule.
  In this project it is the **primary** interaction: the owner always uses override and
  never on-device scheduling.
- **Crono / scheduling** — time-based temperature programming. **Out of scope on-device**;
  owned by Home Assistant.
- **Thin client** — the device holds no logic/history; it displays state and sends
  commands. HA is the brain.
- **Setpoint / target temperature** — the temperature the system aims to reach.
- **Detected temperature** — the real room temperature, sourced from HA sensors (not from
  a sensor embedded in the device).
- **Mode** — heat vs cool (equivalently winter vs summer).
- **HA** — Home Assistant, the home automation platform that manages this device.
- **ESPHome** — firmware framework with native HA integration; includes an LVGL component.
- **LVGL** — embedded graphics library used to render the UI on the ESP32-S3.
- **SC01-Plus** — the dev board: ESP32-S3 + 3.5" capacitive touch, 480×320 landscape.
