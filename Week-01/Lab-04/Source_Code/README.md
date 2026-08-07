Source Code of lab 4:
=========================================================================

NOTE: Use procedural assignments (behavioral modeling), 
except where hierarchical design is needed (for example a top-level module).

=========================================================================

1.	Design an Arithmetic and Logic Unit (ALU) that implements 4 functions as described in Table 1.
The table also illustrates the encoding of the control input.
The 32-bit ALU has the following inputs/outputs:
• A: 32-bit input
•	B: 32-bit input
•	Cin: 1-bit input
•	Output: 64-bit output
•	Opcode: 2-bit control input
Simulate each operation with at least 1 random value of A and B.

Opcode	Instruction	 Operation
00	     ADD	       Output = A + B + Cin
01	     SUB	       Output = A – B
10	     MUL	       Output = A × B
11	     DIV	       Output = A / B

## Verilog Code of ALU:

     module alu(input [31:0] A,input [31:0] B, input Cin,input [1:0] Opcode,output reg [63:0] Output);

always @(*)
begin
case(Opcode)

    2'b00:
        Output = A + B + Cin;

    2'b01:
        Output = A - B;

    2'b10:
        Output = A * B;

    2'b11:
    begin
        if(B == 0)
            Output = 0;
        else
            Output = A / B;
    end

    default:
        Output = 0;

endcase
end

endmodule

=========================================================================

2.	 Design a negative edge-triggered D flip-flop with clock enable, active-low asynchronous set and reset,
   and both active-high and active-low outputs. It is illegal for both set and reset inputs to be active together.

## Verilog code of D-Flipflop:
module dff(input clk,input en,d,set_n,reset_n,output reg q,reg q_bar);

always @(negedge clk or negedge set_n or negedge reset_n)
begin
   
    if (!reset_n)
    begin
        q     <= 1'b0;
        q_bar <= 1'b1;
    end

   
    else if (!set_n)
    begin
        q     <= 1'b1;
        q_bar <= 1'b0;
    end

   
    else if (en)
    begin
        q     <= d;
        q_bar <= ~d;
    end

   
    else
    begin
        q     <= q;
        q_bar <= q_bar;
    end

end

endmodule

=========================================================================

3.	 The aim of the Verilog code, given in front, is to display 2, 3 and 4 in three consecutive clock cycles.
Do you think, this code is doing so or not?
Write a testbench for this code and simulate. Explain the output / behavior and justify your answer to the TA/Instructor.

module counter2to4 (out, clk);
input clk;
output [2:0] out;
reg [2:0] out;
integer n;

always @ (posedge clk) begin
for (n = 2; n >= 0; n = n-1) begin
if (n == 2) begin out <=3'b010;
end
else if (n == 1) begin out <=3'b011;
end
else if (n == 0) begin out <=3'b100;
end end
end endmodule


## Verilog Code of Counter 2 to 4:

module counter2to4 (input clk, output reg [2:0] out);

reg [1:0] state;

always @(posedge clk)
begin
    case(state)
        2'd0:
        begin
            out <= 3'b010;   
            state <= 2'd1;
        end

        2'd1:
        begin
            out <= 3'b011;   
            state <= 2'd2;
        end

        2'd2:
        begin
            out <= 3'b100;   
            state <= 2'd0;
        end

        default:
        begin
            out <= 3'b010;
            state <= 2'd1;
        end
    endcase
end

endmodule


=========================================================================

4.	 Design a clock with time-period = 20ns and a duty cycle of 25% by using always and initial statements.
The value of clock at time=0 (simulation start) should be initialized to 0.

## Verilog Code of Clock Generation:

module clock_generator;

reg clk;

initial
begin
    clk = 0;
end
always
begin
    #15 clk = 1;
    #5  clk = 0;
end

endmodule


=========================================================================

5.	 Design a Verilog model for a sequential circuit that computes the average of corresponding values,
 in three streams of input values, a, b, and c. The sequential circuit consists of three stages:
the first stage sums values of a and b and saves the value of c; the second stage adds on the saved value of c;
and the third stage divides by 3. The inputs and output are all 6-bit unsigned numbers.

## Verilog Code of Average of 3:

module average3(input clk,input [3:0] a, b,c, output reg [4:0] avg);

reg [5:0] sum;

initial
begin
    sum = 0;
    avg = 0;
end

always @(posedge clk)
begin
    sum = a + b + c;
    avg <= sum / 3;
end

endmodule

=========================================================================

