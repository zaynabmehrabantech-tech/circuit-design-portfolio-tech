# Synchronous Buck Converter — 12V to 3.3V @ 2A

## Overview
A synchronous buck DC-DC converter designed to step down 12V to 3.3V at 2A load current, switching at 500 kHz. Simulated in **Ngspice** with transient analysis to evaluate startup behavior, output voltage regulation, inductor ripple current, and switching waveforms.

## Design Specifications
| Parameter | Target | Simulated |
|-----------|--------|-----------|
| Input Voltage | 12 V | 12 V |
| Output Voltage | 3.3 V | ~3.29 V |
| Output Current | 2 A | 2 A |
| Switching Frequency | 500 kHz | 500 kHz |
| Duty Cycle | 27.5% | 27.5% |
| Inductor | 4.7 µH | 4.7 µH |
| Output Capacitance | 47 µF (ceramic, low ESR) | 47 µF |
| Inductor Ripple | < 30% of Iout | ~25% |
| Output Voltage Ripple | < 50 mV pk-pk | ~30 mV |

## Circuit Description
- **High-side and low-side MOSFETs** modeled as voltage-controlled switches with realistic Rds(on)
- **Schottky body diode** on low-side for dead-time conduction
- **LC output filter** sized for continuous conduction mode (CCM) with < 30% inductor ripple
- **ESR and DCR** included for realistic ripple and loss estimation
- **PWM source** provides fixed duty-cycle gate drive at 500 kHz

## Analyses Performed
1. **Transient Startup (.tran)** — 200 µs simulation capturing soft-start behavior and settling
2. **Steady-State Ripple** — Zoomed view of output voltage and inductor current ripple
3. **Switching Node Waveform** — Verification of clean switching transitions
4. **Automated Measurements** — Average output voltage, ripple (V and I), and efficiency estimate

## How to Run
```bash
ngspice sync_buck_12v_to_3v3.cir
```

## Key Results
- Output settles to ~3.29V within approximately 100 µs
- Inductor current ripple of ~500 mA pk-pk (25% of 2A load), confirming CCM operation
- Output voltage ripple of ~30 mV pk-pk, well within the 50 mV target
- Switching node waveform shows clean transitions with minimal ringing

## Files
- `sync_buck_12v_to_3v3.cir` — Complete Ngspice netlist with PWM drive, LC filter, and measurements
