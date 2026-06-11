---
project: JustTheTip
type: component-research
---

# Component Selection

The current selected/candidate components are mirrored in [../../Component_Research.md](../../Component_Research.md).

## Selected Direction

- Sensor: TMF8829.
- MCU: STM32H573ZI-class STM32H573.
- USB-C protection: TCPP01-M12.
- USB D+/D- ESD: USBLC6-2 family.
- Debug UART bridge: CP2102N.
- Buck regulators: TPS62825/TPS62826/TPS62827 family.
- FFC connector: 16-position, 0.5 mm pitch ZIF FPC/FFC, Hirose FH12-class candidate.

## Revisit Before Schematic Freeze

- Exact STM32 package.
- Exact USB-C receptacle.
- Exact FFC connector and cable orientation.
- Whether per-port ESD or load switching is needed.
- Whether USB full-speed is enough for the final output format.

## Related Notes

- [[MCU And Interfaces]]
- [[Power Tree]]
- [[FFC Sensor Port Pinout]]
