## About this tutorial 
:stopwatch: 20 min

**Key learnings:**

* Simulate a custom logic using Vivado Xsim

* Use RTL testbench 
* Use TCL script for stimulus for stimulus generation

**Description**:

In this tutorial we are going to simulate the operation of custom VHDL counter. Behavioural simulation is a key procedure to test and debug custom FPGA logic, which is strongly recommended before synthesis, implementation and hardware deployment. Note that this is an additional step not required in software development, where (in opposite to FPGA logic) compilation is typically completed after a few seconds and it is simple to perform runtime debugging. 

## Open Vivado Design
In this case we are not going to create a new design, instead we are going to simulate the VHDL counter that is part of the [LED blink](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/LED-blink) Vivado project. 

## Vivado Simulator
The Vivado toolchain allows you to simulate your logic at different points of the build process:
 * **Behavioral simulation**: *ideal* simulation, only based on the provided RTL (Verilog, VHDL...) code.
 * **Post-synthesis simulation**: simulation of the RTL code when converted to actual FPGA logic building blocks (Flip-Flops, LUTs...). 
 * **Post-implementation simulation**: simulation of the RTL code when converted to actual FPGA logic building blocks and placed within the specified FPGA chip. 

For most application it is sufficient to verify your logic via **behavioural simulations**. Vivado has built-in mechanisms that raise an error if synthesis and implementation fail (e.g. when the requested logic cannot meet timing constraints, when the requested resources are not available in the specified FPGA chip...).


The following discussion covers two different methods to simulate custom FPGA logic. 
1. Creating and executing an RTL testbench 
2. TCL stimulus. 


## 1. TCL stimulus

* Select top simulation file
Since we only want to simulate the [counter.vhd](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/hdl/counter.vhd) module, we have to make sure that it is set as the *Top* simulation file. 

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/behavioural-simulation/set_top.png" width="1000"/>

* Start the integrated Vivado behavioural simulator by clicking on *SIMULATION --> Run Simulation --> Run Behavioral Simulation*. 

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/behavioural-simulation/start_sim_tcl.png" width="1000"/>









## Simulation comparison
|RTL testbench |TCL stimulus |
|---|---|
| :heavy_check_mark: Standard procedure| :x: Vivado Xsim only procedure |
| :heavy_check_mark: Fast simulation and suited for exhaustive testing| :x:  Slow simulator and suited for simple tests.|
| :heavy_check_mark: Single programming language (Verilog, VHDL...)| :x: Requires to learn/use TCL scripts |
| :x: Requires development of testbench that instantiate the RTL to test| :heavy_check_mark: No testbench required  |
| :x: Slow to write| :heavy_check_mark: Fast and easy to write|
| :x: Testbench is fixed. Changes require to recompile simulation.| :heavy_check_mark: Simulation is entirely based on runtime TCL commands. Recompilation is not needed.|


