# Week 02 – Portion 01  [Day 1,2,3]

## SystemVerilog Fundamentals & RTL Design Concepts

### Overview

This portion of the training introduces the fundamentals of **SystemVerilog** and, its use in Digital IC Design.
The sessions focus on understanding the language structure, data types, RTL modeling techniques, parameterised designs,
generate constructs, procedural blocks, event control, and assignment behavior.

The main goal is to build a strong foundation for writing **clean, reusable, and synthesizable RTL code**.

---

## 📚 Topics Covered

### 1. SystemVerilog Basics

The first part introduced the basic structure and syntax of SystemVerilog and how it differs from traditional Verilog.

**Key areas covered:**

- SystemVerilog heritage and HDL design mindset
- RTL design and simulation flow
- Vivado project structure
- Module declaration and port connections
- `` `timescale ``

#### Data Types

Learned how SystemVerilog represents hardware signals using different types.

- `wire`, `tri`, `wand`, `wor`
- `logic` vs `wire` vs `reg`
- 4-state and 2-state data types
- Signed and unsigned values
- Packed and unpacked arrays
- `parameter` and `localparam`

#### Structural & Dataflow Modeling

Learned how hardware can be described using continuous assignments and module hierarchy.

- `assign` statements
- Operators and expressions
- Reduction operators
- Shift operators
- Concatenation
- Equality operators
- Ternary operator
- Module instantiation
- Hierarchical design

#### Simulation & Testbench Basics

Learned basic SystemVerilog simulation constructs used to observe and control simulations.

- `$display`
- `$monitor`
- `$time`
- `$finish`
- `$stop`


Declare Signals → Instantiate DUT → Apply Inputs → Check Outputs → Finish


### 2. Parameterised Modules & Generics

The second part focused on making RTL modules **reusable and configurable** instead of creating separate modules for different sizes.

#### Parameterisation

Learned how parameters can control module characteristics such as bus width, memory depth, and other design configurations.

Important practices included:

- Using `parameter` for externally configurable values
- Using `localparam` for internal constants
- Using named parameter overrides
- Avoiding `defparam`
- Validating parameters during elaboration

#### Advanced Parameter Techniques

Explored more advanced SystemVerilog parameter features:

- `parameter type`
- `$clog2`
- Derived `localparam` values
- Conditional parameters
- String and real parameters
- SystemVerilog packages
- Explicit package imports

A key concept learned was using `$clog2` to automatically calculate address or pointer widths based on a parameter such as `DEPTH`.

#### Generate Constructs

Learned how generate constructs can create hardware structures automatically during elaboration.

Covered:

- `for-generate`
- `if-generate`
- `case-generate`
- `genvar`
- Named generate blocks
- Constant generate conditions

Generate constructs are especially useful when designing **parameterised and scalable hardware**.

---

### 3. Procedural Blocks & Event Control

The third part introduced procedural programming constructs used to describe hardware behavior and simulation processes.

#### Procedural Blocks

Learned the purpose and behavior of:

- `initial` blocks
- `always` blocks
- Procedural statements
- Sequential execution

#### Event Control & Timing

Learned how SystemVerilog controls when procedural statements execute.

Covered:

- `@`
- `posedge`
- `negedge`
- `wait`
- Events
- `fork/join`
- `disable`
- Timing controls
- `forever` loops

#### Blocking vs Non-Blocking Assignments

Studied the difference between:

##  systemverilog =
and
##  systemverilog <=


Blocking assignments execute immediately in procedural order, while non-blocking assignments schedule updates for a later simulation phase.

A fundamental RTL guideline learned was:

- **Blocking (`=`)** → generally used for combinational procedural logic
- **Non-blocking (`<=`)** → generally used for clocked sequential logic

Also explored:

- Simulation scheduling
- Race conditions
- Swap test
- Vivado lint
- Synthesis implications

---

## 🎯 Key Learning Outcomes

After completing this portion, I developed an understanding of:

- SystemVerilog syntax and module structure
- Hardware data types
- RTL and dataflow modeling
- Testbench fundamentals
- Parameterised and reusable modules
- `$clog2` and generate constructs
- SystemVerilog packages
- Procedural blocks
- Event control and timing
- Blocking and non-blocking assignments
- Basic RTL coding best practices

---

## 🛠️ Tools & Technologies

- SystemVerilog
- Verilog HDL
- Xilinx Vivado
- RTL Simulation


## Week: 02 [Day: 1,2,3]  
## Portion: 01  
