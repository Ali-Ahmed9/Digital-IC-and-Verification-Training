## Here is the Testbench code for the RISC-V Single Cycle Processor.
=========================================================

## SystemVerilog Code:

module tb_processorTop();

    // Testbench Signals
    logic clk;
    logic reset;

    // Instantiate the Processor
    processorTop DUT(

        .clk(clk),
        .reset(reset)

    );

    // Clock Generation
    initial
    begin
        clk = 0;

        forever #5 clk = ~clk;
    end

    // Reset Generation
    initial
    begin

        reset = 1;

        #20;

        reset = 0;

    end

    // Stop Simulation
    initial
    begin

        #1000;

        $finish;

    end

endmodule

=========================================================



