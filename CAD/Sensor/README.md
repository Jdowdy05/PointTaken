# Standalone fingertip sensor

Envelope: **24.2 ×44.5 ×33.8 mm** (width ×height ×depth, including rear locating posts).

| Path | Use |
| --- | --- |
| `sensor_assembly.step` | Complete 54-solid sensor assembly, including PCB and hardware references. |
| `parts/` | Five rigid-part STEP files. |
| `print/` | Matching STL files for the main housing, back housing, one-piece retainer, optical cassette and window clamp. |
| `compliant_surface/` | Black outer cap and white inner target STEP/STL geometry for silicone casting. |
| `reference/` | PCB, optical boot and window reference solids/meshes. |
| `images/` | Actual CAD renders, including six assembled views and an exploded assembly. |
| `manifest.json` | Dimensions, file hashes, export checks and standalone rear-fastener contact checks. |

The cap and retainer remove together after the three M2 ×6 front screws are removed. Separating the silicone from the one-piece ring requires flexing the flange and must be tried on a sacrificial cap. The corrected rear nuts load from the sides and bear on main-housing shoulders; the standalone rear screws are M2 ×8.

Coordinates are X across the sensor, Y toward the arched tip and Z toward the contact surface. All dimensions are millimetres. Orient parts deliberately in the slicer. Candidate rigid material is FDM PETG; printer tolerances, nut fit and allowable tightening torque need physical verification.

These are editable STEP solids and STL exports. The CAD construction feature history is not included. [Assembly](../../docs/Assembly.md) and [material guidance](../../docs/Materials.md) apply to this revision.
