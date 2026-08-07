Lab Tasks: You can only use Gate-Level Modeling in this Lab.
=========================================================================

1.	[In-Lab Task] Design a half adder using gate-level modeling.
   a.	Verify the truth table in Vivado simulator

## Figure: Half Adder Gate level Design.
<img width="395" height="145" alt="image" src="https://github.com/user-attachments/assets/5d1a5849-907a-4116-990c-2cb1bca6a56e" />

 ## Verilog Code for Half Adder
module half_gate( input A, B, output S,C);
xor g1 (S,A,B);
and g2 (C,A,B);

endmodule

F
=========================================================================

b.	Design a full adder using two half adders using hierarchical modeling
and other primitive logic (if required). Verify the following truth table in Vivado simulator.
Simulation should show output of all possible inputs.

### Figure: Full Adder Gate level Design using two Half Adder.
<img width="471" height="160" alt="image" src="https://github.com/user-attachments/assets/8b6702b7-fa75-473d-95cd-06a81cf6a95f" />


## Verilog code for full adder:
module full_adder ( input A,B,Cin,output Sum, Cout);
   
wire S1, C1, C2;  
   
    half_gate HA1 (.A(A),.B(B), .S(S1),.C(C1));
    half_gate HA2 (.A(S1),.B(Cin),.S(Sum), .C(C2));
    or g3 (Cout, C1, C2);
endmodule

=========================================================================

2.	[In-Lab Task] Design a 2×1 multiplexers using gate-level modeling.
   a.	Verify the following truth table in Vivado simulator (no need to upload the simulation).
  	
## Figure: 2*1 Mux Gate level Design.
<img width="241" height="239" alt="image" src="https://github.com/user-attachments/assets/bc508ce6-bd44-4305-b9c6-1d822cef840a" />

  ## Verilog Code for 2*1 Mux
module mux2_1(input i1,i2,s, output y);
wire w1,w2,ns;
assign ns=~s;
and g1 (w1,i1,ns);
and g2 (w2,i2,s);
or g3 (y,w1,w2);
endmodule

=========================================================================

b.	Design and simulate 4×1 multiplexer using 2×1 multiplexers shown in Figure 4 and
simulate with at least 4 random input combinations of data and control inputs. 
Record your random combinations and possible value for the output “out”.

## Figure 4: 4×1 Multiplexer using Hierarchical Design
<img width="384" height="279" alt="image" src="https://github.com/user-attachments/assets/f04a2c92-0d8e-49f3-87b7-e691fbd1ed51" />


## Verilog code of 4*1 Mux:
module mux4_1( input i1,i2,i3,i4,s1,s2, output out);
 wire w1,w2;
 
 mux2_1 mux1 (.i1(i1),.i2(i2),.s(s1),.y(w1));
 mux2_1 mux2 (.i1(i3),.i2(i4),.s(s1),.y(w2));
 mux2_1 mux3 (.i1(w1),.i2(w2),.s(s2),.y(out));
endmodule


=========================================================================

3.	[In-Lab Task] Design and simulate a 3×8 Decoder with Enable shown in Figure 5
	 using the 1×2 decoder as shown in Figure 6 and the 2×4 decoders created in DSD Lab-2.
	 Show your work/steps. Record your random combinations and possible value for the output “out”.

## Figure 5: 3*8 Line decoder
<img width="687" height="456" alt="image" src="https://github.com/user-attachments/assets/01df734e-b411-499f-aa20-fccd98919580" />

## Figure 6: 1 2 Line Decoder with Enable
<img width="424" height="88" alt="image" src="https://github.com/user-attachments/assets/1149fcd1-ee84-4632-950a-a5cad24dcdec" />

## Verilog Code for 1*2 Decoder:
module decoder1_2(input a0, en,output d0, d1);

    wire na0;
    assign na0 = ~a0;
    
    and g1 (d0, na0, en);
    and g2 (d1, a0, en);
endmodule


## Verilog Code for 2*4 Decoder
module decoder2_4(input a0, a1, en,output d0, d1, d2, d3);
    wire na0, na1;
    
    assign na0 = ~a0;
    assign na1 = ~a1;
    
    and g1 (d0, na0, na1, en);
    and g2 (d1, na0, a1, en);
    and g3 (d2, a0, na1, en);  
    and g4 (d3, a0, a1, en);
endmodule


## Verilog Code for 3*8 Decoder:
module decoder3_8(input a0, a1, a2, en, output d0, d1, d2, d3, d4, d5, d6, d7);
wire w1, w2;  
decoder1_2 dec1 (.a0(a2),.en(en),.d0(w1),.d1(w2)); 
decoder2_4 dec2 (.a0(a0), .a1(a1), .en(w1), .d0(d0), .d1(d1),  .d2(d2),.d3(d3));   
decoder2_4 dec3 (.a0(a0),.a1(a1), .en(w2), .d0(d4), .d1(d5),.d2(d6),.d3(d7));  
endmodule

=========================================================================

4.	[In-Lab Task] Design and stimulate 16-bit adder using full adder module designed in Task-1(b).
 The adder takes 16-bit Inputs A and B and a Carry-In input and generates 16-bit output S
 and a Carry-Out ouput. Make the high-level block diagram of the module and show your
working/steps. Upload simulation results for any 4 random values for the data inputs A and B.

## Verilog code of Full Adder:
module full_adder ( input A,B,Cin,output Sum, Cout);
   
wire S1, C1, C2;  
   
    half_gate HA1 (.A(A),.B(B), .S(S1),.C(C1));
    half_gate HA2 (.A(S1),.B(Cin),.S(Sum), .C(C2));
    or g3 (Cout, C1, C2);
endmodule

## Verilog Code of 4-bit Adder:
module adder4(input  [3:0] A,input  [3:0] B, input  Cin,output [3:0] Sum,output Cout);
    
wire C1, C2, C3;

full_adder FA0(.A(A[0]),.B(B[0]),.Cin(Cin),.Sum(Sum[0]),.Cout(C1));
    
full_adder FA1(.A(A[1]),.B(B[1]),.Cin(C1),.Sum(Sum[1]),.Cout(C2));  

full_adder FA2(.A(A[2]),.B(B[2]),.Cin(C2),.Sum(Sum[2]), .Cout(C3));

full_adder FA3(.A(A[3]),.B(B[3]),.Cin(C3),.Sum(Sum[3]),.Cout(Cout));

endmodule

## Verilog Code of 16-bit Adder:
module adder16(input  [15:0] A,input  [15:0] B,input  Cin,output [15:0] Sum,output Cout);
wire C1, C2, C3;

adder4 ADD0( .A(A[3:0]),.B(B[3:0]),.Cin(Cin),.Sum(Sum[3:0]),.Cout(C1)); 

adder4 ADD1(.A(A[7:4]),.B(B[7:4]),.Cin(C1),.Sum(Sum[7:4]),.Cout(C2));

adder4 ADD2(.A(A[11:8]),.B(B[11:8]),.Cin(C2),.Sum(Sum[11:8]),.Cout(C3));

adder4 ADD3(.A(A[15:12]),.B(B[15:12]),.Cin(C3),.Sum(Sum[15:12]),.Cout(Cout));
    
endmodule

=========================================================================

