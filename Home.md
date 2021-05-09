# Introduction
## About my first experience with FPGAs
I discovered my passion for FPGAs during my PhD in (quantum) physics. The first months were quite challenging, where learning VHDL/Verilog, understanding  the chipset architecture and using the huge Xilinx/Intel toolchain involved a steep initial learning curve and a significant amount of frustration. In fact, one of the biggest limitation was the lack of simple programming examples and hands-on tutorials. But once these hurdles were overcome, I became capable of designing my own signal generation/acquisition systems and replaced many of the old OP-27 circuits with an FPGA running a few lines of code. 

This makes it very difficult for the _profane_ folks, i.e. makers, enthusiasts and scientists without a degree in electrical engineering, to get their hands on these powerful platforms.

## About these notes
I am convinced that other _profane_ folks, i.e. makers, enthusiasts and scientists without a degree in electrical engineering, can take advantage of custom FPGA designs. For this reason, 

These notes intend to speed up the initial learning curve by providing working examples that incrementally incorporate new FPGA programming concepts. The hardware and software platform I use for this are:
* [Redpitaya STEMlab 125-14](https://www.redpitaya.com/Catalog/p20/stemlab-125-14-starter-kit?cat=c105): development board around the Xilinx Zynq-7010 SoC, which combines an ARM processor and a FPGA. The board includes digital IOs and 14-bit ADCs/DACs that operate at 125MSa/s.

* [Xilinx Vivado WebPACK](https://www.xilinx.com/products/design-tools/vivado.html): free version of this very complete FPGA design tool.

* [PYNQ](http://www.pynq.io/): Python environment to control FPGA designs and stream data into/out of them. It is based on Jupyter Notebooks that are executed on the ARM processor of the Zynq-7010 SoC.

# Outline
* [Setting up your system](Setting-up-your-system)
* [LED blink](LED-blink)
* [Analogue echo](Analogue-echo)






