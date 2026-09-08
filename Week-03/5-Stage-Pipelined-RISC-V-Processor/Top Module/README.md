## Here is the code of Top Module Code

## SystemVerilog Code:

module pipelineTop(

    input logic clk,
    input logic reset

);

//////////////////////////////////////////////////////////
// IF STAGE SIGNALS
//////////////////////////////////////////////////////////

logic [31:0] pc;
logic [31:0] next_pc;
logic [31:0] pcPlus4;
logic [31:0] instruction;

//////////////////////////////////////////////////////////
// IF/ID PIPELINE REGISTER SIGNALS
//////////////////////////////////////////////////////////

logic [31:0] ifid_pc;
logic [31:0] ifid_pcPlus4;
logic [31:0] ifid_instruction;

//////////////////////////////////////////////////////////
// CONTROL UNIT SIGNALS
//////////////////////////////////////////////////////////

logic branch;
logic memRead;
logic memWrite;
logic memtoReg;
logic regWrite;
logic aluSrc;
logic [1:0] aluOp;

//////////////////////////////////////////////////////////
// REGISTER FILE SIGNALS
//////////////////////////////////////////////////////////

logic [31:0] readData1;
logic [31:0] readData2;

//////////////////////////////////////////////////////////
// IMMEDIATE GENERATOR
//////////////////////////////////////////////////////////

logic [31:0] immediate;

//////////////////////////////////////////////////////////
// ID/EX PIPELINE REGISTER SIGNALS
//////////////////////////////////////////////////////////

logic [31:0] idex_pc;
logic [31:0] idex_pcPlus4;

logic [31:0] idex_readData1;
logic [31:0] idex_readData2;

logic [31:0] idex_immediate;

logic [4:0] idex_rs1;
logic [4:0] idex_rs2;
logic [4:0] idex_rd;

logic [2:0] idex_funct3;
logic       idex_funct7;

logic       idex_branch;
logic       idex_memRead;
logic       idex_memWrite;
logic       idex_memtoReg;
logic       idex_regWrite;
logic       idex_aluSrc;
logic [1:0] idex_aluOp;

//////////////////////////////////////////////////////////
// EX STAGE SIGNALS
//////////////////////////////////////////////////////////

logic [3:0] aluControlSignal;

logic [31:0] aluInput2;

logic [31:0] aluResult;

logic zero;

logic [31:0] shiftedImmediate;

logic [31:0] branchAddress;

//////////////////////////////////////////////////////////
// EX/MEM PIPELINE REGISTER SIGNALS
//////////////////////////////////////////////////////////

logic [31:0] exmem_branchAddress;
logic [31:0] exmem_aluResult;
logic [31:0] exmem_writeData;

logic exmem_zero;

logic [4:0] exmem_rd;

logic exmem_branch;
logic exmem_memRead;
logic exmem_memWrite;

logic exmem_regWrite;
logic exmem_memtoReg;

//////////////////////////////////////////////////////////
// MEM STAGE SIGNALS
//////////////////////////////////////////////////////////

logic [31:0] memoryReadData;

//////////////////////////////////////////////////////////
// MEM/WB PIPELINE REGISTER SIGNALS
//////////////////////////////////////////////////////////

logic [31:0] memwb_readData;
logic [31:0] memwb_aluResult;

logic [4:0] memwb_rd;

logic memwb_regWrite;
logic memwb_memtoReg;

//////////////////////////////////////////////////////////
// WRITE BACK SIGNAL
//////////////////////////////////////////////////////////

logic [31:0] writeBackData;

//////////////////////////////////////////////////////////
// NEXT PC LOGIC
//////////////////////////////////////////////////////////

assign next_pc =
        (exmem_branch && exmem_zero) ?
        exmem_branchAddress :
        pcPlus4;

//////////////////////////////////////////////////////////
// PROGRAM COUNTER
//////////////////////////////////////////////////////////

programCounter PC(

    .clk(clk),
    .reset(reset),
    .next_pc(next_pc),
    .pc_out(pc)

);

//////////////////////////////////////////////////////////
// PC + 4 ADDER
//////////////////////////////////////////////////////////

adder PC_ADDER(

    .a(pc),
    .b(32'd4),
    .sum(pcPlus4)

);

//////////////////////////////////////////////////////////
// INSTRUCTION MEMORY
//////////////////////////////////////////////////////////

instructionMemory IM(

    .pc_out(pc),
    .inst(instruction)

);

//////////////////////////////////////////////////////////
// IF / ID PIPELINE REGISTER
//////////////////////////////////////////////////////////

IF_ID IFID(

    .clk(clk),
    .reset(reset),

    .pc_in(pc),
    .pcPlus4_in(pcPlus4),
    .instruction_in(instruction),

    .pc_out(ifid_pc),
    .pcPlus4_out(ifid_pcPlus4),
    .instruction_out(ifid_instruction)

);

//////////////////////////////////////////////////////////
// CONTROL UNIT
//////////////////////////////////////////////////////////

controlUnit CU(

    .opcode(ifid_instruction[6:0]),

    .branch(branch),
    .memRead(memRead),
    .memtoReg(memtoReg),
    .aluOp(aluOp),
    .memWrite(memWrite),
    .aluSrc(aluSrc),
    .regWrite(regWrite)

);

//////////////////////////////////////////////////////////
// REGISTER FILE
//////////////////////////////////////////////////////////

registerFile RF(

    .clk(clk),

    .regWrite(memwb_regWrite),

    .rs1(ifid_instruction[19:15]),
    .rs2(ifid_instruction[24:20]),
    .rd(memwb_rd),

    .writeData(writeBackData),

    .readData1(readData1),
    .readData2(readData2)

);

//////////////////////////////////////////////////////////
// IMMEDIATE GENERATOR
//////////////////////////////////////////////////////////

immediateGenerator IG(

    .instruction(ifid_instruction),
    .immediate(immediate)

);

//////////////////////////////////////////////////////////
// ID / EX PIPELINE REGISTER
//////////////////////////////////////////////////////////

ID_EX IDEX(

    .clk(clk),
    .reset(reset),

    .pc_in(ifid_pc),
    .pcPlus4_in(ifid_pcPlus4),

    .readData1_in(readData1),
    .readData2_in(readData2),

    .immediate_in(immediate),

    .rs1_in(ifid_instruction[19:15]),
    .rs2_in(ifid_instruction[24:20]),
    .rd_in(ifid_instruction[11:7]),

    .funct3_in(ifid_instruction[14:12]),
    .funct7_in(ifid_instruction[30]),

    .aluSrc_in(aluSrc),
    .aluOp_in(aluOp),

    .branch_in(branch),
    .memRead_in(memRead),
    .memWrite_in(memWrite),

    .regWrite_in(regWrite),
    .memToReg_in(memtoReg),

    .pc_out(idex_pc),
    .pcPlus4_out(idex_pcPlus4),

    .readData1_out(idex_readData1),
    .readData2_out(idex_readData2),

    .immediate_out(idex_immediate),

    .rs1_out(idex_rs1),
    .rs2_out(idex_rs2),
    .rd_out(idex_rd),

    .funct3_out(idex_funct3),
    .funct7_out(idex_funct7),

    .aluSrc_out(idex_aluSrc),
    .aluOp_out(idex_aluOp),

    .branch_out(idex_branch),
    .memRead_out(idex_memRead),
    .memWrite_out(idex_memWrite),

    .regWrite_out(idex_regWrite),
    .memToReg_out(idex_memtoReg)

);
//////////////////////////////////////////////////////////
// ALU CONTROL
//////////////////////////////////////////////////////////

aluControl ALUCTRL(

    .aluOp(idex_aluOp),
    .funct3(idex_funct3),
    .funct7(idex_funct7),

    .aluControl(aluControlSignal)

);

//////////////////////////////////////////////////////////
// ALU SOURCE MUX
//////////////////////////////////////////////////////////

mux2x1 ALU_MUX(

    .in0(idex_readData2),
    .in1(idex_immediate),
    .sel(idex_aluSrc),

    .out(aluInput2)

);

//////////////////////////////////////////////////////////
// ALU
//////////////////////////////////////////////////////////

alu ALU(

    .operandA(idex_readData1),
    .operandB(aluInput2),

    .aluControl(aluControlSignal),

    .result(aluResult),
    .zero(zero)

);

//////////////////////////////////////////////////////////
// SHIFT LEFT
//////////////////////////////////////////////////////////

shiftLeft1 SHIFT(

    .in(idex_immediate),
    .out(shiftedImmediate)

);

//////////////////////////////////////////////////////////
// BRANCH ADDRESS ADDER
//////////////////////////////////////////////////////////

adder BRANCH_ADDER(

    .a(idex_pc),
    .b(shiftedImmediate),

    .sum(branchAddress)

);

//////////////////////////////////////////////////////////
// EX / MEM PIPELINE REGISTER
//////////////////////////////////////////////////////////

EX_MEM EXMEM(

    .clk(clk),
    .reset(reset),

    .branchAddress_in(branchAddress),
    .zero_in(zero),

    .aluResult_in(aluResult),
    .writeData_in(idex_readData2),

    .rd_in(idex_rd),

    .branch_in(idex_branch),
    .memRead_in(idex_memRead),
    .memWrite_in(idex_memWrite),

    .regWrite_in(idex_regWrite),
    .memToReg_in(idex_memtoReg),

    .branchAddress_out(exmem_branchAddress),
    .zero_out(exmem_zero),

    .aluResult_out(exmem_aluResult),
    .writeData_out(exmem_writeData),

    .rd_out(exmem_rd),

    .branch_out(exmem_branch),
    .memRead_out(exmem_memRead),
    .memWrite_out(exmem_memWrite),

    .regWrite_out(exmem_regWrite),
    .memToReg_out(exmem_memtoReg)

);

//////////////////////////////////////////////////////////
// DATA MEMORY
//////////////////////////////////////////////////////////

dataMemory DM(

    .clk(clk),

    .memRead(exmem_memRead),
    .memWrite(exmem_memWrite),

    .address(exmem_aluResult),

    .writeData(exmem_writeData),

    .readData(memoryReadData)

);

//////////////////////////////////////////////////////////
// MEM / WB PIPELINE REGISTER
//////////////////////////////////////////////////////////

MEM_WB MEMWB(

    .clk(clk),
    .reset(reset),

    .readData_in(memoryReadData),
    .aluResult_in(exmem_aluResult),

    .rd_in(exmem_rd),

    .regWrite_in(exmem_regWrite),
    .memToReg_in(exmem_memtoReg),

    .readData_out(memwb_readData),
    .aluResult_out(memwb_aluResult),

    .rd_out(memwb_rd),

    .regWrite_out(memwb_regWrite),
    .memToReg_out(memwb_memtoReg)

);

//////////////////////////////////////////////////////////
// WRITE BACK MUX
//////////////////////////////////////////////////////////

mux2x1 WB_MUX(

    .in0(memwb_aluResult),
    .in1(memwb_readData),

    .sel(memwb_memtoReg),

    .out(writeBackData)

);



=========================================================


endmodule
