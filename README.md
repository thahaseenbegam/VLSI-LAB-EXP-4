SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS
AIM:
  To simulate and implement SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using VIVADO 2023.2.

APPARATUS REQUIRED:
  VIVADO 2023.2

PROCEDURE:

STEP:1 Launch the Vivado 2023.2 software.
STEP:2 Click on “create project ” from the starting page of vivado.
STEP:3 Choose the design entry method:RTL(verilog/VHDL).
STEP:4 Crete design source and give name to it and click finish.
STEP:5 Write the verilog code and check the syntax.
STEP:6 Click “run simulation” in the navigator window and click “Run behavioral simulation”.
STEP:7 Verify the output in the simulation window.

SR Flipflop:
Logic Diagram:
image VERILOG CODE:

module sr(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @ (posedge clk)
begin 
if (rst==1)
q=1'b0;
else
begin
case ({s,r})
2'b00: q = q;
2'b01: q = 1'b0;
2'b10: q = 1'b1;
2'b11: q = 1'bx;
endcase
end
end
endmodule
OUTPUT WAVEFORM:

Screenshot 2024-04-06 111951

JK Flipflop:
Logic Diagram:
image

VERILOG CODE:
module jk(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @ (posedge clk)
begin 
if (rst==1)
q=1'b0;
else
begin
case ({j,k})
2'b00: q = q;
2'b01: q = 1'b0;
2'b10: q = 1'b1;
2'b11: q = ~q;
endcase
end
end
endmodule
OUTPUT WAVEFORM:

Screenshot 2024-04-06 112629

T Flipflop:
Logic Diagram:
image

VERILOG CODE:
module t(t,clk,rst,q);
input t,clk,rst;
output reg q;
always @ (posedge clk)
begin 
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
OUTPUT WAVEFORM:

Screenshot 2024-04-06 111656

D Flipflop:
Logic Diagram:
image

VERILOG CODE:
module d(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @ (posedge clk)
begin 
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
OUTPUT WAVEFORM:

Screenshot 2024-04-06 112153

Counter:
Logic Diagram:
image

Updown Counter:
Verilog code:
module updowncounter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always @(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if (updown==1)
out=out+1;
else
out=out-1;
end
endmodule
OUTPUT WAVEFORM:

Screenshot 2024-04-02 133943

Mod 10 Counter:
VERILOG CODE:
module mod10counter(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always @(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
OUTPUT WAVEFORM:

Screenshot 2024-04-02 135812

Ripple Carry Counter:
VERILOG CODE:
module ripplecounter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tff0(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule

module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
OUTPUT WAVEFORM:

image

RESULT:

  Thus the simulation of sequential circuits is done and outputs are verified successfully.
