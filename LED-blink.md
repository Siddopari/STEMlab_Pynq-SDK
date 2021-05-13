## About this tutorial
In this tutorial we are going to demonstrate how to blink the LEDs of your Redpitaya-124-14. The LEDs will be driven by the most-significant-bit (MSB) bit value of a counter implemented within the Programable Logic (PL). The counter is controlled and configured through a simple PYQN Jupyer Notebook running on the Processing System (PS). 

## Building the Vivado Design
* Open Vivado and click on *Create Project* and hit _Next_.

* Set the name of the new project (e.g. _LED_blink_) and hit _Next_.

* Use the default project type (_RTL Project_) and hit _Next_.

* Leave the _Add Sources_ screen empty and hit _Next_.

```python
import pynq
ol = pynq.Overlay("LED_blink.bit")
```

```python
import pynq
ol = pynq.Overlay("LED_blink.bit")
```