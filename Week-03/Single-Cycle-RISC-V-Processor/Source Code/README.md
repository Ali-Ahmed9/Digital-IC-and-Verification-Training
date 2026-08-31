## Design and Verification of Single Cycle RISC–V Component

1. ## Program Counter

## Block Diagram:
<img width="915" height="225" alt="image" src="https://github.com/user-attachments/assets/eaa93cc7-f427-4a18-87d1-49e28e38d5bf" />

## Verilog Code:

module programCounter (input  logic clk,reset,input  logic [31:0] next_pc,    output logic [31:0] pc_out);
    always_ff @(posedge clk or posedge reset)
    begin
        if (reset)
            pc_out <= 32'd0;       // Start execution from address 0
        else
            pc_out <= next_pc;     // Load next instruction address
    end
endmodule

2. ## Instruction Memory

## Block Diagram:
<img width="975" height="225" alt="image" src="https://github.com/user-attachments/assets/9519a6ae-8b11-495f-863e-3b85b404baa2" />


## Verilog Code:

module instructionMemory( input  logic [31:0] pc_out, output logic [31:0] inst);

    logic [31:0] data [0:255];

    integer i;

    initial
    begin

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
        data[164] = 32'b01000000001100001000001110110011;

        for(i = 41; i < 256; i = i + 1)
        begin
            data[i] = 32'h00000013;
        end

    end

    assign inst = data[pc_out >> 2];

endmodule



3. ## Register File

## Block Diagram:
<img width="945" height="350" alt="image" src="https://github.com/user-attachments/assets/19e2ea99-5496-4ea4-961a-049baa676691" />


# Verilog Code:

module registerFile(input  logic clk,regWrite,input  logic [4:0]  rs1,rs2,rd,

    input  logic [31:0] writeData,output logic [31:0] readData1,readData2);


    logic [31:0] registers [0:31];

    integer i;

    initial
    begin
        for(i = 0; i < 32; i = i + 1)
            registers[i] = 32'd0;
    end

    always_ff @(posedge clk)
    begin
        if(regWrite && (rd != 5'd0))
            registers[rd] <= writeData;
    end

    assign readData1 = registers[rs1];
    assign readData2 = registers[rs2];

endmodule



4. ## Immediate Generator

## Block Diagram:
<img width="945" height="350" alt="image" src="https://github.com/user-attachments/assets/784c6f44-4b5d-44bc-a2dc-f4b8904fb431" />


## Verilog Code:

module immediateGenerator(input  logic [31:0] instruction,output logic [31:0] immediate);

    logic [6:0] opcode;

    assign opcode = instruction[6:0];

    always_comb
    begin

        case(opcode)

            7'b0010011,
            7'b0000011:
            begin
                immediate = {{20{instruction[31]}}, instruction[31:20]};
            end

            7'b0100011:
            begin
                immediate = {{20{instruction[31]}},
                             instruction[31:25],
                             instruction[11:7]};
            end

            7'b1100011:
            begin
                immediate = {{19{instruction[31]}},
                             instruction[31],
                             instruction[7],
                             instruction[30:25],
                             instruction[11:8],
                             1'b0};
            end

 
            default:
            begin
                immediate = 32'd0;
            end

        endcase

    end

endmodule



5. ## ALU / Execute Unit

## Block Diagram:
<img width="945" height="350" alt="image" src="https://github.com/user-attachments/assets/e11b14a1-887a-4b11-9b8d-831cf0c1c546" />

## Verilog Code:

module alu( input  logic [31:0] operandA,operandB,input  logic [3:0]  aluControl,
    output logic [31:0] result, output logic zero);
    
    always_comb
    begin

        case(aluControl)

            4'b0000:
                result = operandA + operandB;

            4'b0001:
                result = operandA - operandB;

            4'b0010:
                result = operandA & operandB;

            4'b0011:
                result = operandA | operandB;

            4'b0100:
                result = operandA ^ operandB;

            default:
                result = 32'd0;

        endcase

    end

    assign zero = (result == 32'd0);

endmodule



6. ## Control Unit

## Block Diagram:
<img width="945" height="448" alt="image" src="https://github.com/user-attachments/assets/395b9a12-d1be-4ca0-8f3a-f351fda0c653" />

## Verilog Code:

module controlUnit(input  logic [6:0] opcode, output logic branch, memRead,memtoReg,
    output logic [1:0] aluOp,output logic memWrite,aluSrc,regWrite);
    
    always_comb
    begin

        branch   = 0;
        memRead  = 0;
        memtoReg = 0;
        aluOp    = 2'b00;
        memWrite = 0;
        aluSrc   = 0;
        regWrite = 0;

        case(opcode)

            7'b0110011:
            begin
                regWrite = 1;
                aluSrc   = 0;
                aluOp    = 2'b10;
            end

            7'b0010011:
            begin
                regWrite = 1;
                aluSrc   = 1;
                aluOp    = 2'b00;
            end

            7'b0000011:
            begin
                regWrite = 1;
                aluSrc   = 1;
                memRead  = 1;
                memtoReg = 1;
                aluOp    = 2'b00;
            end

            7'b0100011:
            begin
                aluSrc   = 1;
                memWrite = 1;
                aluOp    = 2'b00;
            end

            7'b1100011:
            begin
                branch = 1;
                aluOp  = 2'b01;
            end

            default:
            begin
            end

        endcase

    end

endmodule




7. ## Data Memory

## Block Diagram:
<img width="945" height="399" alt="image" src="https://github.com/user-attachments/assets/6e5ae675-6e2c-4a82-9298-73df92658ee3" />

## Verilog Code:

module dataMemory (input  logic clk,memRead,memWrite, input  logic [31:0] address,writeData,output logic [31:0] readData);

    logic [31:0] memory [0:255];

    integer i;
    initial
    begin
        for(i = 0; i < 256; i = i + 1)
            memory[i] = 32'd0;
    end
    always_ff @(posedge clk)
    begin
        if(memWrite)
            memory[address >> 2] <= writeData;
    end
    always_comb
    begin
        if(memRead)
            readData = memory[address >> 2];
        else
            readData = 32'd0;
    end

endmodule



8. ## Multiplexer (2*1)

## Block Daigram:
<img width="945" height="350" alt="image" src="https://github.com/user-attachments/assets/0cbab4a6-11df-4f21-abc2-5374dd322bca" />

## Verilog Code:

module mux2x1(input  logic [31:0] in0,in1, input  logic sel,output logic [31:0] out);

    always_comb
    begin
        if (sel)
            out = in1;
        else
            out = in0;
    end

endmodule


9. ## Alu Control Unit

## Block Diagram:
<img width="945" height="350" alt="image" src="https://github.com/user-attachments/assets/de629f68-af5c-489c-a6d7-8fc692307865" />

## Verilog Code:

module aluControl (input logic [1:0] aluOp,input logic [2:0] funct3,input logic funct7, output logic [3:0] aluControl);

    always_comb
    begin

        case(aluOp)
            2'b00:
            begin
                aluControl = 4'b0000; 
            end
            2'b01:
            begin
                aluControl = 4'b0001;  
            end
            2'b10:
            begin

                case(funct3)

                    3'b000:
                    begin
                        if(funct7)
                            aluControl = 4'b0001;  
                        else
                            aluControl = 4'b0000;  
                    end
                    3'b111:
                        aluControl = 4'b0010;

                    3'b110:
                        aluControl = 4'b0011;

                   
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



10. ## Shiftleft1

## Veilog Code:
module shiftLeft1( input  logic [31:0] in, output logic [31:0] out);

    assign out = in << 1;

endmodule


11. ## Branch Adder

## Block Daigram:
<img width="945" height="251" alt="image" src="https://github.com/user-attachments/assets/a75e5507-f64a-4dc1-a4b8-3a6234226c90" />

## Verilog Code:

module adder ( input  logic [31:0] a,b,output logic [31:0] sum);
    assign sum = a + b;

endmodule
