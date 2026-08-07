Testbench Code of Lab 5:
=========================================================================
1. ## Testbench Code Sequence Detector: 

module tb_seq_rec();
    reg clk;
    reg rst;
    reg A;
  
    wire Z;

    seq_rec uut (.clk(clk), .rst(rst), .A(A), .Z(Z) );

    initial clk = 0;
    always  #10 clk = ~clk;

    initial begin
    
        rst = 1;
        A   = 0;
        #20; 
        rst = 0;
        A = 1; #20; 
        A = 0; #20; 
        A = 1; #20; 
        A = 1; #20;
        
        #20;        
        A = 0; #20;
        A = 0; #20; 
        A = 0; #20; 
        A = 1; #20; 
        A = 0; #20; 
        A = 1; #20; 
        A = 1; #20; 
        #20;
        A = 0; #20;
        A = 1; #20; 
        A = 1; #20; 
        A = 0; #20; 
        A = 1; #20; 
        A = 1; #20; 
        
        #20;
        A = 0; #20;
        A = 1; #20; 
        A = 0; #20; 
        A = 1; #20; 
        A = 0; #20; 
        A = 1; #20; 
        A = 1; #20; 
        
        #20;
        A = 0; #20;

      
        $finish;
    end

endmodule

=========================================================================

2. ## Testbench Code of Decade Counter : 
module decade_counter_tb();
reg clk;
reg reset;
wire [3:0] count;
decade_counter uut (.clk(clk),  .reset(reset), .count(count) );  
always #5 clk = ~clk;

initial begin
    clk = 0;
    reset = 1;
    #10;
    reset = 0;
    #120;
    reset = 1;
    #10;
    reset = 0;
    #100;
    $finish;
end
endmodule


=========================================================================

3. ## Testbench Code of consecutive_detector 111 /000 : 

module tb_consecutive_detector();

    reg clk;
    reg rst;
    reg B;

    wire Z;
    consecutive_detector uut (.clk(clk), .rst(rst), .B(B), .Z(Z) );

    initial clk = 0;
    always #10 clk = ~clk;

    initial begin

        rst = 1; B = 0;
        #20;
        rst = 0;

        B = 1; #20; // S0?S1
        B = 1; #20; // S1?S2
        B = 1; #20; // S2?S3  Z=1 ?
        B = 1; #20;
       
        B = 0; #20; // S3?S4
        B = 0; #20; // S4?S5
        B = 0; #20; // S5?S6  Z=1 ?

        B = 0; #20; 

        B = 1; #20; 
        B = 0; #20; 
        B = 1; #20; 
        B = 1; #20; 
        B = 1; #20;       
        rst = 1; #20;
        rst = 0;
        $display("After reset state=%b Z=%b",
                  uut.state, Z);

        #40;
        $finish;
    end

endmodule

=========================================================================
