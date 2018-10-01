---
layout: page
alt_title: UART
image: /assets/images/background.jpg
actions:
- label: "View on GitHub"
  icon: github
  url: https://github.com/bonfireprocessor/bonfire/releases
---


There are two goals of this project:
1. To implement an UART on two FPGAs, in this case spartan 3e and cyclone IV.
2. Communicate serially between two FPGA boards through tx and rx pins using switches.

Here's a brief overview of this project:
The main part of this project is the UART itself which is coded in verilog. I have used two FPGA boards and implemented the same UART in both of them. The tx and rx pin from one FPGA board is connected to rx and tx pin of other. This way it is possible to establish a full duplex communication between the two FPGAs. The inputs to both the UARTs are given through switches and the outputs are observed on the LEDs and seven segment display. 

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

#### UART Protcol

![UART Transaction](/assets/images/UART_timing_diagram.svg.png)
