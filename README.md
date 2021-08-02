# Phase-Locked-Loop (PLL) IC design on Open Source Google-Skywater 130nm
### _VSD-IAT Cloud based 2-day Workshop_
##### _Date: 31st July and 1st August, 2021_
---
---

## Table of Contents

- [Day 1: Theory of PLL & Lab Set up](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#day-1-pll-theory--lab-set-up)
  - [Significance of PLL](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#significance-of-pll)
  - [Components of PLL](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#components-of-pll)
  - [Tool Set Up](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#tool-set-up)
  - [PLL Specifications](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#pll-specifications)
- [Day 2: PLL Simulation (Pre-Layout and Post-Layout)](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#day-2-pll-simulation-pre-layout-and-post-layout)
  - [Pre-Layout Simulation](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#pre-layout-simulation)
  - [Layout](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#layout)
  - [Post-Layout Simulation](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#post-layout-simulation)
 - [Tapeout Idea](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#tapeout-idea)
 - [References](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#references)
 - [Acknowledgements](https://github.com/supriyakhatoniar/avsd_PLL/blob/main/README.md#acknowlegements)

## Day 1: PLL Theory & Lab Set up
---
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

- [Google Skywater PDK](https://github.com/google/skywater-pdk) contains transistor's configuration, parameters, occupied area which is a hybrid technology for 180nm-130nm.
  Here,
  - SKY130 primitive libraries i.e. the transistor level informations need to run the simulation
  - For magic, technology file is required for the 130nm node

### PLL Specifications
- Corner : 'TT'
- Supply Voltage : 1.8V
- Operating Temperature : 27°C (Room Temperature)
- Input Frequency Range: 5MHz - 12.5Mhz
- Multiplier: 8x
- Jitter (RMS variation) < ~ 20ns
- Duty Cycle: 50%


## Day 2: PLL Simulation (Pre-Layout and Post-Layout)
---
- To get the full PLL IP, the separate spice netlist and layout is created for each block and the combination of these give the overall IP.

### Pre-Layout Simulation
- With referece to the circuit diagram, spice file(.cir) is created using notepad.

The Output of the components of PLL using Ngspice:
- #### Phase Frequency Detector Output
<img width="800" alt="pll_pfd" src="https://user-images.githubusercontent.com/69808870/127878278-e3224452-c5ba-4dcf-938b-b496da74792e.png">
  - Red: Clock 1
  - Blue: Clock 2
  - Orange: Up Signal
  - Green: Down Signal

- #### Charge Pump Output (rise due to leakage current)
<img width="800" alt="pll_cp" src="https://user-images.githubusercontent.com/69808870/127878305-9b4cf5c9-4fa0-4f1e-a7c9-0d02f38bc81f.png">
- Red: Charge pump output voltage
- Leakage: 40uV increase every 1us

- #### Frequency Divider Output
<img width="800" alt="pll_layout_fd" src="https://user-images.githubusercontent.com/69808870/127905804-33a23bde-193e-4a8c-8c9d-9176900b04d8.png">

  - Red: Output Clock
  - Blue: Input Clock

- #### Voltage Control Oscillator Output
<img width="800" alt="pll_vco" src="https://user-images.githubusercontent.com/69808870/127878367-ac2ccaaf-60be-4178-8b94-bc2cc5440d0e.png">
  - Red: Control Voltage
  - Blue: Output Clock

### Layout

Layout Design in Magic are shown below:

- #### Phase Frequency Detector Layout
<img width="800" alt="pll_layout_pfd" src="https://user-images.githubusercontent.com/69808870/127880799-a0a99d79-7c2b-43b9-9d6b-ffbb835dcee8.png">
Area: 49.09um square

- #### Charge Pump Layout
<img width="800" alt="pll_layout_cp" src="https://user-images.githubusercontent.com/69808870/127880828-7ade9151-91b2-496f-b85a-100cf62dd37a.png">
Area: 132.29um square

- #### Frequency Divider Layout
<img width="800" alt="pll_layout_fd" src="https://user-images.githubusercontent.com/69808870/127880852-0da6c1b3-7f0e-474a-86aa-024bc2f23b0d.png">
Area: 29.92um square

- #### Voltage Control Oscillator Layout
<img width="800" alt="pll_layout_vco" src="https://user-images.githubusercontent.com/69808870/127881991-75f805d3-5f58-4601-97ca-a96d07ab0e4b.png">
Area: 57.73um square

- #### MUX Layout

<img width="800" alt="pll_layout_mux" src="https://user-images.githubusercontent.com/69808870/127888316-19d25c2c-6d08-421c-8783-cd9d59f60a36.png">

Area: 12.12um square


- #### Integrated PLL Layout
<img width="800" alt="pll_layout_pll" src="https://user-images.githubusercontent.com/69808870/127881468-b47b03d0-7cae-4fd9-a3c7-083a8d443e22.png">
Area: 496.03um square

- #### A snaps of Terminal Window
<img width="800" alt="pll_layout_terminal" src="https://user-images.githubusercontent.com/69808870/127891654-7ae19920-a824-49f8-a72e-9c770aa09834.png">


### Post-Layout Simulation
The Output of the components of PLL using Ngspice:
- #### Phase Frequency Detector Output (response to 'Up' signal)
<img width="800" alt="pll_postlay_pfd2" src="https://user-images.githubusercontent.com/69808870/127889471-3ac058b7-b36a-47dd-8120-eea4868d8dd0.png">
  - Red: Clock 1
  - Blue: Clock 2
  - Orange: Up Signal
  - Green: Down Signal

- #### Charge Pump Output (response to 'Up' signal)
<img width="800" alt="pll_postlay_cp" src="https://user-images.githubusercontent.com/69808870/127889482-1bca397c-f5dd-4f3c-8e11-8e7968f0de74.png">
Orange: Charge Pump Output Voltage
  - Red: Up Signal
  - Blue: Down Signal

- #### Frequency Divider Output
<img width="800" alt="pll_postlay_fd" src="https://user-images.githubusercontent.com/69808870/127889511-a0d00c4a-250b-432a-813b-f31526ca5e4b.png">
  - Red: Input Clock
  - Blue: Output Clock

- #### Voltage Control Oscillator Output
<img width="800" alt="pll_postlay_vco" src="https://user-images.githubusercontent.com/69808870/127889512-df440524-ccc4-4a04-9999-ad03bbf6002f.png">
  - Red: Output Clock
  - Blue: Control Voltage
  
## Tapeout Idea
- To meet the requirements of a proper GPIO, it is neccessary to connect the IP pins to package.
- This task is complicated and time consuming, so we can use [Efabless Caravel](https://github.com/efabless/caravel) SoC template as vehicle to meet the requirements of fabrication.
- After successfully doing all the process, the next step is to Write GDS file which is the complete Layout information that can be sent to the fabrication centre to fabricate the IC.

## References
[1] lakshmi Sathi, "130nm PLL Clock Multiplier IP", https://github.com/lakshmi-sathi/avsdpll_1v8

## Acknowlegements
- I am grateful to Mr. [Kunal Ghosh](https://in.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836), Co-founder of [VSD](https://www.vlsisystemdesign.com/), for providing me 2-day wonderful workshop and his expert advice.
- I would like to thank Lakshmi Sathi, for guiding throught the workshop.
- I would also like to extend my thanks to Mansi Mohapatra, Mili Anand and Mukesh Nadar for their support during the workshop.
