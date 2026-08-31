# 5-Stage Pipelined RISC-V Processor

## Overview

This project extends the previously developed **Single-Cycle RISC-V Processor** into 
a **5-Stage Pipelined RISC-V Processor** using Verilog HDL.

The main objective is to understand how instruction execution can be divided into multiple stages 
so that several instructions can be processed simultaneously.

The processor is organized into five pipeline stages:

IF → ID → EX → MEM → WB
Where:

IF — Instruction Fetch
ID — Instruction Decode
EX — Execute
MEM — Memory Access
WB — Write Back

## Pipeline Architecture

The five stages are separated by pipeline registers:
IF
 ↓
IF/ID
 ↓
ID
 ↓
ID/EX
 ↓
EX
 ↓
EX/MEM
 ↓
MEM
 ↓
MEM/WB
 ↓
WB

The pipeline registers store the required data and control signals between consecutive stages.

Main Components

The pipelined processor builds upon the components developed for the Single-Cycle RISC-V Processor.

Major components include:

Program Counter (PC)
Instruction Memory
Register File
ALU
Control Unit
Immediate Generator
Data Memory
Multiplexers
Pipeline Registers
. IF/ID
. ID/EX
. EX/MEM
. MEM/WB

## Pipeline Stages

## 1. Instruction Fetch (IF)

The processor fetches an instruction from Instruction Memory using the Program Counter.

The next PC value is also calculated.

## 2. Instruction Decode (ID)

The fetched instruction is decoded.

The Register File is accessed to read the required source operands, while control signals
are generated for the remaining stages.

## 3. Execute (EX)

The ALU performs the required operation.

This stage also handles:

Arithmetic and logical operations
Address calculation
Branch comparison
Immediate-based operations.

## 4. Memory Access (MEM)

The processor interacts with Data Memory.

Load instructions read data from memory.
Store instructions write data to memory.

## 5. Write Back (WB)

The final result is written back into the Register File.

The result may come from:

ALU
Data Memory

## Pipeline Registers

Pipeline registers allow information to move from one stage to the next while maintaining the state of each instruction.

## IF/ID
Transfers information from Instruction Fetch to Instruction Decode.

## ID/EX
Transfers decoded instruction information, register operands, immediate values, and control signals to the Execute stage.

## EX/MEM
Transfers ALU results, memory-related information, and control signals to the Memory stage.

## MEM/WB
Transfers memory data or ALU results to the Write Back stage.



