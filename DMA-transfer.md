## About this tutorial
:stopwatch: 45 min

**Key learnings:**

* Long custom waveform generation generation/acquisition.

* PL (Programable Logic): use AXI DMA IP for reading/writing data from/to RAM memory.

* PS (Processing System): use PYNQ for reading/writing data from/to RAM memory.

**Description:** 

FPGAs have typically very low on-chip memory resources (~250kB for the ZYNQ-7010 of your Redpitaya-125-14). This limitation is circumvented through one (or several) external DDR memories which are connected to the FPGA through high bandwidth ports and controlled through a Direct Memory Access (DMA) engine. The Redpitaya-125-14 includes a 512MB DDR memory, which serves as RAM for the Zynq PS but can also be used to exchange data with the Zynq PL. 

In this tutorial we are going to build a dual channel data acquisition and generation design, where the samples are directly read form (written to) RAM memory via DMA. A PYNQ Jupyter Notebook will be used to preload a waveform to RAM memory for waveform generation, simultaneously trigger the waveform generation/acquisition and plot the acquired samples.

## Building the Vivado Design
### Create a new Vivado Project
Follow the steps in [LED blink](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/LED-blink#create-a-new-vivado-project) and use *DMA_transfer* as the new project name. 

### Import the Redpitaya-125-14 IP library
Follow the steps in [Analog echo](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/Analog-echo#import-the-redpitaya-125-14-ip-library).

### Block Design
* Create a new block design.
* Create an instance of the following IPs:
    * ZYNQ7 Processing System
    * Processor System Reset
    * AXI GPIO
    * AXI Interconnect (x2)
    * AXI Direct Memory Access (x2)
    * Redpitaya-125-14-clk
    * Redpitaya-125-14-adc
    * Redpitaya-125-14-dac
* Double click on the ZYNQ7 instance and go to *HP Slave AXI Interface* and enable the high performance interfaces *S AXI HP0 interface* and *S AXI HP1 interface* (data width 64 bit).
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/DMA-transfer/zynq.PNG" width="600"/>

* (x2) Double click on the AXI Interconnect instance and configure it to have 2 Slave Interfaces and 1 Master Interface

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/DMA-transfer/axi_interconnect.PNG" width="600"/>

