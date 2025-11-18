## Summary

This research notebook presents an exploration of Hurst exponent estimation methods and their drawbacks through the lense of a quantitative finance practitioner.

![Hurst Estimation](https://github.com/S-D-Willis/hurst-headaches/blob/597f14d80e1766640d6507ee4b93efed1f03c84d/Estimated_Hurst.png)

## Motivation

Market momentum exists despite efficient market hypotheses, but detecting it quickly and reliably remains challenging. While numerous momentum indicators exist, the Hurst exponent offers a mathematically rigorous approach to quantifying autocorrelation persistence - a key signature of trending vs mean-reverting regimes.

However, off-the-shelf implementations often fail catastrophically in real market conditions, as demonstrated in the opening case study where a naive Hurst-informed strategy produces significant losses despite clear trending periods.

## Notebook Contents

### 1. Algorithm Comparison and Analysis
- **Variance of Differences Method**: Implementation and analysis of lag-sensitivity
- **Rescaled Range (R/S) Analysis**: Custom implementation with power-of-2 optimization
- **Detrended Fluctuation Analysis (DFA)**: Integration and testing of the `nolds` implementation

### 2. Robustness Testing Framework
- Validation against fractional Brownian motion (fBM) with known Hurst parameters
- Systematic error analysis across H ∈ [0.05, 0.95]
- Monte Carlo simulations (100 paths) for statistical significance
- Testing on multiple stochastic processes (Brownian motion, GBM, Ornstein-Uhlenbeck)

### 3. Critical Implementation Insights
- Identified optimal lag windows for different market conditions
- Quantified estimation variance as a function of sample size and true H value
- Highlighted regime-specific biases in standard estimators

## Key Findings
1. **Estimation Instability**: Standard DFA implementations can produce 70% swings in estimated H over days, making them unsuitable for production trading

2. **Regime Detection Lag**: All methods exhibit significant lag in detecting regime changes, with delay length contigent upon the number of lags considered

3. **False Signal Problem**: During 2020's trending market, the estimator incorrectly identified breakout periods, leading to missed opportunities


## Requirements

```python
numpy
pandas
matplotlib
statsmodels
yfinance
nolds
stochastic 
```

## References

- Hurst, H.E. (1951). "Long-term storage capacity of reservoirs"
- Peters, E.E. (1994). "Fractal Market Analysis"
- Di Matteo, T. (2007). "Multi-scaling in finance"

---
