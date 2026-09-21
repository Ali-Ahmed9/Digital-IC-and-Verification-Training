## Section 02 — Embedded Toolchain, Build Process & Driver Development

## Overview

Section 02 covers **Day 04 and Day 05** of Week 05.

This section focuses on understanding how embedded source code is transformed into executable firmware and how the software interacts with the target hardware.

## Days Covered

======================================================

### Day 04 — Toolchain & Driver Development

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

======================================================

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

======================================================

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

======================================================
