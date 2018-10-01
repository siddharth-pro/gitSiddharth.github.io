---
layout: page
alt_title: I2C
image: /assets/images/background.jpg
actions:
- label: "View on GitHub"
  icon: github
  url: https://github.com/
---
The goal of this project is to design an I2C core in verilog, implement it on FPGA, interface it with I2C sensor LM75A to read the temperature data.
One part of this project is to design an I2C controller which in itself is a bit complicated thing to do. But this project wouldn't be possible without a good documentation of [LM75A](https://www.nxp.com/docs/en/data-sheet/LM75A.pdf). Thanks to NXP for this excellent [datasheet](https://www.nxp.com/docs/en/data-sheet/LM75A.pdf).
LM75A is a digital temperature sensor and thermal watchdog, since the I2C controller has to read data from LM75A, knowing which register to access, what bits to consider is essential here and it is explained very well in the [datasheet](https://www.nxp.com/docs/en/data-sheet/LM75A.pdf).

![Temperature register](/assets/images/Temp_register.png)

LM75A has four registers, but the register of our interest is the temperature register which stores two byte of information. During power up the pointer value is already at 0, so we need not specify the pointer value to read the temperature.

![slave address](/assets/images/address.png)

The address which is to be sent is shown above. Here 0th bit indicates read/write operation. As we are reading from the sensor, it should be 1. Bits 1 to 3 specifies the slave address. It is taken as 000 since we have only one slave. Bit 4 to 7 is preset to 1001 by hard-wiring inside the LM75A.



