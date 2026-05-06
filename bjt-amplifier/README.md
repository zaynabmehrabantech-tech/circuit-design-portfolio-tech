# Three-Stage BJT Common-Emitter Amplifier

## Overview
A three-stage cascaded common-emitter amplifier designed for wideband audio/IF applications, simulated entirely in **Ngspice**.

## Design Specifications
| Parameter | Target | Simulated |
|-----------|--------|-----------|
| Supply Voltage | 12 V | 12 V |
| Total Voltage Gain | ~60 dB | ~58 dB |
| Bandwidth (-3 dB) | 20 Hz – 10 MHz | 18 Hz – 15 MHz |
| Input Signal | 10 mV pk, 1 kHz | — |
| Load | 10 kΩ | 10 kΩ |

## Circuit Description
- **Three identical CE stages** using 2N2222 NPN transistors with voltage-divider biasing
- **AC coupling** between stages (0.47 µF interstage, 1 µF input/output)
- **Emitter bypass capacitors** for full AC gain per stage
- **Resistive biasing** designed for stable Q-point across temperature

## Analyses Performed
1. **DC Operating Point (.op)** — Verifies bias stability across all three stages
2. **AC Small-Signal (.ac)** — Bode plot: gain and phase from 10 Hz to 100 MHz
3. **Transient (.tran)** — Time-domain response to 1 kHz sinusoidal input

## How to Run
```bash
ngspice three_stage_ce_amplifier.cir
```

## Key Results
- Gain peaks at approximately 58 dB in the midband region
- Lower -3 dB frequency at ~18 Hz (set by input coupling capacitor)
- Upper -3 dB frequency at ~15 MHz (limited by transistor ft and Miller effect)
- Phase margin remains adequate for stable operation across the passband

## Files
- `three_stage_ce_amplifier.cir` — Complete Ngspice netlist with analysis commands
