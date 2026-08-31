# Week 03 — RISC-V Processor Design & Pipelining

## Overview

Week 03 focused on the practical design and implementation of a **RISC-V processor using Verilog HDL**. 
The processor was developed step-by-step, starting from individual hardware components and gradually 
integrating them into a complete processor architecture.

After completing the single-cycle processor, the design was extended toward a 
**5-stage pipelined architecture**, followed by the study and implementation of 
**forwarding and hazard handling**.

=========================================================

##  Week Structure

## Single-Cycle RISC-V Processor

Designed a RISC-V single-cycle processor from scratch by analyzing the architecture
and implementing its major components individually.

The development included:

- Program Counter (PC)
- Instruction Memory
- Register File
- ALU
- Control Unit
- Immediate Generator
- Data Memory
- Multiplexers and supporting logic
- Top-Level Processor Module
- Testbench
- Schematic and Datapath
- Simulation and Instruction Verification

=========================================================

##  5-Stage Pipelined RISC-V Processor

Extended the processor design into a 5-stage pipeline:

The design includes the pipeline registers:
IF → ID → EX → MEM → WB


=========================================================

Then we processed through different stages of the processor simultaneously....
## Forwarding & Hazard Handling

After implementing the basic pipeline, advanced pipeline concepts were introduced:

Data Forwarding
Forwarding Unit
Data Dependencies
Pipeline Hazards
Hazard Detection
Load-Use Hazards
Pipeline Stalling

=========================================================

## Tools & Technologies
Verilog HDL
RISC-V ISA
Xilinx Vivado
RTL Design
RTL Simulation

