# References and component geometry

- [ams OSRAM TMF8829 product and datasheets](https://ams-osram.com/products/sensor-solutions/direct-time-of-flight-sensors-dtof/ams-tmf8829-48x32-multi-zone-time-of-flight-sensor): sensor capabilities, electrical interface and optical guidance. Existing reference PDFs and optical models are retained under `references/`.
- [Smooth-On Ecoflex 00-30](https://www.smooth-on.com/products/ecoflex-00-30/): current prototype silicone candidate and preparation/cure instructions.
- [Smooth-On Dragon Skin 10 NV technical bulletin](https://www.smooth-on.com/tb/files/DRAGON_SKIN_10_NV_TB.pdf): earlier outer-layer material candidate.
- [Stretchable silicone reflective coating study](https://doi.org/10.1039/D2SM00869F): supporting material research; its formulation does not qualify the current sensor.
- [JST NSHD series](https://www.jst-mfg.com/product/pdf/eng/eNSHD.pdf): board header, cable housing, contacts and recommended footprint.
- [KiCad libraries](https://www.kicad.org/libraries/): standard symbols, footprints and 3D models used by the PCB projects.

Files named `*_proxy.step` are project component-envelope approximations. The PCB/CAD assembly also includes optical reference geometry; use manufacturer drawings for exact dimensions, optical tolerances and mating requirements. No model color establishes a material's infrared properties.

Manufacturer documents and reference geometry retain their original ownership and terms. KiCad-derived library content remains subject to its upstream terms. This repository does not declare a blanket license over third-party reference material, and no new project-wide license is assigned by this update.
