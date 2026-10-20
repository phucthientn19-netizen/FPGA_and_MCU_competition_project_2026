# Chilli Da Nang 2026 — FPGA & MCU Embedded Systems Project

## Overview

**Chilli Da Nang 2026** is an embedded systems and digital hardware project developed for a technical competition. The repository brings together two main development areas:

- **FPGA Digital Design:** Verilog HDL, digital control logic, PWM-based LED control, finite state machines (FSMs), button debouncing, clock/reset management, and UART transmission.
- **Microcontroller Firmware:** Embedded C development for the SN32F407F platform, with peripheral drivers and supporting firmware modules.

The project provides source code, development project files, simulation resources, implementation reports, and technical documentation for studying digital hardware design and microcontroller-based embedded systems.

## Project Objectives

- Explore FPGA-based digital system design using Verilog HDL.
- Develop and organize embedded C firmware for a microcontroller.
- Understand digital control, timing, and state-machine-based design.
- Work with communication interfaces such as UART.
- Study MCU peripheral drivers and hardware-software interaction.
- Practice simulation, implementation, firmware building, and technical documentation.

## Main Components

### 1. FPGA Digital Design

The FPGA project focuses on implementing digital control functions in hardware.

**Main features documented in the repository:**

- **Verilog HDL:** Modular RTL source code for digital logic.
- **PWM LED Control:** LOW, HIGH, and AUTO operating modes.
- **Finite State Machines:** Control logic for operating-mode transitions and UART transmission.
- **Button Debouncing:** Filters mechanical button transitions to generate reliable control signals.
- **Clock and Reset Management:** PLL-based clock generation and power-on reset logic.
- **UART Transmission:** Sends operating-mode information to a serial terminal.
- **Simulation and Implementation:** Includes simulation resources, waveform images, project files, and implementation reports.

**Development tool:** Gowin FPGA design software.

Project directory: [`Chilli_FPGA/`](Chilli_FPGA/)

### 2. MCU Firmware — SN32F407F

The MCU component contains an embedded C development project for the SN32F407F microcontroller platform. Its source tree is organized into driver, module, runtime-environment, and supporting documentation directories.

**Firmware resources include:**

- Peripheral driver source code.
- GPIO and UART-related support.
- DMA and timer drivers.
- Watchdog support.
- EEPROM and Flash-related functions.
- CRC and other hardware-support functions.
- Keil uVision project configuration.

This part of the repository provides a foundation for exploring MCU peripherals, embedded C programming, firmware organization, and low-level hardware control.

**Development tool:** Keil MDK / uVision.

Project directory: [`Chilli_MCU/`](Chilli_MCU/)

### 3. System-Level Learning

The repository covers both programmable digital hardware and microcontroller firmware. Together, these areas support learning about:

- Hardware description and RTL design.
- Firmware development in C.
- Digital timing and control.
- PWM signal generation.
- UART serial communication.
- GPIO and peripheral management.
- Hardware simulation and implementation.
- Embedded project organization and technical reporting.

The repository contains separate FPGA and MCU project directories. Any direct integration between the two should be verified against the corresponding hardware design, pin assignments, and implementation documentation.

## Repository Structure

```text
FPGA_and_MCU_competition_project_2026/
├── Chilli_FPGA/
│   ├── src/
│   │   └── fpga_project-demo/
│   ├── sim/
│   └── Chilli_BaoCaoKyThuat_FPGA.pdf
├── Chilli_MCU/
│   ├── Source/
│   │   ├── Driver/
│   │   ├── Module/
│   │   └── Readme/
│   ├── RTE/
│   └── project.uvprojx
├── 289.TB.TTVM.16.09.2026.signed.signed.pdf
└── README.md
```

*Note: This is a simplified view of the repository. Additional source files, generated implementation files, simulation artifacts, and supporting resources are stored within the project directories.*

## Technologies and Tools

| Area | Technologies / Tools |
|---|---|
| FPGA hardware description | Verilog HDL |
| FPGA development | Gowin FPGA design software |
| Digital control | FSM, synchronous logic |
| Signal generation | PWM |
| Serial communication | UART |
| Input processing | Button debouncing |
| MCU firmware | Embedded C |
| MCU platform | SN32F407F |
| MCU development | Keil MDK / uVision |
| Verification | Simulation waveforms and implementation reports |
| Documentation | Technical reports and project files |

## Getting Started

### FPGA Development

1. Install a compatible version of the Gowin FPGA design software.
2. Open the FPGA project file:

   `Chilli_FPGA/src/fpga_project-demo/fpga_project-demo.gprj`

3. Review the Verilog source files, top-level module, target FPGA device, clock configuration, and pin assignments.
4. Run synthesis and implementation using the target device configuration.
5. Inspect the available simulation resources, waveforms, and implementation reports.

### MCU Firmware Development

1. Install Keil MDK / uVision with the appropriate device support and toolchain.
2. Open the MCU project file:

   `Chilli_MCU/project.uvprojx`

3. Review the project configuration and source files under `Chilli_MCU/Source/`.
4. Confirm that the required headers, driver files, libraries, and device configuration are available.
5. Build the firmware and review any compiler or linker errors before testing on hardware.

*Exact tool versions, board configuration, and hardware connections should be confirmed from the project files and technical documentation.*

## Verification and Documentation

The repository includes FPGA simulation resources, waveform images, implementation-related files, and technical reports. These materials can be used to inspect the design and understand the development process.

Before hardware testing:

- Verify the target FPGA and MCU configurations.
- Check clock, reset, and pin assignments.
- Confirm UART settings and physical connections.
- Build the MCU firmware with the intended device configuration.
- Re-run simulations and implementation checks where applicable.
- Verify hardware behavior on the actual development boards.

The repository also contains technical documentation and competition-related materials for further reference.

## Learning Outcomes

This project supports practical experience in:

- Verilog RTL design and digital hardware implementation.
- FPGA-based control systems and finite state machines.
- PWM generation and timing control.
- UART communication.
- Embedded C programming for microcontrollers.
- MCU peripheral drivers and firmware structure.
- Simulation, debugging, and implementation workflows.
- Technical documentation for embedded hardware projects.

## Project Resources

- [FPGA Source and Project Files](Chilli_FPGA/)
- [MCU Firmware and Keil Project](Chilli_MCU/)
- [FPGA Technical Report](Chilli_FPGA/Chilli_BaoCaoKyThuat_FPGA.pdf)
- [Competition Documentation](289.TB.TTVM.16.09.2026.signed.signed.pdf)

## License

No license is currently specified. Please contact the repository owner before reusing or redistributing the source code.
