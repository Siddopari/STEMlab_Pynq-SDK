## About this tutorial 
:stopwatch: 20 min

**Key learnings:**

* Simulate a custom logic using Vivado Xsim

* Use VHDL testbench for stimulus generation

* Use TCL script for stimulus for stimulus generation

**Description**:

In this tutorial we are going to simulate the operation of custom VHDL counter. Behavioural simulation is a key procedure to test and debug custom FPGA logic, which is strongly recommended before synthesis, implementation and hardware deployment. Note that this is an additional step not required in software development, where (in opposite to FPGA logic) compilation is typically completed after a few seconds and it is simple to perform runtime debugging. 

## Open Vivado Design
In this case we are not going to create a new design, instead we are going to simulate the VHDL counter that is part of the [LED blink](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/LED-blink) Vivado project. 

## Vivado Simulator
The following discussion covers two different methods to simulate the [counter.vhd](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/hdl/counter.vhd) module. Namely, by creating and executing a testbench or by using TCL stimulus. 






## Create a test bench


### Select top simulation file
Since we only want to simulate the [counter.vhd](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/hdl/counter.vhd) module, we have to make sure that it is set as the *Top* simulation file. 

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/behavioural-simulation/set_top.png" width="1000"/>

## Vivado Simulator
The Vivado toolchain allows you to simulate your logic at different points of the build process:
 * **Behavioural simulation**: *ideal* simulation, only based on the provided RTL (Verilog, VHDL...) code.
 * **Post-synthesis simulation**: simulation of the RTL code when converted to actual FPGA logic building blocks (Flip-Flops, LUTs...). 
 * **Post-implementation simulation**: simulation of the RTL code when converted to actual FPGA logic building blocks and placed within the specified FPGA chip. 

For most application it is sufficient to verify your logic via **behavioural simulations**. Vivado has built-in mechanisms that raise an error if synthesis and implementation fail (e.g. when the requested logic cannot meet timing constraints, when the requested resources are not available in the specified FPGA chip...).


Start the integrated Vivado behavioural simulator. 


