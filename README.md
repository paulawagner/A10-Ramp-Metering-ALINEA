# A10 Ramp Metering Using ALINEA

## Overview

This project investigates whether closed-loop ramp metering can mitigate congestion and the **capacity drop phenomenon** on a highly constrained 12 km section of the Autostrada A10 in Genoa, Italy.

A macroscopic **METANET traffic flow model** was used to simulate peak-hour traffic along the corridor. The model was evaluated under two scenarios:

* **No control:** uncontrolled on-ramp inflows
* **ALINEA control:** closed-loop ramp metering based on measured mainline density

The study focuses on whether local feedback control can improve the utilization of existing highway infrastructure without physical expansion.

## Study Area

The simulated corridor consists of **24 sections**, each 0.5 km long, with four major on-ramps:

| Ramp       | Section |
| ---------- | ------: |
| San Nicola |       2 |
| Pra'       |       5 |
| Pegli      |      14 |
| Aeroporto  |      22 |

The simulation covers a two-hour peak-demand period using a 10-second time step.

## Method

### METANET

METANET was used as the macroscopic traffic-flow model. The model represents traffic through density, velocity and flow variables for each road section.

Key model parameters include:

* Free-flow speed: 130 km/h
* Critical density: 110 veh/km
* Maximum density: 400 veh/km
* Section length: 0.5 km
* Simulation time step: 10 s

### ALINEA

The ramp metering controller uses the ALINEA feedback law:

```text
r(k) = r(k-1) + KR [ρcr - ρ(k)]
```

where the ramp inflow is adjusted according to the difference between the target critical density and the measured mainline density.

The implementation uses a feedback gain of `KR = 0.015`, with ramp-flow limits between 200 and 1800 veh/h.

The controller is implemented directly in the MATLAB simulation loop.

## Results

The controlled and uncontrolled scenarios were evaluated using Total Travel Time, vehicle throughput and average system speed.

| Metric            |    No Control |        ALINEA |   Change |
| ----------------- | ------------: | ------------: | -------: |
| Total Travel Time | 2317.04 veh·h | 1346.11 veh·h |  -41.90% |
| Throughput        |   1468.23 veh |   6038.81 veh | +311.27% |
| Average Speed     |    91.99 km/h |   109.13 km/h |  +18.63% |

ALINEA stabilized the downstream sections and substantially reduced the congestion that developed around the major merge points.

The controller reduced Total Travel Time by **41.9%** while increasing the number of vehicles served by the corridor by approximately **311%**.

## Key Findings

* **Capacity drop mitigation:** ALINEA maintained downstream traffic closer to the critical density and prevented the severe flow collapse observed in the uncontrolled scenario.
* **Higher infrastructure utilization:** The controlled simulation served approximately 6,039 vehicles compared with approximately 1,468 without control.
* **Reduced travel time:** Total Travel Time decreased from 2317.04 to 1346.11 veh·h.
* **Control limitations:** The first section remained a limiting point because the upstream mainline demand was already close to the available capacity. Local ramp metering could therefore not completely eliminate congestion at this bottleneck.

## Technologies

* MATLAB
* METANET
* ALINEA
* Traffic flow modelling
* Feedback control
* Numerical simulation
* Data analysis and visualization

## Repository Contents

```text
src/
└── A10_ALINEA.m

results/
└── Simulation plots
```

## Authors

Marko Stošić
Apostolia M. Sofianopolou
Paula Wagner

Sustainable Systems Engineering — Faculty of Information Technology, Tirana
May 2026
