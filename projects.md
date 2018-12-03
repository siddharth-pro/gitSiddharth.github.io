---
title: 🄿🅁🄾🄹🄴🄲🅃🅂
---

### Serial communication between two FPGAs using UART
* UART receiver and transmitter is coded in verilog
* The reciever and transmitter functionality is verified using a testbench
* The design is synthesized and implemented on both spartan 3e and cyclone IV FPGA
* Tools used: Xilinx ISE, Quartus II and Questasim                             
#### [View Project](/serialfpga.html)

### Design of an I2C to read data from LM75A
* Implemented in verilog
* Address and data cycles are as per the datasheet of LM75A
* Design is verified on cyclone IV FPGA board                                     
* Temperature data is obtained in hexadecimal
#### [View Project](/i2cread.html)

### 8-bit RISC CPU
* The processor is coded in verilog
* The design is verified by writing the instructions to memory through backdoor access and letting the processor operate on those instructions
* Operations such as reading from memory to register, writing to memory, addition and subtraction are verified 
#### [View Project](/prorisc.html)

### Digital Clock on FPGA
* Design is coded in verilog
* Synthesized and Implemented on Spartan 3E FPGA
#### [View Project](/digitalclock.html) 
