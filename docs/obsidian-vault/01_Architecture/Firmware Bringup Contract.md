---
project: JustTheTip
type: firmware
---

# Firmware Bringup Contract

The hardware should make these steps easy:

1. Boot with all sensor EN pins low.
2. Read DET/ID lines for all five ports.
3. Enable and configure populated sensors one at a time.
4. Select SPI mode and verify communication.
5. Start measurements on populated sensors in a tight sequence.
6. Wait for INT or poll status per sensor.
7. Read FIFO data over SPI, preferably with DMA.
8. Stream packets over native USB with sensor ID, timestamp, mode, confidence, signal, ambient, and zone data.

## Hardware Requirements

- Per-port EN and INT.
- Per-port CS.
- DET/ID line for missing-board handling.
- Debug access to SWD, reset, BOOT0, UART, and rails.
- A USB data path that does not depend on CP2102N for high-rate multi-sensor output.

## Related Notes

- [[System Architecture]]
- [[MCU And Interfaces]]
- [[FFC Sensor Port Pinout]]
