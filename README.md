# Coursework Project: UK Offshore Wind Analysis

## Overview

This repository consists of work I completed for a coursework on Renewable Energy Systems. The work examines historical UK electricity generation trends (2013-2024), projects future energy scenarios through 2050, and presents a detailed conceptual design for an offshore wind farm at Dogger Bank in the UK.

This analysis demonstrates that wind power is positioned to become the dominant renewable energy source in the UK, capable of meeting projected electricity demand increases from 278 TWh (2024) to over 560 TWh by 2050. The study includes Python power curve modeling tools adapted from academic literature to estimate wind turbine performance under various environmental conditions.

---

## Project Files

**`0-UK-offshore-wind-analysis.pdf`**  
Technical report containing:
- Historical electricity generation trends and renewable energy transition analysis
- Future energy demand projections and renewable capacity scenarios
- Detailed offshore wind farm design for Dogger Bank site including turbine selection, energy production calculations, network topology, and economic assessment
- Environmental impact evaluation and climate change considerations

**`1-Power_Curve_Modelling.ipynb`**  
Implementation of parametric wind turbine power curve models based on Saint-Drenan et al. (2020):
- Six different power coefficient (Cp) models for turbine aerodynamic performance
- Environmental effects modeling including turbulence intensity, wind shear, and wind veer
- Rotor Equivalent Wind Speed (REWS) calculations for non-uniform wind conditions
- Generic power curve generation from basic turbine specifications (nominal power, rotor diameter)

**`2-Power_Curve_Sensitivity_Analysis.ipynb`**  
Comprehensive sensitivity analysis of power curve parameters:
- Impact assessment of rotor diameter, nominal power, and operational limits
- Environmental factor sensitivity (turbulence intensity, wind shear, wind veer)
- Comparison of different Cp models and their effects on power output
- Air density and conversion efficiency parameter studies

**`3-Model_Comparison.ipynb`**  
Validation study comparing the generic power curve model with DTU's PyWake library:
- Cross-validation of power curve generation methods
- Performance comparison across different turbine configurations
- Turbulence intensity modeling verification
- Model accuracy assessment for various rotor diameters

**`4-Monthly_Power_Estimate.ipynb`**  
Statistical wind analysis and power calculations:
- Weibull and Rayleigh distribution modeling for wind speed variability
- Monthly average power curve generation from hourly wind data
- Comparison of instantaneous vs. time-averaged power calculations
- Wind resource assessment methodologies

