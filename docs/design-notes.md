# Design Notes

## 1. Project Goal

The goal of this project is to design a simple 12 V PWM controller for
DC loads using an NE555 timer and a discrete N-channel MOSFET power stage.

The design is intended as a practical introductory PCB project focused on:

- schematic design
- component selection
- PCB layout
- power routing
- grounding
- design rule verification
- manufacturing output generation

The controller is intended for resistive and inductive 12 V loads such as
small DC motors, solenoids, lamps, and heaters.


## 2. Electrical Architecture

The design consists of three main functional blocks:

1. 12 V input and local decoupling
2. NE555 adjustable PWM generator
3. N-channel MOSFET low-side power switch

The external load is connected between +12 V and the switched LOAD_SW node.


## 3. PWM Generator

The PWM generator is based on the NE555 timer.

Two 1N4148W switching diodes separate the capacitor charge and discharge
paths, allowing the duty cycle to be adjusted using a 50 kOhm linear
potentiometer.

The timing capacitor is:

- 1 nF
- C0G dielectric
- ±1 %

C0G was selected because the timing capacitor directly affects the switching
frequency and benefits from low temperature drift and good capacitance
stability.

The target PWM frequency is approximately 25 kHz.

This places the switching frequency above the normal audible range while
remaining easily achievable with the NE555 and the selected MOSFET.


## 4. Power MOSFET

The output stage uses the Infineon IPD053N06N N-channel MOSFET.

Main parameters:

- VDS: 60 V
- RDS(on): approximately 5.3 mOhm at VGS = 10 V
- DPAK / TO-252 package

The NE555 operates from the 12 V supply, therefore its output provides
sufficient gate voltage for the MOSFET to fully enhance.

A 47 Ohm series gate resistor is used to limit peak gate current and reduce
ringing.

A 100 kOhm gate-to-source resistor ensures that the MOSFET remains off when
the gate is not actively driven.

The gate resistor is placed close to the MOSFET gate.


## 5. Flyback Protection

A Vishay SSA34HE3 Schottky diode is connected across the load output.

The diode provides a freewheel current path when switching inductive loads.

Main parameters:

- 3 A forward current
- 40 V repetitive reverse voltage
- approximately 0.49 V forward voltage
- SMA package

The diode is placed close to the output connector and MOSFET to minimize the
high-current switching loop.


## 6. Decoupling

The design includes:

- 100 uF bulk input capacitor
- 100 nF ceramic decoupling capacitor near the NE555 supply pins
- 10 nF capacitor on the NE555 control-voltage pin

The 100 nF capacitor is placed close to the NE555 and connected to the ground
plane through a short local return path.


## 7. PCB Stackup

The PCB is designed as a standard 2-layer board.

- Material: FR-4
- Board thickness: approximately 1.6 mm
- Copper thickness: 1 oz
- Top layer: components, signals and power routing
- Bottom layer: nearly continuous ground plane

The bottom ground plane is kept as continuous as possible to provide short
return-current paths.


## 8. Grounding Strategy

The design uses a single common ground plane.

Separate analog and power ground planes were not used because the circuit is
simple and does not require split-ground architecture.

Low-current ground connections are routed locally to the bottom ground plane
using vias.

The MOSFET source uses a wide local copper area and multiple vias to connect
to the bottom ground plane and reduce resistance and inductance in the load
current return path.

The MOSFET gate pull-down resistor returns locally to the MOSFET source.


## 9. PCB Design Rules

The PCB uses conservative manufacturing rules.

Main values:

- Minimum track width: 10 mil
- Minimum clearance: 10 mil
- Silk-to-solder-mask clearance: 6 mil
- Standard via: approximately 28 mil / 12 mil drill

These values are intentionally larger than the minimum capabilities of most
modern PCB manufacturers.


## 10. Manufacturing Outputs

The Altium OutJob generates:

- Gerber X2 files
- NC Drill files
- Bill of Materials
- Pick and Place data

Manufacturing files are available in:

[`../manufacturing/`](../manufacturing/)


## 11. Design Verification

Final PCB Design Rule Check:

- 0 warnings
- 0 rule violations
- 0 unrouted nets

The schematic was also checked using Altium schematic validation/ERC.



