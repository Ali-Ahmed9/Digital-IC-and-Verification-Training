# Week 01 – Lab 05

# Finite State Machine (FSM) Design Using Verilog HDL

---

## 📖 Overview

This lab introduces the design and implementation of **Finite State Machines (FSMs)** using Verilog HDL.
The experiments focus on sequence detection, synchronous counters, and pattern recognition using 
both **Mealy** and **Moore** machine concepts.

---

# 🎯 Objectives

- Understand the fundamentals of Finite State Machines (FSMs).
- Learn the difference between Mealy and Moore machines.
- Design FSMs using Verilog HDL.
- Implement sequence detectors and synchronous counters.
- Analyze state transitions and simulation results.

---

# 📝 Lab Tasks

## Task 1 – Sequence Recognizer (1011)

Designed a **non-overlapping sequence detector** that recognizes the binary sequence **1011**.

### Features

- Input: A
- Output: Z
- Detects sequence **1011**
- Non-overlapping detection
- Resets after successful detection

---

## Task 2 – Decade Counter

Designed a **synchronous decade counter**.

### Features

- Counts from 0 to 9
- Synchronous Reset
- Clock Driven
- Automatically rolls over from 9 to 0

---

## Task 3 – Pattern Detector (111 / 000)

Designed an **overlapping FSM** that detects:

- 111
- 000

### Features

- Overlapping detection
- Does not reset after detection
- Output becomes HIGH whenever either pattern is detected

---


# 🛠️ Tools Used

- Verilog HDL
- Vivado Design Suite


---

# 📚 Key Concepts Learned

- Finite State Machines
- Mealy Machine
- Moore Machine
- State Encoding
- Sequence Detection
- Overlapping Sequence Detector
- Non-Overlapping Sequence Detector
- Synchronous Counter
- State Transition Logic

---

# 👨‍💻 Author

**Ali Ahmed**
