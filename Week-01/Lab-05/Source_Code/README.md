Source Code of Lab 5:
Lab Task: You will be performing the simulations on Vivado.
=========================================================================
1.  Design a sequence recognizer that gives output Z=1 when it recognize a sequence “1011” in a single-bit input stream A.
 Make a non-overlapping machine that resets once a valid sequence is detected.

## Verilog Code for sequence Recognizer (1011):

// Sequence Recognizer : 1011..........

module seq_rec (input  clk,  input  rst,  input  A,        output reg Z );

// Define State Names....
parameter S0 = 3'b000; 
parameter S1 = 3'b001;
parameter S2 = 3'b010; 
parameter S3 = 3'b011; 
parameter S4 = 3'b100; 

reg [2:0] state;
reg [2:0] next_state;

// BLOCK 1 — STATE REGISTER

always @(posedge clk or posedge rst) begin

    if (rst)
        state <= S0;
    else
        state <= next_state;

end

// BLOCK 2 — next logic state , ehrere to go right now ??

always @(state or A) begin

    next_state = S0;

    case(state)
        S0: begin
            if (A == 1)
                next_state = S1; 
            else
                next_state = S0; 
        end
        S1: begin
            if (A == 0)
                next_state = S2; 
            else
                next_state = S1; 
        end

        S2: begin
            if (A == 1)
                next_state = S3;
            else
                next_state = S0; 
        end

        S3: begin
            if (A == 1)
                next_state = S4; 
            else
                next_state = S2;
        end

        S4: begin
            next_state = S0;
        end
        default: next_state = S0;

    endcase
end

// BLOCK 3 — output logic

always @(state) begin

    if (state == S4)
        Z = 1; 
    else
        Z = 0; 

end

endmodule


=========================================================================

2.	 Design a decade counter that counts from (0)10 to (9)10 and then goes back to (0)10.
 Counter uses Clock and Reset as input and outputs are the counting number. You are suppoed to use a synchronous Reset.

## Verilog Code Decade Counter:

module decade_counter(input clk, input reset, output reg [3:0] count);

// State Encoding
parameter S0 = 4'd0,
          S1 = 4'd1,
          S2 = 4'd2,
          S3 = 4'd3,
          S4 = 4'd4,
          S5 = 4'd5,
          S6 = 4'd6,
          S7 = 4'd7,
          S8 = 4'd8,
          S9 = 4'd9;

reg [3:0] current_state;
reg [3:0] next_state;


always @(*)
begin
    count = current_state;
end


always @(*)
begin
    case(current_state)

        S0 : next_state = S1;
        S1 : next_state = S2;
        S2 : next_state = S3;
        S3 : next_state = S4;
        S4 : next_state = S5;
        S5 : next_state = S6;
        S6 : next_state = S7;
        S7 : next_state = S8;
        S8 : next_state = S9;
        S9 : next_state = S0;

        default : next_state = S0;

    endcase
end
always @(posedge clk)
begin
    if(reset == 1'b1)
        current_state <= S0;
    else
        current_state <= next_state;
end

endmodule

=========================================================================
3.	 Consider the case of a circuit to detect a series of three consecutive 1's (111) or 0's (000) in the single-bit input,
stream B. That is, the input will be a series of random 1’s and 0’s. If three consecutive ones or zeros are detected,
the output Z should go high, else it should remain low. Make an overlapping machine which does not reset 
after detecting a correct pattern.

## Verilog Code of Consecutive 111 or 000 Detector:

// Consecutive 111 or 000 Detector
// Moore FSM — Overlapping


module consecutive_detector (input  clk,      input  rst,  input  B,  output reg Z);
// Defining state names 
parameter S0 = 3'b000; 
parameter S1 = 3'b001; 
parameter S2 = 3'b010; 
parameter S3 = 3'b011; 
parameter S4 = 3'b100; 
parameter S5 = 3'b101; 
parameter S6 = 3'b110; 
reg [2:0] state;
reg [2:0] next_state;

// BLOCK 1 — STATE REGISTER
always @(posedge clk or posedge rst) begin

    if (rst)
        state <= S0;
    else
        state <= next_state;
end


// BLOCK 2 — NEXT STATE LOGIC

always @(state or B) begin

    next_state = state;
    case(state)

        S0: begin
            if (B == 1)
                next_state = S1; 
            else
                next_state = S4; 
        end

        S1: begin
            if (B == 1)
                next_state = S2; 
            else
                next_state = S4; 
        end
        S2: begin
            if (B == 1)
                next_state = S3; 
            else
                next_state = S4; 
        end
        S3: begin
            if (B == 1)
                next_state = S3; 
            else
                next_state = S4; 
        end
        S4: begin
            if (B == 0)
                next_state = S5; 
            else
                next_state = S1; 
        end

        S5: begin
            if (B == 0)
                next_state = S6; 
            else
                next_state = S1;
        end

        // overlapping 
        S6: begin
            if (B == 0)
                next_state = S6; 
            else
                next_state = S1;
        end

        default: next_state = S0;

    endcase
end

// BLOCK 3 — OUTPUT LOGIC

always @(state) begin

    if (state == S3 || state == S6)
        Z = 1; 
    else
        Z = 0; 

end

endmodule


=========================================================================

