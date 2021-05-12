***

:information_source: **INFO** For more details on the Redpitaya-125-14 platform and the Zynq chipset architecture, I recommend visit the [Redpitaya Developer Guide](https://redpitaya.readthedocs.io/en/latest/developerGuide/devGuideTop.html) and to read the [Zynq Book](http://www.zynqbook.com/).

***
## Schematic

<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/doc/Zynq-architecture-&-Redpitaya-125-14/Redpitaya.png" width="600"/>

## Description
The diagram above outlines the basic components of the Redpitaya-125-14 board. At the core of it is the the **Zynq-7010 SoC**, which combines a processing system (PS) and programmable logic (PL) within the same chipset. Both parts are strongly interconnected via high-bandwidth data busses (not shown in the diagram). 
* The **PS** is a dual core 32bit ARM processor. It runs Ubuntu 18.04 LTS and hosts the Jupyter Notebook over which we to control the PL. The connected peripherals are: 
    * **Ethernet** (1Gb/s): see [Setting up your system](Setting-up-your-system) to configure a static IP addresses and verify the SSH connectivity.

    * **USB-A** : configured as a USB-host. 

    * **USB-microB** (CON) : connected to the UART0 of Zynq PS and that serves as a serial terminal. Details on the required terminal settings can be found [here](https://pynq.readthedocs.io/en/v2.0/getting_started.html#opening-a-usb-serial-terminal).

    * **USB-microB** (PWR): used to power the Redpitaya-125-14 board.

    * **SD**: the SD card contains the boot image and root file system for Ubuntu 18.04 LTS.

    * **RAM** (512 MB): random access memory for the PS. The PYNQ environment provides simple tools to reserve part of the memory and perform DMA operations, i.e data streams of type RAM --> PS --> PL for custom waveform synthesis and PL --> PS --> RAM for long waveform acquisition. 

* The **PL** is the *actual* FPGA, which includes look-up tables (LUTs), flip-flops, DSP logic, BRAM ... to implement custom designs. It is connected to (*): 

    * **DAC** (125MSa/s, 14bit):  *fast* digital-to-analog converter that generates the waveforms for the OUT1 and OUT2 ports.
    * **ADC** (125MSa/s, 14bit): *fast* analog-to-digital converter that samples the IN1 and IN2 ports.
    * **xadc_i** (x4, 1MSa/s): *slow* analog-to-digital converters within the Zynq-7010.
    * **dig_o + LPF** (x4): digital outputs with analog low-pass filters (cut-off frequency: 190kHz). They can be used as *slow* digital-to-analog converters by performing pulse-width modulation (PWM) on the *dig_o* ports. 
   * **led_o** (x8): user LEDs.
   * **dig_i/dig_o** (x16): digital IOs
   * **daisy chain**: used to interconnect and synchronize multiple Redpitaya boards. 



(*) *Please refer to the [Redpitaya-125-14 Extension Documentation]( https://redpitaya.readthedocs.io/en/latest/developerGuide/125-14/extent.html) for the exact pinout.* 



