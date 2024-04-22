# VLSI-LAB-EXP-4
SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

APPARATUS REQUIRED:
     Xilinx 14.7
     Spartan6 FPGA

PROCEDURE:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

**LOGIC DIAGRAM**

SR FLIPFLOP

![301740946-77fb7f38-5649-4778-a987-8468df9ea3c3](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/4e11d72e-7401-4fa7-9e17-977a8e5c056a)

JK FLIPFLOP

![301743103-1510e030-4ddc-42b1-88ce-d00f6f0dc7e6](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/20ec58e1-ff7d-48ad-896f-325fd15b9978)

T FLIPFLOP

![301743290-7a020379-efb1-4104-85ee-439d660baa08](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/f59a93a1-c4a1-4f0d-b8ec-59afae83aaba)


D FLIPFLOP

![301743389-dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/061329ff-7ea8-4011-88a0-a346b84b7329)

COUNTER

![301743514-a1fc5f68-aafb-49a1-93d2-779529f525fa](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/48d8dfc6-1504-43fc-8178-4baca02ac055)


VERILOG CODE

# D Flip Flop
```
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
```
# JK Flip Flop
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# SR Flip Flop
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# T Flip Flop
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
# Ripple Carry Counter
```
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
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
# MOD 10 Counter
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```
UP-DOWN COUNTER

VERILOG CODE:
```
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
```

OUTPUT WAVEFORM

# D Flip Flop

![324338612-16eaae0c-044c-4e5b-a12c-d819fcd455f4](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/c69130e3-a98b-4e74-8d93-00fd9a28adee)

<img width="962" alt="324343987-72ae525c-06de-47e7-bc16-6975cee06f25" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/8dcd27b3-b314-44e0-98b3-4ca014a3f29f">

# JK Flip Flop

![324338647-b91e64d4-589d-42c8-98f8-e0defd8d8167](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/9ac25e31-d982-4048-801f-34c8e60e4a15)

<img width="962" alt="324343845-4e699ef4-69e7-48cf-96ed-c19502876284" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/db0d3db0-bc32-4390-b6f7-9e73cb218cd8">

# SR Flip Flop

![324338686-ac45a8ed-2c8a-4688-ad43-2cac9b51106e](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/0d97e53a-3527-4823-b4ab-38272498b06c)

<img width="962" alt="324343676-d2d32841-0693-4964-881d-08f9ec15fb7b" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/d11d0554-21eb-4149-b27c-2cfc51b85b42">

# T Flip Flop

![324338729-883e3448-3fcb-4cb6-b2d8-843afe8704fd](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/8efaa494-0b44-47b6-ad6e-91cea49a5587)

<img width="962" alt="324343615-05ca7d14-49d2-4b53-b97f-2b8464ffb28b" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/c7c6823d-c6d0-4f28-b517-85b10bbd58b1">

# MOD-10 Counter

<img width="962" alt="324344088-68ca3a3d-432a-4acd-bca7-8e566b06f98f" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/d3e95591-8f66-43c6-883f-2db39ae45171">

<img width="962" alt="324344112-96a0dae3-a178-4ef5-8af1-056c7effd627" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/3617b0e2-e8e2-4b09-bbd2-9f41a2e7daab">

# Ripple Carry Counter

<img width="962" alt="324344223-66cfbd77-8a37-413a-8f55-1e034eb051bf" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/d54c5740-b120-4b02-a412-9c9e99b59a37">

<img width="962" alt="324344265-34cd41d4-b988-4cb4-b548-0a269e53c100" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/526b194a-682f-4dc9-af1f-38d8ac487508">

# UP Down Counter

<img width="617" alt="324343532-4093e481-68ab-4d30-8cd5-a91b2933dcdc" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/22c82bbc-4741-4d42-a438-598b1bcab13c">

<img width="962" alt="324343572-10b19508-5408-46d8-a279-81fdaf7eb2d5" src="https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/6e3117fd-23a2-4993-bf44-c2db45b62240">

RESULT

Thus the simulation and implementation of sequential logic gates is done and verified.

