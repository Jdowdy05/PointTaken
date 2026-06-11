---
project: JustTheTip
type: component
---

# Power Tree

USB-C VBUS feeds the board through protection and current limiting, then generates local rails for the controller and five sensor ports.

## Rails

- 3V3_TOF_MCU: powers STM32 I/O and TMF8829 VDD, VDDV, and VDDC.
- 1V8_TOF_DIG: powers TMF8829 VDDD.
- VIO: tied to 3.3 V for the first design.

## Regulator Direction

- 3.3 V rail: TPS62826 or TPS62827 class buck.
- 1.8 V rail: TPS62825 or TPS62826 class buck.

## Layout Notes

- Keep switching loops compact.
- Place rail bulk capacitance near the FFC connector group.
- Add test pads for 5V, 3V3, 1V8, and GND.
- Add optional current measurement jumpers during bring-up.
- Keep regulator switch nodes away from FFC sensor signals.

## Related Notes

- [[PCB1 Controller Board]]
- [[TMF8829 Sensor]]
- [[Component Selection]]
