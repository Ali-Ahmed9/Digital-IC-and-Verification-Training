# Week 05 — Embedded Systems, Bare-Metal Programming & RISC-V Toolchain

## Overview

Week 05 focused on developing practical knowledge of **Embedded Systems, Embedded C, Bare-Metal Programming, I2C communication, RISC-V embedded toolchains, build processes, linker scripts, startup code, and driver development**.

The week combined theory sessions, technical exercises, quizzes, hands-on programming, and laboratory activities.

=============================================

The work was divided into two major sections:

### Section 01 — Embedded Systems Fundamentals & Bare-Metal Programming

**Day 01 to Day 03**

This section covered:

- Embedded systems and microcontroller fundamentals
- C and Embedded C fundamentals
- RTL-oriented exercises and processor concepts
- Bare-metal programming
- I2C communication
- Direct access to microcontroller hardware registers
- ADS1115 ADC interfacing
- I2C configuration and register-level communication
- Practical sensor/ADC data acquisition

=============================================

### Section 02 — Embedded Toolchain, Build Process & Driver Development

**Day 04 to Day 05**

This section focused on the complete journey from source code to executable firmware and hardware execution.

Topics included:

- Embedded software toolchains
- Cross-compilation
- Preprocessing
- Compilation
- Assembly
- Linking
- ELF generation
- HEX/BIN generation
- Flashing and execution
- RISC-V GCC toolchain
- STRIVE IDE workflow
- Linker scripts
- Startup code
- RAM and FLASH organization
- LMA and VMA concepts
- GPIO, UART, I2C and SPI driver development
- `linker.ld` development
- `startup.S` development
- Symbol matching and linker errors
- Build and debugging workflow

=============================================


##  Week 05 Breakdown

### 🔹 Section 01 — Day 01 to Day 03

#### Day 01 — Evaluation Quiz & RTL Exercises

The first day included a practical evaluation consisting of multiple RTL-oriented exercises.

The evaluation covered:

- FIFO implementation
- Forwarding logic
- Hazard-related logic
- Stall and flush control
- Handshake logic
- Mini-pipeline implementation
- Beat sender FSM
- Periodic pulse generation

The exercises required parameter calculation based on the student ID and implementation of the required RTL modules followed by simulation and debugging.

=============================================

#### Day 02 — Embedded Systems & Microcontroller Fundamentals

Day 02 focused on the fundamentals of embedded systems and microcontrollers.

Topics included:

- Embedded Systems fundamentals
- Microcontroller fundamentals
- C programming fundamentals
- Embedded C concepts
- Relationship between software and embedded hardware

=============================================

#### Day 03 — Bare-Metal Programming & I2C

Day 03 focused on **bare-metal programming and register-level I2C communication**.

A practical ADS1115 interface was developed without using the Arduino `Wire` library.

The implementation directly accessed the AVR TWI hardware registers to perform:

START
   ↓
I2C Address + Write
   ↓
Register Pointer
   ↓
Configuration MSB
   ↓
Configuration LSB
   ↓
STOP

=============================================

## Section 02 — Embedded Toolchain, Build Process & Driver Development


Section 02 covers **Day 04 and Day 05** of Week 05.

This section focuses on understanding how embedded source code is transformed into executable firmware and how the software interacts with the target hardware.

=============================================

## Day 04 — Toolchain & Driver Development

Topics include:

- Embedded toolchains
- Cross compilation
- RISC-V GCC
- STRIVE IDE
- Preprocessing
- Compilation
- Assembly
- Linking
- ELF generation
- HEX/BIN generation
- Flashing
- Execution
- GPIO drivers
- UART drivers
- I2C drivers
- SPI drivers

=============================================

### Day 05 — Build Process & Linker/Startup

Practical work covering:

- Build pipeline
- Compiler output
- Assembly listing
- Map files
- ELF disassembly
- RAM and FLASH
- Linker scripts
- Startup assembly
- LMA / VMA
- Symbol matching
- Build debugging
- STRIVE IDE laboratory exercises

## Build Flow


Source
  ↓
Preprocessor
  ↓
Compiler
  ↓
Assembler
  ↓
Linker
  ↓
ELF
  ↓
HEX / BIN
  ↓
Flash
  ↓
Execute

=============================================
