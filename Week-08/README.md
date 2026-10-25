# Week 08 — ASIC Design Flow, CMOS Manufacturing & Static Timing Analysis

## Overview

Week 08 of my **Digital IC Design and Verification Training** focused on the fundamentals of Digital ASIC Design, CMOS Manufacturing, HDL Coding Guidelines, and Static Timing Analysis (STA).

The week introduced the front-end and back-end ASIC design flow, the importance of RTL coding practices, and the role of timing analysis in verifying whether a digital design can operate at its target frequency. It also included a practical lab on implementing half-adder and full-adder circuits using Verilog and Cadence NC Launch.

======================================================

## Topics Covered

## 1. Digital ASIC and FPGA Design Flow
- Introduction to Digital ASIC Design Flow.
- ASIC and FPGA implementation concepts.
- Digital implementation techniques and design considerations.
- RTL preparation and validation.
- Synthesis and post-synthesis verification.

======================================================

## 2. HDL Coding Guidelines and Techniques
- Verilog HDL coding fundamentals.
- Coding guidelines for digital hardware design.
- Design considerations for synthesis.
- Preparing RTL for ASIC implementation.

======================================================

## 3. CMOS Manufacturing Process
- Introduction to CMOS manufacturing.
- CMOS manufacturing process — Part I.
- CMOS manufacturing process — Part II.

======================================================

## 4. Static Timing Analysis (STA)
- Need for timing analysis in digital circuits.
- Timing simulation versus static timing analysis.
- Timing analysis using design, clock definitions, and external environment constraints.
- Setup and hold timing concepts.
- Timing violations and operating frequency.
- Interconnect delay, noise, and crosstalk in deep-submicron designs.

======================================================

## STA evaluates timing paths throughout a design without relying on specific input stimulus patterns. Unlike timing simulation, which depends on applied testbench stimuli, STA systematically checks timing requirements against defined constraints.

## 5. ASIC Design and Verification Concepts
The broader course outline also introduces:
- Standard cells and I/O library structures
- I/O pad selection and configuration
- Formal verification
- RISC-V design-verification-based ASIC front-end flow
- Design for Testability (DFT) and Memory Built-In Self-Test (MBIST)
- Introduction to Zynq SoC and RFSoC design and configuration

======================================================

## Lab 1 — Half Adder and Full Adder Using Cadence NC Launch

Aim: To implement and simulate half-adder and full-adder circuits using Verilog HDL and Cadence NC Launch.

## Objectives:

Verify that Cadence NC Launch is operational.

Become familiar with the tool and its functionalities.

Write Verilog code for half-adder and full-adder circuits.

Simulate and verify the circuit functionality.

Understand the basic digital design and simulation workflow.

======================================================

## Lab 2 — Logic Synthesis Using Cadence Genus

Aim: To synthesize Verilog HDL code using Cadence tools and generate a netlist.

## Objectives:

Understand the provided Verilog HDL code.

Generate the required synthesis script file.

Learn the procedure for synthesizing Verilog code and generating a netlist.

Understand the basic commands used to launch Cadence tools and Genus.

Key Focus: Understanding the transition from RTL code to a synthesized netlist using a logic synthesis tool.

======================================================

## Tools and Technologies
- Verilog HDL
- Cadence NC Launch
- Digital ASIC Design Flow
- Static Timing Analysis (STA)
- CMOS Manufacturing Concepts

======================================================
*This repository documents my learning, practical exercises, and progress throughout the Digital IC Design and Verification Training.*
