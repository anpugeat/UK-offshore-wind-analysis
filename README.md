# UK Offshore Wind Power Transition Analysis & Conceptual Farm Design

This repository contains two complementary pieces of work:

1. **A feasibility report** — an end-to-end analysis that models historical UK electricity generation (2013–2024), forecasts 2050 Net-Zero demand requirements, and culminates in a conceptual design and 15-year financial lifecycle assessment for a **70 MW commercial offshore wind farm** in the North Sea (Dogger Bank).
2. **An Python modelling framework** — a Python library (`GenericWindTurbinePowerCurve.py`) plus four Jupyter notebooks that generate, analyse, and validate **generic wind turbine power curves**. Because manufacturer power curves are typically proprietary, this framework provides an accessible, parameterised alternative for energy yield assessment. It underpins the energy yield modelling in the report.

The power-curve library is an implementation and extension of the published parametric model of **Saint-Drenan et al. (2020)**, with a constant-*Cp* option and a non-aerodynamic conversion-efficiency factor. 

---

## Key Results


| Metric                                      | Result                                                                       |
| ------------------------------------------- | ---------------------------------------------------------------------------- |
| Levelised Cost of Energy (LCOE)             | **£42.17/MWh** — ~14% below contemporary contracted strike prices            |
| Total project lifecycle cost (15 yr, 70 MW) | £257.91m                                                                     |
| Net lifetime production                     | 6,120.75 GWh                                                                 |
| Annual Energy Production per turbine        | 81.61 GWh/year                                                               |
| True capacity factor                        | 63.4%                                                                        |
| Selected turbine                            | GE Haliade-X 14 MW (150 m hub height)                                        |
| Site                                        | Dogger Bank, Round 4 zone (54.636°, 2.461°), ~20 m depth, 9.91 m/s mean wind |


Historical trend analysis (2013–2024) tracked the UK's coal phase-out (**38.4% → 1%** of the generation mix) against the concurrent scaling of wind (**6.9% → 29.3%**), and modelled a **495.9 TWh/year grid deficit** arising from electrifying 28.2 million gas-heated households.

---

## Repository Structure

```
.
├── README.md
├── requirements.txt
├── report/
│   └── UK_Offshore_Wind_Transition_Analysis.pdf   # Analysis Report
└── notebooks/
    ├── GenericWindTurbinePowerCurve.py            # Power-curve library imported by the notebooks
    ├── 1-Power-Curve-Modelling.ipynb              # Core parametric power-curve model
    ├── 2-Power-Curve-Sensitivity_Analysis.ipynb   # Parameter sweeps & robustness checks
    ├── 3-Model-Comparison.ipynb                   # Validation against DTU PyWake
    └── 4-Monthly-Power-Estimate.ipynb             # Statistical energy-yield forecasting
```

---

## The Feasibility Report

The report (`/report`) is structured in four parts:

**1. Historical Data Analysis & Long-term Forecasting** — Granular analysis of the UK generation mix (2013–2024), modelling of the household electrification deficit, and validation of theoretical 2050 generating capacity (2,895 TWh) against projected demand (>560 TWh) using spatial utility models.

**2. Conceptual Offshore Wind Farm Design** — Site siting and selection from Crown Estate seabed leasing data; turbine evaluation across major commercial offshore platforms (Vestas, Siemens Gamesa, GE) on specific power, swept area, and turbulence limits; energy yield modelling via a Rayleigh wind frequency distribution and the Saint-Drenan parametric power-curve model; and a radial network topology oriented against prevailing southwesterly winds to minimise aerodynamic wake losses.

**3. Grid Intermittency & Environmental Impact Assessment** — Hourly/monthly/annual wind variability indices feeding a proposed hybrid grid (pumped storage + grid-scale battery storage); UKCP18 climate projections applied to future turbine performance; and an Environmental Impact Assessment covering eutrophication, benthic habitat alteration, EMF emissions, and material leaching.

**4. Financial Lifecycle Analysis** — A full 15-year CAPEX/OPEX model aggregating seabed leasing rights, foundations, cabling, offshore substations, and decommissioning, producing the headline LCOE figure.

---

## The Analysis Notebooks

The four notebooks in `/notebooks` form a sequential modelling and analysis pipeline, adapted from **Saint-Drenan et al. (2020)**

### 1. `1-Power-Curve-Modelling.ipynb`

Builds the core mathematical model and the `GenericWindTurbinePowerCurve` library. Constructs a parametric model of the power coefficient *Cp* as a function of tip-speed ratio (λ) and pitch angle (β), selectable across **six published *Cp* formulations** plus a constant-*Cp* option. It then extends the ideal power curve to incorporate real-world effects: turbulence intensity (Gaussian smoothing), air density, wind shear and wind veer via the **Rotor Equivalent Wind Speed** (REWS, per IEC 61400-12-1), non-aerodynamic conversion losses (gear, generator, converter), and cut-in / cut-out wind speeds. A notable feature: a full power curve can be estimated from as little as nominal power and rotor diameter.

### 2. `2-Power-Curve-Sensitivity-Analysis.ipynb`

Evaluates model robustness. Starting from a single reference turbine (a generic 2 MW machine, 80 m rotor, 100 m hub — distinct from the report's 14 MW design), it sweeps **12 model parameters** one at a time, each over a 20-point interval: rotor diameter, nominal power, cut-in / cut-out speeds, minimum / maximum rotor speed, maximum *Cp*, turbulence intensity, wind shear, wind veer, air density, and conversion efficiency — plus the choice of *Cp* model. Each sweep is rendered as a colour-graded family of power curves against the reference, isolating each parameter's effect on output.

### 3. `3-Model-Comparison.ipynb`

Benchmarks and validates the `GenericWindTurbinePowerCurve` (GWTPC) library against the `GenericWindTurbine` class from DTU's `PyWake` library, using a 10 MW reference turbine. GWTPC is first configured to mirror PyWake's assumptions (constant *Cp*, no cut-in, zero turbulence) to establish a like-for-like baseline, then the two models are compared along three axes — choice of *Cp* model (all seven options), rotor diameter, and turbulence intensity — contrasting PyWake's empirical defaults with GWTPC's explicitly parameterised inputs.

### 4. `4-Monthly-Power-Estimate.ipynb`

Applies the power-curve model to practical yield forecasting. Defines the Weibull and Rayleigh distributions analytically — showing Rayleigh as the *k* = 2 special case of Weibull — and compares them across a range of mean wind speeds and Weibull shape parameters. It then computes a monthly power curve as the expected value of the instantaneous (hourly) power curve under a Rayleigh wind-speed distribution, and contrasts the hourly and monthly curves for a 10 MW reference turbine.

---

## Methodology

**Data analysis & forecasting** —  Analysis of a decade of UK generation data, trend decomposition of the generation mix, demand forecasting from electrification scenarios.

**Statistical modelling** — Rayleigh and Weibull probability distributions for wind-speed characterisation, with Gamma-function integration for expected-value calculations across the power curve.

**Parametric aerodynamic modelling** — implementation of the Saint-Drenan et al. (2020) parametric power-curve model: a *Cp*(λ, β) formulation across six published coefficient sets, including here for turbulence intensity, air density, wind shear/veer (Rotor Equivalent Wind Speed, per IEC 61400-12-1), and non-aerodynamic conversion losses.

**Validation & benchmarking** — Direct comparison of the GWTPC implementation against an established open-source reference (`PyWake`).

**Financial modelling** — Bottom-up CAPEX/OPEX aggregation and LCOE calculation over a 15-year asset lifecycle.

---

## Data Sources

67 sources (see report)

---

## References

- Saint-Drenan, YM., Besseau, R., Jansen, M., Staffell, I., Troccoli, A., Dubus, L., Schmidt, J., Gruber, K., Simões, S.G., Heier, S. (2020). *A parametric model for wind turbine power curves incorporating environmental conditions.* Renewable Energy, 157, 754–768. [https://doi.org/10.1016/j.renene.2020.04.123](https://doi.org/10.1016/j.renene.2020.04.123)
- IEC 61400-12-1, Ed. 2 (2015) — Rotor Equivalent Wind Speed methodology for power performance measurements.

