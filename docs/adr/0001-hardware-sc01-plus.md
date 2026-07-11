# ADR-0001 — Hardware platform: SC01-Plus

**Status:** accepted

## Context

Building a custom thermostat to replace an old, non-IoT unit. Need an MCU with a good
touch display and at least one output to drive a relay. The owner already has the board.

## Decision

Use the **SC01-Plus** dev board: ESP32-S3 with a 3.5" capacitive touch screen
(IPS, ST7796 display driver, FT6336U touch controller). One output is enough for the
single relay needed.

## Alternatives rejected

- Off-the-shelf smart thermostat — rejected: does not solve the sensor-placement problem
  and offers less control / worse HA integration than desired.
- Other custom boards — not considered; the owner already has the SC01-Plus.

## Consequences

- ESP32-S3 gives WiFi for HA connectivity.
- Limited GPIO, but only one relay output is required.
- The 3.5" touch screen is the centerpiece — makes UI quality the dominant concern.
