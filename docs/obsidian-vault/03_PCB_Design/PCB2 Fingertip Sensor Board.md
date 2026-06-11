---
project: JustTheTip
type: pcb
board: PCB2
---

# PCB2 Fingertip Sensor Board

PCB2 is the compact fingertip board. It carries one TMF8829 sensor and connects back to PCB1 over FFC.

## Blocks

- TMF8829 sensor.
- Five local decoupling capacitors.
- 16-pin 0.5 mm FFC connector.
- Two mounting holes.
- Optional DET/ID resistor.
- Optical aperture/boot/cover-glass region.

## Layout Rules

- Place TMF8829 first.
- Keep decoupling close to sensor pins.
- Use solid ground around the sensor.
- Keep hardware and cable geometry out of the optical field.
- Put mounting holes outside optical and FFC bend keepouts.

## Size Target

The package is small, but the connector and mounting holes dominate. A first mechanical target is roughly 14 mm to 18 mm by 10 mm to 14 mm, then reduce after final connector and screw choices.

## Related Notes

- [[TMF8829 Sensor]]
- [[FFC Sensor Port Pinout]]
- [[Reference Documents]]
