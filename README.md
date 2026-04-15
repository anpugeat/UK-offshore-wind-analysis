# Coursework Project: UK Offshore Wind Analysis

## Overview

This repository contains coursework completed for a Renewable Energy Systems module. The project analyses historical UK electricity generation (2013–2024), models future energy scenarios through 2050, and presents a conceptual design for an offshore wind farm at Dogger Bank.

The analysis indicates that wind is positioned to become the UK's dominant renewable energy source, capable of meeting projected demand growth from 278 TWh in 2024 to over 560 TWh by 2050. The repository also includes Python tools for power curve modelling, adapted from academic literature, to estimate wind turbine performance across a range of environmental conditions.

---

## Project Files

**`0-UK-offshore-wind-analysis.pdf`**  
Technical report containing:
- Historical electricity generation trends and renewable energy transition analysis
- Future energy demand projections and renewable capacity scenarios
- Detailed offshore wind farm design for Dogger Bank site including turbine selection, energy production calculations, network topology, and economic assessment
- Environmental impact evaluation and climate change considerations

**`1-Power_Curve_Modelling.ipynb`**  
Calculates the raw power output based on rotor area and aerodynamic efficiency (Cp).

**`2-Power_Curve_Sensitivity_Analysis.ipynb`**  
Tests how variables like Air Density or Rotor Diameter impact total power.

**`3-Model_Comparison.ipynb`**  
Validation study comparing the generic power curve model with DTU's PyWake library.

**`4-Monthly_Power_Estimate.ipynb`**  
Converts hourly data into monthly projections using probability distributions.
