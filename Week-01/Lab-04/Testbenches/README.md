TestBench Codes of Lab 4:
===========================================================================
1. ## TestBench Code of ALU :
module tb_alu;

reg [31:0] A;
reg [31:0] B;
reg Cin;
reg [1:0] Opcode;

wire [63:0] Output;

// DUT Instantiation
alu DUT( .A(A), .B(B), .Cin(Cin), .Opcode(Opcode), .Output(Output));
  
initial begin


    // ADD
    A = 20;
    B = 10;
    Cin = 1;
    Opcode = 2'b00;
    #10;

    // SUB
    A = 20;
    B = 10;
    Cin = 0;
    Opcode = 2'b01;
    #10;

    // MUL
    A = 20;
    B = 10;
    Opcode = 2'b10;
    #10;

    // DIV
    A = 20;
    B = 10;
    Opcode = 2'b11;
    #10;

    // DIV by ZERO
    A = 20;
    B = 0;
    Opcode = 2'b11;
    #10;

    $finish;

end

endmodule


============================================================================

2. ## TestBench Code of D- Flipflop :
module tb_dff;

reg clk;
reg en;
reg d;
reg set_n;
reg reset_n;

wire q;
wire q_bar;

// DUT Instantiation
dff DUT(.clk(clk), .en(en), .d(d),.set_n(set_n), .reset_n(reset_n),.q(q),  .q_bar(q_bar));
   
initial begin

    clk = 1'b1;
    forever #10 clk = ~clk;
end


initial
begin

   
    en      = 0;
    d       = 0;

   
    reset_n = 0;
    set_n   = 1;

   
    #15;
    reset_n = 1;

   
    #20;

    set_n = 0;
    #20;

    set_n = 1;
    #20;
  
    en = 1;
    d  = 1;
    #20; 

    d = 0;
    #20;

    en = 0;
    d  = 1;
    #20;

    $finish;

end

endmodule

============================================================================

3. ## TestBench Code of 2 to 4 Counter :

module tb_counter2to4();

reg clk;
wire [2:0] out;
counter2to4 DUT (.clk(clk),.out(out));
initial begin
    clk = 0;
    forever #5 clk = ~clk;
end

endmodule

============================================================================

4. ## TestBench Code of Clock Generation :

module tb_clock_generator;

// Instantiate DUT
clock_generator DUT();

initial
begin
    #100;
    $finish;
end

endmodule

=============================================================================

5. ## TestBench Code of Average of 3 :
`timescale 1ns/1ps

module tb_average3;

reg clk;
reg [3:0] a;
reg [3:0] b;
reg [3:0] c;

wire [4:0] avg;

// DUT Instantiation
average3 DUT( .clk(clk),.a(a), .b(b),.c(c), .avg(avg));

initial begin

    clk = 0;
    forever #10 clk = ~clk;
end

initial
begin

    a = 4'd6;
    b = 4'd9;
    c = 4'd12;
    #20;
   
    a = 4'd3;
    b = 4'd6;
    c = 4'd9;
    #20;
    a = 4'd15;
    b = 4'd12;
    c = 4'd9;
    #20;
    a = 4'd1;
    b = 4'd2;
    c = 4'd3;
    #20;

    $finish;
end
endmodule

===========================================================================================
