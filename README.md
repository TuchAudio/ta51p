# TuchAudio L51p
Passive crossover filter for two-way speakers

## Purpose
This is a crossover filter intended for a homebrew speaker. Design is a bit unorthodox, but the circuit itself is flexible enough for many designs.

### L51p
Name comes from the desired configuration:

- `L`oudspeaker
- `5` in. woofer
- `1` in. dome tweeter
- Powered by **`P`hilips**

### Intended drivers

- Woofer: **Philips AD5060W8**
- Tweeter: **Philips AD0140T8**

### Filter design
The _woofer_ is expected to be **directly** connected to the speaker output, as the `AD5060W8` does perform as a _nearly-**full range**_ speaker -- space for a _series coil_ (`L1`) is included on the board if so desired.

The _tweeter_ branch includes an **attenuator** as the `AD0140T8` is extremely sensitive... Being a resistor (`R2`) in series with the tweeter, total impedance is higher, thus a second resistor (`R1`) _in parallel_ with this branch is included for correction. _Since the woofer is directly connected, keeping this branch on a somewhat higher impedance (around **14.5 Ω** with suggested values) is desired to avoid amplifier overload._

The high-pass filter is a simple **first-order** one (6 dB/oct) using a **1.5 µF** capacitor (`C1`). _Actual value must be matched to the desired cutoff frequency and the tweeter network impedance._

## Specs

### Original design (with recommended drivers)

- **Power handling:** 10 W RMS
- **Crossover frequency:** 7.3 kHz
- **Tweeter attenuation:** -10.2 dB
- **Nominal impedance:** 8Ω _(somewhat lower at very high frequencies)_

### Computing alternative values

$L_1 = \frac{1}{2π·f·Z_w}$

$R_2 = Z_t·(A_t-1)$

$\frac{1}{Z_n} = \frac{1}{R_1} + \frac{1}{Z_t+R_2}$, thus: $R_1 = \frac{Z_n(R_2+Z_t)}{R_2+Z_t - Z_n}$

$C_1 = \frac{1}{2π·f·Z_n}$

where:
- **$f$:** desired crossover frequency (Hz)
- **$Z_w$:** nominal woofer impedance (Ω)
- **$Z_t$:** nominal tweeter impedance (Ω)
- **$Z_n$:** desired tweeter network impedance, _less or equal than_ $Z_t+R_2$ (Ω)
- **$A_t$:** attenuation factor (linear, e.g.: $2$ for -6 dB)
