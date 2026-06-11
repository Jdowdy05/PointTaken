# PCB Design Layout

This is the primary layout context for schematic capture and PCB planning. It records the current design direction for the two-board TMF8829 fingertip sensor system.

## Summary Recommendation

Use PCB1 as a 50 mm x 50 mm controller/power/USB board with an STM32H573ZI-class MCU, native USB-C data, protected USB-C sink power, two buck rails, and five identical 16-pin FFC sensor ports. Use PCB2 as a minimal TMF8829 sensor module with the TMF8829, required local capacitors, one 16-pin 0.5 mm FFC connector, two mounting holes, and optical-stack provisions from the TMF8829 optical design guide.

For the five-sensor architecture, use SPI as the primary TMF8829 transport. Keep I3C/I2C as optional/debug pins on the connector. The TMF8829 supports I3C, I2C-compatible operation, and SPI, but the datasheet explicitly points histogram readout toward I3C or SPI because I2C limits data rate. SPI also avoids address-assignment complexity when five sensors are present.

## Reference Sensor Facts

TMF8829 device facts used for this design:

- 48 x 32 maximum zone grid, 1536 zones total.
- Configurable modes include 8 x 8, 16 x 16, 32 x 32, and 48 x 32.
- Integrated dual VCSELs at 940 nm.
- Module size: 5.7 mm x 2.9 mm x 1.5 mm.
- Field of view: 80 deg diagonal, about 67.9 deg X and 52.8 deg Y.
- Supply range for VDD/VDDV/VDDC: 2.9 V to 3.5 V functional, 3.1 V to 3.5 V for full performance.
- VIO can be 1.2 V, 1.8 V, or 3.3 V-class depending on host I/O.
- Recommended lower-power digital core approach: VDDD from a 1.8 V regulator.
- External capacitors per sensor:
  - VDDC: 1 uF, 0402, close to pin 1.
  - VDD: 1 uF, 0402, close to pin 8.
  - VDDD: 1 uF, 0402, close to pin 14.
  - VDDV: 1 uF, 0402, close to pin 16.
  - VIO: 2.2 uF, 0201 or compact 0402, close to pin 9.
- For optical stack design, maintain the cover-glass and boot guidance from the optical design guide: short air gap, 940 nm transparent cover material, and crosstalk-controlled aperture geometry.

## Board Partition

### PCB1: Controller Board

Target size: 50 mm x 50 mm.

Functional blocks:

- USB-C receptacle at board edge.
- USB-C sink/PD protection and CC/VBUS protection.
- Native STM32 USB data path for main host communications.
- STM32H573ZI-class MCU.
- CP2102N USB-UART debug bridge option.
- 3.3 V buck rail for MCU I/O and TMF8829 VDD/VDDV/VDDC.
- 1.8 V buck rail for TMF8829 VDDD.
- Five identical FFC sensor ports.
- SWD, BOOT0, RESET, UART, and power test pads.

### PCB2: Fingertip Sensor Board

Target: smallest practical board after connector and mounting-hole standard are selected.

Functional blocks:

- One TMF8829 placed at the optical/mechanical reference point.
- Required local capacitors placed as close as possible to their sensor pins.
- One 16-pin 0.5 mm FFC/ZIF connector.
- Two mounting holes outside the field of view/illumination and outside the FFC bend keepout.
- Optional local ID resistor for port presence/board revision detection.
- Optical boot, cover glass, or aperture geometry per the optical design guide.

## Interface Strategy

### Preferred Data Path: SPI

Use SPI for the first electrical design. The recommended PCB1 layout supports either:

- Preferred prototype topology: one SPI peripheral per sensor where MCU pin budget permits. This allows parallel DMA readout and avoids loading a single long shared bus across five FFC cables.
- Fallback topology: one shared SPI bus with separate CS, EN, and INT for each sensor. This reduces MCU pins but increases bus capacitance and makes high-rate readout more serialized.

Each port should have:

- SCLK, MOSI, MISO, and CS.
- EN controlled by the MCU and held low by a local pull-down.
- INT from the sensor to the MCU with a pull-up on PCB1.
- DET/ID line to detect installed sensor boards and optionally encode board revision.

Simultaneous capture should be handled by issuing measurement start commands to all populated sensors in a tight sequence, then collecting data after per-sensor INT. True readout simultaneity depends on using separate SPI peripherals and DMA; one shared SPI bus can still trigger near-simultaneous measurements but reads results sequentially.

### Optional I3C/I2C Path

Carry optional SCL/SDA pins through the FFC for bring-up and future I3C experiments. The TMF8829 datasheet allows multiple I3C devices through address arbitration. I2C multi-device operation needs dedicated EN control and runtime address assignment because sensors reset to the default address when EN is low.

Do not make I2C the primary transport for five 48 x 32 sensors. It is useful for low-rate control or early bring-up, but it is the wrong bottleneck for high-rate multi-sensor data.

### Unused Interface Pin Rules

The TMF8829 datasheet requires unused digital pins not to float. Capture this in the schematic as explicit population options:

- SPI build: use SPI pins normally. Strap the unused I2C/I3C pins according to the datasheet recommendation before disabling I2C/I3C in firmware.
- I3C/I2C build: connect SCL/SDA normally and strap unused SPI pins according to the datasheet recommendation, with CSN held high.

## Recommended FFC Sensor Port

Use a 16-pin, 0.5 mm pitch FFC/ZIF connector family for both PCB1 and PCB2. Sixteen pins keep the cable compact but leave enough conductors for separate grounds, power rails, SPI, optional I3C/debug lines, and board detection.

| Pin | Signal | Direction | Notes |
| --- | --- | --- | --- |
| 1 | GND | - | Ground and return path near rail. |
| 2 | 3V3_TOF | PCB1 to PCB2 | TMF8829 VDD/VDDV/VDDC rail. |
| 3 | 3V3_TOF | PCB1 to PCB2 | Parallel conductor for current and lower drop. |
| 4 | GND | - | Return next to power. |
| 5 | 1V8_TOF | PCB1 to PCB2 | TMF8829 VDDD rail. |
| 6 | GND | - | Return next to 1.8 V rail. |
| 7 | SPI_SCLKx | MCU to sensor | Individual per port preferred. Add optional 22 to 33 ohm source resistor on PCB1. |
| 8 | SPI_MOSIx | MCU to sensor | Individual per port preferred. |
| 9 | SPI_MISOx | Sensor to MCU | Individual per port preferred. |
| 10 | SPI_CSn | MCU to sensor | Per-sensor chip select, default inactive. |
| 11 | I3C_SCLx / AUX1 | Bidirectional | Optional I3C/I2C/debug. DNP or strap as needed in SPI-only builds. |
| 12 | I3C_SDAx / AUX2 | Bidirectional | Optional I3C/I2C/debug. DNP or strap as needed in SPI-only builds. |
| 13 | ENx | MCU to sensor | Per-sensor enable. Pull down on PCB1. |
| 14 | INTx | Sensor to MCU | Open-drain/Hi-Z interrupt. Pull up on PCB1. |
| 15 | DET_IDx | PCB2 to MCU | Presence/revision resistor read by MCU GPIO/ADC. |
| 16 | GND / shield | - | Cable edge return/shield/drain reference. |

FFC design notes:

- Put ground conductors beside rails and at the cable edge.
- Keep SCLK away from INT/DET if connector escape allows.
- Add clearly labeled pin-1 markers on both PCBs.
- Decide and document same-side or opposite-side exposed FFC cable orientation before final footprints.
- Add small test pads for each port on PCB1, at least CS, EN, INT, SCLK, MISO, 3V3, 1V8, and GND.

## PCB1 Layout Plan

Use a 4-layer board for the first revision:

1. Top: components, short high-speed routes, local fanout.
2. Layer 2: uninterrupted ground plane.
3. Layer 3: power pours and slower routing.
4. Bottom: secondary signals, debug/test routing.

Placement guidance:

- USB-C receptacle on an edge with ESD/protection directly behind it.
- Keep USB D+/D- short, length matched, and routed as a 90 ohm differential pair.
- Do not connect the same USB D+/D- lines directly to both STM32 native USB and CP2102N. Choose one of:
  - STM32 USB as primary plus CP2102N available on a separate debug connector.
  - A USB 2.0 switch/mux or 0 ohm population option.
  - A small USB hub, if simultaneous native USB and UART bridge are required.
- Place the STM32 near the center so all five FFC ports can route radially.
- Place five FFC connectors around the perimeter, leaving cable bend clearance.
- Place bucks and inductors away from FFC exits and sensitive sensor signals.
- Keep buck switch loops compact; stitch ground around regulators.
- Put the 1.8 V and 3.3 V rail bulk capacitors near the FFC connector cluster.
- Put SWD, BOOT0, RESET, UART, and rail test pads on a reachable board edge.

Per-port schematic elements:

- EN pull-down so unconfigured sensors stay off.
- CS pull-up or MCU-controlled default inactive state.
- INT pull-up to VIO/3V3.
- Optional SCLK/MOSI source resistors near MCU.
- Optional ESD array or low-capacitance TVS at each FFC if cable exits a mechanically exposed fingertip harness.
- DET/ID pull-up on PCB1 and resistor-to-ground option on PCB2.

## PCB2 Layout Plan

The TMF8829 and optical/mechanical geometry dominate PCB2.

Placement guidance:

- Place TMF8829 first, aligned to the fingertip optical aperture.
- Place VDDC, VDD, VDDV, VDDD, and VIO capacitors immediately adjacent to their sensor pins with direct ground vias.
- Use a solid ground reference under and around the sensor, tied to the center ground pads.
- Keep copper, soldermask openings, mounting hardware, adhesive, connector bodies, and cable bends out of the optical field of view and illumination area.
- Place the FFC connector so the cable exits away from the aperture and does not cross the optical path.
- Put two mounting holes outside optical and FFC keepouts. M1.0 or M1.4 should be evaluated against the robotic fingertip mechanics.
- Keep a board-revision/ID resistor footprint near the connector.

Size expectation:

- The TMF8829 package is small, but the 16-pin FFC connector, mounting holes, and optical aperture will set the real board size.
- A realistic first mechanical target is about 14 mm to 18 mm wide by 10 mm to 14 mm tall, then reduce after the FFC connector and screw size are locked.

## Power Architecture

USB-C VBUS feeds the board through Type-C/PD protection, fuse/current limiting, and local bulk capacitance.

Recommended rails:

- 3V3_TOF_MCU: TPS62826 or TPS62827 class buck, sized for five TMF8829 analog/VCSEL rails plus MCU and margin.
- 1V8_TOF_DIG: TPS62825 or TPS62826 class buck, used for TMF8829 VDDD on all sensors.
- VIO: use 3.3 V for TMF8829 I/O to match STM32 GPIO unless the final MCU pin bank or power strategy requires a lower I/O voltage.

Power budget notes:

- TMF8829 VDD/VDDV/VDDC current can be under 200 mA per active sensor depending on mode.
- TMF8829 VDDD current can be under 100 mA per active sensor.
- Five sensors can therefore approach 1 A on the 3.3 V ToF rail and 0.5 A on the 1.8 V rail before MCU and conversion margin.
- Choose regulators with headroom; do not size the rails only for one or two sensors.
- Add rail test pads and optional current-measure jumpers for 3V3_TOF and 1V8_TOF during bring-up.

## USB-C, Data, and Debug

Primary host data should be native STM32 USB. The ams OSRAM Arduino/EVM driver uses UART for convenience, but it also warns that high zone-count settings can overrun lower serial rates. Five sensors should not depend on a CP2102N UART bridge as the main data pipe.

Recommended USB-C front end:

- USB-C receptacle.
- TCPP01-M12 or equivalent USB-C/PD protection for CC and VBUS sink protection.
- USBLC6-2 or equivalent low-capacitance USB 2.0 ESD protection on D+/D-, placed close to the connector.
- STM32 UCPD peripheral handles Type-C/PD sink negotiation if the final design needs more than default USB current.
- Native STM32 USB FS handles host communications for the first revision.

CP2102N role:

- Use as debug UART only.
- Do not hardwire CP2102N and STM32 native USB to the same D+/D- pair.
- If a single USB-C connector must expose both, add a USB hub, mux, or explicit population option.

## MCU Choice

Baseline choice: STM32H573ZI or a close STM32H573 variant.

Rationale:

- 250 MHz Cortex-M33-class MCU with 2 MB flash and 640 KB SRAM.
- Native USB full-speed and USB Type-C/USB PD controller.
- One I3C, six SPI, multiple I2C and UART peripherals.
- Enough package/pin options to give each sensor its own CS/EN/INT and potentially its own SPI peripheral.
- Good STM32 ecosystem support for CubeMX, USB, DMA, and power/peripheral planning.

Upgrade trigger:

- If the project requires continuous raw histogram streaming from all five sensors at high frame rates, move to an STM32H7-class MCU with USB high-speed and more memory/bandwidth, or add a dedicated high-speed aggregation architecture.

## Firmware Bring-Up Contract

Hardware should support this firmware sequence:

1. Boot MCU with all EN pins low and all CS pins inactive.
2. Read DET/ID pins to identify populated sensor ports.
3. Enable one sensor at a time for first firmware download/configuration.
4. Configure SPI mode and any address or GPIO identity.
5. Start measurements on all populated sensors in a tight sequence.
6. Wait for INT or poll status per populated port.
7. Read each sensor FIFO over SPI, preferably using DMA.
8. Expose synchronized packets over native USB with sensor ID, timestamp, mode, zone count, confidence, signal, and ambient values.

## First KiCad Tasks

- Create symbols/footprints for TMF8829, the selected STM32H573 package, USB-C receptacle, TCPP01-M12, USBLC6-2, CP2102N, buck regulators, and 16-pin FFC connector.
- Capture one reusable sensor-port schematic sheet and instantiate it five times.
- Capture one reusable TMF8829 sensor-board sheet for PCB2.
- Generate a CubeMX pin plan before finalizing MCU package pinout.
- Lock FFC orientation and pin-1 convention before routing PCB1/PCB2.
- Import the TMF8829 optical STEP and shield-board references for mechanical keepouts.

## Source References

- TMF8829 product page: https://ams-osram.com/products/sensor-solutions/direct-time-of-flight-sensors-dtof/ams-tmf8829-48x32-multi-zone-time-of-flight-sensor
- TMF8829 datasheet, local copy: [references/TMF8829-Time-of-flight-sensor.pdf](references/TMF8829-Time-of-flight-sensor.pdf)
- TMF8829 optical design guide ZIP, local copy: [references/TMF8829_Optical_Design_Guide_AD001029_1-00.zip](references/TMF8829_Optical_Design_Guide_AD001029_1-00.zip)
- Extracted optical guide folder: [references/TMF8829_Optical_Design_Guide](references/TMF8829_Optical_Design_Guide)
- Host driver communication note, local copy: [references/TMF8829-Host-driver-communication.pdf](references/TMF8829-Host-driver-communication.pdf)
- EVM user guide, local copy: [references/TMF8829-EVM-UG001071-2-00.pdf](references/TMF8829-EVM-UG001071-2-00.pdf)
- Shield board schematic/layout reference, local copy: [references/TMF8829_Shield_Board_Schematic_Layout_AD001028_1-00.pdf](references/TMF8829_Shield_Board_Schematic_Layout_AD001028_1-00.pdf)
- STM32H573ZI product page: https://www.st.com/en/microcontrollers-microprocessors/stm32h573zi.html
- TCPP01-M12 datasheet: https://www.st.com/resource/en/datasheet/tcpp01-m12.pdf
- USBLC6-2 datasheet: https://www.st.com/resource/en/datasheet/usblc6-2.pdf
- CP2102N datasheet: https://www.silabs.com/documents/public/data-sheets/cp2102n-datasheet.pdf
- TPS62825/TPS62826/TPS62827 datasheet: https://www.ti.com/lit/ds/symlink/tps62825.pdf
- TMF8829 Arduino driver repository: https://github.com/ams-OSRAM/tmf8829_driver_arduino
- Hirose FH12 FPC/FFC connector family: https://www.hirose.com/en/product/series/FH12
