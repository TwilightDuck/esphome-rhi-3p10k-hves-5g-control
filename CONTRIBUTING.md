# Contributing

Thanks for contributing.

## Scope

This project is Solis-only. Please do not add Batrium-specific logic here.

## Pull Request Guidelines

- Explain which registers and control paths are changed.
- Keep changes small and focused.
- Update `README.md` if behavior changes.
- Validate config with `esphome config solis-bridge.yaml`.

## Safety Notes

- Do not remove boot/reset safety behavior.
- Do not bypass `solis_stop_all_overrides` for state transitions.
