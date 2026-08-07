TestBench Code Vending Machine
=========================================================================

module tb_vending_machine;
    reg clk;
    reg rst;
    reg coin5;
    reg coin10;
   
    wire dispense;
    vending_machine uut (.clk(clk), .rst(rst), .coin5(coin5), .coin10(coin10), .dispense(dispense));
  
    initial clk = 0;
    always #10 clk = ~clk;

    initial begin

        rst    = 1;
        coin5  = 0;
        coin10 = 0;
        #20;       
        rst = 0;    

        // insert Rs.5 coin
        coin5 = 1; coin10 = 0;
        #20;               
        coin5 = 0;        
        #20;             

        // insert Rs.5 coin again
        coin5 = 1; coin10 = 0;
        #20;
        coin5 = 0;
        #20;
        
        // insert Rs.5 coin third time
        // this makes Rs.15 ? dispense!
        coin5 = 1; coin10 = 0;
        #20;
        coin5 = 0;
        #20;               
        #20;              
  
        // Test 2: Rs.10 + Rs.5 = Rs.15

        // insert Rs.10 coin
        coin5 = 0; coin10 = 1;
        #20;
        coin10 = 0;
        #20;
        // insert Rs.5 coin
        // this makes Rs.15 ? dispense!
        coin5 = 1; coin10 = 0;
        #20;
        coin5 = 0;
        #20;
        #20;
        // Test 3: Rs.5 + Rs.10 = Rs.15
        coin5 = 1; coin10 = 0;
        #20;
        coin5 = 0;
        #20;

        coin5 = 0; coin10 = 1;
        #20;
        coin10 = 0;
        #20;
        #20;

        // Test 4: Rs.10 + Rs.10 = Rs.20

        coin5 = 0; coin10 = 1;
        #20;
        coin10 = 0;
        #20;

        =========================================================================
        coin5 = 0; coin10 = 1;
        #20;
        coin10 = 0;
        #20;
        #20;
        $finish;
    end
endmodule
