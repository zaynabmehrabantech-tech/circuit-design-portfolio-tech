# 4th-Order Sallen-Key Butterworth Low-Pass Filter

## Overview
A 4th-order active low-pass filter using two cascaded 2nd-order Sallen-Key sections, designed for audio signal conditioning with a 10 kHz cutoff frequency. Simulated in **Ngspice**.

## Design Specifications
| Parameter | Target | Simulated |
|-----------|--------|-----------|
| Filter Order | 4th (Butterworth) | 4th |
| Cutoff Frequency (fc) | 10 kHz | ~10.1 kHz |
| Passband Ripple | 0 dB (maximally flat) | < 0.1 dB |
| Stopband Rolloff | -80 dB/decade | -80 dB/decade |
| DC Gain | 0 dB (unity) | ~0 dB |
| Supply Voltage | ±12 V | ±12 V |

## Circuit Description
- **Stage 1**: 2nd-order Sallen-Key section with Q = 0.5412 (Butterworth coefficient pair a₁ = 1.8478, b₁ = 1.0)
- **Stage 2**: 2nd-order Sallen-Key section with Q = 1.3066 (Butterworth coefficient pair a₂ = 0.7654, b₂ = 1.0)
- **Op-amps** modeled as ideal VCVS sources (gain = 200,000) in unity-gain configuration
- **Component values** calculated using standard Butterworth polynomial coefficients and scaled for fc = 10 kHz

## Analyses Performed
1. **AC Analysis (.ac)** — Frequency sweep from 1 Hz to 10 MHz: magnitude, phase, and group delay
2. **Transient Analysis (.tran)** — Time-domain response verifying passband signal fidelity
3. **Measurements** — Automated gain extraction at dc, fc, 2fc, and 10fc to verify rolloff slope

## How to Run
```bash
ngspice sallen_key_butterworth_lpf.cir
```

## Key Results
- Maximally flat passband response confirmed up to ~8 kHz
- -3 dB point measured at approximately 10.1 kHz
- Stopband attenuation reaches -80 dB/decade as expected for a 4th-order Butterworth
- Group delay is nearly constant across the passband, confirming minimal phase distortion

## Files
- `sallen_key_butterworth_lpf.cir` — Complete Ngspice netlist with all analysis commands
