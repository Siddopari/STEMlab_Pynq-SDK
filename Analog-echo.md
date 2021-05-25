## About this tutorial 
:stopwatch: 20 min

**Key learnings:**

* Interface the 125 MSa/s ADCs and DACs of the Redpitaya-125-14.

* Build a simple AXI stream module. 

**Description:** 

In this tutorial we are going to build a simple analog echo design, where the analog inputs IN1 and IN2 are forwarded to the analog outputs OUT1 and OUT2, respectively. In between, we add an offset control module, which is configured through a PYNQ Jupyter Notebook.

## Building the Vivado Design
### Create a new Vivado Project
Follow the steps in [LED blink](../LED-blink#create-a-new-vivado-project) and name it *analog_echo*. 

### Create a new Vivado Project
Follow the steps in [LED blink](../LED-blink#create-a-new-vivado-project) and name it *analog_echo*. 

### Import the Redpitaya-125-14 IP library
After creating a new project, we have to add the IP repository that has been created to simplify the use of analog frontends of the Redpitaya-125-14:
* Go to the left panel click on *Project Manager --> Settings*. 
* Navigate to *IP --> Repository*.
* Add the repository *\<FPGA-Notes-for-Scientists\>/ip*.

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/add_ip.PNG" width="450"/>

### Block Design
* Create a new block design.
* Create an instance of the following IPs:
    * ZYNQ7 Processing System
    * AXI GPIO
    * Redpitaya-125-14-clk
    * Redpitaya-125-14-adc
    * Redpitaya-125-14-dac


* Connect the clocks as shown in the diagram below. 
   * We use *clk_125*, which operates at 125MHz, to drive the main logic of the design. All data paths in this tutorial will be synchronous to this clock. 
   * We connect *clk_250_m150* and *clk_250_m120* to the DAC only. They operate at 250Mhz and are phase locked to *clk_125* with a relative phase shift of -150 deg and -120 deg.  

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/connect_clk.PNG" width="1000"/>

* Instantiate a *Processor System Reset* IP and connect the external input to *Redpitaya-125-14-clk/locked* and use the *...aresetn* output as a source for the resets of this designs
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/reset.PNG" width="1000"/>


* Configure the AXI GPIO to have a dual 16-bit output.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/axi_gpio.PNG" width="450"/>

### AXI stream offset module

***
:information_source: If this is first time you are dealing with an AXI stream interface, I recommend to go over [this](http://fpgasite.blogspot.com/2017/07/xilinx-axi-stream-tutorial-part-1.html) blog. For more details, you can have a look at the [AXI Reference Guide UG761](https://www.xilinx.com/support/documentation/ip_documentation/ug761_axi_reference_guide.pdf).
***

* Within the left panel go to *Project Manager --> Add sources* and select  *Add or create design sources*
* I will omit the creation of a HDL file, which was explained in [LED blink](../LED-blink#create-a-hdl-counter) and directly import *\<FPGA-Notes-for-Scientists\>/hdl/offset_ctrl.vhd*.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/add_offset_ctrl.PNG" width="450"/>

* Add the HDL offset_ctrl module to your design (right-click on the design and select *Add Module*) and draw the required connections within your design:
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/offset_ctrl.PNG" width="1000"/>









 

