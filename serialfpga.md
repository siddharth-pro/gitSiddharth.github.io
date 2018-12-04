---
layout: page
alt_title: UART
actions:
- label: "View code on GitHub"
  icon: github
  url: https://github.com/gitSiddharth/UART
---


##### The goal of this project is to:                    
1. To design an UART in Verilog.
2. Test the design using a SystemVerilog testbench.
3. Synthesize the design and implement it on Cyclone IV FPGA board.
4. Interface the board with PC using hyperterminal.

##### Here's a brief overview of this project:                                       
The main part of this project is the UART itself which is coded in verilog. I have developed receiver and transmitter as seperate modules. Both the modules are instantiated in the top module through which all the interface takes place. The design is verified using testbench written in SV. After the design works in simulation, it is synthesized using Altera Quartus II to generate the bitstream for the FPGA. The FPGA board is interfaced with PC at a baud rate of 19200 using hyperterminal software and to and fro communication between PC and FPGA is verified. I have used switches to give input the PC which is indicated as ASCII character on the screen. The input from keyboard is indicated on the LEDs.


#### UART Protcol:

![UART Transaction](/assets/images/UART_timing_diagram.svg.png)

* In UART the data transmission and receiving takes place without a common clock between the two devices. Hence the two devices must work at the same speed called baud rate. In this project the baud rate of the UART is considered to be 19200. 
Using baud rate and FPGA clock frequency, the clock per bit is calculated: clock per bit = (clock frequency/baud rate)

For Cyclone IV FPGA board: 

clock per bit = (50000000/19200) = 2604
To accomodate count of 2604 the counter width should be [11:0].

Receiver:
* During the idle state the data line is high. The data line becoming low suggests an incoming signal. It should remain low at least for one-half of the bit time (clock per bit). After the start condition is established the data is received one bit at a time (clock per bit) from LSB to MSB. 

* After all the 8 bits are received, the receiver then looks for the stop bit which is high for one bit time.

Transmitter:
* The transmitter works in same way as the receiver. In that, it sends the start bit for one bit time. The one byte data is sent serially starting from LSB, one bit at a time. After all the data bits are transmitted. The stop bit is sent for one bit time marking the end of transmission.


Simulation output on the transcript window:

```
# RESET INITIATED, time in ns = 0
# RESET TERMINATED, time in ns= 150
# ---------------------------------------------
# 	 Transaction no. = 0
# 	 start = 1, 	 tx_data_in = c1,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = 24, 	 Obtained data = 48
# [TRANSACTION]::RX FAIL
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 1
# 	 start = 1, 	 tx_data_in = b0,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = 81, 	 Obtained data = 81
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 2
# 	 start = 1, 	 tx_data_in = 9d,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = 9, 	 Obtained data = 9
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 3
# 	 start = 1, 	 tx_data_in = 1e,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = 63, 	 Obtained data = 63
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 4
# 	 start = 1, 	 tx_data_in = de,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = d, 	 Obtained data = d
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 5
# 	 start = 1, 	 tx_data_in = db,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = 8d, 	 Obtained data = 8d
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 6
# 	 start = 1, 	 tx_data_in = 97,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = 65, 	 Obtained data = 65
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 7
# 	 start = 1, 	 tx_data_in = 7b,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = 12, 	 Obtained data = 12
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 8
# 	 start = 1, 	 tx_data_in = 2d,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = 1, 	 Obtained data = 1
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ---------------------------------------------
# 	 Transaction no. = 9
# 	 start = 1, 	 tx_data_in = d7,	 done_tx = 1
# [TRANSACTION]::TX PASS
# 	 Expected data = d, 	 Obtained data = d
# [TRANSACTION]::RX PASS
# ---------------------------------------------
# ** Note: $finish    : uart_env.sv(54)
#    Time: 33343950 ns  Iteration: 3  Instance: /tb_uart_top/t1
```
