## Here  is the code of the Top Module of RISC-V Single Cycle Processor.

## SystemVerilog Code:

module processorTop( input logic clk,input logic reset);

//==========================
// Internal Signals
//==========================

logic [31:0] pc;
logic [31:0] nextPC;
logic [31:0] pcPlus4;

logic [31:0] instruction;

logic [31:0] readData1;
logic [31:0] readData2;

logic [31:0] immediate;

logic [31:0] branchOffset;
logic [31:0] branchAddress;

logic [31:0] aluInputB;

logic [31:0] aluResult;

logic [31:0] memoryData;

logic [31:0] writeData;

logic zero;

logic branch;
logic memRead;
logic memWrite;
logic memtoReg;
logic regWrite;
logic aluSrc;

logic [1:0] aluOp;
logic [3:0] aluControlSignal;

logic pcSrc;


//==========================
// PC
//==========================

programCounter PC(

    .clk(clk),
    .reset(reset),
    .next_pc(nextPC),
    .pc_out(pc)

);

//==========================
// Instruction Memory
//==========================

instructionMemory IM(

    .pc_out(pc),
    .inst(instruction)

);

//==========================
// Control Unit
//==========================

controlUnit CU(

    .opcode(instruction[6:0]),

    .branch(branch),
    .memRead(memRead),
    .memtoReg(memtoReg),
    .aluOp(aluOp),
    .memWrite(memWrite),
    .aluSrc(aluSrc),
    .regWrite(regWrite)

);

//==========================
// Register File
//==========================

registerFile RF(

    .clk(clk),
    .regWrite(regWrite),

    .rs1(instruction[19:15]),
    .rs2(instruction[24:20]),
    .rd(instruction[11:7]),

    .writeData(writeData),

    .readData1(readData1),
    .readData2(readData2)

);

//==========================
// Immediate Generator
//==========================

immediateGenerator IMM(

    .instruction(instruction),
    .immediate(immediate)

);

//==========================
// Shift Left
//==========================

shiftLeft1 SHIFT(

    .in(immediate),
    .out(branchOffset)

);

//==========================
// ALU Control
//==========================

aluControl ALUCTRL(

    .aluOp(aluOp),
    .funct3(instruction[14:12]),
    .funct7(instruction[30]),

    .aluControl(aluControlSignal)

);

//==========================
// ALUSrc MUX
//==========================

mux2x1 ALUMUX(

    .in0(readData2),
    .in1(immediate),
    .sel(aluSrc),

    .out(aluInputB)

);

//==========================
// ALU
//==========================

alu ALU(

    .operandA(readData1),
    .operandB(aluInputB),

    .aluControl(aluControlSignal),

    .result(aluResult),
    .zero(zero)

);

//==========================
// Data Memory
//==========================

dataMemory DM(

    .clk(clk),
    .memRead(memRead),
    .memWrite(memWrite),

    .address(aluResult),

    .writeData(readData2),

    .readData(memoryData)

);

//==========================
// MemtoReg MUX
//==========================

mux2x1 MEMMUX(

    .in0(aluResult),
    .in1(memoryData),

    .sel(memtoReg),

    .out(writeData)

);

//==========================
// PC + 4 Adder
//==========================

adder PCADD(

    .a(pc),
    .b(32'd4),

    .sum(pcPlus4)

);

//==========================
// Branch Adder
//==========================

adder BRANCHADD(

    .a(pc),
    .b(branchOffset),

    .sum(branchAddress)

);

//==========================
// Branch Logic
//==========================

assign pcSrc = branch & zero;


//==========================
// PC MUX
//==========================

mux2x1 PCMUX(

    .in0(pcPlus4),
    .in1(branchAddress),

    .sel(pcSrc),

    .out(nextPC)

);

endmodule

=========================================================
