## About this tutorial 
:stopwatch: 30 min

**Key learnings:**

* Interface the 125 MSa/s ADCs and DACs of the Redpitaya-125-14.

* Use a simple AXI stream module. 

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
    * Processor System Reset
    * AXI GPIO
    * Redpitaya-125-14-clk
    * Redpitaya-125-14-adc
    * Redpitaya-125-14-dac


* Connect the clocks and resets as shown in the diagram below. 
   * We use *clk_125*, which operates at 125MHz, to drive the main logic of the design. All data paths in this tutorial will be synchronous to this clock. 
   * We connect *clk_250_m150* and *clk_250_m120* to the DAC only. They operate at 250Mhz and are phase locked to *clk_125* with a relative phase shift of -150 deg and -120 deg.  

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/connect_clk.PNG" width="1000"/>

* Configure the AXI GPIO to have a dual 16-bit output.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/axi_gpio.PNG" width="450"/>

### AXI stream offset module

***
:information_source: If this is first time you are dealing with an AXI stream interface, I recommend to go over [this](http://fpgasite.blogspot.com/2017/07/xilinx-axi-stream-tutorial-part-1.html) blog. For more details, you can have a look at the [AXI Reference Guide UG761](https://www.xilinx.com/support/documentation/ip_documentation/ug761_axi_reference_guide.pdf).
***

* Within the left panel go to *Project Manager --> Add sources* and select  *Add or create design sources*.
* We omit the creation of a HDL file, which was explained in [LED blink](../LED-blink#create-a-hdl-counter) and directly import *\<FPGA-Notes-for-Scientists\>/hdl/offset_ctrl.vhd*.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/add_offset_ctrl.PNG" width="450"/>

* Add the HDL offset_ctrl module to your design (right-click on the design and select *Add Module*) and draw the required connections within your design.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/offset_ctrl.PNG" width="1000"/>


### Constraints and port creation
* Edit the constraints in *redpitaya-125-14.xdc* and uncomment the sections:
  * ADC (lines 8-56)
  * DAC (lines 59-90)
  * Clock constraints (lines 181-183)
* Go back to your design and create the required input/output ports for the *Redpitaya-125-14-clk*, *Redpitaya-125-14-adc* and *Redpitaya-125-14-dac* IPs. The fastest way is to right-click on a every port and choose *Create Port*  (*CTRL + K*) and proceed with the default settings. 
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/create_port.png" width="1000"/>

* Including all the required ports, the design becomes:
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/all_ports.PNG" width="1000"/>

### Block and connection automation.
* Use the *Block Automation* and *Connection Automation* (green field above your design) to route the DDR and FIXED_IO ports and to connect the AXI GPIO instances. 
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/final_design.PNG" width="1000"/>


### Bitstream generation
Please follow the steps detailed in [LED blink](../LED-blink#bitstream-generation).

## Running the design
***
:information_source: Please make sure to complete first the steps in [Prepare your Redpitaya-125-14](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/Setting-up-your-system#prepare-your-redpitaya-125-14) and [Speed up the design flow](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/Setting-up-your-system#speed-up-the-design-flow).
***

* Before bitstream generation, a HDL wrapper around the design needs to be created. Within your project source tree, right-click on top of your design  and select *Create HDL Wrapper* (use default settings).
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/analog-echo/hdl_wrapper.png" width="1000"/>


* Click on *Generate Bitstream* (left panel) and proceed with the default settings. This will automatically take you through:
     * **Synthesis**: translates the custom design FPGA design into logical elements such as flip-flops, LUTs...
     * **Implementation**: places the logical elements of the synthesized design into the particular chip architecture.
     * **Bitstream generation**: creates a binary image that contains the implemented design.

* After a few minutes, the process completes. Press *Cancel* to close the the pop-up window.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/bitstreamCompleted.PNG" width="200"/>

## Running the design
***
:information_source: Please make sure to complete first the steps in [Prepare your Redpitaya-125-14](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/Setting-up-your-system#prepare-your-redpitaya-125-14) and [Speed up the design flow](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/Setting-up-your-system#speed-up-the-design-flow).
***

* Verify that you Redpitaya-125-14 is connected to your local network, e.g. using ping:
```bash
ping <static-ip-address>
```

* Create and upload the *overlay* for your custom design by pressing the <img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/Setting-up-your-system/tclButton.png" width="15"/> button. The following message should appear within your Vivado Tcl console:
```bash
Overlay "analog_echo" successfully uploaded to: 
xilinx@<static-ip-address>:/home/xilinx/pynq/overlays/LED_blink
```

* Open your preferred web browser and navigate to *\<static-ip-address\>* and enter the PYNQ Jupyter Notebook environment (password: *Xilinx*).

* Create a new Python 3 Jupyter Notebook.

* Open the Jupyter Notebook and edit it as shown in [analog_echo.ipynb](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/jupyter_notebooks/analog_echo.ipynb). 

* Run the Jupyter notebook. 

