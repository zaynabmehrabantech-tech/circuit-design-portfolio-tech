# Transmission Line Signal Integrity Analysis

## Overview
A comprehensive study of transmission line effects on high-speed digital signals, simulated in **Ngspice**. This project characterizes impedance mismatch, reflections, termination strategies, and crosstalk to establish PCB routing design rules for signals operating above 100 MHz.

## Test Cases

### Test 1 — Matched Termination (50Ω → 50Ω line → 50Ω load)
Baseline reference showing clean signal transmission with no reflections when source, line, and load impedances are matched.

### Test 2 — Unterminated Line (Open Load)
Demonstrates full positive reflection (Γ = +1) at an open-circuited load. The reflected wave doubles the voltage at the far end, a common cause of overshoot and ringing in poorly terminated digital buses.

### Test 3 — Mismatched Load (150Ω)
Partial reflection with Γ = 0.5. Shows how a moderate impedance mismatch produces voltage overshoot and multiple reflections that degrade signal quality and eye diagram margins.

### Test 4 — Series (Source) Termination
Source-end termination strategy commonly used for point-to-point CMOS-to-CMOS interconnects. The half-amplitude initial wave reflects at the high-impedance load and settles to full amplitude after one round trip.

### Test 5 — Crosstalk (NEXT and FEXT)
Models capacitive and inductive coupling between adjacent parallel traces. Measures near-end crosstalk (NEXT) and far-end crosstalk (FEXT) on a quiet victim line induced by a switching aggressor.

## Design Rules Derived
Based on the simulation results, the following PCB routing guidelines are recommended for signals above 100 MHz:

| Guideline | Recommendation |
|-----------|----------------|
| Termination | Always terminate lines where round-trip delay > 25% of rise time |
| Trace impedance | Control to 50Ω ± 10% with continuous ground reference plane |
| Series termination | Place resistor within 0.5 inches of driver for point-to-point links |
| Parallel termination | Use at far end for multi-drop buses or when load capacitance is low |
| Crosstalk spacing | Maintain ≥ 3× trace width separation for < 3% coupling |
| Trace length matching | Match lengths within 50 mils for differential pairs |
| Via transitions | Minimize layer transitions; use ground vias adjacent to signal vias |

## How to Run
```bash
ngspice transmission_line_si.cir
```

## Key Results
- Unterminated lines produce 2× voltage overshoot — destructive for 3.3V CMOS I/O
- 150Ω mismatch causes ~25% overshoot with multi-cycle ringing settling over ~8 ns
- Series termination achieves clean settling within one round-trip delay (~2 ns for 6-inch trace)
- Near-end crosstalk peaks at ~5% of aggressor amplitude with 0.15 coupling coefficient

## Files
- `transmission_line_si.cir` — Complete Ngspice netlist with five test scenarios and automated measurements
