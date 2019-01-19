---
title: Projects
---

### UART
* UART receiver and transmitter is coded in SystemVerilog.
* The reciever and transmitter functionality is verified using UVM and SystemVerilog.
* The design is synthesized and implemented on Cyclone IV FPGA.
* Achieved timing closure using TimeQuest Timing Analyzer.
* Tools used: Altera Quartus II, TimeQuest and Questasim                             
#### [View Project](/serialfpga.html)

### Design of an I²C to read data from LM75A
* Design and testbench coded in Verilog.
* Address and data cycles are as per the datasheet of LM75A.
* Design is implemented on Spartan 3E FPGA of Papilio One FPGA board.                                  
* Temperature data is obtained in hexadecimal and displayed on seven segment display.
* Tools used: Xilinx ISE and Questasim
#### [View Project](/i2cread.html)

### 8-bit RISC CPU
* The processor is coded in Verilog.
* The design is verified by loading testvalue.bin file containing  all the instructions to memory through backdoor access and applying clock to the design in testbench.
* Operations such as reading from memory to register, writing to memory, addition and subtraction are verified through the waveform. 
* Tool used: Questasim
#### [View Project](/prorisc.html)

### Digital Clock on FPGA
* Design is coded in Verilog.
* Synthesized and Implemented on Spartan 3E FPGA.
* Time is displayed on the seven segment display.
* Tool used: Xilinx ISE
#### [View Project](/digitalclock.html) 

