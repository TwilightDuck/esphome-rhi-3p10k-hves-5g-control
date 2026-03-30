# AGENTS Guide

This repository is optimized for LLM-assisted maintenance.

## Goals

- Keep Solis RHI-3P10K-HVES-5G control behavior stable and predictable.
- Make register-level intent explicit.
- Avoid broad refactors unless requested.

## Change Rules

1. Make surgical edits only.
2. Do not change control register order casually.
3. Preserve safe reset behavior in `solis_stop_all_overrides`.
4. Keep Battery Hold behavior: manual amps reset to `0`.
5. Keep Zero Export behavior synchronized:
   - enable path writes `43072=1` and `43074=0`
   - disable path writes `43072=0` and `43074=20000`

## Verification

At minimum, run:

```bash
esphome config rhi-3p10k-hves-5g-bridge.yaml
```

If hardware is available, verify in Home Assistant:
- Force Charge reacts
- Force Discharge reacts
- Hold mode keeps 0A
- Zero export toggles and restores correctly

## References

- https://esphome.io/components/modbus_controller.html
- https://esphome.io/components/switch/template.html
- https://github.com/fboundy/solis-modbus
