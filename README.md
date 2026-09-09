## Pujitha Bomidi

VLSI and digital design engineer — Chicago, IL

M.A.S. Electrical & Computer Engineering, Illinois Institute of Technology (2026).
RTL design and verification through synthesis, place-and-route, timing closure, and
transistor-level characterization. I like problems where the answer is a measured
number, not an opinion.

---

### Worked so far

<details>
<summary><b>32-bit pipelined CPU — I chose the adder by measuring, not by reputation</b></summary>

<br>

Textbooks tell you carry-lookahead beats ripple-carry. That's true in the abstract and
useless for a specific critical path in a specific library.

So I scripted Design Compiler in Tcl and swept **ripple-carry, carry-lookahead,
carry-skip, and carry-select** datapaths, then picked the winner from gate-level
results rather than from the textbook.

I also replaced the ALU's comparator with a **6-level structural 32-bit tree**, which
lifted post-place-and-route Fmax from **147.84 MHz to 152.5 MHz** — clearing the
30 MHz constraint by 5x.

The part I'm most pleased with isn't the frequency. It's that I carried the block
through SimVision → Design Compiler → Innovus → Formality → Virtuoso and proved
**zero functional mismatches at every handoff**. RTL and layout described the same
machine.

`Verilog` · `Design Compiler` · `Innovus` · `Formality` · `Virtuoso`

</details>

<details>
<summary><b>16-bit ALU power optimization — 16.6% saved, and I know which technique paid for itself</b></summary>

<br>

Applied six RT-level low-power techniques to a 16-bit ALU in a 45nm library: clock
gating, operand isolation, LECG, precomputation, guarded evaluation, and FSM
re-encoding. Dynamic power fell **281.16 µW → 234.47 µW (16.6%)**.

The interesting question wasn't the total. It was *which techniques earned their area
cost* — several didn't, and isolating that required measuring them independently.

I also refused to trust the tool's default estimates. Synthesis power numbers assume a
switching activity that may have nothing to do with your workload. Instead I drove
random and corner-case vectors, captured **VCD traces in ModelSim**, and
back-annotated real activity into Design Compiler. The savings are defensible because
they came from actual toggling, not an assumed 0.5 activity factor.

`Verilog` · `Design Compiler` · `ModelSim` · `VCD back-annotation`

</details>

<details>
<summary><b>FinFET dual-Vt domino logic and 6T vs 8T SRAM — six orders of magnitude</b></summary>

<br>

On ASAP7 7nm FinFET, I assigned RVT to the keeper, precharge and foot devices of an
8-input domino AND gate while holding LVT in the evaluation stack. **Average leakage
dropped 11%**, trading 3.5 ps of fall delay for 7.7 ps of rise delay — the kind of
asymmetric trade you only see by measuring both edges.

Separately, I quantified the 6T vs 8T SRAM read trade-off at VDD 0.7 V from HSPICE
`.mt0` measurements. The isolated 8T read path cut read dynamic power by **six orders
of magnitude at identical 6.78 ns delay**. That result surprised me enough that I went
back and checked the measurement setup twice.

`Virtuoso` · `HSPICE` · `ASAP7 7nm PDK`

</details>

<details>
<summary><b>FPGA CNN acceleration — quantization sweep on PYNQ-Z2</b></summary>

<br>

Swept weight-only quantization across INT8/INT16/INT32 on a custom VGGTiny, improving
inference score from 1.0029 to 1.0391 and cutting per-image latency from **0.883 ms to
0.852 ms** while holding **88.5% CIFAR-10 accuracy**.

Fitting a 3x3 convolution and batch-norm kernel inside PYNQ-Z2's on-chip memory meant
tiling the convolution, pipelining across four DATAFLOW stages, partitioning arrays
channel-wise, and exposing AXI4 interfaces.

Correctness gated deployment: fixed-point kernel output was scored by mean squared
error against the golden PyTorch reference in a **C/RTL co-simulation** testbench. No
deployment without a passing comparison.

`Vitis HLS` · `PYNQ-Z2` · `AXI4` · `PyTorch`

</details>

<details>
<summary><b>Currently: 100 Days of RTL, in open-source EDA</b></summary>

<br>

Most of my flow experience is on commercial tools — Design Compiler, Innovus,
Formality. **[100 Days of RTL](https://github.com/Puji7tha/100DaysOfRTL)** is me
rebuilding that flow entirely in open source: Yosys, OpenSTA, OpenROAD, Icarus,
GTKWave.

One design a day, each taken RTL → simulation → verification → synthesis → timing.

Day 1 was an 8-bit ALU, where a single `/` operator turned out to be **43% of the
combinational area** and set the critical path for all sixteen operations — capping
Fmax at 110 MHz on Nangate45. Division resists parallelisation in a way multiplication
doesn't: each compare-and-subtract stage waits on the previous stage's remainder.

`Yosys` · `OpenSTA` · `OpenROAD` · `Icarus Verilog` · `GTKWave` · `Nangate45` · `Sky130`

</details>

---

### Toolchain

| | |
|---|---|
| **Languages** | Verilog · SystemVerilog · Tcl · Python · C/C++ · Bash |
| **Synthesis & PnR** | Design Compiler · Innovus · Yosys · OpenROAD |
| **Verification** | ModelSim · SimVision · Icarus · Formality · GTKWave |
| **Circuit & Layout** | Virtuoso · HSPICE · ASAP7 · Nangate45 · Sky130 |
| **FPGA & Embedded** | Vivado · Vitis HLS · PYNQ-Z2 · AXI4 · I2C · SPI · AVR |

---

### How I work

**Measure, don't assume.** The adder choice, the power savings, the leakage
trade — every one of those numbers came from a tool run I set up rather than a
rule of thumb I inherited.

**Prove equivalence at every handoff.** A design that changes meaning between RTL
and layout is a bug you find at bring-up, which is the worst possible time.

**Predict before running.** I guessed multiplication would dominate that ALU's area.
It was division, by nearly 3x. Writing down the wrong guess is more useful than
recording only the right answer.

---

### Get in touch

Happy to talk about RTL, timing closure, low-power design, or open-source EDA —
especially if you've spotted an error in something here.

📧 [pujithabomidi@gmail.com](mailto:pujithabomidi@gmail.com) · 
💼 [LinkedIn](www.linkedin.com/in/pujithabomidi) · 
📍 Chicago, IL
