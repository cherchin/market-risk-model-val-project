# Market Risk VaR Models Validation Project

This repository contains a hands-on implementation of market risk model validation for a two-asset portfolio (S&P 500 and EUR/USD).

## Project Overview
- Objective: Independently validate a Monte Carlo 95% Value-at-Risk (VaR) model.
- Methods:
  1. Parametric VaR
  2. Historical Simulation VaR
  3. Monte Carlo VaR
  4. Expected Shortfall (ES)
- Validation:
  - Backtesting: Kupiec POF, Christoffersen Independence, Basel Traffic-Light
  - Assumption Testing: Normality, Autocorrelation, Volatility Clustering
  - Stress Testing: COVID-19 crisis, hypothetical volatility shocks

## Repository Structure
- `data/`: raw and processed datasets
- `data_processing/`: exploratory and modeling notebooks
- `src/`: modular Python notebooks
- `report/`: final PDF report
