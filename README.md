## Hi there 👋

## Pujitha

Digital design and verification, working entirely in open-source EDA.

**Currently:** [100 Days of RTL](https://github.com/Puji7tha/100DaysOfRTL) — one design a day,
each taken from RTL through simulation, verification, synthesis, and static timing analysis.
Not just "does it simulate" — what does it cost in gates, in area, in nanoseconds?

**Toolchain:** Verilog · Icarus · GTKWave · Yosys · OpenSTA · OpenROAD · Nangate45 / Sky130

**Recent finding:** in an 8-bit ALU, a single `/` operator consumed 43% of the
combinational area and set the critical path for all sixteen operations —
capping Fmax at 110 MHz where the rest of the design could have run far faster.
