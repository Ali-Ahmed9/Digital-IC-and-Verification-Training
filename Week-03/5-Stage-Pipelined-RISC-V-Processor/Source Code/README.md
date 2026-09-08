## Here is the Source Code for the 5 stage pipelined processor.

IF/ID → ID/EX → EX/MEM → MEM/WB

## 1. Program Counter

## SystemVerilog Code:

module programCounter(

    input  logic        clk,
    input  logic        reset,
    input  logic [31:0] next_pc,

    output logic [31:0] pc_out

);

    always_ff @(posedge clk or posedge reset)
    begin
        if (reset)
            pc_out <= 32'd0;       // Start execution from address 0
        else
            pc_out <= next_pc;     // Load next instruction address
    end

endmodule

=========================================================

## 2. Adder

## SystemVerilog Code:

module adder(

    input  logic [31:0] a,
    input  logic [31:0] b,

    output logic [31:0] sum

);

    assign sum = a + b;

endmodule

=========================================================

## 3. Instruction Memory

## SystemVerilog Code:

module instructionMemory(

    input  logic [31:0] pc_out,
    output logic [31:0] inst

);

    // 256 words of instruction memory
    logic [31:0] data [0:255];

    integer i;

    initial
    begin

        // Program Instructions

        data[0]  = 32'b00000000000000000000000010010011;
        data[1]  = 32'b00000000000000000000000100010011;
        data[2]  = 32'b00000001000000000000000110010011;
        data[3]  = 32'b00000000101000000000001000010011;
        data[4]  = 32'b11111111111100100000001010010011;
        data[5]  = 32'b00000000110100000000001100010011;
        data[6]  = 32'b00000000011000011000000000100011;
        data[7]  = 32'b00000000001000000000001100010011;
        data[8]  = 32'b00000000011000011000000010100011;
        data[9]  = 32'b00000000101000000000001100010011;
        data[10] = 32'b00000000011000011000000100100011;
        data[11] = 32'b00000001000100000000001100010011;
        data[12] = 32'b00000000011000011000000110100011;
        data[13] = 32'b00000001010100000000001100010011;
        data[14] = 32'b00000000011000011000001000100011;
        data[15] = 32'b00000000111000000000001100010011;
        data[16] = 32'b00000000011000011000001010100011;
        data[17] = 32'b00000001100000000000001100010011;
        data[18] = 32'b00000000011000011000001100100011;
        data[19] = 32'b00000000101100000000001100010011;
        data[20] = 32'b00000000011000011000001110100011;
        data[21] = 32'b00000000111100000000001100010011;
        data[22] = 32'b00000000011000011000010000100011;
        data[23] = 32'b00000000000000000000001100010011;
        data[24] = 32'b00000000011000011000010010100011;
        data[25] = 32'b00000100010100001000000001100011;
        data[26] = 32'b00000000000100001000000100010011;
        data[27] = 32'b00000010010000010000100001100011;
        data[28] = 32'b00000000001100001000001110110011;
        data[29] = 32'b00000000000000111000010000000011;
        data[30] = 32'b00000000001100010000010010110011;
        data[31] = 32'b00000000000001001000010100000011;
        data[32] = 32'b00000000100001010100011001100011;
        data[33] = 32'b00000000000100010000000100010011;
        data[34] = 32'b11111110000000000000001011100011;
        data[35] = 32'b00000000100001001000000000100011;
        data[36] = 32'b00000000101000111000000000100011;
        data[37] = 32'b00000000000100010000000100010011;
        data[38] = 32'b11111100000000000000101011100011;
        data[39] = 32'b00000000000100001000000010010011;
        data[40] = 32'b11111100000000000000001011100011;

        // Fill remaining memory with NOPs (ADDI x0, x0, 0)
        for(i = 41; i < 256; i = i + 1)
        begin
            data[i] = 32'h00000013;
        end

    end

    // Word Addressing
    assign inst = data[pc_out >> 2];

endmodule

=========================================================

## 4. IFID (Fetch//Decode)

## SystemVerilog Code:

module IF_ID(

    input  logic        clk,
    input  logic        reset,

    // Inputs from IF Stage
    input  logic [31:0] pc_in,
    input  logic [31:0] pcPlus4_in,
    input  logic [31:0] instruction_in,

    // Outputs to ID Stage
    output logic [31:0] pc_out,
    output logic [31:0] pcPlus4_out,
    output logic [31:0] instruction_out

);

always_ff @(posedge clk or posedge reset)
begin

    if(reset)
    begin
        pc_out          <= 32'd0;
        pcPlus4_out     <= 32'd0;
        instruction_out <= 32'd0;
    end

    else
    begin
        pc_out          <= pc_in;
        pcPlus4_out     <= pcPlus4_in;
        instruction_out <= instruction_in;
    end

end

endmodule

=========================================================

## 5. Control Unit

## SystemVerilog Code:

module controlUnit(

    input  logic [6:0] opcode,

    output logic       branch,
    output logic       memRead,
    output logic       memtoReg,
    output logic [1:0] aluOp,
    output logic       memWrite,
    output logic       aluSrc,
    output logic       regWrite

);

    always_comb
    begin

        // Default values
        branch   = 0;
        memRead  = 0;
        memtoReg = 0;
        aluOp    = 2'b00;
        memWrite = 0;
        aluSrc   = 0;
        regWrite = 0;

        case(opcode)

            // R-Type
            7'b0110011:
            begin
                regWrite = 1;
                aluSrc   = 0;
                aluOp    = 2'b10;
            end

            // ADDI
            7'b0010011:
            begin
                regWrite = 1;
                aluSrc   = 1;
                aluOp    = 2'b00;
            end

            // LW
            7'b0000011:
            begin
                regWrite = 1;
                aluSrc   = 1;
                memRead  = 1;
                memtoReg = 1;
                aluOp    = 2'b00;
            end

            // SW
            7'b0100011:
            begin
                aluSrc   = 1;
                memWrite = 1;
                aluOp    = 2'b00;
            end

            // BEQ
            7'b1100011:
            begin
                branch = 1;
                aluOp  = 2'b01;
            end

            default:
            begin
                // Keep all signals 0
            end

        endcase

    end

endmodule

=========================================================

## 6. Register File

## SystemVerilog Code:

module registerFile(

    input  logic        clk,
    input  logic        regWrite,

    input  logic [4:0]  rs1,
    input  logic [4:0]  rs2,
    input  logic [4:0]  rd,

    input  logic [31:0] writeData,

    output logic [31:0] readData1,
    output logic [31:0] readData2

);

    // 32 registers of 32 bits
    logic [31:0] registers [0:31];

    integer i;

    // Initialize all registers to zero
    initial
    begin
        for(i = 0; i < 32; i = i + 1)
            registers[i] = 32'd0;
    end

    // Write Operation
    always_ff @(posedge clk)
    begin
        if(regWrite && (rd != 5'd0))
            registers[rd] <= writeData;
    end

    // Read Operation
    assign readData1 = registers[rs1];
    assign readData2 = registers[rs2];

endmodule

=========================================================

## 7. Immediaate Generator

## SystemVerilog Code:

module immediateGenerator(

    input  logic [31:0] instruction,

    output logic [31:0] immediate

);

    logic [6:0] opcode;

    assign opcode = instruction[6:0];

    always_comb
    begin

        case(opcode)

            // I-Type (ADDI, LW)
            7'b0010011,
            7'b0000011:
            begin
                immediate = {{20{instruction[31]}}, instruction[31:20]};
            end

            // S-Type (SW)
            7'b0100011:
            begin
                immediate = {{20{instruction[31]}},
                             instruction[31:25],
                             instruction[11:7]};
            end

            // B-Type (BEQ)
            7'b1100011:
            begin
                immediate = {{19{instruction[31]}},
                             instruction[31],
                             instruction[7],
                             instruction[30:25],
                             instruction[11:8],
                             1'b0};
            end

            // Default
            default:
            begin
                immediate = 32'd0;
            end

        endcase

    end

endmodule

=========================================================

## 8. IDEX (Decode/Execute)

## SystemVerilog Code:


module ID_EX(

    input logic clk,
    input logic reset,

    // Data Inputs
    input logic [31:0] pc_in,
    input logic [31:0] pcPlus4_in,
    input logic [31:0] readData1_in,
    input logic [31:0] readData2_in,
    input logic [31:0] immediate_in,

    // Instruction Fields
    input logic [4:0] rs1_in,
    input logic [4:0] rs2_in,
    input logic [4:0] rd_in,
    input logic [2:0] funct3_in,
    input logic       funct7_in,

    // EX Control Signals
    input logic       aluSrc_in,
    input logic [1:0] aluOp_in,

    // MEM Control Signals
    input logic       branch_in,
    input logic       memRead_in,
    input logic       memWrite_in,

    // WB Control Signals
    input logic       regWrite_in,
    input logic       memToReg_in,

    // Data Outputs
    output logic [31:0] pc_out,
    output logic [31:0] pcPlus4_out,
    output logic [31:0] readData1_out,
    output logic [31:0] readData2_out,
    output logic [31:0] immediate_out,

    // Instruction Fields
    output logic [4:0] rs1_out,
    output logic [4:0] rs2_out,
    output logic [4:0] rd_out,
    output logic [2:0] funct3_out,
    output logic       funct7_out,

    // EX Control Signals
    output logic       aluSrc_out,
    output logic [1:0] aluOp_out,

    // MEM Control Signals
    output logic       branch_out,
    output logic       memRead_out,
    output logic       memWrite_out,

    // WB Control Signals
    output logic       regWrite_out,
    output logic       memToReg_out

);

always_ff @(posedge clk or posedge reset)
begin

    if(reset)
    begin

        pc_out          <= 32'd0;
        pcPlus4_out     <= 32'd0;
        readData1_out   <= 32'd0;
        readData2_out   <= 32'd0;
        immediate_out   <= 32'd0;

        rs1_out         <= 5'd0;
        rs2_out         <= 5'd0;
        rd_out          <= 5'd0;
        funct3_out      <= 3'd0;
        funct7_out      <= 1'b0;

        aluSrc_out      <= 1'b0;
        aluOp_out       <= 2'b00;

        branch_out      <= 1'b0;
        memRead_out     <= 1'b0;
        memWrite_out    <= 1'b0;

        regWrite_out    <= 1'b0;
        memToReg_out    <= 1'b0;

    end

    else
    begin

        pc_out          <= pc_in;
        pcPlus4_out     <= pcPlus4_in;
        readData1_out   <= readData1_in;
        readData2_out   <= readData2_in;
        immediate_out   <= immediate_in;

        rs1_out         <= rs1_in;
        rs2_out         <= rs2_in;
        rd_out          <= rd_in;
        funct3_out      <= funct3_in;
        funct7_out      <= funct7_in;

        aluSrc_out      <= aluSrc_in;
        aluOp_out       <= aluOp_in;

        branch_out      <= branch_in;
        memRead_out     <= memRead_in;
        memWrite_out    <= memWrite_in;

        regWrite_out    <= regWrite_in;
        memToReg_out    <= memToReg_in;

    end

end

endmodule

=========================================================

## 9. Alu Control

## SystemVerilog Code:

module aluControl(

    input  logic [1:0] aluOp,
    input  logic [2:0] funct3,
    input  logic       funct7,

    output logic [3:0] aluControl

);

    always_comb
    begin

        case(aluOp)

            // LW, SW, ADDI
            2'b00:
            begin
                aluControl = 4'b0000;   // ADD
            end

            // BEQ
            2'b01:
            begin
                aluControl = 4'b0001;   // SUB
            end

            // R-Type
            2'b10:
            begin

                case(funct3)

                    // ADD / SUB
                    3'b000:
                    begin
                        if(funct7)
                            aluControl = 4'b0001;   // SUB
                        else
                            aluControl = 4'b0000;   // ADD
                    end

                    // AND
                    3'b111:
                        aluControl = 4'b0010;

                    // OR
                    3'b110:
                        aluControl = 4'b0011;

                    // XOR
                    3'b100:
                        aluControl = 4'b0100;

                    default:
                        aluControl = 4'b0000;

                endcase

            end

            default:
                aluControl = 4'b0000;

        endcase

    end

endmodule

=========================================================

## 10. Mux 2*1

## SystemVerilog Code:

module mux2x1(

    input  logic [31:0] in0,
    input  logic [31:0] in1,
    input  logic        sel,

    output logic [31:0] out

);

    always_comb
    begin
        if (sel)
            out = in1;
        else
            out = in0;
    end

endmodule


## 11. ALU 

## SystemVerilog Code:

module alu(

    input  logic [31:0] operandA,
    input  logic [31:0] operandB,
    input  logic [3:0]  aluControl,

    output logic [31:0] result,
    output logic        zero

);

    always_comb
    begin

        case(aluControl)

            // ADD
            4'b0000:
                result = operandA + operandB;

            // SUB
            4'b0001:
                result = operandA - operandB;

            // AND
            4'b0010:
                result = operandA & operandB;

            // OR
            4'b0011:
                result = operandA | operandB;

            // XOR
            4'b0100:
                result = operandA ^ operandB;

            // Default
            default:
                result = 32'd0;

        endcase

    end

    // Zero Flag
    assign zero = (result == 32'd0);

endmodule

=========================================================

## 12. Shiftleft1

## SystemVerilog Code:

module shiftLeft1(

    input  logic [31:0] in,

    output logic [31:0] out

);

    assign out = in << 1;

endmodule

=========================================================

## 13. EXMEM (Execute/Memory)

## SystemVerilog Code:

module EX_MEM(

    input logic clk,
    input logic reset,

    // Data Inputs
    input logic [31:0] branchAddress_in,
    input logic        zero_in,
    input logic [31:0] aluResult_in,
    input logic [31:0] writeData_in,
    input logic [4:0]  rd_in,

    // MEM Control Signals
    input logic branch_in,
    input logic memRead_in,
    input logic memWrite_in,

    // WB Control Signals
    input logic regWrite_in,
    input logic memToReg_in,

    // Data Outputs
    output logic [31:0] branchAddress_out,
    output logic        zero_out,
    output logic [31:0] aluResult_out,
    output logic [31:0] writeData_out,
    output logic [4:0]  rd_out,

    // MEM Control Signals
    output logic branch_out,
    output logic memRead_out,
    output logic memWrite_out,

    // WB Control Signals
    output logic regWrite_out,
    output logic memToReg_out

);

always_ff @(posedge clk or posedge reset)
begin

    if(reset)
    begin

        branchAddress_out <= 32'd0;
        zero_out          <= 1'b0;
        aluResult_out     <= 32'd0;
        writeData_out     <= 32'd0;
        rd_out            <= 5'd0;

        branch_out        <= 1'b0;
        memRead_out       <= 1'b0;
        memWrite_out      <= 1'b0;

        regWrite_out      <= 1'b0;
        memToReg_out      <= 1'b0;

    end

    else
    begin

        branchAddress_out <= branchAddress_in;
        zero_out          <= zero_in;
        aluResult_out     <= aluResult_in;
        writeData_out     <= writeData_in;
        rd_out            <= rd_in;

        branch_out        <= branch_in;
        memRead_out       <= memRead_in;
        memWrite_out      <= memWrite_in;

        regWrite_out      <= regWrite_in;
        memToReg_out      <= memToReg_in;

    end

end

=========================================================

## 14. Data Memory

## SystemVerilog Code:

module dataMemory(

    input  logic        clk,
    input  logic        memRead,
    input  logic        memWrite,

    input  logic [31:0] address,
    input  logic [31:0] writeData,

    output logic [31:0] readData

);

    // 256 words of memory
    logic [31:0] memory [0:255];

    integer i;

    // Initialize memory to zero
    initial
    begin
        for(i = 0; i < 256; i = i + 1)
            memory[i] = 32'd0;
    end

    // Write Operation
    always_ff @(posedge clk)
    begin
        if(memWrite)
            memory[address >> 2] <= writeData;
    end

    // Read Operation
    always_comb
    begin
        if(memRead)
            readData = memory[address >> 2];
        else
            readData = 32'd0;
    end

endmodule

=========================================================

## 15. MEMWB ( Memory/writeback)

## SystemVerilog Code:

module MEM_WB(

    input logic clk,
    input logic reset,

    // Data Inputs
    input logic [31:0] readData_in,
    input logic [31:0] aluResult_in,
    input logic [4:0]  rd_in,

    // WB Control Signals
    input logic regWrite_in,
    input logic memToReg_in,

    // Data Outputs
    output logic [31:0] readData_out,
    output logic [31:0] aluResult_out,
    output logic [4:0]  rd_out,

    // WB Control Signals
    output logic regWrite_out,
    output logic memToReg_out

);

always_ff @(posedge clk or posedge reset)
begin

    if(reset)
    begin

        readData_out <= 32'd0;
        aluResult_out <= 32'd0;
        rd_out <= 5'd0;

        regWrite_out <= 1'b0;
        memToReg_out <= 1'b0;

    end

    else
    begin

        readData_out <= readData_in;
        aluResult_out <= aluResult_in;
        rd_out <= rd_in;

        regWrite_out <= regWrite_in;
        memToReg_out <= memToReg_in;

    end

end

endmodule


=========================================================

