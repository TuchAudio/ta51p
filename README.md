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
- **Nominal impedance:** 8Ω _(somewhat lower at very high frequencies, around **5.2 Ω**)_

### Computing alternative values

`L1` = 1/(2π·f·Zw)

`R2` = Zt·(At-1)

Zn = `R1` || (Zt+`R2`)

`C1` = 1/(2π·f·Zn)

where:
- **f**: desired crossover frequency
- **Zw**: nominal woofer impedance
- **Zt**: nominal tweeter impedance
- **Zn**: desired tweeter network impedance
- **At**: attenuation factor (linear)
