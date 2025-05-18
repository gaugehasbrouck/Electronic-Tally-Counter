# FPGA-Based Theater Counter Project

## Contents

* [Why This Project?](#why-this-project)
* [Block Overview](#block-overview)

  * [1. Power Supply Block](#1-power-supply-block)
  * [2. FPGA Block](#2-fpga-block)
  * [3. Display Block](#3-display-block)
* [Bill of Materials (BOM)](#bill-of-materials-bom)

  * [Core Components](#core-components)
  * [Display & Driver](#display--driver)
  * [Power Management](#power-management)
  * [Controls & Output](#controls--output)
  * [Passive Components](#passive-components)
* [Next Steps](#next-steps)

---

## Why This Project?

This project is a compact, battery/USB/DC-powered up/down/reset counter inspired by the counters used in movie theaters or event spaces. The goal is to develop a fully self-contained, handheld or desktop-friendly device that leverages an FPGA for logic implementation, uses a 2-digit 7-segment display for visual output, and supports JTAG programming and debug. The project showcases:

* Low-power embedded hardware design
* FPGA digital design
* Real-world multiplexed display driving
* PCB layout and SMD/assembly readiness

---

## Block Overview

### 1. Power Supply Block

**Input Options:**

* 9V Battery via DC barrel jack
* 5V USB via barrel adapter

**Voltage Rails:**

* **5V** – for ULN2003A driver, 7-segment display, and buzzer (from barrel jack directly or via AMS1117-5.0)
* **3.3V** – for FPGA I/O (AMS1117-3.3 or MCP1700-3.3)
* **1.2V** – for FPGA core (MIC5317-1.2 or LD1117-1.2)

**Protection:**

* Schottky diode (e.g., 1N5819) for reverse polarity
* Bulk capacitors and decoupling caps for stability

---

### 2. FPGA Block

**FPGA:** Lattice iCE40LP384-SG32 (QFN-32)

* Non-volatile (external SPI flash required)
* I/O: Operates at 3.3V
* Core: 1.2V
* Logic: Handles debounced button inputs, counter FSM, and display multiplexing

**Programming Interface:**

* JTAG header (FTDI or compatible USB Blaster)

---

### 3. Display Block

**Display:**

* SunLED XZFMDK10A2 – Red 2-digit 7-segment display, Common Anode, SMD

**Driver IC:**

* ULN2003A – 7-channel NPN Darlington driver

  * Sinks current from 7-segment segments
  * Accepts 3.3V logic inputs from FPGA
  * Powered via 5V rail

**Multiplexing:**

* FPGA will cycle digits using select pins and drive segments via ULN2003

**Buzzer (Optional):**

* Driven via ULN2003 channel or separate NPN transistor
* Enable/disable via SPDT switch

---

## Bill of Materials (BOM)

### Core Components

* **iCE40LP384-SG32** — Lattice FPGA, QFN-32 — Qty: 1
* **SPI Flash (e.g., W25Q16)** — External config memory — Qty: 1

### Display & Driver

* **SunLED XZFMDK10A2** — 2-digit red 7-segment display, SMD — Qty: 1
* **ULN2003A** — 7-channel Darlington driver — Qty: 1

### Power Management

* **AMS1117-5.0** — 5V regulator — Qty: 1
* **AMS1117-3.3** or **MCP1700-3.3** — 3.3V LDO — Qty: 1
* **MIC5317-1.2** or **LD1117-1.2** — 1.2V LDO — Qty: 1
* **1N5819** — Schottky diode for reverse polarity protection — Qty: 1
* **DC Barrel Jack** — Power input (5–9V support) — Qty: 1

### Controls & Output

* **Tactile Buttons** — Up / Down / Reset — Qty: 3
* **SPDT Switch** — For enabling/disabling buzzer — Qty: 1
* **Buzzer** — Small 5V passive buzzer — Qty: 1

### Passive Components

* **Resistors (150Ω, 120Ω)** — LED current limiting — Qty: 7–14
* **Capacitors (0.1µF, 10µF)** — Decoupling and bulk — Qty: \~10

---

## Next Steps

* Design schematic and footprint layout in KiCad
* Assign FPGA I/O pinout for buttons, segments, digit select, buzzer
* Build VHDL or Verilog design for counter and display logic
* Prepare and order assembled PCB
* Program and test via JTAG

---

This README will be updated as the design progresses.
