# Week 02 – Part-02 [Day 4,5]. 

## Advanced Computer Architecture & RISC-V

### Overview

This portion of the training focuses on the fundamentals of **Computer Architecture**, processor performance, parallelism, Instruction Set Architecture (ISA), and the **RISC-V ISA**.

The lectures also introduced processor datapath design and explained how major processor components such as the Program Counter, Register File, ALU, memories, multiplexers, and Control Unit work together to execute instructions.

=============================================================

## 📚 Topics Covered

### 1. Introduction to Computer Architecture

Learned the basic concepts of computer architecture and how a computer system is organized at different levels.

#### Key Concepts

- Computer Architecture definition
- Levels of representation
- The big picture of a computer system
- Execution cycle
- Von Neumann Architecture
- Harvard Architecture
- Processor components
- Datapath and control

Computer architecture focuses on how the hardware components of a computer are organized and how they work together to execute programs.

=============================================================

### 2. Computer Performance

Studied how processor performance can be measured and improved.

#### Performance Concepts

- CPU performance
- Execution time
- Throughput
- Benchmarks
- Types of benchmarks
- Performance evaluation
- Clock rate
- CPI (Cycles Per Instruction)

Performance can be improved by reducing execution time, increasing useful work per cycle, or using architectural techniques that allow multiple operations to be processed efficiently.

=============================================================

### 3. Improving Performance

Explored the major ideas used in computer architecture to improve processor performance.

Important concepts include:

- Making the common case fast
- Parallelism
- Pipelining
- Performance through specialization
- Memory hierarchy
- Predicting and reducing bottlenecks
- Efficient hardware organization

=============================================================

### 4. Performance Through Parallelism

Learned how parallelism allows multiple operations to be performed at the same time or overlapped to improve overall system performance.

Topics included:

- Instruction-level parallelism
- Pipelining
- Multicore processing
- Parallel execution
- Scalability

=============================================================

# 🧠 Instruction Set Architecture (ISA)

### 5. Introduction to ISA

Learned what an **Instruction Set Architecture (ISA)** is and how it defines the interface between software and hardware.

The ISA specifies:

- Instructions supported by the processor
- Registers
- Data types
- Instruction formats
- Addressing methods
- Memory access
- Control-flow operations

=============================================================

### 6. ISA Classification

Studied different approaches to instruction set design and the characteristics of different ISA types.

Key concepts included:

- RISC
- CISC
- Instruction types
- Addressing modes
- ISA design principles

=============================================================

# 🟢 RISC-V ISA

### 7. Introduction to RISC-V

Introduced the **RISC-V Instruction Set Architecture**, an open and modular ISA widely used in education, research, embedded systems, and processor design.

Studied:

- RISC-V architecture
- RV32I
- Register state
- Instruction encoding
- Instruction formats
- Assembly instructions
- Binary representation

=============================================================

### 8. RISC-V Instruction Types

Studied the major categories of RISC-V instructions.

#### Computational Instructions

Used for arithmetic and logical operations such as:

- ADD
- SUB
- AND
- OR

#### Load & Store Instructions

Used to transfer data between registers and memory.

Examples include:

- Load
- Store

The effective memory address is calculated using a base register and an immediate offset.

#### Control Instructions

Used to change the normal program execution flow.

Examples include:

- Conditional branches
- Jumps
- `BEQ`

=============================================================

### 9. RISC-V Instruction Formats

Learned how instructions are represented using fixed fields within the instruction word.

Important concepts:

- Opcode
- Register fields
- Function fields
- Immediate fields
- Instruction encoding

Also studied how assembly instructions are converted into binary machine instructions.

=============================================================

### 10. Assembly Code vs Binary

Learned the relationship between human-readable assembly instructions and their binary machine representation.

For example:

```text
Assembly Code
      ↓
Assembler
      ↓
Machine / Binary Code
      ↓
Processor

=============================================================
## 🖥️ Processor Datapath

## 11. Understanding the Processor Datapath 

Studied how the major components of a processor are connected to form a complete **datapath**. The datapath provides the hardware required to fetch instructions, read operands, perform operations, access memory, and write results back to the registers.

The major components studied include:

- Program Counter (PC)
- Instruction Memory
- Register File
- Arithmetic Logic Unit (ALU)
- Data Memory
- Adders
- Multiplexers
- Control Unit
- Sign Extension
- Branch and Jump logic

The datapath and control unit work together to execute different types of instructions.

=============================================================

## 12. Program Counter & Instruction Fetch

The **Program Counter (PC)** stores the address of the instruction currently being executed.

During instruction fetch:

PC
 ↓
Instruction Memory
 ↓
Instruction
