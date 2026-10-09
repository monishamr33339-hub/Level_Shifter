\# Cascode Voltage Level Shifter Design (90nm CMOS)



This repository contains the schematic design, layout implementation, and Spectre simulation setup for a \*\*Cascode Voltage Level Shifter\*\* designed in Cadence Virtuoso using the GPDK 90nm PDK (`gpdk090`).



\## Project Overview



Level shifters convert low-voltage digital signals ($VDDL$) to higher voltage domain signals ($VDDH$) without degrading switching performance or over-stressing low-voltage thin-oxide transistors. The cascode architecture provides intermediate voltage shielding for lower NMOS devices while enabling cross-coupled PMOS pull-up switching.



\### Specifications \& Operating Parameters



| Parameter | Value / Unit | Description |

| :--- | :--- | :--- |

| \*\*Process Technology\*\* | 90nm CMOS (`gpdk090`) | Generic Process Design Kit |

| \*\*Low Supply Domain ($VDDL$)\*\* | 1.5 V | Core signal domain |

| \*\*High Supply Domain ($VDDH$)\*\* | 2.5 V | Output driving domain |

| \*\*Input Signal ($IN / IN\\\_B$)\*\* | 0 V – 1.5 V | Differential pulse input |

| \*\*Output Signal ($OUT$)\*\* | 0 V – 2.5 V | Level-shifted output |

| \*\*Operating Frequency\*\* | 50 MHz ($T = 20\\text{ ns}$) | Transient simulation period |



\---



\## Circuit Architecture \& Transistor Sizing



The cascode level shifter consists of four primary sections:

1\. \*\*Low-Voltage Input NMOS (`NM0`, `NM1`)\*\*: $W/L = 3.0\\,\\mu\\text{m} / 100\\text{ nm}$ (`gpdk090\_nmos1v`) driven by differential inputs $IN$ and $IN\\\_B$.

2\. \*\*Cascode NMOS Shield Transistors (`M0`, `M1`)\*\*: $W/L = 800\\text{ nm} / 280\\text{ nm}$ (`gpdk090\_nmos2v`) with gates biased to $VDDL$ to limit maximum voltage across input devices.

3\. \*\*Cross-Coupled PMOS Pull-Up Pair (`M2`, `M3`)\*\*: $W/L = 500\\text{ nm} / 500\\text{ nm}$ (`gpdk090\_pmos2v`) connected to $VDDH$ to latch the level-shifted state.



\---



\## Repository Structure

.

├── Layout.jpeg               # Custom IC layout view

├── schematic.jpeg            # Level shifter schematic view

├── schematic\_zoomed.jpeg     # Detailed transistor sizing view

├── Test\_Schematic.jpeg       # Testbench setup view (VDDL, VDDH, pulse sources)

├── Transient Analysis.jpeg   # Spectre transient waveforms

├── .gitignore                # Git ignore rules for Cadence/Spectre logs

├── LICENSE                   # MIT License

└── README.md                 # Project documentation



\---



\## Simulation Results



A transient analysis ($t\_{\\text{stop}} = 100\\text{ ns}$) was performed in Spectre to verify dynamic level shifting:



\* \*\*Input ($IN$)\*\*: 0 V to 1.5 V pulse waveform ($t\_r = t\_f = 100\\text{ ps}$, period = $20\\text{ ns}$).

\* \*\*Output ($OUT$)\*\*: Successfully shifts to full swing (0 V to 2.5 V) with clean rising and falling transitions and negligible overshoot.



\---



\## Prerequisites \& Setup



1\. \*\*Cadence Virtuoso\*\*: IC6.1.7 or later.

2\. \*\*Spectre Circuit Simulator\*\*: Integrated ADE L/XL workflow.

3\. \*\*PDK\*\*: `gpdk090\_v4.6` configured in `cds.lib`.

