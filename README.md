# 4Bit-Up-Down-Asynchronous-Reset-Counter-Synthesis

## Aim:

Synthesize 4Bit-Up-Down-Asynchronous-Reset-Counter design using Constraints and analyse reports, Timing, area and Power.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

◦ SDC (Synopsis Design Constraint) File (.sdc)

   ### Counter.tcl
 ```
read_libs/cadence/install/FOUNDRY-01/digital/90nm/dig/lib/slow.lib
read hdl counter.v
elaborate
read_sdc counter_input_constraint.sdc
syn_generic
report_area
syn_map
report_a
syn_opt
report_area
report_area > counter area.txt
report_power > counter_power.txt
report_gates > counter_cells.rpt
report_timing > counter_timing.txt
write_hdl > counter netlist.v
write_sdc > counter_output_constraints.sdc
 ```
  ### Counter.v
```
`timescale 1ns/1ns
module counter(clk,m,rst,count);
input clk,m,rst;
output reg [3:0] count;
always@(posedge clk or negedge rst)
begin
if (!rst)
count=0;
else if(m)
count=count+1;
else
count=count-1;
end
endmodule
```
  ### Input constraints.sdc
```
create_clock name clk period 2 waveform {01} [get_ports "clk"]
set_clock_transition rise 0.1 [get_clocks "clk"]
set_clock transition fall 0.1 [get_clocks "clk"]
set_clock_uncertainty 0.01 [get_ports "clk"]
set_input_delay max 0.8 [get_ports "rst"] -clock [get_clocks "clk"]
set output delay-max 0.8 [get_ports "count"] -clock [get_clocks "clk"]
```
 
 ### Step 2 : Creating an SDC File

•	In your terminal type “gedit input_constraints.sdc” to create an SDC File if you do not have one.

•	The SDC File must contain the following commands;

create_clock -name clk -period 2 -waveform {0 1} [get_ports "clk"]

set_clock_transition -rise 0.1 [get_clocks "clk"]

set_clock_transition -fall 0.1 [get_clocks "clk"]

set_clock_uncertainty 0.01 [get_ports "clk"]

set_input_delay -max 0.8 [get_ports "rst"] -clock [get_clocks "clk"]

set_output_delay -max 0.8 [get_ports "count"] -clock [get_clocks "clk"]

i→ Creates a Clock named “clk” with Time Period 2ns and On Time from t=0 to t=1.

ii, iii → Sets Clock Rise and Fall time to 100ps.

iv → Sets Clock Uncertainty to 10ps.

v, vi → Sets the maximum limit for I/O port delay to 1ps.

### Step 3 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![exp4](https://github.com/user-attachments/assets/5914bbd8-2548-478e-aa77-ef1891ac1140)


#### Area report:
![WhatsApp Image 2025-05-17 at 13 54 05_19002f87](https://github.com/user-attachments/assets/0150f830-1bea-454b-a1ae-0ccdd444954f)



#### Power Report:
![WhatsApp Image 2025-05-17 at 13 54 06_2a95e465](https://github.com/user-attachments/assets/4d06a415-730b-4955-aa05-b7ddeb0bb8c7)


#### Timing Report: 
![WhatsApp Image 2025-05-17 at 13 54 06_f7d2a161](https://github.com/user-attachments/assets/7854dc6a-4e13-4c7e-826b-442df5df8b10)


#### Result: 

The generic netlist has been created, and area, power, and timing reports have been tabulated and generated using Genus.





