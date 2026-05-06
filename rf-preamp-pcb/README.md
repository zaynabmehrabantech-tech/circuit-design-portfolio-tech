# Low-Noise RF Preamplifier — PCB Design (KiCad)

## Overview
A compact low-noise amplifier (LNA) board designed for 100–500 MHz reception, built around the NXP BFR92A NPN RF transistor. This project covers the full design flow from pre-layout SPICE simulation in **Ngspice** through schematic capture and PCB layout in **KiCad**, with RF-specific design rules applied throughout.

## Design Specifications
| Parameter | Target | Simulated (Pre-Layout) |
|-----------|--------|------------------------|
| Frequency Range | 100 – 500 MHz | 95 – 520 MHz (-3 dB) |
| Center Frequency | 200 MHz | 200 MHz |
| Gain at 200 MHz | > 15 dB | ~17 dB |
| Noise Figure | < 2.0 dB | ~1.4 dB (estimated) |
| Supply Voltage | 5.0 V | 5.0 V |
| Bias Current (Ic) | 8 mA | 8.1 mA |
| Input / Output Impedance | 50 Ω | 50 Ω (matched) |
| Board Size | ≤ 30 mm × 25 mm | 28 mm × 22 mm |

## Circuit Description
- **Topology**: Common-emitter with partial emitter degeneration for gain stability
- **Transistor**: BFR92A (ft ≈ 5 GHz, NF = 1.1 dB at 200 MHz)
- **Input matching**: L-network transforming 50Ω source to transistor optimal noise impedance
- **Output matching**: L-network transforming collector impedance to 50Ω load
- **Bias**: Resistive voltage divider with RF-bypassed emitter resistor
- **Supply filtering**: Two-stage decoupling (100 nF MLCC + 10 pF C0G)

## PCB Design Details

### Layer Stackup (2-layer, 1.0 mm FR4)
| Layer | Function |
|-------|----------|
| Top (L1) | Signal, components, RF traces |
| Bottom (L2) | Continuous ground plane |

### RF Design Rules Applied
| Rule | Value | Rationale |
|------|-------|-----------|
| Trace width (50Ω microstrip) | 1.85 mm | Calculated for 1.0 mm FR4, εr = 4.4 |
| Ground plane clearance | Continuous, unbroken | Minimize return path inductance |
| Via stitching pitch | ≤ 3 mm | Suppress parallel-plate resonance |
| Component placement | All RF on top layer | Minimize via transitions in signal path |
| Input/output isolation | Components on opposite sides | Prevent feedback oscillation |
| SMA connector grounding | 4 ground vias per pad | Low-inductance RF ground transition |
| Decoupling cap placement | < 2 mm from Vcc pin | Minimize supply loop area |
| Trace bends | 45° chamfered or curved | Avoid impedance discontinuities |

### Grounding Strategy
- Unbroken bottom-layer ground plane with no splits or cuts under RF signal paths
- Star-ground concept: separate via connections for bias network and RF return
- Via stitching ring around board perimeter for edge radiation suppression

### Component Selection Notes
- All matching and bypass capacitors are **C0G/NP0** dielectric for low loss and stable RF performance
- Inductors selected from Murata **LQW15** series (high-Q wirewound, SRF well above 500 MHz)
- 0402 package size chosen for minimal parasitic inductance at operating frequencies

## Project Files
```
rf-preamp-pcb/
├── README.md                        # This file
├── BOM.csv                          # Bill of materials with MPN and sourcing
├── lna_preamp_prelayout.cir         # Pre-layout Ngspice simulation netlist
└── design-notes.md                  # Detailed RF layout rationale
```

> **Note on KiCad source files:** The original KiCad project (.kicad_pro, .kicad_sch, .kicad_pcb) and exported Gerber/drill files are available upon request. They are not included in this public repository to keep the focus on design methodology and simulation validation.

## Pre-Layout Simulation
The Ngspice netlist (`lna_preamp_prelayout.cir`) validates the circuit before committing to layout:
- **DC operating point**: Confirms Ic ≈ 8 mA, Vce ≈ 2.5 V for low-noise bias
- **AC gain**: Swept from 10 MHz to 2 GHz — confirms > 15 dB gain across 100–500 MHz
- **Input impedance**: Verifies matching network centers near 50Ω at 200 MHz

## How to Run the Simulation
```bash
ngspice lna_preamp_prelayout.cir
```

## Key Design Decisions
1. **BFR92A over BFP640**: Lower cost, adequate ft for sub-GHz, well-characterized SPICE model available
2. **2-layer vs 4-layer**: Sufficient for sub-GHz single-stage LNA; keeps fabrication cost low for prototyping
3. **Partial emitter degeneration**: 12Ω unbypassed at DC for bias stability; bypassed at RF by 1 nF cap for full gain
4. **L-match over pi-match**: Fewer components, lower insertion loss for narrowband 50Ω matching
5. **0402 passives**: Good balance between parasitic performance and hand-soldering feasibility for prototypes
