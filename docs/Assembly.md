# Sensor assembly

## Rigid parts and hardware

Print one each of the five parts in `CAD/Sensor/print/`: main housing, back housing, one-piece cap retainer, optical cassette and window clamp. The silicone cap/inner target, PCB, optical boot, window and metal fasteners are not rigid print jobs.

| Fastener | Quantity | Purpose |
| --- | ---: | --- |
| M1.6 ×8 socket-head screw | 4 | Optical core retention |
| M1.6 hex nut | 4 | Optical core retention |
| M2 ×6 socket-head screw | 3 | Front cap-retainer ring |
| M2 hex nut | 3 | Front retainer seats |
| M2 ×8 socket-head screw | 2 | Standalone back housing |
| M2 hex nut | 2 | Corrected side-loading rear seats |

Screw lengths are measured under the head. The modeled M2 nuts are 4.0 mm across flats and 1.6 mm thick. Check the actual hardware and printed pockets before assembly; there is no qualified tightening torque.

## Sequence

1. Inspect and finish the print surfaces and holes. Check each nut pocket and screw bore off the assembly. Ensure the rear nuts seat and resist spinning.
2. Assemble the PCB, cassette, optical boot and window/clamp with their four M1.6 fasteners. Keep the optical window clean, the transmit/receive isolation intact and the harness clear of hardware.
3. Fit the front retainer nuts into the housing before closing the front. Gently flex the cast cap's flange into the one-piece ring off the housing, checking the skins and flange for damage. This operation needs a physical trial on a sacrificial cap.
4. Seat the cap/ring cartridge on the housing and install the three M2 ×6 screws: one at the arched tip and two at the heel. The screws bear on rigid mounting faces; they do not pierce the silicone.
5. Insert the two rear M2 nuts through the outer left/right slots near the body's flat heel. These slots leave **4 mm housing shoulders between the nuts and the backplate**. Hold the nuts in their seats until engaged by the screws.
6. Seat the back housing and install the two **M2 ×8** rear screws. Tighten evenly. The load path is screw head → back housing → main-housing shoulder → nut.
7. Check cable strain relief and printed fit before powering the PCB. The existing strain-relief allocation is 4 mm; a thinner harness needs appropriate packing or a separately checked restraint. Calibrate the cast cap before interpreting deformation as force.

For front service, remove all three front screws and withdraw the **ring and soft cap together** from the sensing face. Their combined extraction path clears the rigid assembly in CAD. Do not force the ring alone past the undeformed flange. To replace only the silicone, detach the cartridge first, then gently fold/peel its flange out of the ring.

The current prototype has geometric fit and retention checks. Material strength, printed tolerances, flange tear resistance, repeated service, optical sensitivity and overload survival remain unqualified.
