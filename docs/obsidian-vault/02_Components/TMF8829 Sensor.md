---
project: JustTheTip
type: component
part: TMF8829
---

# TMF8829 Sensor

The TMF8829 is the sensing element for each fingertip board.

## Key Specs

- 48 x 32 maximum zone grid.
- 1536 zones total.
- Configurable 8 x 8, 16 x 16, 32 x 32, and 48 x 32 modes.
- 940 nm integrated dual VCSELs.
- 80 deg diagonal field of view.
- Package/module size: 5.7 mm x 2.9 mm x 1.5 mm.
- Interfaces: I3C, I2C-compatible, and SPI.
- VDD/VDDV/VDDC are 3.3 V-class rails.
- VDDD should use 1.8 V for the lower-power design.
- VIO should be 3.3 V for the first STM32 design unless a final pin bank requires otherwise.

## Local Components

Each PCB2 needs these close to the sensor:

- VDDC: 1 uF.
- VDD: 1 uF.
- VDDD: 1 uF.
- VDDV: 1 uF.
- VIO: 2.2 uF.

## Layout Priorities

- Place the sensor first, then the optical aperture.
- Keep copper, soldermask openings, screws, cable bends, and connector bodies out of the field of view and illumination.
- Use a solid ground reference and short capacitor returns.
- Follow the optical design guide for cover glass, boot, aperture, and crosstalk control.

## Sources

- Local datasheet: [../../references/TMF8829-Time-of-flight-sensor.pdf](../../references/TMF8829-Time-of-flight-sensor.pdf)
- Optical design guide: [../../references/TMF8829_Optical_Design_Guide/TMF8829_Optical_Design_Guide(ODG)_1v0.pdf](../../references/TMF8829_Optical_Design_Guide/TMF8829_Optical_Design_Guide(ODG)_1v0.pdf)

## Related Notes

- [[PCB2 Fingertip Sensor Board]]
- [[FFC Sensor Port Pinout]]
- [[Power Tree]]
