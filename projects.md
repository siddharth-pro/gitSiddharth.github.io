---
title: Projects
image: /assets/images/background.jpg
---

### Serial communication between two FPGAs using UART
* Supports RV32IM based on RISC-V User Level  ISA 2.1. (M-Spec is optional)
* Supports M-Mode according to RISC-V privilege Spec 1.10 and a Subset of CSR Registers

   + Implements all CSRs for Trap and Interrupt Handling (e.g. mtvec, mcause)
   + mcycle counter
   + Supports timer, external and up to 16 local Interrupts

### Design of an I2C to read data from LM75
* Implemented  in  readable VHDL code
* Clean module structure
* Leverages FuseSoC as build system
* Testbenches can be run with Xilinx ISE, Xilinx Vivado and GHDL
[View Project](https://github.com/ThomasHornschuh/elua)


