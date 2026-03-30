# ESPHome RHI-3P10K-HVES-5G Control

ESPHome bridge for Modbus RTU control and telemetry, focused on the Solis RHI-3P10K-HVES-5G.

This repository intentionally excludes Batrium BMS integration and focuses on:
- manual force charge/discharge controls
- battery hold mode
- zero export mode
- key Solis telemetry sensors for Home Assistant

## Why this repo exists

This project is a clean, publishable control implementation extracted from a larger mixed integration. It is designed to be easy to understand, modify, and operate with LLM coding agents.

## Features

- Solis RHI-3P10K-HVES-5G RS485 Modbus RTU integration (ESP32 + MAX485)
- Force Charge / Force Discharge switches
- Battery Hold switch (resets manual amps to 0A)
- Zero Export switch (writes both enable and backflow limit registers)
- Self-Use reset button and safe boot reset behavior
- Home Assistant friendly entities via ESPHome API

## Hardware

- ESP32-C3 (or compatible ESP32 board)
- MAX485 (or equivalent RS485 transceiver)
- RS485 A/B wiring to Solis RHI-3P10K-HVES-5G communication bus

Default pin mapping in `rhi-3p10k-hves-5g-bridge.yaml`:
- TX: GPIO0
- RX: GPIO1
- DE/RE: GPIO3

## Quick Start

1. Copy secrets template:

```bash
cp secrets.example.yaml secrets.yaml
```

2. Fill in your Wi-Fi / API / OTA secrets.

3. Validate config:

```bash
esphome config rhi-3p10k-hves-5g-bridge.yaml
```

4. Flash and run:

```bash
esphome run rhi-3p10k-hves-5g-bridge.yaml
```

## Control Behavior

- `Manual Amps`: 0-25A target for force modes
- `Force Charge`: applies charge-related control registers
- `Force Discharge`: applies discharge-related control registers
- `Battery Hold`: sets amps to 0A and applies hold registers
- `Zero Export`:
  - ON: writes `43072=1`, `43074=0`
  - OFF: writes `43072=0`, `43074=20000`
- `Self-Use` and boot reset also clear manual control and zero export state

## Register Notes

The implementation uses practical register behavior tested against Solis RHI-3P10K-HVES-5G control paths.

Compatibility note:
- Confirmed working on **Solis RHI-3P10K-HVES-5G**
- May work on related Solis hybrid models, but that is not guaranteed

Key writes used here:
- `43072`: zero export enable
- `43074`: backflow power limit
- `43110`: storage control mode
- `43114`/`43115`: battery control enable + direction
- `43135`: remote-control mode
- `43136` / `43129`: RC charge/discharge power

## LLM Agent Friendly

Read `AGENTS.md` before editing control logic.

Design principles in this repo:
- minimal moving parts
- explicit register intent in code
- safe defaults on boot/reset
- avoid hidden side effects

## References

Documentation and upstream references used:

- ESPHome docs: https://esphome.io/
- ESPHome Modbus Controller: https://esphome.io/components/modbus_controller.html
- ESPHome Template Switch: https://esphome.io/components/switch/template.html
- Solis Modbus integration project (register context): https://github.com/fboundy/solis-modbus

## License

MIT. See `LICENSE`.
