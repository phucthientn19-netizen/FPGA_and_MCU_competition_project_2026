# FPGA & MCU Design Danang 2026 — Team Chilli

Team **Chilli** solution for the *FPGA and MCU Design Competition – Da Nang 2026* (University of Danang – University of Science and Technology, Faculty of Electronics and Artificial Intelligence). The repository contains two independent hardware projects:

| Track | Project | Board | Language / tool |
|---|---|---|---|
| **FPGA** | Multi-mode PWM LED monitoring and control system via UART | Kiwi 1P5 (Gowin GW1N-UV1P5) | Verilog HDL, Gowin EDA |
| **MCU** | Digital clock with alarm, EEPROM storage and buzzer | SONiX SN32F407_EVK-V1.0 (SN32F407FG) | Embedded C, Keil uVision |

The two projects do not communicate with each other.

---

## 1. FPGA — Multi-mode PWM control and UART monitoring (Kiwi 1P5)

A synchronous design in which a single LED is driven in three PWM modes selected by two push buttons, and the current mode is reported to a PC over UART.

### Architecture

`top_system` connects the following blocks (all on one 50.1429 MHz clock):

| Block | Function |
|---|---|
| PLL (Gowin PLLO IP) | 27 MHz on-board clock → 50.1429 MHz system clock |
| Power-on reset | 16-bit counter holds `rst_n` low for about 1.3 ms after power-up |
| Debounce ×2 | 2-stage synchronizer, 20 ms stability filter (1,002,857 cycles), single-cycle pulse on the falling edge |
| Main FSM | Mode FSM (LOW / HIGH / AUTO) plus a UART string FSM (IDLE → SEND → WAIT_BUSY → WAIT_DONE) |
| PWM LED | 1 kHz PWM (`PWM_MAX` = 50,143) |
| UART TX | 115200 bps, 8N1, 4 states (IDLE, START, DATA, STOP), `tx_busy` handshake |

### Operating modes

| Mode | LED behaviour | UART message |
|---|---|---|
| LOW | Fixed 25% duty cycle | `MODE: LOW` |
| HIGH | Fixed 100% duty cycle | `MODE: HIGH` |
| AUTO | Breathing effect, 0% → 100% → 0% in a 2 s cycle (1 s up, 1 s down) | `MODE: AUTO` |

- **Button 1:** toggles LOW ↔ HIGH, and returns to LOW from AUTO.
- **Button 2:** always switches to AUTO.
- A message is sent at start-up and on every mode change, each ending in `\r\n`.

### UART baud-rate divider

`50,142,900 Hz / 115,200 bps ≈ 435.27` → divider **435** → actual 115,271 bps (error ≈ +0.06%).

### Pin assignment (Kiwi 1P5, LVCMOS33)

| Signal | Pin | Function |
|---|---|---|
| `clk_27m` | 4 | 27 MHz on-board clock |
| `btn1` | 35 | Button 1 (active-low) |
| `btn2` | 36 | Button 2 (active-low) |
| `led` | 27 | PWM-controlled LED |
| `uart_tx` | 34 | UART TX to the on-board USB-UART bridge (GWU2U) |

### Results

- Simulation waveforms confirm the 20 ms debounce, the 25% / 100% duty cycles (12,535 / 50,143 ≈ 25%) and the breathing cycle in AUTO mode.
- On hardware, the LED shows the three modes and a PC terminal (e.g. Hercules, COM port, 115200 8N1) receives `MODE: LOW`, `MODE: HIGH` and `MODE: AUTO`.

Details: `Chilli_FPGA/Chilli_BaoCaoKyThuat_FPGA.pdf`.

---

## 2. MCU — Digital clock with alarm (SN32F407_EVK)

A digital clock written in C on the SONiX SN32F407 evaluation board. The firmware uses a **superloop with polling** and a **non-blocking 1 ms time base**; the user interface is a finite state machine over five modes (normal, set hour, set minute, alarm hour, alarm minute).

### Features

- Time shown as **HH.MM** on the four 7-segment digits; starts at 00:00 after power-up, hours 00–23.
- The digits being edited flash with a 1 s cycle (0.5 s on / 0.5 s off).
- Alarm time stored in **EEPROM** with a magic byte (`0xAA`); it is restored automatically after a reset or power loss (alarm seconds = 0).
- **Buzzer:** "beep-beep" for 5 s when the alarm time is reached (0.5 s on / 0.5 s off); a 0.3 s beep on every button press and when a setting mode times out.
- **LED D6** blinks (1 s cycle) while a setting mode is active.
- **30 s timeout:** with no button press, the system leaves the setting mode and returns to normal.
- **Watchdog timer** restarts the MCU if the program hangs.

### Buttons

| Button | Function |
|---|---|
| SW3 | Time setting: normal → hour → minute → normal |
| SW16 | Alarm setting: normal → alarm hour → alarm minute → save to EEPROM and enable the alarm |
| SW6 (+) | Increase hour or minute (wraps 23 → 0 and 59 → 0) |
| SW10 (−) | Decrease hour or minute (wraps 0 → 23 and 0 → 59) |

### Firmware structure

The main loop runs: feed watchdog → display scan → update time and check alarm → buzzer and alarm handling → timeout → key processing → display render.

The `Chilli_MCU/Source/Driver` folder holds the SONiX SDK peripheral drivers that the application uses; the clock application itself is in `Chilli_MCU/Source/Module`.

Details: the MCU technical report (`Chilli_BaoCaoKyThuat_MCU.pdf`).

---

## Repository structure

```
FPGA_and_MCU_competition_project_2026/
├── Chilli_FPGA/
│   ├── src/fpga_project-demo/      # Gowin project (.gprj) and Verilog sources
│   ├── sim/                        # simulation resources
│   └── Chilli_BaoCaoKyThuat_FPGA.pdf
├── Chilli_MCU/
│   ├── Source/                     # Driver (SONiX SDK), Module (application), Readme
│   ├── RTE/
│   └── project.uvprojx             # Keil uVision project
├── 289.TB.TTVM.16.09.2026.signed.signed.pdf   # competition notice
└── README.md
```

## Build

- **FPGA:** open `Chilli_FPGA/src/fpga_project-demo/fpga_project-demo.gprj` in Gowin EDA, select the GW1N-UV1P5 device, run synthesis and place & route, then program the Kiwi 1P5 through its on-board USB-JTAG.
- **MCU:** open `Chilli_MCU/project.uvprojx` in Keil uVision with the SN32F407 device pack, build and flash the SN32F407_EVK board.

## Tools

Verilog HDL · Gowin EDA · Hercules serial terminal · Embedded C · Keil uVision

## Team

Team **Chilli** — Phạm Huỳnh Đức, Huỳnh Phúc Thiện, Dương Quốc Bảo, Nguyễn Đức Anh Tuấn.

## License

No license has been specified yet. Please contact the repository owner before reusing the source code.
