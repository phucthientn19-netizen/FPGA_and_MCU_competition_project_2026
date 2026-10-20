# Chilli Da Nang 2026 — Embedded Systems & FPGA Project

## Overview

**Chilli Da Nang 2026** is an embedded hardware project combining FPGA-based digital design with microcontroller firmware. The project explores hardware control logic, serial communication, timing management, and peripheral drivers.

The FPGA design is implemented in Verilog HDL and includes a system controller, PWM-based LED control, button debouncing, and UART transmission for reporting the current operating mode.

## Key Features

- **FPGA Digital Design:** Modular RTL implementation using Verilog HDL.
- **PWM LED Control:** Supports LOW, HIGH, and AUTO operating modes.
- **Button Debouncing:** Filters mechanical button transitions to generate reliable control pulses.
- **UART Communication:** Transmits operating-mode information over a serial interface.
- **Finite State Machines (FSMs):** Controls operating-mode transitions and UART transmission sequences.
- **Clock and Reset Management:** Uses a PLL-based system clock and power-on reset logic.
- **MCU Firmware:** Includes peripheral driver source files for GPIO, UART, DMA, timers, watchdog, EEPROM, flash, CRC, and other hardware functions.
- **Simulation and Reports:** Contains simulation projects, waveform images, synthesis reports, and technical documentation.

## System Architecture

The FPGA controller follows this general signal flow:

1. **Clock Generation:** A PLL generates the internal system clock from the board's input clock.
2. **Reset Initialization:** Power-on reset logic initializes the system.
3. **Button Processing:** Debounce modules process button inputs.
4. **Mode Control:** An FSM manages transitions between LOW, HIGH, and AUTO modes.
5. **LED Control:** A PWM module generates the LED control signal according to the selected mode.
6. **UART Transmission:** A UART transmitter sends the current mode as a text message to a connected serial terminal.

The UART transmitter uses a baud-rate divider configured for a nominal 115200 bps at the intended 50.1429 MHz system clock.

## Repository Structure

```text
Chilli_Danang2026/
├── Chilli_FPGA/
│   ├── src/
│   │   └── fpga_project-demo/
│   │       ├── src/
│   │       │   ├── uart_tx_byte.v
│   │       │   └── gowin_pllo/
│   │       ├── impl/
│   │       └── fpga_project-demo.gprj
│   ├── sim/
│   │   ├── top_system.v
│   │   ├── uart_tx_byte.v
│   │   └── waveform/
│   └── Chilli_BaoCaoKyThuat_FPGA.pdf
├── Chilli_MCU/
│   ├── Source/
│   │   ├── Driver/
│   │   ├── Module/
│   │   └── Readme/
│   ├── RTE/
│   └── project.uvprojx
├── Chilli_SlideBaoCaoTongHop.pdf
└── README.md
```

*Note: The tree above highlights the main project files. Some generated implementation and simulation files are included in the repository.*

## Technologies

| Area | Technologies / Concepts |
|---|---|
| Hardware description | Verilog HDL |
| FPGA design | Gowin FPGA toolchain and project files |
| Digital control | Finite State Machines, synchronous logic |
| LED control | Pulse Width Modulation (PWM) |
| Serial communication | UART, 8-bit data transmission |
| Input handling | Button debouncing |
| Embedded firmware | C |
| MCU development | Keil uVision project format |
| Verification | Simulation waveforms and synthesis reports |

## Getting Started

### FPGA Project

1. Install a compatible version of the Gowin FPGA design software.
2. Open `Chilli_FPGA/src/fpga_project-demo/fpga_project-demo.gprj`.
3. Review the Verilog source files and confirm the top-level module and target FPGA device.
4. Run synthesis and implementation.
5. Review the generated reports and inspect the simulation resources.

### MCU Firmware

1. Install Keil MDK/uVision with support for the target SN32F407F device.
2. Open `Chilli_MCU/project.uvprojx`.
3. Review the source files and device configuration.
4. Build the firmware after confirming that all required project dependencies are available.

## Verification

The repository contains FPGA simulation resources, waveform images for selected modules, and implementation reports. These artifacts can help inspect signal behavior and review the hardware design flow.

Before using the design on physical hardware, verify the FPGA device configuration, pin assignments, clock settings, reset behavior, and UART connection. Confirm the complete source set and rerun the simulations and implementation flow in the target development environment.

## Learning Outcomes

This project provides practical experience with:

- RTL design and modular hardware development.
- FSM-based control and sequential logic.
- PWM generation and digital timing.
- UART serial communication.
- FPGA synthesis, implementation, and simulation.
- Microcontroller peripheral drivers and embedded firmware organization.

## Documentation

Technical reports and presentation materials are included in the project folders. Refer to these documents for additional implementation details.

## License

No license has been specified yet. Please contact the project owner before reusing or redistributing the source code.
