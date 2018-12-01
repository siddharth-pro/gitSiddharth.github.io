---
layout: page
alt_title: UART
actions:
- label: "View code on GitHub"
  icon: github
  url: https://github.com/gitSiddharth/UART {:target="_blank"}
---


##### There are two goals of this project:                    
1. To implement UART on two FPGAs, in this case spartan 3e and cyclone IV.
2. Communicate serially between two FPGA boards through tx and rx pins using switches.

##### Here's a brief overview of this project:                                       
The main part of this project is the UART itself which is coded in verilog. I have used two FPGA boards and implemented the same UART on both the FPGAs. The tx and rx pin from one FPGA board is connected to rx and tx pin of the other. This way it is possible to establish a full duplex communication between the two FPGAs. The inputs to both the UARTs are given through switches and the outputs are observed on the LEDs and seven segment display. 

##### Ports:
```verilog
module uart
(
 input clk, //32MHz clock in case of Spartan 3E FPGA board and 50MHz in case of Cyclone IV FPGA board
 input rst, //Global synchronous reset to make all register contents zero
 input rx, //Serial input to UART receiver
 input [7:0] tx_data_in, //Parallel input to UART transmitter
 input start, //Start the transmission
 output tx, //Serial output from UART transmitter
 output [7:0] rx_data_out, //Parallel output from UART receiver
 output tx_active, //High during data transmission
 output done_tx //Transmission is over
 );
 ```


#### UART Protcol:

![UART Transaction](/assets/images/UART_timing_diagram.svg.png)

* In UART the data transmission and receiving takes place without a common clock between the two devices. Hence the two devices must work at the same speed called baud rate. In this project the baud rate of the UART is considered to be 19200. 
Using baud rate and FPGA clock frequency, the clock per bit is calculated: clock per bit = (clock frequency/baud rate)

For Spartan 3E FPGA board: 

clock per bit = (32000000/19200) ≈ 1666
Hence counter width is [10:0].

For Cyclone IV FPGA board: 

clock per bit = (50000000/19200) = 2604
Hence counter width is [11:0].

Receiver:
* During the idle state the data line is high. The data line becoming low suggests an incoming signal. It should remain low at least for one-half of the bit time (clock per bit). After the start condition is established the data is received one bit at a time (clock per bit) from LSB to MSB. 

* After all the 8 bits are received, the receiver then looks for the stop bit which is high for one bit time.

Transmitter:
* The transmitter works in same way as the receiver. In that, it sends the start bit for one bit time. The one byte data is sent serially starting from LSB, one bit at a time. After all the data bits are transmitted. The stop bit is sent for one bit time marking the end of transmission.

Final Implementation:

![serial fpga](/assets/images/Serial_comm_fpga.jpg)
