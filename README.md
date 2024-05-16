# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

APPARATUS REQUIRED:

Vivado 2023.1

PROCEDURE:

 1.Open Vivado: Launch Xilinx Vivado software on your computer.
 
 2.Create a New Project: Click on "Create Project" from the welcome page or navigate through "File"
 > "Project" > "New".
 
 3.Project Settings: Follow the prompts to set up your project. Specify the project name, location,
 and select RTL project type.
 
 4.Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on
 "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files
 from the file browser.

 5.Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation
 language (Verilog in this case) and simulation tool (Vivado Simulator).
 
 6.Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch
 the Vivado Simulator and compile your design for simulation.
 
 7.Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set
 automatically. This determines how long the simulation will run.

 8.Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

 9.View Results: After the simulation completes, you can view waveforms, debug signals, and analyze
 the behavior of your design.

**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)


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

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/6743e22d-f3c2-4dc7-a43d-787e1afd4b38)

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/2fd92371-7a17-4f62-a6fe-b7aa1b3cb953)


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

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/039f055a-0d24-4c23-9054-344564d3481e)

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/a4ad80de-c1ae-4ce7-82be-39a7a6a1f6cb)


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

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/d95ad8e2-eea8-4c94-9e9f-db5d396588cf)

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/53eddac2-6802-41ca-ba73-baa69de46309)


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

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/d9b8f92b-36bb-4d16-bd00-2d511ccdbb63)

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/d8c3485c-f722-412b-bb9d-698aa3a0a696)


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

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/68003a30-cd17-4c14-a886-d67876fdbb06)

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/82a5bf2f-d469-46ae-93b0-a5bb22e545b8)


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

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/02d192aa-5d83-4361-8917-d4ffb341e2e6)

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/e7e3ccf7-3df5-48b6-8d39-b7ca38e5adeb)



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

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/3a8e296e-3c6d-4d78-9f2e-fa9bc77e2b56)

![image](https://github.com/lakshanad1306/VLSI-LAB-EXP-4/assets/161121355/8d68aa1e-50b9-4a87-8aa5-2d7d53e09671)


RESULT:

Hence The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023 is done and output verified successfully.


