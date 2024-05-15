
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1.

# APPARATUS REQUIRED:

Vivado 2023.1

**LOGIC DIAGRAM**

# SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


# JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)


# T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)



# D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


# COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)



# PROCEDURE:
1.Open Vivado: Launch Xilinx Vivado software on your computer.
2.Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".
3.Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.
4.Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.
5.Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).
6.Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.
7.Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.
8.Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.
9.View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

# D-FLIP FLOP
VERILOG CODE
~~~
module Dflipflop(D,clk,reset,Q);
input D;
input clk;
input reset;
output reg Q;
always @(posedge clk)
begin
 if(reset==1'b1)
  Q <= 1'b0;
 else
  Q <= D;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329915856-03e5b43e-8fd1-42db-bec9-d8e1cd6342b0" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/1f386a4d-4941-4a17-a9b2-2738aee014a4">


<img width="962" alt="329915890-3b92b980-ac92-4606-a838-c6d9648e3a01" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/f42c707a-82b2-48c6-a989-ed8efd720ac7">


# JK FLIP FLOP

VERILOG CODE:
~~~
module JK_flipflop (q, q_bar, j,k, clk,reset);
input j,k,clk, reset;
output reg q;
output q_bar;
always@(posedge clk)
begin
  if(!reset)        
    q <= 0;
  else 
  begin
      case({j,k})
        2'b00: q <= q;    // No change
        2'b01: q <= 1'b0; // reset
        2'b10: q <= 1'b1; // set
        2'b11: q <= ~q; // Toggle
      endcase
  end
end
assign q_bar = ~q;
endmodule
~~~

# OUTPUT:
<img width="962" alt="329915958-4a094ca4-dfb9-47e5-8a78-b95b280128cf" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/094edd5f-6d7b-4184-8dd9-d2c33d505dd0">

<img width="962" alt="329916044-8e770e54-6496-4f60-85cb-b508304bc995" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/777b0a35-e1a9-4c27-b20a-ae4bbec0bee1">



# MOD-10 COUNTER

VERILOG CODE:
~~~
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329916097-35aedae2-4db5-4e7d-8adf-6c4fd4293013" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/ab8e40a8-37eb-4ff4-9b37-0f627dcdf177">


<img width="962" alt="329916128-01a592b8-068c-4dca-be79-f060cf02930f" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/d317a63e-cde4-4842-ba48-d2cc09d1c754">



# RIPPLE CARRY COUNTER

VERILOG CODE:
~~~
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule
module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule
module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf0(q[0],clk,rst);
tff tf1(q[1],q[0],rst);
tff tf2(q[2],q[1],rst);
tff tf3(q[3],q[2],rst);
endmodule
~~~

# OUTPUT:
![Upload<img width="962" alt="329916212-af913a78-3179-4fbb-b0e6-ee33c1efb1cf" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/02a1c356-4f63-4272-981c-af38b53e7c0c">

<img width="962" alt="329916212-af913a78-3179-4fbb-b0e6-ee33c1efb1cf" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/a05f34eb-81c7-4ea3-9091-88c309751777">


# SR FLIP FLOP

VERILOG CODE:
~~~
module sr_flipflop(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
~~~

# OUTPUT:

<img width="962" alt="329916278-bdee999f-58b1-4a98-95a8-11411516bdc3" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/357d9396-7c6a-4214-98ff-9e965d813e56">


<img width="962" alt="329916308-26a92567-0cf6-41da-ac9d-d5afc43d865d" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/989ccc3e-546d-4012-af0b-5b8c3299afb9">

# T FLIP FLOP

VERILOG CODE:
~~~
module T_flipflop(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
~~~

# OUTPUT:
<img width="962" alt="329916401-64d9a351-3be8-4bb5-9b09-40ec166f94be" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/081f014e-caff-46de-8fca-6ea91cb7f2b8">

<img width="962" alt="329916437-6540708a-a079-4138-a05d-a326b34277fa" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/3523845b-4096-49e1-b176-75a5621dc8a9">

# UP-DOWN COUNTER

VERILOG CODE:
~~~
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
~~~

# OUTPUT:

<img width="617" alt="329916515-530d78ab-9c07-4497-b308-fea125c000c3" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/9c73a3cf-9306-4670-b0dc-8272b8eb96b8">

<img width="962" alt="329916546-9b5a2a72-aaf6-451b-ac4d-d2774f326aaf" src="https://github.com/Vishnu782/VLSI-LAB-EXP-4/assets/102226356/a00eb47e-fff1-4696-9c80-82054fe52383">

# RESULT:
Hence The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023 is done and output verified successfully.
