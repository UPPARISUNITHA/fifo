# FIFO Design using Verilog

## Project Overview

This project implements a **FIFO (First-In First-Out) memory** using Verilog HDL.

A FIFO is a memory structure in which the data written first is read first. FIFO memory is widely used for data buffering, communication systems, processors, and digital systems.

## FIFO Specifications

| Parameter       | Value       |
| --------------- | ----------- |
| Data Width      | 8 bits      |
| FIFO Depth      | 4           |
| Clock           | Synchronous |
| Write Operation | `wr_en`     |
| Read Operation  | `rd_en`     |
| Full Flag       | `full`      |
| Empty Flag      | `empty`     |

## Block Diagram

```text
             +----------------------+
 data_in --->|                      |
             |       FIFO           |---> data_out
 wr_en ----->|                      |
 rd_en ----->|                      |
 clk -------->|                      |
 reset ------>|                      |
             |                      |
             |  Full / Empty Flags  |
             +----------------------+
                  |          |
                 full       empty
```

## FIFO Operation

FIFO follows the **First-In First-Out** principle.

For example:

```text
Write: A1 → B2 → C3 → D4

Read:  A1 → B2 → C3 → D4
```

The first data written into the FIFO is the first data read from it.

## Inputs

### `clk`

Clock signal used to synchronize FIFO operations.

### `reset`

Resets the FIFO pointers, counter, and output.

### `wr_en`

Write enable signal. When `wr_en` is high and the FIFO is not full, data is written into the FIFO.

### `rd_en`

Read enable signal. When `rd_en` is high and the FIFO is not empty, data is read from the FIFO.

### `data_in`

8-bit input data.

## Outputs

### `data_out`

8-bit data read from the FIFO.

### `full`

Indicates that the FIFO is full.

### `empty`

Indicates that the FIFO is empty.

## Internal Components

The FIFO contains:

* Memory array
* Write pointer
* Read pointer
* Data counter
* Full flag
* Empty flag

## Files in This Repository

```text
FIFO-Verilog/
│
├── README.md
├── fifo.v
├── fifo_tb.v
└── simulation/
    └── waveform.png
```

### `fifo.v`

Contains the RTL design of the FIFO.

### `fifo_tb.v`

Contains the testbench used to verify FIFO write and read operations.

### `simulation/waveform.png`

Contains the waveform generated during simulation.

## Test Sequence

The testbench performs the following operations:

1. Reset the FIFO.
2. Write `A1`.
3. Write `B2`.
4. Write `C3`.
5. Write `D4`.
6. FIFO becomes full.
7. Read the stored data.
8. Verify that data is read in FIFO order.
9. FIFO becomes empty.

## Expected Read Sequence

```text
A1 → B2 → C3 → D4
```

## Simulation Tools

This project can be simulated using:

* Icarus Verilog
* GTKWave
* ModelSim
* Xilinx Vivado

## Icarus Verilog Commands

Compile the design:

```bash
iverilog -o fifo_sim fifo.v fifo_tb.v
```

Run the simulation:

```bash
vvp fifo_sim
```

Open the waveform:

```bash
gtkwave fifo.vcd
```

## Applications

FIFO memory is commonly used in:

* Data buffering
* UART communication
* SPI communication
* Processor systems
* Networking
* Digital signal processing
* Clock-domain data transfer
* SoC and VLSI systems

## Conclusion

The FIFO was successfully designed and verified using Verilog HDL. The simulation demonstrates correct write and read operations and confirms the **First-In First-Out** behavior of the memory.
