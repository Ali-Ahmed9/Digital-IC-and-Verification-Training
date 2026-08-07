TestBench codes of Lab 3:
-------------------------------------------------------------------------------

## Testbench Code of 2*4 decoder:
module decoder2x4_tb();
reg a0, a1;         
wire D0, D1, D2, D3;
decoder2x4 uut(.A0(a0), .A1(a1),.D0(D0), .D1(D1), .D2(D2),.D3(D3));       
initial begin
    a1 = 0; a0 = 0; #5;
    a1 = 0; a0 = 1; #5;
    a1 = 1; a0 = 0; #5;
    a1 = 1; a0 = 1; #5; 
end
endmodule

Same test bench for the part (b).

----------------------------------------------------------------------------------

## TestBench Code of 8*1 Mux:
module mux8x1_tb();

reg I0, I1, I2, I3, I4, I5, I6, I7;
reg S2, S1, S0;
wire Y;

mux8x1 uut(.I0(I0), .I1(I1), .I2(I2), .I3(I3),.I4(I4), .I5(I5), .I6(I6), .I7(I7),.S2(S2), .S1(S1), .S0(S0),.Y(Y));

initial
begin
    I0=0; I1=1; I2=0; I3=1;
    I4=0; I5=1; I6=0; I7=1;
    S2=0; S1=1; S0=0;   
    #10;


    I0=1; I1=0; I2=1; I3=0;
    I4=1; I5=1; I6=0; I7=0;
    S2=1; S1=0; S0=1;   
    #10;

  
    I0=0; I1=0; I2=1; I3=1;
    I4=0; I5=0; I6=1; I7=1;
    S2=1; S1=1; S0=0;   
    #10;

    $finish;

end

endmodule

----------------------------------------------------------------------------------

## Testbench Code 4 bit Subtractor:

module subtractor4_tb();

reg [3:0] A;
reg [3:0] B;
wire [3:0] Diff;
wire Borrow;

subtractor4 uut(.A(A),.B(B),.Diff(Diff),.Borrow(Borrow));

initial
begin
    A = 4'd12;
    B = 4'd5;
    #10;
    
    A = 4'd3;
    B = 4'd9;
    #10;

    $finish;

end
endmodule

-----------------------------------------------------------------------------

## TestBench Code of 4 bit BCD:

module bcd_div4_tb();

reg [3:0] A;
wire Z;

bcd_div4 uut(.A(A),.Z(Z));
initial
begin

A=4'b0000; #10;
A=4'b0001; #10;
A=4'b0010; #10;
A=4'b0011; #10;
A=4'b0100; #10;
A=4'b0101; #10;
A=4'b0110; #10;
A=4'b0111; #10;
A=4'b1000; #10;
A=4'b1001; #10;
A=4'b1010; #10;
A=4'b1011; #10;
A=4'b1100; #10;
A=4'b1101; #10;
A=4'b1110; #10;
A=4'b1111; #10;

$finish;

end

endmodule 

------------------------------------------------------------------------------------


