# Week 07 — FPGA Timing Analysis, SoC Integration & AXI Design

Week 07 of the **Digital IC Design & Verification Training** focused on FPGA synthesis, static timing analysis (STA), timing optimization, System-on-Chip (SoC) integration, and AXI-based hardware design.

The week combined theoretical lectures, technical notes, and practical lab activities to explore how RTL is synthesized into FPGA resources, how timing violations are identified and resolved, and how processor cores, interconnects, memories, and peripherals are integrated into an SoC.

======================================================
##  Lectures

## 1. FPGA Design Flow: Synthesis & Timing Analysis

This topic covered the transformation of RTL into FPGA hardware resources and the importance of verifying timing after synthesis.

Topics included:

* FPGA synthesis and implementation flow
* LUTs, flip-flops, adders, comparators, and multiplexers
* Static Timing Analysis (STA)
* Setup and hold timing
* Critical path identification
* Worst Negative Slack (WNS) and Total Negative Slack (TNS)
* Clock skew and clock uncertainty
* Logic delay vs. routing delay
* Timing optimization and timing closure

======================================================


## 2. SoC Integration & Testing

This lecture explored the major components of an SoC and how they work together.

Topics included:

* SoC architecture and design components
* Processor cores, interconnects, peripherals, and memories
* SCR1 RISC-V MCU-class core
* AXI crossbar and address decoding
* AXI-Lite to APB4 bridge
* Memory-mapped peripheral access
* UART, GPIO, and SPI integration
* Hardware component sourcing and design reuse
* SoC integration and testing concepts

======================================================

## 3. AXI-Slave Dot-Product Accelerator

An introduction to integrating a compute core into an SoC using an AXI slave interface.

Key concepts:

* AXI-based accelerator integration
* Memory-mapped control and status registers
* Connecting a compute core to an SoC
* Finite State Machine (FSM) control
* Register-based communication between software and hardware

======================================================

##  Labs

## FPGA Synthesis, Timing Analysis & Timing Closure

**Tool:** Xilinx Vivado
**Design:** PWM Controller

The practical lab focused on synthesizing a Verilog PWM controller, inspecting its synthesized schematic, analyzing timing reports, and optimizing RTL to reduce unnecessary combinational logic.

Practical activities included:

* Creating an RTL project and applying clock constraints
* Running synthesis and implementation
* Examining FPGA resource utilization
* Analyzing setup and hold timing reports
* Identifying the critical path
* Comparing inefficient and optimized RTL
* Re-synthesizing and re-implementing the design
* Verifying timing closure

The lab demonstrated how RTL optimization can reduce logic depth and improve timing performance.

======================================================


##  Notes

The Notes section contains supporting material for Week 07, covering the key concepts of FPGA design flow, synthesis, static timing analysis, setup and hold timing, critical paths, timing closure, and SoC architecture.

These notes provide a reference for understanding the relationship between RTL design, FPGA implementation, timing constraints, and system-level hardware integration.

======================================================


##  Tools & Technologies

* Verilog HDL
* Xilinx Vivado
* FPGA Synthesis and Implementation
* Static Timing Analysis (STA)
* SystemVerilog and RTL concepts
* RISC-V SCR1 Core
* AXI and AXI-Lite
* APB4
* Memory-Mapped I/O
* UART, GPIO, and SPI

======================================================


##  Week 07 Focus

**RTL Synthesis → Static Timing Analysis → Timing Optimization → SoC Integration → AXI-Based Accelerator Design**

Week 07 strengthened the connection between RTL implementation, timing verification, and SoC-level architecture, providing a foundation for designing efficient FPGA hardware and integrating reusable components into larger digital systems.

======================================================

