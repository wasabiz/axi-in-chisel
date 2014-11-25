axi-in-chisel
=============
by Yaman Umuroglu (yamanu@idi.ntnu.no)

A collection of AXI4 interface definitions and simple peripherals in Chisel.

I started working on this because I wanted more hands-on experience with Chisel and a faster way of making my hardware prototypes work with AXI interfaces found on e.g Xilinx FPGA/programmable SoCs. There are 50+ signals/ports on a full-blown AXI interface, which can be daunting. However, these can be organized into address and data channels based on the decoupled (ready/valid) abstraction, which fits nicely with Chisel's Decoupled-style interfaces and custom types.

It is worth mentioning that the code here targets the Verilog backend and hardware synthesis only, since there are no testbenches. The generated Verilog should be straightforward to use with the Xilinx IP packager. The peripherals aren't extensively tested, but they performed as expected on a ZedBoard (pushed through Vivado for synthesis).

Right now the repository is a haphazard collection of Chisel source files, with varying degree of comments in each:

SimpleReg - a translation of the AXI Lite slave template (register file) generated by Vivado

SumAccel - read 3 consecutive words from address 0x10000000 using AXI Lite master and sum them (the result can be read through the AXI Lite slave interface)

HPSumAccel - read specified number of words from specified address in large bursts and sum them. Note that number of words should be a multiple of the burst length (set to 512 32-bit words by default), since this doesn't handle chopping the burst into bits. The result and total elapsed cycles can be read through the slave interface.
