---
project: JustTheTip
type: pcb
board: PCB1
---

# PCB1 Controller Board

PCB1 is the 50 mm x 50 mm controller and power board.

## Blocks

- USB-C receptacle and protection.
- STM32H573ZI-class MCU.
- Native USB data link.
- Optional CP2102N debug UART.
- 3.3 V and 1.8 V buck regulators.
- Five 16-pin FFC sensor ports.
- SWD, reset, BOOT0, UART, and power test pads.

## Layout Shape

- USB-C at a board edge.
- ESD/protection close to USB-C.
- MCU near the middle.
- FFC ports around the perimeter.
- Regulators away from FFC exits.
- Solid ground plane on layer 2.

## Critical Notes

- Do not wire STM32 native USB and CP2102N directly to the same USB pair without a mux, hub, or population option.
- Size power for five active sensors.
- Each sensor port must work independently and tolerate missing boards.

## Related Notes

- [[System Architecture]]
- [[Power Tree]]
- [[FFC Sensor Port Pinout]]
