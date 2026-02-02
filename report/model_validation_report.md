# Model Validation Report

## Executive Summary
This report independently validates a Monte Carlo 95% Value-at-Risk (VaR) model for a two-asset portfolio. While the model performs adequately under normal market conditions, it exhibits significant weaknesses during crisis periods, including clustered VaR violations and underestimation of tail risk.

## Model Overview
- Risk: market risk
- Risk measure: 1-day 95% VaR
- Methodologies: 
    1. Parametric VaR 
    2. Historical Simulation 
    3. Monte Carlo VaR (also, rolling VaR with 250 day time lag for backtesting)
- Assets: S&P 500 index, EUR/USD exchange rate, and combination at 60% SP500 and 40% EUR/USD
- Output: Daily VaR estimates

## Data Description
- Data source: FRED
- Justification for SP500 and FX: 
    1. Highly liquid 
    2. Commonly used as market proxies
- Time horizon: 2013-01-01 to 2024-12-31
- Frequency: Daily 
- Cleaning steps: 1. Alignment of dates 2. Computation of log returns to ensure stationarity and additivity over time

## Model Results: VaR and Expected Shortdall

### Parametric VaR (95%)
- SP500: -0.0182
- EURUSD at 95%: -0.00758
- Portfolio: -0.0117

### Historical VaR (95%)
- SP500: -0.0171
- EURUSD: -0.00725
- Portfolio: -0.0107

### Monte Carlo VaR and ES (95%)
- SP500 VaR: -0.0182
- SP500 ES: -0.0230
- EURUSD VaR: -0.00762
- EURUSD ES: -0.00950
- Portfolio VaR: -0.0116
- Portfolio ES: -0.0147

## Backtesting
- Kupiec POF test: p-value = 0.0994 > 0.05. Fail to reject H0 and conclude that the model is consistent with the data.
- Christoffersen independence test: p-value = 0.0079 < 0.01. We reject H0 at the 1% level and conclude that violations are not independent and clustering exist.
- Basel traffic-light framework: Red (at 95% level)

## Assumption testing
- Normality test - Jaque-Bera: p-value = 0.00 < 0.05. We reject H0 and conclude that the data is not normal and it is highly possible that the returns are fat-tailed.
- Autocorrelation: From the ACF plot, we conclude that autocorrelation is present.
- Volatility clustering: ARCH test p-value = 0.00 < 0.05. Since the p-value is statistically significant, we reject H0 and conclude that the volatility is time-varying

## Stress-testing
- COVID stress period: realized losses exceeded model's 95% VaR on 12.9% of days. This indicates that the VaR mdoel significantly underestimated tail risks during crisis regimes.
- Hypothetical stresstesting with 2x volatility: VaR increased from -0.0116 to -0.0236. This highlights significant sensitivity to volatility assumptions and model risk under stressed conditions.

## Model Limitations & Model Risk
- From the above, we conclude that the Gaussian assumption ignores fat tails. Hence, VaR does not capture tail severity
- Furthermore, the constant volatility assumption is violated hence the model performs poorly in crisis regimes.

## Recommendations
- Replace Gaussian with Student-t (to simulate fat tails better)
- Introduce GARCH volatility