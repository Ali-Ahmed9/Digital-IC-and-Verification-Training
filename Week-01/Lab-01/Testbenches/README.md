   TestBench Code 
=========================================================================

1. ## Testbench Code for 4 input OR Gate:
`timescale 1ns/1ps

module tb_or4();

reg A,B,C,D;
wire Y;

or4 dut(A,B,C,D,Y);

initial begin

A=0;B=0;C=0;D=0;
#10;

A=1;B=0;C=0;D=0;
#10;

A=0;B=1;C=1;D=0;
#10;

A=1;B=1;C=1;D=1;
#10;

$finish;

end

=========================================================================

2. ## Testbench Code:

module task1new_tb();

reg A,B,C,D;
wire Z;

task1new dut(.A(A),.B(B),.C(C),.D(D),.Z(Z));

initial begin
A=0; B=0; C=0; D=0;
#10;

A=1; B=1; C=0; D=0;
#10;

A=1; B=0; C=1; D=0;
#10;

A=1; B=1; C=1; D=1;
#10;
$finish;
end

endmodule

=========================================================================

3. ## Testbench Code for 4*1 Mux:

module mux4_1_tb();
reg i0,i1,i2,i3;
reg s1,s0;

wire out;

mux4_1 DUT(.i0(i0),.i1(i1),.i2(i2),.i3(i3),.s1(s1),.s0(s0),.out(out));

initial begin

i0=1; i1=0; i2=0; i3=0;
s1=0; s0=0;
#10;

i0=0; i1=1; i2=0; i3=0;
s1=0; s0=1;
#10;

i0=0; i1=0; i2=1; i3=0;
s1=1; s0=0;
#10;

i0=0; i1=0; i2=0; i3=1;
s1=1; s0=1;
#10;

$finish;

end
endmodule

=========================================================================

4. ## Testbench Code for 2*4 Decoder:

module dec2_4_tb();
reg EN;
reg A1,A0;
wire D0,D1,D2,D3;

dec2_4 dut(.EN(EN),.A1(A1),.A0(A0),.D0(D0),.D1(D1),.D2(D2),.D3(D3));

initial begin

EN=1; A1=0; A0=0;
#10;

EN=1; A1=0; A0=1;
#10;

EN=1; A1=1; A0=0;
#10;

EN=0; A1=1; A0=1;
#10;

$finish;

end
endmodule

=========================================================================

