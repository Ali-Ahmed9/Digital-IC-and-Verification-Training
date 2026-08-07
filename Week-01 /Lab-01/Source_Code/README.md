Lab Tasks: You can only use Gate-Level Modeling in this Lab.
------------------------------------------------------------------

Design four-input OR, XOR and XNOR gates using 2 input primitive gates.
Simulate each circuit with at least 4 random inputs

## Verilog Code of 4 input OR Gate:

module or4(input A,B,C,D,output Y);

wire w1,w2;

or g1(w1,A,B);
or g2(w2,C,D);
or g3(Y,w1,w2);

endmodule

--------------------------------------------------------------------------

Simulate the design given in Figure 1 using gate level modeling with the following inputs A, B, C, and D.
Simulate each circuit with at least four random inputs and record them.

## Verilog code:

module task1new(input A,B,C,D,output Z);

wire X,Y;

and g1(X,A,B);
or  g2(Y,C,D);
xor g3(Z,X,Y);
endmodule

------------------------------------------------------------------------------

Design the gate level model of 4  1 Mux using Verilog HDL shown in Figure 2,
and simulate with at least 4 random input combinations of data and control inputs.
Record your random combinations and possible value for the output “out” .

## Verilog Code:
module mux4_1(input i0,i1,i2,i3,input s1,s0,  output out);

wire s1n,s0n;
wire y0,y1,y2,y3;

not g1(s1n,s1);
not g2(s0n,s0);
and g3(y0,i0,s1n,s0n);
and g4(y1,i1,s1n,s0);
and g5(y2,i2,s1,s0n);
and g6(y3,i3,s1,s0);
or g7(out,y0,y1,y2,y3);

endmodule

--------------------------------------------------------------------------------

