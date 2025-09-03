# FIFO_Verification
FIFO Verification Environment (SystemVerilog)
This repository contains a SystemVerilog Verification Environment for a First-In First-Out (FIFO) memory.
The environment is built using transaction-level modeling with components like generator, driver, monitor, scoreboard, and environment class.
It demonstrates a structured verification flow that resembles UVM-style testbenches.

Project Structure
Design Overview

FIFO (design/FIFO.sv)

16x8 synchronous FIFO with read and write pointers.

Signals:

clk : Clock

rst : Reset

wr : Write enable

rd : Read enable

din : 8-bit data input

dout: 8-bit data output

full: FIFO full flag

empty: FIFO empty flag

Behavior:

On reset → FIFO cleared.

On write (wr=1 & not full) → Data stored at write pointer.

On read (rd=1 & not empty) → Data read from read pointer.

full and empty flags update accordingly.

Testbench Architecture (tb/tb.sv)

Transaction → Defines fields (wr, rd, din, dout, full, empty). Randomizes operations.

Generator → Creates random read/write transactions, sends to driver & scoreboard.

Driver → Drives signals to DUT (handles reset, write, read).

Monitor → Samples DUT activity and sends data to scoreboard.

Scoreboard → Reference model using queue. Compares expected vs actual data.

Environment → Instantiates & connects all components. Controls test flow.

Top Testbench → Instantiates DUT, generates clock, runs environment, dumps waveforms.

Running the Simulation

Option 1: Run on EDA Playground

Copy design/FIFO.sv into Design section.

Copy tb/tb.sv into Testbench section.

Run simulation and check waveforms.

Option 2: Run Locally with Icarus Verilog

# Compile design and testbench
iverilog -o fifo_tb design/FIFO.sv design/fifo_if.sv tb/tb.sv

# Run simulation
vvp fifo_tb

# View waveforms
gtkwave dump.vcd
