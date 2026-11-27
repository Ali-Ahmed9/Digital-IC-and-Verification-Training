# Lab 06 — PLL Instantiation in a Verilog Design
======================================================

## Project

**16-bit Counter — Clock Divider to SMIC40 PLL**

======================================================

## Overview

This lab explores replacing a behavioral Verilog clock divider with an instantiated SMIC40 PLL hard macro in a 16-bit counter design.

======================================================

## Objectives

1. Build a 16-bit counter clocked by a Verilog-based clock divider.
2. Replace the behavioral clock divider with an instantiated SMIC40 PLL hard macro.
3. Calculate PLL configuration values:
   - M — Feedback Divider
   - N — Reference Divider
   - OD — Output Divider
4. Simulate both divider-based and PLL-based designs.
5. Verify functional equivalence.
6. Synthesize the PLL-based design using Cadence Genus.
7. Write SDC constraints for the reference and PLL-generated clocks.
8. Perform gate-level verification of the synthesized netlist using `irun`.

======================================================

## Task 3 — Synthesis in Genus with Clock Constraints

The key concept is distinguishing the primary reference clock from the generated PLL output clock.

## Primary Clock — REFCLK

Use `create_clock` to define the reference clock supplied by the board or testbench.

### Generated Clock — CLKOUT

Use `create_generated_clock` to define the PLL output clock, referencing REFCLK as its source and specifying the PLL multiplication/division relationship.

This allows the timing tools to understand the relationship between the reference clock and the generated PLL clock.

======================================================

## Synthesis and Verification Flow

1. Prepare the PLL-based Verilog design.
2. Configure the PLL parameters M, N, and OD.
3. Write the SDC timing constraints.
4. Define REFCLK using `create_clock`.
5. Define CLKOUT using `create_generated_clock`.
6. Synthesize the design using Cadence Genus.
7. Inspect synthesis and QoS reports.
8. Run gate-level simulation using `irun`.
9. Inspect the generated waveforms.

======================================================

[Lab 6Sol.pdf](https://github.com/user-attachments/files/35525383/Lab.6Sol.pdf)
