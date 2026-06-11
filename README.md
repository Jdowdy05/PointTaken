# JustTheTip

Documentation and design research for a two-board fingertip time-of-flight sensor system for a robotic hand.

The current hardware concept uses five optional TMF8829 48x32 multi-zone dToF sensor boards connected by FFC cables to a 50 mm x 50 mm controller board. The controller board owns USB-C power/data, an STM32 MCU, debug serial, power conversion, and five identical sensor ports. Each fingertip board is kept as small as practical and carries one TMF8829, local decoupling, a compact FFC connector, and two mounting holes.

## Documentation

- Main PCB layout context: [docs/PCB_Design_Layout.md](docs/PCB_Design_Layout.md)
- Component research: [docs/Component_Research.md](docs/Component_Research.md)
- Project context: [docs/Project_Context.md](docs/Project_Context.md)
- Reference index: [docs/Reference_Index.md](docs/Reference_Index.md)
- Obsidian vault: [docs/obsidian-vault](docs/obsidian-vault)
- Downloaded reference PDFs and 3D files: [docs/references](docs/references)

## Current Design Direction

- Use SPI as the primary sensor data path for five TMF8829 modules.
- Use STM32H573ZI or a close STM32H573 variant as the baseline MCU.
- Use native STM32 USB for the main host data link.
- Keep CP2102N as a debug UART bridge option, not the primary data path.
- Use a 16-pin 0.5 mm FFC/ZIF sensor-port pinout so each sensor board has power, grounds, SPI, enable, interrupt, optional I3C/debug pins, and a detect/ID line.

See [docs/PCB_Design_Layout.md](docs/PCB_Design_Layout.md) before starting schematic capture.
