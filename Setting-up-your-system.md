## 1. Preparing your PC
### 1.1. System Requirements
The system requirements are detailed within the Vivado User Guide UG973. To summarize, you are typically fine with:
* OS: Windows & Linux
* ~ 4GB of RAM
* ~ 50GB free storage 

### 1.2. Install Vivado WebPACK
I recommend to follow the step-by-step instructions within the [Digilent Reference Documentation](https://reference.digilentinc.com/vivado/installing-vivado/start).

### 1.3. Clone this repository
```bash
git clone https://github.com/dspsandbox/FPGA-Notes-for-Scientists
```

### 1.4. Install the Redpitaya-125-14 board files
To be able to generate your custom FPGA designs, it is recommended to use a board files that pre-configures your Vivado design environment. To date, no official board files for the Redpitaya-125-14 exist. For this reason, I created a custom board file that includes the most important settings of the Redpitaya-125-14. To install it, you have to:
* Within the cloned repository, navigate to *\<FPGA-Notes-for-Scientists\>/board_files*.
* Copy the *redpitaya-125-14* folder.
* Within your Vivado installation path, navigate to *\<Vivado-Path\>/data/boards/board_files*.
* Paste the *redpitaya-125-14* folder. 

## 2. Prepare your Redpitaya-125-14
### 2.1. SD card image
* Download the [Pynq-Redpitaya-125-14-2.6.0.img](https://drive.google.com/file/d/1YY4HYoDWa3E1ZVyxrV7naTFVoDieKrwm/view)
* Write the Pynq image onto the SD card. You can find instructions within the [PYNQ Documentation](https://pynq.readthedocs.io/en/v2.6.1/appendix.html#writing-the-sd-card-image).

### 2.2. Power up the Redpitaya-125-14
* Insert the SD card into your Redpitaya-125-14.
* Connect the Redpitaya-125-14 to your ethernet switch/router.
* The Redpitaya-125-14 has two micro usb connectors label as **CON** and **PWR**:
   * Connect the **CON** port to your PC and access it via a serial terminal using baudrate=115200.
   * Connect the **PWR** port to your PC or external power supply. The Redpitaya-125-14 will immediately boot and you can follow the boot sequence over the serial terminal.

### 2.3. Assign a static IP address
* Use the **CON** terminal to enter the network configurations (password: *xilinx*):
sudo vi /etc/network/interfaces.d/eth0

* Press *a* and edit the file:
```bash
auto eth0
iface eth0 inet dhcp

auto eth0:1
iface eth0:1 inet static
address <static-ip-address>
netmask <net-mask>
```
* Press *Esc* followed by *:wq* and *Enter*, which will save the modified interface configurations.

* Reboot your Redpitaya-125-14:
```bash
sudo reboot
```

* Open a separate CMD / Terminal and verify that you can SSH into your Redpitaya-125-14 (password: *xilinx*):
```bash
ssh xilinx@<static-ip-address>
```

### 2.4 Verify Jupyter Server & Samba File sharing service
* Open your web browser and navigate to \<static-ip-address\>. You should be prompted to the Jupyter Notebook welcome page (password: *xilinx*).
<img src="https://github.com/dspsandbox/FPGA-Notes-for-Scientists/doc/Setting-up-your-system/welcome.png" width="400"/>




