# Week 09 — Static Timing Analysis, Timing Constraints & Sequential Design Synthesis

======================================================

## Overview

Week 09 of my **Digital IC Design and Verification Training** focused on Static Timing Analysis (STA), timing constraints for synchronous digital designs, timing models, and sequential design synthesis.

The lectures explored how timing constraints define the operating environment of a digital design, including input and output delays, clock definitions, external attributes, setup and hold checks, and timing calculations.

The practical labs covered sequential design synthesis using Cadence Genus and transistor-level inverter schematic and layout implementation using Cadence Virtuoso.

======================================================

## Topics Covered

## 1. Static Timing Analysis and Timing Models

- Digital IC Front-End: Constraints for Synchronous Design
- Timing arcs and delay value computation
- Negative values of rise time
- Output slew and rise/fall transition times
- Types of timing tables in delay libraries
- Cell rise and fall timing tables
- Transition time and delay table examples
- Threshold specifications and slew derating
- Cell characterization and operating conditions
- Process variables and derating K-factors
- Positive and negative K-factors
- Library units and timing models
- Combinational and sequential timing models
- Timing arcs with respect to the active clock edge

======================================================

## 2. Setup and Hold Timing Analysis

- Synchronous setup and hold checks
- Timing parameters and setup/hold time
- Setup and hold timing examples
- Reading timing tables
- Definition of timing table indices
- Negative values in setup and hold checks
- Possibility of both setup and hold values being negative
- Slack calculation
- Estimation of required time
- Launch and capture flip-flops

======================================================

## 3. Timing Constraints for Synchronous Designs

- STA environment through practical examples
- Case study of timing constraints
- Constraining input paths
- Input path analysis for DUA (Design Under Analysis)
- Time required for data to be stable
- Constraining output paths
- Intended waveforms and timing constraints
- Modeling external attributes
- Driving cell configuration
- Input transition and output load constraints
- Design Rule Checks (DRC)
- Virtual clocks and their definitions

======================================================

## 4. Timing Constraint Commands and Design Environment

Introduction to timing constraint commands and their role in defining the design environment:

- `set_driving_cell`
- `set_input_transition`
- `set_load`
- `set_min_library`
- `set_operating_conditions`
- `set_wire_load_model`
- `set_wire_load_mode`
- `set_drive`

======================================================

## Lab Work

======================================================

## Lab 03 — Sequential Design Synthesis

**Aim:** To synthesize ALU Verilog HDL code using Cadence tools, generate a netlist, and write clock constraints.

**Objectives:**
- Write Verilog code for sequential logic.
- Generate the `synthesis_script.tcl` file.
- Generate the `constraint.sdc` file.
- Synthesize Verilog code using Cadence Genus.
- Generate the synthesized netlist.
- Run the netlist using Cadence Incisive.

**Key Focus:** Sequential RTL synthesis, timing constraint definition, and netlist generation.

======================================================

## Lab 03 B — Inverter Schematic and Layout on Virtuoso

**Objective:** To learn schematic creation and simulation using the CMOS gpdk045 technology design kit.

**Practical Activities:**
- Create and simulate a basic CMOS inverter schematic.
- Perform transistor-level implementation.
- Conduct transient analysis of basic gates.
- Modify transistor sizing.
- Create a circuit symbol.
- Explore schematic and layout design using Cadence Virtuoso.

**Key Focus:** Understanding transistor-level CMOS circuit design, schematic simulation, and layout implementation.

======================================================

## Tools and Technologies

- Verilog HDL
- Cadence Genus
- Cadence Incisive
- Cadence Virtuoso
- CMOS gpdk045 Technology Design Kit
- Tcl Synthesis Scripts
- Synopsys Design Constraints (SDC)
- Static Timing Analysis (STA)

======================================================
