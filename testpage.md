---
layout: page
title: proRISC
image: /assets/images/arty.png
---

## Core

####  RISC-V RV32IM compatible
* Supports RV32IM based on RISC-V User Level  ISA 2.1. (M-Spec is optional)
* Supports M-Mode according to RISC-V privilege Spec 1.10 and a Subset of CSR Registers

   + Implements all CSRs for Trap and Interrupt Handling (e.g. mtvec, mcause)
   + mcycle counter
   + Supports timer, external and up to 16 local Interrupts

####  Easy to understand and use
* Implemented  in  readable VHDL code
* Clean module structure
* Leverages FuseSoC as build system
* Testbenches can be run with Xilinx ISE, Xilinx Vivado and GHDL

#### Architecture
* 3-Stage Pipeline
* Separate Instruction and Data Buses
* Fast Multiplier (4 Cycles latency)
* Barrel Shifter (2 Cycle latency)
* Optional Instruction and Data Caches

## Configurations
### Flexible interfacing - Several Toplevel configurations available

#### Basic Core
* CPU Core only
* Low Latency Instruction Bus Interface
* Wishbone Data Bus Interface

#### Extended Core
* Instruction Cache
* Separate Wishbone Instruction and Data Buses
* Direkt Block RAM Interface

