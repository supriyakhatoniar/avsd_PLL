# Phase-Locked-Loop (PLL) IC design on Open Source Google-Skywater 130nm
### _VSD-IAT Cloud based 2-days Workshop_
##### _Date: 31st July and 1st August, 2021_
---

## Table of Contents

- [Day 1: Theory of PLL & Lab Set up](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#day-1-theory-of-pll--lab-set-up)

## Day 1: PLL Theory & Lab Set up

### Significance of PLL
- Significance of PLL is to get a very precise clock signal without frequency or phase noise and simultaneously flexibility of variation of frequency as user's choice. Entire purpose of PLL is to make the voltage control oscillator meet the Spectral purity of the quartz crystal oscillator while still mainatining the flexibility.


### Components of PLL

![PLL components git](https://user-images.githubusercontent.com/69808870/127848939-f242b644-21f3-49f6-97e2-1991dfef1863.png)

- VCO is the on chip oscillator
- PFD compares the output signal with the reference signal.
- CP converts the digital signal comes from the PFD to analog signal to control the VCO.
- LPF smoothens the charge from output signal. It also have a role in sustainibility of the feedback loop.
- FD converts the whole system into a frequency multiplier.

Such PLL is commonly called as clock multiplier PLL.


### Tool Set Up
- Ngspice
  - For Transistor level Circuit Simulation

- Magic
  - For Layout design and Parasitic Extraction ( and also GDS Write feature in later)


SKY130 primitive libraries i.e. the transistor level informations need to run the simulation

For magic, technology file is required for the 130nm node

### PLL Specifications
- Corner : 'TT'
- Supply Voltage : 1.8V
- Operating Temperature : 27°C (Room Temperature)
- Input Frequency Range: 5MHz - 12.5Mhz
- Multiplier: 8x
- Jitter (RMS variation) < ~ 20ns
- Duty Cycle: 50%
