# Sensor harness

The connector is a 16-circuit, 1.0 mm pitch JST NSHD wire harness: BM16B-NSHDZS-TFT board headers, NSHDR-16V-Z housings and SNSHD-003T-P0.2 contacts.

| Pin | Signal | Notes |
| --- | --- | --- |
| 1 | GND | Ground return. |
| 2 | 3V3_TOF | Sensor 3.3 V rail. |
| 3 | TOF_VIO | TMF8829 I/O rail; strapped to 3.3 V on PCB1 by default. |
| 4 | GND | Power return. |
| 5 | 1V8_TOF | Sensor VDDD rail. |
| 6 | GND | Power return. |
| 7 | SPI_SCLKx | Per-port SCLK preferred. |
| 8 | SPI_MOSIx | Per-port MOSI preferred. |
| 9 | SPI_MISOx | Per-port MISO preferred. |
| 10 | SPI_CSn | Per-port chip select. |
| 11 | I3C_SCLx / AUX1 | Optional bring-up/debug I3C/I2C; pull up to TOF_VIO. |
| 12 | I3C_SDAx / AUX2 | Optional bring-up/debug I3C/I2C; pull up to TOF_VIO. |
| 13 | ENx | Per-port sensor enable. |
| 14 | INTx | Per-port interrupt. |
| 15 | DET_IDx | Presence/revision detection. |
| 16 | GND | Fourth ground return at the cable edge. |

Pin numbers and signal roles match the native PCB2 connector. Net names vary by controller; pin 3 is the explicit I/O supply and pin 16 is ground. Define housing orientation and pin-1-to-pin-1 continuity in the physical harness drawing before assembly. The older FFC/FPC interface is retired.
