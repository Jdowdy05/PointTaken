---
project: JustTheTip
type: architecture
---

# System Architecture

The system is split into one controller board and up to five fingertip sensor boards.

## PCB1

PCB1 owns:

- USB-C power and data.
- USB-C sink/PD protection.
- STM32H573ZI-class MCU.
- Native USB host data link.
- Optional CP2102N debug UART bridge.
- 3.3 V and 1.8 V buck regulators.
- Five identical 16-pin FFC ports.

## PCB2

Each PCB2 owns:

- One TMF8829.
- Sensor-local decoupling.
- One 16-pin 0.5 mm FFC connector.
- Two mounting holes.
- Optical aperture/boot/cover-glass geometry.
- Optional detect/ID resistor.

## Data Flow

The preferred transport is SPI from each TMF8829 to the STM32. Firmware enables only populated ports, triggers measurements close together, waits for per-sensor interrupts, and streams timestamped results over native USB.

## Related Notes

- [[PCB1 Controller Board]]
- [[PCB2 Fingertip Sensor Board]]
- [[FFC Sensor Port Pinout]]
- [[MCU And Interfaces]]
- [[Power Tree]]
