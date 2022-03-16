## FPGA Pendulum Waves (Digital IO)
We are going to implement a digital version of the beautiful [Pendulum Waves Experiment](https://www.youtube.com/watch?v=yVkdfJ9PkRQ&t=22s&ab_channel=HarvardNaturalSciencesLectureDemonstrations).

1. Extend the [LED_blink](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/wiki/LED-blink) example to use 8 independent counters for every LED of your Redpitaya-125-14 with independently controllable counter **incr** but common **resetn**. 
 
---
ℹ️ The AXI GPIO IP features only 2 register outputs. For more register outputs please use multiple instances of this IP or replace it by a [AXI4 Register Bank](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/tree/main/ip/AXI4-register-bank) IP instance, which has up to 16 independent register inputs/outputs.

---

2. Extend the [LED_blink.ipynb](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/jupyter_notebooks/LED_blink.ipynb) Jupyter Notebook to configure LED frequencies of the type:

    **f[i] = f0 + i * df**

    for **i=0,1...,7** and where **f0** is the base frequency and **df** the frequency increment.


## PWM (Digital IO & Simulation)
In this assignment we are going to develop a [Pulse-Width Modulation (PWM)](https://en.wikipedia.org/wiki/Pulse-width_modulation) module.

1. Based on the [counter.vhd](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/hdl/counter.vhd), create a new VHDL module that has the following ports

|Name|In/Out | Width (bits) |Description |
|---|---|---|---|
|clk|in|1|System clock|
|resetn|in|1|System reset (active low)|
|incr_i|in|32|Internal counter increment per clock cycle| 
|duty_cycle_i|in|32|Internal counter threshold below (above) which *pwm_o = 1* (*pwm_o = 0*) |
|pwm_o|out|1|Pulse-width modulation output| 
  
2. Simulate and validate the new VHDL module (follow the instructions in [Behavioral Simulation](Behavioral-simulation)).

3. Connect the PWM module to the Redpitaya LEDs and verify that you can use it to dim the LED power.

4. Connect the PWM module to the *pwm_o* ports (requires to uncomment *PWM DAC* section in [redpitaya-125-14.xdc](https://github.com/dspsandbox/FPGA-Notes-for-Scientists/blob/main/sdc/redpitaya-125-14.xdc)) and verify on an oscilloscope that the you can use PWM in combination with the integrated low-pass filter to generate an analogue output.
 