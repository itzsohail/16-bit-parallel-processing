# Asynchronous Parallel Communication Using FIFO and CDC

This project implements reliable 16-bit data transfer between two independent clock domains using transmit and receive FIFOs, a ready/valid handshake, and clock-domain-crossing synchronizers.

## Features

- 16-bit parallel data path
- 16-word transmit and receive FIFOs
- Independent transmit and receive clocks
- Two-flop  synchronizers
- Ready/valid handshake protocol
- Self-checking SystemVerilog testbench
- Vivado XSim simulation project

## Architecture

```text
Input Data → Transmit FIFO → Transmitter FSM → CDC Handshake
                                             ↓
Output Data ← Receive FIFO ← Receiver FSM ←──┘
```

## Modules

| File | Description |
|---|---|
| `FIFO.sv` | 16-entry × 16-bit FIFO with full and empty flags |
| `Transmitter.v` | Buffers and transmits data using the valid/ready protocol |
| `Receiver.v` | Captures transferred data into the receive FIFO |
| `cdc_syn.v` | Two-flop synchronizer for CDC control signals |
| `tb.sv` | Testbench that sends and verifies 40 data words |

## Handshake Operation

1. The transmitter places data on the parallel bus.
2. `parallel_valid_out` is asserted.
3. The receiver captures the data after synchronization.
4. `parallel_ready_out` acknowledges the transfer.
5. Both sides return to the idle state before the next transfer.

## Specifications

| Parameter | Value |
|---|---|
| Data width | 16 bits |
| FIFO depth | 16 words |
| Transmit clock | 100 MHz in testbench |
| Receive clock | Approximately 80 MHz in testbench |
| CDC method | Two-flop synchronizer |
| Simulator | Vivado XSim |
| Vivado version | 2024.2 |
| Target device | Kintex-7 `xc7k70tfbv676-1` |

## Running the Simulation

1. Open `Project/Parallel_communication/Parallel_communication.xpr` in Vivado 2024.2.
2. Select `tb` as the simulation top module.
3. Run **Simulation → Run Behavioral Simulation**.
4. Check the waveform and simulator console.

## Directory Structure

```text
VLSI_PROJECT/
├── Project/Parallel_communication/
│   ├── Parallel_communication.xpr
│   └── Parallel_communication.srcs/
│       ├── sources_1/new/
│       │   ├── FIFO.sv
│       │   ├── Transmitter.v
│       │   ├── Receiver.v
│       │   └── cdc_syn.v
│       └── sim_1/new/tb.sv
└── README.md
```

## Future Improvements

- Parameterize FIFO depth and data width
- Add FPGA pin and timing constraints
- Add SystemVerilog assertions
- Use Gray-coded asynchronous FIFO pointers
- Add throughput and latency measurements

## Author

VLSI/FPGA project demonstrating FIFO buffering, clock-domain crossing, and reliable parallel communication.
