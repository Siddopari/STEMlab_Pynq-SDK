# Introduction
## About my first experience with FPGAs
I discovered my passion for fast programable logic during my PhD in (quantum) physics. Very helpful in this regard was the Arduino IDE, which makes microcontrollers accessible to the _profane_ folks, i.e. makers, enthusiasts and scientists without a degree in electrical engineering. The situation is different for FPGAs, where learning VHDL/Verilog, understanding  the chipset architecture and using the huge Xilinx/Intel toolchain involve a steep initial learning curve and a significant amount of frustration. But once these hurdles are overcome, you are capable of designing your own signal generation/acquisition systems and replace many of your old OP-27 circuits with an FPGA running a few lines of code. I had no prior experience in FPGA programming and to reach this point took me several months. 
## About these notes
These notes intend to speed up the initial learning curve by providing working examples that incrementally incorporate new FPGA programming concepts. The hardware and software platform I use for this are:
* [Redpitaya STEMlab 125-14](https://www.redpitaya.com/Catalog/p20/stemlab-125-14-starter-kit?cat=c105): development board around the Xilinx Zynq-7010 SoC, which combines an ARM processor and a FPGA. The board includes digital IOs and 14-bit ADCs/DACs that operate at 125MSa/s.

* [Xilinx Vivado Webpack](https://www.xilinx.com/products/design-tools/vivado.html): free version of this very complete FPGA design tool.

* [PYNQ](http://www.pynq.io/): Python environment to control FPGA designs and stream data into/out of them. It is based on Jupyter Notebooks that are executed on the ARM processor of the Zynq-7010 SoC.

# Outline
* [Setting up your system](Setting-up-your-system)
* [LED blink](LED-blink)
* [Analogue echo](Analogue-echo)






