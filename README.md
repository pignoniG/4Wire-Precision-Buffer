# 4-Wire Precision Buffer

A bipolar, two-channel precision buffer with 4-wire (force/sense) outputs, designed in KiCad 9. I built it to buffer a DC voltage reference (an ADR1399 module) without loading it, and to add remote sense to sources that don't have it, such as the HP 3245A.

## View the design

Open the files in the browser with [KiCanvas](https://kicanvas.org), no KiCad needed:

- [Schematic](https://kicanvas.org/?github=https://github.com/pignoniG/4Wire-Precision-Buffer/blob/main/kicad/4wPrecisionBuffer.kicad_sch)
- [PCB layout](https://kicanvas.org/?github=https://github.com/pignoniG/4Wire-Precision-Buffer/blob/main/kicad/4wPrecisionBuffer.kicad_pcb)

## How it works

Each channel is a composite amplifier:

- an **ADA4523** chopper op amp sets the DC accuracy;
- a **BUF634A** inside its loop supplies the output current;
- at DC, feedback comes from the **sense** terminal, so lead resistance doesn't matter. At higher frequencies, feedback comes from the BUF634A output through a capacitor, for stability;
- a small resistor isolates the BUF634A from the force terminal, and 200 kΩ from force to sense keeps the output defined if the sense leads are open;
- an RC filter protects each input.

One channel follows the HI input and the other the LO input, so the input floats with respect to the ±15 V supply.

The layout is aimed at keeping thermoelectric EMF and leakage low:

- identical, translated channels;
- high-impedance nodes on the top layer with no vias;
- slots and a split ground pour between the warm parts and the inputs;
- bare-copper (OSP) pads for copper ring lugs.

## Repository

- `kicad/`: KiCad project (schematic and PCB).
- `fabrication/gerbers/`: Gerber and drill files for the v6 board.

## Status

The v6 board is built and working. The PCB file carries the current component values; some values in the schematic are older. Characterisation (offset, noise, load regulation, stability) is in progress.

## Licence

MIT, see [LICENSE](LICENSE).
