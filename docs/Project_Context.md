# Project Context

## Goal

Design two PCB types for a robotic-hand fingertip sensor system based on the ams OSRAM TMF8829 48x32 multi-zone time-of-flight sensor.

## Board Split

- PCB1: 50 mm x 50 mm controller, power, USB-C, MCU, debug serial, regulators, and five FFC sensor ports.
- PCB2: smallest practical TMF8829 sensor board with one FFC connector, local decoupling, optical/mechanical clearances, and two mounting holes.

## Sensor Count

PCB1 must support up to five TMF8829 boards, but the design must also boot and operate with fewer boards connected. Firmware and hardware should treat each sensor port independently:

- EN defaults low so missing sensors do not affect boot.
- CS defaults inactive.
- INT is pulled up on PCB1 and handled per port.
- DET/ID identifies whether a fingertip board is connected.
- Firmware scans all five ports and enables only populated sensors.

## Baseline Architecture

- Main sensor interface: SPI, one logical port per sensor.
- Optional expansion/debug interface: I3C/I2C pins carried on the FFC but not required for the first SPI design.
- Host interface: native STM32 USB over USB-C.
- Debug interface: CP2102N UART bridge option or test-pad/UART header.
- Power: USB-C VBUS feeds protected power tree; local bucks generate 3.3 V and 1.8 V rails.

## Principal Constraints

- TMF8829 needs local decoupling on VDD, VDDV, VDDC, VDDD, and VIO.
- TMF8829 optical stack must follow the optical design guide for crosstalk control.
- PCB2 must reserve clean optical field-of-view and field-of-illumination openings.
- PCB1 must stay within 50 mm x 50 mm.
- FFC pinout should be stable enough for prototype spins and future alternate sensor-board shapes.

## Open Decisions

- Final FFC connector family and cable orientation.
- Final STM32 package pinout after CubeMX peripheral mapping.
- Whether all five sensors get independent SPI peripherals or whether one shared SPI bus with per-sensor CS/EN/INT is acceptable for the first prototype.
- Whether the first host link is USB full-speed only or whether a later board should move to USB high-speed for raw histogram streaming.
- Exact PCB2 outline after the FFC connector and mounting-hole standard are selected.
