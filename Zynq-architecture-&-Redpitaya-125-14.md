***

:information_source: For more details on the Zynq chipset architecture and the Redpitaya-125-14 platform, I recommend to read the [Zynq Book](http://www.zynqbook.com/) and visit the [Redpitaya Developer Guide](https://redpitaya.readthedocs.io/en/latest/developerGuide/devGuideTop.html).

***
## Schematic

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/Zynq-architecture-&-Redpitaya-125-14/Redpitaya.png" width="600"/>

## Description
The diagram above outlines the basic components of the Redpitaya-125-14 board. At the core of it is the the **Zynq-7010 SoC**, which combines a processing system (PS) and programmable logic (PL) within the same chipset:
* The **PS* is a dual core 32bit ARM processor. It runs a Ubuntu 18.04 LTS and hosts the Jupyter Notebook we will use to control the PL. The connected peripherals are: 
    * Ethernet (1Gb). See [Setting up your system](Setting-up-your-system) to configure a static IP addresses and verify the SSH connectivity.

    * USB-