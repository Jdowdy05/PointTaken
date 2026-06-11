# Component Research

This file records the current component choices and why they fit the five-sensor TMF8829 controller architecture.

## Recommended Parts

| Function | Recommended Part or Family | Reason |
| --- | --- | --- |
| Multi-zone dToF sensor | ams OSRAM TMF8829-1A or TMF8829-1AM | 48 x 32 zones, integrated dual VCSELs, 80 deg diagonal FOV, 5.7 mm x 2.9 mm x 1.5 mm module, SPI/I3C/I2C-compatible interfaces. |
| MCU | STM32H573ZI or close STM32H573 package | 250 MHz Cortex-M33, 2 MB flash, 640 KB SRAM, native USB FS, USB-C/PD controller, one I3C, six SPI, enough pins for five sensor ports. |
| USB-C/PD protection | ST TCPP01-M12 | Protects CC and VBUS for USB-C sink/PD designs and pairs naturally with STM32 UCPD. |
| USB 2.0 ESD | ST USBLC6-2SC6 or package variant | Low-capacitance D+/D- ESD protection for USB 2.0 lines. Place close to the USB-C connector. |
| Debug UART bridge | Silicon Labs CP2102N | Compact USB-to-UART bridge with built-in oscillator and broad VCP driver support. Use for debug only, not primary five-sensor data. |
| 3.3 V buck | TI TPS62826 or TPS62827 family | High-efficiency 3 A/4 A-class buck option with small package and enough headroom for five ToF sensors plus MCU overhead. |
| 1.8 V buck | TI TPS62825 or TPS62826 family | 2 A/3 A-class buck option for TMF8829 VDDD across five sensors with margin. |
| FFC connector | 16-position, 0.5 mm pitch ZIF FFC/FPC, candidate family Hirose FH12 | Available as 16-position, 0.5 mm pitch ZIF FPC/FFC family with 0.5 A/contact rating. Final exact part depends on cable exit direction and board-side contact orientation. |
| TMF8829 decoupling | Murata GRM series values from TMF8829 datasheet | Datasheet lists 1 uF capacitors for VDD/VDDV/VDDC/VDDD and 2.2 uF for VIO. |

## MCU Notes

The STM32H573ZI is a strong baseline because the five-sensor architecture benefits from both peripheral count and SRAM:

- Six SPI peripherals let the design avoid a single heavily loaded shared SPI cable bus if pin budget permits.
- I3C support is available for future experiments or alternate sensor topologies.
- Native USB FS is better suited than a debug UART bridge for live multi-sensor output.
- The integrated UCPD controller simplifies USB-C sink/PD designs when combined with Type-C protection.

Use CubeMX early to lock these decisions:

- Exact STM32H573 package and ball/pin map.
- Five SPI instances versus one shared SPI instance.
- DMA channels for SPI reads.
- USB FS pins and UCPD CC pins.
- SWD, BOOT0, reset, UART, and timing/debug pins.

## Sensor Interface Notes

SPI is the preferred first-spin interface. The TMF8829 can be used on I3C/I2C-compatible buses, and the datasheet describes multi-device I3C and I2C arrangements, but five sensors at high zone counts are more naturally handled over SPI.

I2C should be treated as a fallback or bring-up interface only. Multiple I2C sensors require dedicated EN handling and address reassignment after boot. The TMF8829 datasheet also recommends I3C or SPI for histogram readout because I2C is data-rate limited.

## USB Notes

The board should expose native STM32 USB as the main data path. CP2102N belongs in the design as a debug convenience:

- Good for logs, bootloader/debug UART, manufacturing bring-up, and simple command shells.
- Not good as the primary continuous data path for five 48 x 32 sensors.
- Must not be connected in parallel with STM32 native USB on the same D+/D- pair unless a mux, hub, or population option is added.

## Power Notes

Power sizing should assume all five sensors may be active:

- Five TMF8829 sensors can approach 1 A demand on the 3.3 V sensor rail depending on operating mode.
- Five TMF8829 sensors can approach 0.5 A demand on the 1.8 V digital rail.
- MCU, USB, regulator losses, and margin require sizing above these raw sensor estimates.

Recommended rail structure:

- USB-C VBUS input with Type-C/PD protection and bulk capacitance.
- 3.3 V buck for MCU I/O and TMF8829 VDD/VDDV/VDDC.
- 1.8 V buck for TMF8829 VDDD.
- Optional per-port measurement jumpers or current sense footprints for bring-up.

## FFC Connector Notes

Sixteen pins are recommended because they keep the sensor board compact while carrying enough independent conductors:

- Multiple grounds.
- Two 3.3 V pins.
- One 1.8 V pin.
- SPI SCLK/MOSI/MISO/CS.
- Optional I3C/I2C/debug pair.
- EN.
- INT.
- DET/ID.

During footprint selection, decide:

- Top-contact versus bottom-contact connector.
- Same-side versus opposite-side FFC cable ends.
- Horizontal versus vertical cable exit.
- Locking style and actuator accessibility after the sensor board is installed in the fingertip.
- Cable length and bend radius for the robotic hand routing.

## Parts To Revisit Before Ordering

- Final STM32H573 package and availability.
- Exact USB-C receptacle footprint.
- Exact FFC connector and cable orientation.
- Per-port ESD/load switch/current sense strategy.
- Whether USB FS bandwidth is enough for the final firmware data format.
- Mechanical aperture, cover glass, boot, and screw size for PCB2.

## Sources

- TMF8829 product page: https://ams-osram.com/products/sensor-solutions/direct-time-of-flight-sensors-dtof/ams-tmf8829-48x32-multi-zone-time-of-flight-sensor
- TMF8829 datasheet: https://look.ams-osram.com/m/4215c1ea1a30e283/original/TMF8829-Time-of-flight-sensor.pdf
- STM32H573ZI product page: https://www.st.com/en/microcontrollers-microprocessors/stm32h573zi.html
- TCPP01-M12 datasheet: https://www.st.com/resource/en/datasheet/tcpp01-m12.pdf
- USBLC6-2 datasheet: https://www.st.com/resource/en/datasheet/usblc6-2.pdf
- CP2102N datasheet: https://www.silabs.com/documents/public/data-sheets/cp2102n-datasheet.pdf
- TPS62825/TPS62826/TPS62827 datasheet: https://www.ti.com/lit/ds/symlink/tps62825.pdf
- Hirose FH12 connector family: https://www.hirose.com/en/product/series/FH12
