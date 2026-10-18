# Aluminium-air battery with an agarose-KOH gel electrolyte

Lab project at BITS Pilani: design, fabrication and optimisation of a low-cost
aluminium-air cell that uses a KOH-loaded agarose gel as a leak-free electrolyte.
The cell was developed to power the team's AIChE Chem-E-Car (2025).

The repository holds the fabrication protocol, the design-of-experiments tables,
the measured results for the first optimisation batch, and photos of the cells and the car.

## Cell design

| Part | Material |
|---|---|
| Anode | Aluminium 5000-series sheet |
| Electrolyte | 2.5 % (w/v) agarose gel loaded with 8 M KOH |
| Air cathode | Activated carbon + carbon black + MnO2 catalyst, polymer binder, on a metal mesh current collector |

Overall reaction: 4 Al + 3 O2 + 6 H2O -> 4 Al(OH)3 (with some parasitic H2 evolution at the anode).

Step-by-step preparation is in [`docs/protocols.md`](docs/protocols.md).

## Optimisation method

A Taguchi L9 orthogonal array was used to screen cathode composition with nine trials
instead of 27:

- **Batch 1:** three factors at three levels each, carbon black (8 / 9 / 10 parts),
  activated carbon (1 / 2 / 3) and MnO2 (1 / 2 / 3)
  ([Table 3.1](docs/Table_3.1_Optimization_Parameters.xlsx),
  [3.2](docs/Table_3.2_L9_Orthogonal_Array.xlsx),
  [3.3](docs/Table_3.3_Material_Compositions.xlsx), masses in
  [3.4](docs/Table_3.4_Mass_Batch1.xlsx)).
- **Batch 2:** binder and solvent ratios (PTFE and propanol at three levels each)
  ([Table 3.5](docs/Table_3.5_Mass_Ratio_Levels.xlsx),
  [3.6](docs/Table_3.6_Mass_Batch2.xlsx)). Results for batch 2 are not in this repository.

## Results (batch 1)

From [Table 4.2](docs/Table_4.2_Parameters_Batch1.xlsx), one cell per trial:

| Sample | Plateau voltage (V) | Discharge time (s) | Peak power (W) | Current at shutdown (A) |
|---|---|---|---|---|
| 1 | 0.7 | 8920 | 0.066 | 0.218 |
| 2 | 0.4 | 9997 | 0.053 | 0.183 |
| 3 | 0.8 | 6106 | 0.116 | 0.282 |
| **4** | **1.2** | **8517** | **0.098** | **0.301** |
| 5 | 0.5 | 7574 | 0.043 | 0.133 |
| 6 | 0.7 | 8600 | 0.026 | 0.068 |
| 7 | 0.9 | 8413 | 0.049 | 0.166 |
| 8 | 1.1 | 7823 | 0.070 | 0.261 |
| 9 | 0.6 | 8008 | 0.018 | 0.090 |

Sample 4 (carbon black 9 : activated carbon 1 : MnO2 2) gave the best balance of
voltage, power and run time.

- **Polarisation curve** ([`docs/LSV_graph.png`](docs/LSV_graph.png)):
  about 1.6 V at open circuit, about 0.30 A at short circuit, and peak power of
  about 0.097 W near 0.12 A. This matches sample 4 in Table 4.2.
- **Constant-load discharge** ([`docs/Discharge_graph.png`](docs/Discharge_graph.png)):
  starts near 1.5 V, holds a plateau of about 1.2 V, then about 1.0 V, and cuts off
  after about 8,500 s. That is consistent with sample 4's 8,517 s.
- **Specific capacity** ([Table 4.3](docs/Table_4.3_Specific_Capacity_Batch1.xlsx)):
  2.1 to 3.5 Ah per gram of aluminium consumed, estimated from anode mass loss.

### How to read these numbers

- Every trial is a single cell with no replicates, so there are no error bars and
  small differences between samples are not significant.
- The theoretical capacity of aluminium (Al -> Al3+) is 2.98 Ah/g. Samples 5 (3.51) and
  6 (2.99) are at or above that limit, so the mass-loss method underestimates how much
  aluminium was consumed, probably because corrosion products stay on the anode.
  Treat Table 4.3 as an upper bound, not as coulombic efficiency.
- The photo [`image/Ocv.jpg`](image/Ocv.jpg) shows a cell under test reading 0.987 V on
  the multimeter. It is not the open-circuit value quoted above.

## Chem-E-Car

[`ChemE Car/`](ChemE%20Car/) contains the team's 2025 AIChE Chem-E-Car Engineering
Design Package (EDP) and build photos. The car is propelled by six to seven Al-air
cells in series driving a 3 W motor. It stops by an iodine-clock reaction whose colour
change is detected by a photoresistor read by an Arduino.

## Repository structure

```
docs/
  protocols.md                 fabrication protocol (cathode, gel, assembly, testing)
  Table_3.x_*.xlsx             design-of-experiments levels, L9 array, compositions, masses
  Table_4.x_*.xlsx             batch-1 results (parameters, specific capacity, voltage histogram)
  LSV_graph.png                polarisation (V-I and P-I) curve
  Discharge_graph.png          voltage vs time under load
image/                         cell photos (single cell, 4 in series, gel electrolyte)
ChemE Car/                     competition EDP and car photos
```

## Limitations and next steps

- Batch 2 (binder and solvent) results and a confirmation run of the optimum are not yet recorded here.
- No replicates, no long-term or shelf-life data, and anode self-corrosion (H2 evolution) is not quantified.
- Specific capacity should be measured coulometrically (integrated current) rather than by mass loss.

## Team and licence

Team captain: Aman Arora. Faculty supervisor: Dr. Sarbani Ghosh, BITS Pilani.

Original text, data and figures are released under the MIT licence (see [LICENSE](LICENSE)).
The EDP form layout belongs to AIChE.
