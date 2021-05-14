## About this tutorial
In this tutorial we are going to demonstrate how to blink the LEDs of your Redpitaya-124-14. The LEDs will be driven by the most-significant-bit (MSB) of a counter that continuously overflows. The counter is implemented within the Programable Logic (PL) and controlled through a simple PYQN Jupyter Notebook running on the Processing System (PS). 

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/LED_blink.gif" width="350"/>

## Building the Vivado Design
### Create a new Vivado Project
* Open Vivado and click on *Create Project* and hit _Next_.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/startVivado.PNG" width="450"/>

* Set the name of the new project (e.g. _LED_blink_) and hit _Next_.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/newProject.PNG" width="450"/>

* Use the default project type (_RTL Project_) and hit _Next_.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/projectType.PNG" width="450"/>

* Leave the _Add Sources_ screen empty and hit _Next_.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/addSources.PNG" width="450"/>

* Use *Add File* to include the constraints file within *\<FPGA-Notes-for-Scientists\>/sdc/red_pitaya.xdc* and hit _Next_.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/addConstraints.PNG" width="450"/>

* Under the *Boards* tab select Redpitaya-125-14 (see [Setting up your system](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/Setting-up-your-system) to install the required board files) and hit *Next*.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/defaultPart.PNG" width="450"/>

* After finishing this initial configurations, a new Vivado Project is created. You will see the *Project Manager* page:
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/projectSummary.PNG" width="800"/>

### Create a new Block Design

* Create a new block design by clicking on *Create Block Design* (left panel). The design name will default to *design_1*.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/createBlockDesign.PNG" width="800"/>

* Right-click on the blank design and select *Add IP* to instantiate:
    * ZYNQ 7 Processing System
    * AXI GPIO
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/zynqGpio_1.PNG" width="800"/>

* Click on *Run Block Automation* (green field above your design) to route the DDR and FIXED_IO ports of the ZYNQ instance. To this end, leave the configuration window in its default state.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/blockAutomation.PNG" width="450"/>
  
* Click on *Run Connection Automation* (green field above your design) to create the required clocking, reset and AXI interconnect infrastructure. To this end, within the configuration window only select *S_AXI*. We do not select *GPIO*, because we will manually configure & connect the AXI GPIO.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/connectionAutomation.PNG" width="450"/>

* After running block & connection automation, the design becomes:
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/zynqGpio_2.PNG" width="800"/>

* Double-click on the AXI GPIO instance and enable Channel 1 and Channel 2 as outputs of 1 and 32 bits, respectively. Later in the design process, we will use Channel 1 to reset the counter logic and Channel 2 to define the counter increment value. 
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/axiGpio.PNG" width="450"/>

* Double-click on the ZYNQ instance and verify (under *Clock Configuration --> PL Fabric Clocks*) that *FCLK_CLK0* is enabled and set to 50 MHz. 
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/zynqPLClk.PNG" width="450"/>

### Create a HDL counter
* The next step is to create a counter logic with variable counter increment. Click on *Add Sources* (left panel) and select *Add or create design sources*.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/addSourceVivado.PNG" width="450"/>

* At this point you can either select and already existing HDL file or create a new one. We will follow the latter.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/newSource.PNG" width="450"/>

* Define the module ports (they can also be changed later, within the HDL code).
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/defineModule.PNG" width="350"/>

* The new source file (*counter.vhd*) will be added to the source tree. Open and edit it to include the counter logic.
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/LED-blink/counterVhd.PNG" width="800"/>

***

:information_source: You can use *\<FPGA-Notes-for-Scientists\>/hdl/counter.vhd* (link [here](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/hdl/counter.vhd)) as an example for the HDL counter logic.

***

