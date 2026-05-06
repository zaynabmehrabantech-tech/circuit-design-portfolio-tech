# RF Preamplifier PCB — Design Notes

## 1. Impedance-Controlled Routing

The 50Ω microstrip trace width was calculated using standard microstrip equations for the chosen stackup:

- Substrate: FR4, εr = 4.4, tan δ ≈ 0.02
- Dielectric thickness (h): 1.0 mm
- Copper thickness (t): 35 µm (1 oz)
- Calculated trace width (w): 1.85 mm for Z0 = 50Ω

All RF traces between the SMA connectors and the transistor maintain this width. Non-RF traces (bias, power) are routed at 0.3 mm width to minimize board area without impedance concerns.

## 2. Component Placement Strategy

The layout follows a linear signal flow from input SMA (left) through the LNA stage to output SMA (right):

```
[SMA_IN] → [L_in] → [C_in] → [Q1 BFR92A] → [C_block_out] → [L_out] → [C_out] → [SMA_OUT]
                                    |
                              [Bias network]
                              [Decoupling]
```

- Input and output connectors are placed on opposite edges to maximize reverse isolation
- Bias components are placed perpendicular to the RF signal path to minimize coupling
- Decoupling capacitors are placed within 2 mm of the collector Vcc connection

## 3. Ground Plane Integrity

The bottom copper layer serves as a continuous, unbroken ground plane. Critical rules:

- **No traces routed on the bottom layer** — all routing on top
- **No ground plane cuts or slots** under or near RF signal paths
- **Via stitching** at 3 mm intervals around the board perimeter
- **Four ground vias per SMA connector pad** for low-inductance RF grounding
- **Ground vias adjacent to every signal via** (if any layer transitions are needed)

## 4. Parasitic Considerations

At 200–500 MHz, component parasitics become significant:

- **Capacitors**: Only C0G/NP0 dielectric used in the RF signal path. X7R is acceptable for supply decoupling only. C0G has minimal voltage coefficient and low ESR at RF.
- **Inductors**: Murata LQW15 wirewound series selected for Q > 30 at 200 MHz. Self-resonant frequency (SRF) verified to be > 1.5 GHz for all values used.
- **Resistors**: Thin-film preferred for emitter degeneration (R_e) due to lower parasitic inductance than thick-film at RF.
- **PCB traces**: Kept as short as physically possible between matching network components. Each millimeter of trace adds approximately 1 nH of parasitic inductance.

## 5. Thermal Management

At Ic = 8 mA and Vce = 2.5 V, the transistor dissipates approximately 20 mW — negligible for the SOT-23 package. No special thermal relief is required, but the emitter pad is connected to the ground plane through two vias for moderate heat sinking.

## 6. Test Points

Two test points are included on the board:
- **TP1**: Collector DC voltage (for bias verification without disturbing the RF path)
- **TP2**: Supply voltage at the decoupling network

Test points are implemented as 1.0 mm exposed pads, placed away from RF traces to avoid probe-induced parasitics during measurement.
