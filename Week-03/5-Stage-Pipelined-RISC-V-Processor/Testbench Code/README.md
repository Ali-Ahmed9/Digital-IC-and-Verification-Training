## Here is the Testbench code.

## SystemVerilog Code:

module pipelineTop_tb;

logic clk;
logic reset;

pipelineTop DUT(

    .clk(clk),
    .reset(reset)

);

//////////////////////////////////////////////////////////

initial
begin

    clk = 0;

    forever #5 clk = ~clk;

end

//////////////////////////////////////////////////////////

initial
begin

    reset = 1;

    #20;

    reset = 0;

end

//////////////////////////////////////////////////////////

always @(posedge clk)
begin

$display("---------------------------------------------");

$display("Time = %0t",$time);

$display("PC                = %d",DUT.pc);

$display("Instruction       = %h",DUT.instruction);

$display("ReadData1         = %d",DUT.readData1);

$display("ReadData2         = %d",DUT.readData2);

$display("Immediate         = %d",DUT.immediate);

$display("ALU Result        = %d",DUT.aluResult);

$display("Memory Read Data  = %d",DUT.memoryReadData);

$display("Write Back Data   = %d",DUT.writeBackData);

end

//////////////////////////////////////////////////////////

initial
begin

    #1000;

    $finish;

end

endmodule


=========================================================
