# Compliant surface material

## Current prototype candidate

Use **Ecoflex 00-30 platinum-cure silicone** as the starting base material for the current cap study. It is a candidate formulation, not a demonstrated route to the required force sensitivity. The [manufacturer product page and technical bulletin](https://www.smooth-on.com/products/ecoflex-00-30/) govern its 1A:1B mixing and curing instructions.

| Layer | Nominal normal thickness | Purpose |
| --- | ---: | --- |
| Black outer silicone | 0.90 mm | Contact skin and ambient-light suppression. |
| White TiO₂-filled inner silicone | 0.30 mm | Flexible diffuse reflective target facing the 940 nm sensor. |
| Total skin | 1.20 mm | Bonded bilayer; the inner target deforms with the outside. |

Use silicone-compatible black pigment and a dispersed white titanium-dioxide additive suitable for the selected silicone process. There is no approved additive mass fraction for this final geometry. Additives can change cure, stiffness and optical response, so do not infer performance from color or unfilled-silicone hardness alone.

The intended process is a two-stage cast with reliable interlayer bonding. Preserve the designed flange and bead: the ring mechanically captures those features. The geometry files do not constitute a qualified mold, gate/vent layout or casting process.

## Earlier material study

The original material study proposed Dragon Skin 10 NV outside and Ecoflex 00-10 with micrometric rutile TiO₂ inside. A 1.0 vol% TiO₂ coating was a research starting point, not a validated recipe for Ecoflex 00-30 or this cap. The current cap source identifies Ecoflex 00-30 as a later candidate; physical testing has not resolved the formulation choice. These alternatives should not be treated as interchangeable qualified materials.

## Qualification required

- Cure compatibility, consistent wall thickness and two-layer adhesion.
- Infrared opacity of the black skin at its actual thickness; original target was optical density ≥3 at 940 nm (≤0.1% direct transmission).
- Adequate diffuse return from the inner target without saturation or large baseline drift; original target was 70–90% diffuse/hemispherical return at 940 nm.
- Required 0.5 N contact detection and low-force target displacement after calibration of the actual article.
- Flange insertion/removal without tearing, skin abrasion, creep, fatigue and overload behavior.

The one-piece ring requires the silicone flange to flex during cap replacement. That service operation is not a proven strain or life result.

The compliant-surface STLs are casting references. FDM printing a TPU version changes the mechanics and would require a separate sensitivity evaluation. FDM-printed tooling, if developed, would need surface finishing, dimensional checks and a silicone cure-compatibility trial.
