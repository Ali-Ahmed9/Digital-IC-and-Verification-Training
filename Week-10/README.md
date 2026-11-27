## Week 10 — Advanced Clock Constraints, UART Synthesis, SRAM & PLL Integration
======================================================

## Overview

Week 10 of my **Digital IC Design and Verification Training** focused on advanced clock constraints, 
clock modeling, timing path analysis, UART synthesis, SRAM memory replacement, and PLL integration in Verilog-based designs.

The lectures covered clock definitions, clock latency, skew, uncertainty, generated clocks, clock gating, and advanced timing constraints. Practical activities explored UART synthesis and debugging, single-port and double-port SRAM replacement, and PLL instantiation in a 16-bit counter design.

======================================================

## Topics Covered

======================================================

## 1. Clock Definition and Timing Constraints

- Clock definition and clock specification syntax
- Clock transition time
- Clock uncertainty and inter-clock uncertainty
- Clock latency and skew between signals
- Clock characterization
- Types of clock latency
- Post-clock-tree synthesis scenarios

======================================================

## 2. Generated Clock Analysis

- Generated clock definition
- Generated clock versus master clock
- Clock origin and clock relationships
- Generated clock frequency relationships
- Clock latency for generated clocks
- Clock source and network latency
- Clock gating scenarios
- Multiple clocks at mux inputs

======================================================

## 3. Advanced Timing Constraints

- Advanced clock constraints
- `set_clock_transition`
- `set_propagated_clock`
- Timing path groups
- `group_path`
- Timing path analysis
- `set_false_path`
- `set_multicycle_path`
- Pre-layout timing analysis
- Timing libraries and design constraints
- Maximum capacitance constraints
- SDC script development and application
======================================================

## Lab Work

======================================================

## Lab 04 — UART Synthesis and Debug

**Aim:** To synthesize UART Verilog HDL code using Cadence tools, generate a netlist, and define clock constraints.

**Objectives:**
- Understand the working principle of UART communication.
- Test and verify serial communication using Cadence Incisive.
- Generate the `synthesis_script.tcl` file.
- Generate the `constraint.sdc` file.
- Synthesize Verilog code using Cadence Genus.
- Generate and simulate the synthesized netlist using Incisive.

======================================================

## Lab 05 — Memory Replacement

**Topic:** Single-Port and Double-Port SRAM

Study and implementation activities related to replacing memory structures with SRAM implementations, covering:

- Single-Port SRAM
- Double-Port SRAM
- Memory replacement concepts
- SRAM integration in digital designs

======================================================

## Lab 06 — PLL Instantiation in a Verilog Design

**Project:** 16-bit Counter — Clock Divider to SMIC40 PLL

**Objectives:**
- Build a 16-bit counter using a Verilog-based clock divider.
- Replace the behavioral clock divider with an instantiated SMIC40 PLL hard macro.
- Calculate PLL configuration values: M, N, and OD.
- Simulate divider-based and PLL-based implementations.
- Verify functional equivalence.
- Synthesize the PLL-based design using Cadence Genus.
- Write SDC constraints for reference and generated clocks.
- Perform gate-level netlist verification using `irun`.

======================================================
