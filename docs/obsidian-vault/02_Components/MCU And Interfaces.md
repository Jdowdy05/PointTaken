---
project: JustTheTip
type: component
---

# MCU And Interfaces

Baseline MCU: STM32H573ZI or a close STM32H573 package.

## Why STM32H573ZI

- 250 MHz Cortex-M33.
- 2 MB flash and 640 KB SRAM.
- Six SPI peripherals.
- One I3C peripheral.
- Native USB full-speed.
- USB Type-C/USB PD controller.
- Enough package options for five sensor ports, debug, and USB-C support.

## Sensor Interfaces

SPI is the primary sensor transport. Use one SPI peripheral per sensor if the final package and routing allow it. A shared SPI bus with per-sensor CS/EN/INT is the fallback.

I3C/I2C pins are carried as optional FFC pins for bring-up and future alternate topologies.

## Host Interfaces

Native STM32 USB is the main host link. CP2102N is a debug UART option and should not be wired in parallel with STM32 USB on the same D+/D- pair.

## Related Notes

- [[System Architecture]]
- [[Firmware Bringup Contract]]
- [[Component Selection]]
