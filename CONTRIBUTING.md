# Contributing

Thanks for contributing.

## Scope

This project targets the Solis RHI-3P10K-HVES-5G. Please do not add Batrium-specific logic here.

## Pull Request Guidelines

- Explain which registers and control paths are changed.
- Keep changes small and focused.
- Update `README.md` if behavior changes.
- Validate config with `esphome config rhi-3p10k-hves-5g-bridge.yaml`.

## Safety Notes

- Do not remove boot/reset safety behavior.
- Do not bypass `solis_stop_all_overrides` for state transitions.
