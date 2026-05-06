# Analog & RF Circuit Design Portfolio

**Zaynab Mehraban** — Electronics Engineer | Analog & RF Circuit Designer | Ngspice / LTspice / KiCad

---

## About

This repository contains a selection of personal circuit design, simulation, and PCB layout projects demonstrating hands-on proficiency with **Ngspice**, analog circuit design, RF engineering, power electronics, and signal integrity analysis. Each project includes complete simulation netlists, design rationale, and documented results.

> **Note:** The majority of my professional work has been performed under contract for private clients and is subject to confidentiality agreements. The projects presented here are independent demonstrations of my technical capabilities and workflow, created outside of any client engagement.

## Projects

### 1. [Three-Stage BJT Common-Emitter Amplifier](./bjt-amplifier/)
A cascaded three-stage CE amplifier designed for wideband audio/IF applications (~58 dB gain, 18 Hz – 15 MHz bandwidth). Includes DC bias verification, AC Bode plot analysis, and transient response simulation in Ngspice.

### 2. [4th-Order Sallen-Key Butterworth Low-Pass Filter](./sallen-key-filter/)
An active filter using two cascaded 2nd-order Sallen-Key sections implementing a maximally flat Butterworth response with fc = 10 kHz. Simulated in Ngspice with magnitude/phase response, group delay analysis, and automated measurements.

### 3. [Synchronous Buck Converter — 12V to 3.3V @ 2A](./buck-converter/)
A PWM-driven synchronous buck DC-DC converter switching at 500 kHz. Transient analysis covers startup behavior, output voltage regulation, inductor ripple current, and switching node waveforms with efficiency estimation.

### 4. [Transmission Line Signal Integrity Analysis](./transmission-line-si/)
Comprehensive study of impedance mismatch, reflections, termination strategies, and crosstalk on high-speed digital signals using Ngspice TLINE models. Derives practical PCB routing design rules for signals above 100 MHz.

### 5. [Low-Noise RF Preamplifier — PCB Design (KiCad)](./rf-preamp-pcb/)
Full design flow for a 100–500 MHz LNA board using the BFR92A RF transistor: pre-layout Ngspice simulation, impedance-controlled 50Ω microstrip routing, RF-specific layout rules, BOM with sourcing, and detailed design notes. Demonstrates schematic-to-layout methodology for RF circuits.

## Tools & Skills Demonstrated
- **Ngspice** — Netlist creation, SPICE modeling, AC/DC/transient analysis, parametric measurements
- **KiCad** — Schematic capture, impedance-controlled PCB layout, Gerber generation, BOM management
- **Analog Circuit Design** — Amplifier biasing, active filter synthesis, matching networks
- **RF Engineering** — LNA design, impedance matching, transmission line analysis, crosstalk characterization
- **Power Electronics** — DC-DC converter design, inductor/capacitor sizing, thermal analysis
- **Signal Integrity** — Termination strategies, reflection analysis, design rule derivation
- **Documentation** — Annotated netlists, design specification tables, BOM preparation, layout rationale

## How to Run Simulations
All simulations require [Ngspice](http://ngspice.sourceforge.net/) (tested with v40+):
```bash
cd <project-folder>
ngspice <netlist-file>.cir
```

## Contact
- **Email:** zaynabmehrabantech@gmail.com
- **Phone:** (213) 534-6884
