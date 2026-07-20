# Conductors & Wiring
Part of the **[hardware eXPerience](https://github.com/gom9000/xp-hardware)** collection: reusable engineering knowledges built through practical experimentation.

## Background
When prototyping on stripboards or perforated PCBs, it is customary for hobbyists to use surplus component leads (typically resistors and diodes) as conductors. These leads conveniently come mainly in two recurring diameters, $0.5\text{mm}$ and $0.8\text{mm}$, which this document treats as the two reference gauges. These notes document the practical design rules and wire gauge choices adopted to ensure low voltage drops and structural reliability under load when using these leads.


## Design Basis
Two quantities control the voltage drop per meter of a conductor: the material's resistivity ($\rho$) and the current density you choose to run through it ($J$, current per unit cross-section). Together they set the drop directly:

$$\Delta V_m = I \cdot R_m = (J \cdot A)(\rho/A) = \rho \cdot J$$

**Resistivity ($\rho$)**: Since circuits are often inside closed or poorly ventilated enclosures, these notes deliberately use the temperature-corrected resistivity of copper at $50^\circ \text{ C}$ rather than the standard $20^\circ \text{ C}$ value. This assumes the worst realistic operating condition (a warm chassis, sustained load), giving the numbers below a built-in safety margin without having to track ambient temperature case by case:

$$\rho_{50} = \rho_{20} \times [1+\alpha(50 - 20)]$$

with: $\rho_{20}=0.0175\Omega\cdot\text{mm}^2/\text{m}, \alpha=0.00393^\circ \text{ C}^{-1}$

$$\rho_{50} \approx 20 \ m\Omega\cdot\text{mm}^2/\text{m}$$

**Current density ($J$)**: unlike $\rho$, which is fixed by the material, $J$ is a design choice. The value adopted here is intentionally conservative, prioritizing low voltage drop, modest self-heating, and robustness when using surplus component leads of uncertain quality:

$$J = 5 \text{ A/mm}^2$$

This value is well below the current densities commonly tolerated by bare copper conductors in free air. Keeping $J$ constant across every gauge provides two practical advantages:

- **Thermal margin**: combined with the $50^\circ \text{ C}$ resistivity value, it provides ample thermal margin for conductors used inside enclosed chassis.

- **Predictable losses**: since $\Delta V_m$ depends only on $J$ and $\rho$ (not on the wire's section), fixing $J$ also fixes the voltage drop to a predictable $\approx 100 \text{ mV}$ per meter across all wire sizes, regardless of which of the two gauges is used for a given trace.


## Reference Tables
Calculated with $J = 5 \text{ A/mm}^2$ and $\rho_{50} = 20 \ m\Omega\cdot\text{mm}^2/\text{m}$. *Geometric profiles and electrical values are rounded for better bench-work readability.*

#### Component Leads (Metric Gauge)
| Diameter ($\varnothing$) | Section ($A$) | Reference Current ($I$) | Resistance per Meter ($R_m$) | Voltage Drop per Meter ($\Delta V_m$) |
| :---: | :---: | :---: | :---: | :---: |
| **$0.5 \text{ mm}$** | $\approx 0.2 \text{ mm}^2$ | 1.0 A | $100 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |
| **$0.8 \text{ mm}$** | $\approx 0.5 \text{ mm}^2$ | 2.5 A | $40 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |

#### Equipment Wires (AWG Gauge)
| AWG | Diameter ($\varnothing$) | Section ($A$) | Reference Current ($I$) | Resistance per Meter ($R_m$) | Voltage Drop per Meter ($\Delta V_m$) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **AWG 14** | $\approx 1.63 \text{ mm}$ | $\approx 2.08 \text{ mm}^2$ | 10 A | $10 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |
| **AWG 16** | $\approx 1.29 \text{ mm}$ | $\approx 1.31 \text{ mm}^2$ | 6.5 A | $15 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |
| **AWG 18** | $\approx 1.02 \text{ mm}$ | $\approx 0.82 \text{ mm}^2$ | 4 A | $25 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |
| **→ AWG 20** | **$\approx 0.81 \text{ mm}$** | **$\approx 0.52 \text{ mm}^2$** | **2.6 A** | **$40 \ m\Omega/\text{m}$** | **$100 \text{ mV/m}$** |
| **AWG 22** | $\approx 0.64 \text{ mm}$ | $\approx 0.32 \text{ mm}^2$ | 1.6 A | $60 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |
| **→ AWG 24** | **$\approx 0.51 \text{ mm}$** | **$\approx 0.20 \text{ mm}^2$** | **1 A** | **$100 \ m\Omega/\text{m}$** | **$100 \text{ mV/m}$** |
| **AWG 26** | $\approx 0.40 \text{ mm}$ | $\approx 0.13 \text{ mm}^2$ | 0.65 A | $150 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |
| **AWG 28** | $\approx 0.32 \text{ mm}$ | $\approx 0.08 \text{ mm}^2$ | 0.40 A | $250 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |
| **AWG 30** | $\approx 0.25 \text{ mm}$ | $\approx 0.05 \text{ mm}^2$ | 0.25 A | $400 \ m\Omega/\text{m}$ | **$100 \text{ mV/m}$** |

#### Bench Interconnections
| Accessory | Section ($A$) | Reference Current ($I$) | Practical Note |
| :--- | :---: | :---: | :--- |
| **Standard Pin Headers** (Rigid 2.54mm) | $\approx 0.41\text{ mm}^2$ | 2.0 A / pin | Parallel multiple pins to reduce contact resistance overhead on power rails |
| **Solid-Core Breadboard Jumpers** (AWG 22) | $\approx 0.32\text{ mm}^2$ | 1.6 A | Inside cheap breadboard, internal clips become the limiting factor above roughly 1 A because of increased contact resistance |
| **Flexible Jumper Wires** (AWG 24 - 26) | $0.13$ - $0.20\text{ mm}^2$ | 0.65 - 1.0 A | Suited to digital logic buses, unsafe for bulk power distribution |
| **Dupont Lab Cables** (AWG 28 - 30, often CCA) | $0.05$ - $0.08\text{ mm}^2$ | 0.25 - 0.40 A | Cheap sets use copper-clad aluminum (CCA), which has a resistivity $1.6\times$ higher than pure copper: expect $\Delta V_m$ above 160 mV/m |
