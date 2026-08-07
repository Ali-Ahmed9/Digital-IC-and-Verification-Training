   ## Testbench Codes of Lab 2.
=========================================================================

1. ## Testbench Code for Half Adder: Part (a)

module half_adder_tb();
 reg A,B;
 wire S,C;

half_gate dut (.A(A), .B(B), .S(S), .C(C));

initial begin
A=0;
 B=0;
#10;

A=1'b0; 
B=1;
#10;

A=1;
 B=0;
#10;

A=1;
B=1;
#10;
end
endmodule

=========================================================================
1. ## Tectbench Code for Full Adder : Part (b)

module tb_full_adder;
    reg A, B, Cin;
    wire Sum, Cout;
    
    full_adder uut (.A(A),.B(B),.Cin(Cin),.Sum(Sum),.Cout(Cout));  
    initial begin
        A = 0;
        B = 0; 
        Cin = 0; #10; 
         
        A = 0; 
        B = 0; 
        Cin = 1; #10; 
        
        A = 0; 
        B = 1; 
        Cin = 0; #10;  
        
        A = 0; 
        B = 1; 
        Cin = 1; #10;  
        
        A = 1; 
        B = 0; 
        Cin = 0; #10;  
        
        A = 1; 
        B = 0; 
        Cin = 1; #10; 
        
        A = 1; 
        B = 1; 
        Cin = 0; #10; 
         
        A = 1; 
        B = 1; 
        Cin = 1; #10; 
    end
endmodule

=========================================================================

2. ## Testbench code for 2*1 Mux : Part (a)

module mux2_1_tb();

reg i1,i2,s;
wire y;

mux2_1 dut (.i1(i1),.i2(i2),.s(s), .y(y));

initial begin

    i1 = 0; 
    i2 = 0; 
    s = 0;
    #10;

    i1 = 0; 
    i2 = 1; 
    s = 0;
    #10;

    i1 = 1; 
    i2 = 0; 
    s = 0;
    #10;

    i1 = 1; 
    i2 = 1; 
    s = 0;
    #10;

    i1 = 0; 
    i2 = 0; 
    s = 1;
    #10;

    i1 = 0; 
    i2 = 1; 
    s = 1;
    #10;

    i1 = 1; 
    i2 = 0; 
    s = 1;
    #10;

    i1 = 1; 
    i2 = 1; 
    s = 1;
    #10;

end
endmodule

=========================================================================

2. ## Testbench Code for 4*1 Mux: Part (b)

module mux4_1_tb();

reg i1,i2,i3,i4,s1,s2;
wire out;

mux4_1 dut (.i1(i1),.i2(i2),.i3(i3), .i4(i4),.s1(s1),.s2(s2), .out(out));

initial begin



    i1 = 0; 
    i2 = 0; 
    i3 = 0; 
    i4 = 0;
    s1 = 0; 
    s2 = 0;
    
    #10;
    

    i1 = 0; 
    i2 = 1; 
    i3 = 0; 
    i4 = 0;
    s1 = 0; 
    s2 = 1;
    #10;
    

    i1 = 0; 
    i2 = 1; 
    i3 = 0; 
    i4 = 1;
    s1 = 1; 
    s2 = 0;
    #10;
    

    i1 = 0; 
    i2 = 1; 
    i3 = 0; 
    i4 = 1;
    s1 = 1; 
    s2 = 1;
    #10;
    


end
endmodule

=========================================================================

3. ## Testbench code for 3*8 Decoder:

module decoder3_8_tb();
    reg a0, a1, a2, en;
    wire d0, d1, d2, d3, d4, d5, d6, d7;
    
  
    decoder3_8 dut (.a0(a0),.a1(a1), .a2(a2), .en(en),.d0(d0), .d1(d1), .d2(d2), .d3(d3),
     .d4(d4), .d5(d5), .d6(d6), .d7(d7));
    initial begin
    
        en = 0; 
        a2 = 0; 
        a1 = 0; 
        a0 = 0; #10;
     
        en = 1; 
        a2 = 0; 
        a1 = 0; 
        a0 = 1; #10;
   
        a2 = 0; 
        a1 = 1; 
        a0 = 0; #10;
        
        a2 = 0; 
        a1 = 1; 
        a0 = 1; #10;
        
         a2 = 1; 
        a1 = 0; 
        a0 = 0; #10;
        
         a2 = 1; 
        a1 = 0; 
        a0 = 1; #10;
        
         a2 = 1; 
        a1 = 1; 
        a0 = 0; #10;
        
         a2 = 1; 
        a1 = 1; 
        a0 = 1; #10;
        
        
     
    end
endmodule

=========================================================================

4. ## Testbench Code for 16 bit Adder :
module adder16_tb();

reg  [15:0] A;
reg  [15:0] B;
reg         Cin;
wire [15:0] Sum;
wire        Cout;

adder16 uut (.A(A),.B(B),.Cin(Cin),.Sum(Sum),.Cout(Cout));

initial
begin
    A   = 16'd31;
    B   = 16'd47;
    Cin = 1'b0;
    #10;

    A   = 16'd115;
    B   = 16'd75;
    Cin = 1'b0;
    #10;
    
    A   = 16'd900;
    B   = 16'd500;
    Cin = 1'b1;
    #10;

    A   = 16'd65535;
    B   = 16'd1;
    Cin = 1'b0;
    #10;

    $finish;
end
endmodule

=========================================================================
