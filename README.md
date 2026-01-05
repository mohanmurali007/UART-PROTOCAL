# UART Baud Rate Generator (Verilog HDL)

## 🎯 Objective
The objective of this project is to design a **robust UART baud-rate tick generator** using **Verilog HDL**.  
The module derives a **baud-rate ×16 oversampling clock** from a **100 MHz system clock**, which is a fundamental requirement for accurate UART transmission and reception.

---

## 📌 Project Overview
UART communication relies on strict timing accuracy. This project implements a **counter-based clock divider** that generates a periodic `tick` signal at a frequency equal to:

Baud Rate × 16

The generated tick can be directly used by UART transmit and receive logic for bit timing and data sampling.  
The design follows **standard UART implementation practices** used in FPGA and VLSI systems.

---

## ✨ Key Features
- Designed for **100 MHz FPGA system clock**
- Supports standard UART baud rates
- Uses **16× oversampling**
- Fully synchronous design
- Clean and deterministic reset behavior
- Lightweight and resource-efficient
- Easy integration into UART cores

---

## ⚙️ Baud Rate Calculation
The counter limit value `M` is computed using:


### Typical Configurations

| Baud Rate | Oversampling | M Value | Counter Width |
|----------|-------------|---------|----------------|
| 9600     | 16×         | ~651    | 10 bits |
| 19200    | 16×         | ~326    | 9 bits |
| 115200   | 16×         | ~52     | 6 bits |

> The counter width must be sufficient to count up to `M − 1`.

---

## 🧩 Module Interface

### Inputs
| Signal | Description |
|------|------------|
| `clk_100MHz` | 100 MHz system clock |
| `reset` | Active-high synchronous reset |

### Outputs
| Signal | Description |
|------|------------|
| `tick` | One-clock-cycle pulse at (Baud Rate × 16) |

---

## 🏗️ Architecture Description

### Internal Blocks
1. **Counter Register**
   - Increments on each rising edge of the system clock
   - Resets to zero when `reset` is asserted

2. **Comparator Logic**
   - Detects when the counter reaches `M − 1`

3. **Tick Generation Logic**
   - Generates a single-cycle `tick` pulse when the counter wraps

---

## 🔁 Timing Behavior


Each tick corresponds to **1/16th of one UART bit period**.

---

## 📂 File Details

| File Name | Description |
|----------|------------|
| `baud_gen.v` | UART baud-rate ×16 tick generator |

### Design Characteristics
- HDL Language: **Verilog**
- Clock Domains: **Single-clock**
- Reset Type: **Synchronous, Active-High**
- Target Platform: **FPGA / Digital Hardware**

---

## 🚀 Applications
This baud rate generator is suitable for:

- UART Transmitter (TX) modules
- UART Receiver (RX) modules
- FPGA-to-PC serial communication
- Embedded system debug interfaces
- SoC peripheral subsystems
- Digital communication laboratory experiments
- Academic and industrial VLSI projects

---

## ⚠️ Limitations
- Fixed **16× oversampling** (not dynamically configurable)
- Designed specifically for **100 MHz clock frequency**
- Baud rate modification requires **manual recompilation**
- Does not support **fractional baud rates**
- No compensation for clock drift or jitter
- Not suitable for runtime baud-rate switching

---

## 🛠️ Customization Notes
- Recalculate `M` when changing baud rate
- Ensure adequate counter bit width
- Re-synthesize design after parameter changes

---

## 🔮 Possible Enhancements
- Parameterized system clock frequency
- Runtime-selectable baud rates
- Fractional baud-rate generation
- Support for alternative oversampling ratios
- Integration with a complete UART core

---

## ✅ Design Notes
- Fully synthesizable logic
- No latches or combinational feedback
- Predictable timing behavior
- Suitable for real hardware deployment

---

## 📜 License
This project is intended for **educational, research, and personal use**.  
Users are free to modify and integrate it into their own UART designs.

---

### ⭐ If you find this project useful, consider starring the repository!
