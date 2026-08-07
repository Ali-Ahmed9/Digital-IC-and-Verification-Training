Source Code for Lab 3
------------------------------------------------------------------------------
## Lab Tasks: All designs should be done via dataflow modeling

Simulate 2 × 4 decoder, given in Figure 1, at dataflow level i.e., using assign statements (i.e., dataflow modeling) only.

Figure 1: 2* 4 Decoder
<img width="440" height="312" alt="image" src="https://github.com/user-attachments/assets/60c19eeb-4ec8-4f80-b6ab-382dff4c7c3c" />

a)	Consider propagation delay of inverter N1 is 5 time-units and propagation delay of the AND gate A1 is 6 time-units,
and change input values in testbench after each 5 time-units. Analyze the output.

## Verilog Code of 2*4 decoder:
module decoder2x4( input A0,A1, output D0,D1,D2,D3);
  
wire nA0, nA1;
assign #5 nA0 = ~A0;
assign #5 nA1 = ~A1;


assign #6 D0 = nA1 & nA0;
assign #6 D1 = nA1 & A0;
assign #6 D2 = A1 & nA0;
assign #6 D3 = A1 & A0;
endmodule

b)	Now change the propagation delay of A1 to 5 time-units as well and keep changing the input values,
in testbench after each 5 time-units. Analyze the output.

## Verilog Code :
module decoder2x4( input A0,A1, output D0,D1,D2,D3);
 
wire nA0, nA1;

assign #5 nA0 = ~A0;
assign #5 nA1 = ~A1;

assign #5 D0 = nA1 & nA0;
assign #5 D1 = nA1 & A0;
assign #5 D2 = A1 & nA0;
assign #5 D3 = A1 & A0;

endmodule

c)	Neglect the propagation delays, re-simulate the design and analyze the output.

## Verilog Code:
module decoder2x4(  input A0,A1, output D0,D1,D2,D3);

wire nA0, nA1;

assign nA0 = ~A0;
assign nA1 = ~A1;

assign D0 = nA1 & nA0;
assign D1 = nA1 & A0;
assign D2 = A1 & nA0;
assign D3 = A1 & A0;

endmodule

--------------------------------------------------------------------------------

2.	 Design and simulate an 8 × 1 MUX using only dataflow modeling. Show circuit diagram and truth table as well.
Upload simulation for any 3 random values of data and control inputs.

## Verilog Code 8*1 Mux:
module mux8x1(input I0, I1, I2, I3, I4, I5, I6, I7,  input S2, S1, S0, output Y);
   
wire nS2, nS1, nS0;

assign nS2 = ~S2;
assign nS1 = ~S1;
assign nS0 = ~S0;

assign Y = (nS2 & nS1 & nS0 & I0) |(nS2 & nS1 &  S0 & I1) |(nS2 &  S1 & nS0 & I2) |(nS2 &  S1 &  S0 & I3) |
   ( S2 & nS1 & nS0 & I4) |( S2 & nS1 &  S0 & I5) |( S2 &  S1 & nS0 & I6) |( S2 &  S1 &  S0 & I7);

endmodule

---------------------------------------------------------------------------------------
3.  Design and simulate 4-bit Subtractor. Show the high-level block diagram of your design.
Upload simulation for any 2 random input.

## Verilog Code of 4 bit Suntractor:

module subtractor4(input  [3:0] A,B,output [3:0] Diff,output Borrow);

wire [4:0] Result;

assign Result = {1'b0, A} - {1'b0, B};

assign Diff   = Result[3:0];
assign Borrow = Result[4];

endmodule

-----------------------------------------------------------------------------------------------

Design and simulate a circuit that takes a 4-bit BCD (Binary Coded Decimal) input A and generates,
an output Z if the input A is divisible by 4. Show the complete working. Simulation should show the results of all possible inputs.
Note: 0 is considered to be divisible by 4

## Verilog Code of 4 bit BCD:

module bcd_div4(

input [3:0] A,

output Z

);

assign Z=(~A[1]) & (~A[0]) & ((~A[3]) | (~A[2]));

endmodule


-------------------------------------------------------------------------------------------
