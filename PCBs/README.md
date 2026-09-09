# PCB projects

Open the `.kicad_pro` file in the appropriate folder with KiCad 10 and its standard symbol, footprint and 3D model libraries.

| Project | Nominal board size | Layers | Purpose and state |
| --- | --- | ---: | --- |
| [PCB1_Controller](PCB1_Controller/) | 50 ×50 mm | 6 | Five-sensor STM32H573 controller. Placement present; zero tracks/vias. Unrouted and on manufacturing hold. |
| [PCB1_Single_Sensor_Validation_Rig](PCB1_Single_Sensor_Validation_Rig/) | 50 ×40 mm | 6 | STM32H562 single-sensor bring-up controller. Routed prototype. |
| [PCB2_Fingertip_Sensor](PCB2_Fingertip_Sensor/) | 10 ×15 mm | 4 | TMF8829 fingertip module. Routed prototype. |

`JustTheTip_Connectors.pretty/` and `3dmodels/` are shared by the three projects. Keep the folder relationships intact. Custom symbols and other custom footprints are stored beside their owning projects. Library tables use `${KIPRJMOD}`, `${KICAD10_SYMBOL_DIR}` and `${KICAD10_FOOTPRINT_DIR}`; stock component models use `${KICAD10_3DMODEL_DIR}`.

Schematic and board files retain the electrical design contents. Publication changes library paths and organization, not electrical routing. Four nonexistent PCB1 stock-model references now point to the included exact-part envelope proxies for TCPP01-M12, ESDA25P35-1U1M, TPS259531 and CSD17577Q5A. Native board loading and schematic/board SVG exports were checked; `manifest.json` records file hashes and board statistics. These publication checks are not a fresh ERC/DRC, EMC or manufacturing review.

Each project has `previews/top.svg`, `previews/bottom.svg` and schematic pages in `previews/schematics/`. Bottom previews use the board's unmirrored coordinate convention. Copper plots are for inspection, not fabrication files. Generate fabrication outputs from the selected source revision after reviewing its rules, stackup, DRC/ERC and manufacturing requirements.

The hierarchical filename `Sensor_FFC_Ports.kicad_sch` in PCB1 is historical: its actual connector interface is JST NSHD discrete wire. See the [16-wire interface](../docs/Harness.md).

The custom 3D models named `*_proxy.step` are envelope approximations for packaging; manufacturer drawings govern exact component and mating dimensions.
