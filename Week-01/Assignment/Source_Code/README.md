## Problem Statment
The Cola Vending Machine must satisfy the following specifications:
  •  Machine dispenses one can of cola for exactly Rs. 15/-
  •  Accepted coin denominations: Rs. 5/- and Rs. 10/- only
  •  Machine does NOT provide any change back to the user
  •  Machine automatically resets to initial state after the can is dispensed
  •  Design must use Finite State Machine (FSM) approach in Verilog HDL

=========================================================================

## Verilog Code of Cola Vending Machine

// Cola Vending Machine

module vending_machine (
    input  clk,           
    input  rst,         
    input  coin5,        
    input  coin10,        
    output reg dispense   
);

// State encoding
parameter S0 = 2'b00;  
parameter S1 = 2'b01;  
parameter S2 = 2'b10;  
parameter S3 = 2'b11;  

reg [1:0] state;        
reg [1:0] next_state;   

// BLOCK 1: State Register (Sequential)
always @(posedge clk or posedge rst) begin
    if (rst)  state <= S0;
    else      state <= next_state;
end

// BLOCK 2: Next State Logic (Combinational)
always @(state or coin5 or coin10) begin
    next_state = state;
    case(state)
        S0: begin
            if      (coin10) next_state = S2;
            else if (coin5)  next_state = S1;
            else             next_state = S0;
        end
        S1: begin
            if      (coin10) next_state = S3;
            else if (coin5)  next_state = S2;
            else             next_state = S1;
        end
        S2: begin
            if (coin10 || coin5) next_state = S3;
            else                 next_state = S2;
        end
        S3: begin
            next_state = S0;   // auto reset after dispense
        end
        default: next_state = S0;
    endcase
end

=========================================================================
// BLOCK 3: Output Logic (Moore — state only)
always @(state) begin
    if (state == S3) dispense = 1;
    else             dispense = 0;
end

endmodule

=========================================================================
