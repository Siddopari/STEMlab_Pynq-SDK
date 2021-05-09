## Preparing your PC
### System Requirements
The system requirements are detailed within the Vivado User Guide UG973. To summarize, you are typically fine with:
* OS: Windows & Linux
* ~ 4GB of RAM
* ~ 50GB free storage 

### Instal Vivado WebPACK
Step-by-step instructions of the Vivado WebPACK installation can be found within the [Digilent Reference Documentation](https://reference.digilentinc.com/vivado/installing-vivado/start).

### Clone this repository
```bash
git clone https://github.com/dspsandbox/FPGA-Notes-for-Scientists
```

### Install the Redpitaya-125-14 board files
To be able to generate your custom FPGA designs, it is recommended to use a board files that pre-configures your Vivado design environment. To date, no official board files for the Redpitaya-125-14 exist. For this reason, I created a custom board file that includes the most important settings of the Redpitaya-125-14. To install it, you have to:
* Within the cloned repository, navigate to *\<FPGA-Notes-for-Scientists\>/board_files*.
* Copy the *redpitaya-125-14* folder.
* Within your Vivado installation path, navigate to *\<Vivado-Path\>/data/boards/board_files*.
* Paste the *redpitaya-125-14* folder. 

###