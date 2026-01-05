# UART Baud Rate Generator (Verilog)

## 📌 Objective
The objective of this project is to design a **UART baud rate tick generator** using Verilog HDL.  
The module converts a **100 MHz system clock** into a precise **baud-rate ×16 tick**, which is required for reliable UART transmission and reception.

---

## 📂 Project Description
This repository contains a Verilog module that generates timing ticks for UART communication using a counter-based clock divider approach.

The generated `tick` signal is asserted for **one clock cycle** at a frequency equal to:

Baud Rate × 16 (oversampling)

This design follows standard UART implementation practices used in FPGA and ASIC designs.

---

## ✨ Features
- Designed for **100 MHz FPGA clock**
- Supports standard UART baud rates
- Uses **16× oversampling**
- Fully synchronous logic
- Reset-safe operation
- Easy to modify for different baud rates
- Synthesizable and FPGA-ready

---

## ⚙️ Baud Rate Calculation


### Example Values

| Baud Rate | Oversampling | M Value | Counter Bits |
|----------|-------------|---------|--------------|
| 9600     | 16×         | ~651    | 10 bits      |
| 19200    | 16×         | ~326    | 9 bits       |
| 115200   | 16×         | ~52     | 6 bits       |

> ⚠️ Update the counter width and `M` value when changing baud rates.

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
| `tick` | Baud-rate ×16 pulse (1-clock-cycle wide) |

---

## 🏗️ Internal Working
1. A counter increments on every rising edge of `clk_100MHz`
2. When the counter reaches `M-1`, it resets to zero
3. A one-cycle `tick` pulse is generated at that moment
4. This tick drives UART sampling logic

---

## 🔁 Functional Flow


Each tick corresponds to **1/16 of a UART bit duration**.

---

## 🧪 Example Usage

```verilog
always @(posedge clk_100MHz)
begin
    if (tick)
        rx_sample <= rx;
end

The counter limit value **M** is calculated using:

