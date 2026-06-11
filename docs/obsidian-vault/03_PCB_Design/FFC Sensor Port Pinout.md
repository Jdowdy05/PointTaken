---
project: JustTheTip
type: interface
---

# FFC Sensor Port Pinout

Recommended connector: 16-pin, 0.5 mm pitch ZIF FFC/FPC.

| Pin | Signal | Notes |
| --- | --- | --- |
| 1 | GND | Ground return. |
| 2 | 3V3_TOF | Sensor 3.3 V rail. |
| 3 | 3V3_TOF | Parallel 3.3 V conductor. |
| 4 | GND | Power return. |
| 5 | 1V8_TOF | Sensor VDDD rail. |
| 6 | GND | Power return. |
| 7 | SPI_SCLKx | Per-port SCLK preferred. |
| 8 | SPI_MOSIx | Per-port MOSI preferred. |
| 9 | SPI_MISOx | Per-port MISO preferred. |
| 10 | SPI_CSn | Per-port chip select. |
| 11 | I3C_SCLx / AUX1 | Optional debug/I3C/I2C. |
| 12 | I3C_SDAx / AUX2 | Optional debug/I3C/I2C. |
| 13 | ENx | Per-port sensor enable. |
| 14 | INTx | Per-port interrupt. |
| 15 | DET_IDx | Presence/revision detection. |
| 16 | GND / shield | Edge ground/shield reference. |

## Notes

- Pin 1 markings must be visible on PCB1, PCB2, and cable drawings.
- Lock cable side orientation before layout.
- Add test pads on PCB1 for the first prototype.

## Related Notes

- [[PCB1 Controller Board]]
- [[PCB2 Fingertip Sensor Board]]
- [[Firmware Bringup Contract]]
