# Statistical Arbitrage Pairs Trading with Cointegration


[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A complete implementation of a pairs trading strategy that identifies cointegrated stock pairs, generates trading signals based on z‑score thresholds, and backtests with transaction costs.

## Table of Contents
- [Overview](#overview)
- [Data Sources](#data-sources)
- [Methodology](#methodology)
- [Results](#results)


## Overview
Pairs trading is a market‑neutral strategy that exploits temporary price divergences between two historically correlated assets. This project:
- Screens for cointegrated pairs using the Engle‑Granger test.
- Estimates the hedge ratio via OLS.
- Computes the spread and its z‑score using a rolling window.
- Generates entry/exit signals (e.g., enter when |z| > 2, exit when |z| < 0).
- Backtests the strategy with realistic transaction costs.
- Outputs performance metrics (Sharpe ratio, max drawdown, total P&L).


## Data Sources
- **Yahoo Finance** (via `yfinance`) – daily adjusted close prices.
- Universe: a selection of US financial stocks (e.g., `['JPM', 'BAC', 'WFC', 'C', 'GS', 'MS', 'USB', 'PNC']`). You can easily change the tickers.

## Methodology
1. **Cointegration test**: Test every possible pair for cointegration (p‑value < 0.05).
2. **Select best pair** (lowest p‑value) for trading.
3. **Estimate static hedge ratio** using OLS on the full sample (or rolling in advanced versions).
4. **Calculate spread** and **z‑score** with a rolling window (60 days by default).
5. **Trading rules**:
   - Enter short spread when z > +2, long spread when z < –2.
   - Exit when z crosses zero.
6. **Backtest**: Daily P&L = position × (return₂ − β × return₁) × notional ($10,000). Transaction costs: $10 per one‑way trade.
7. **Performance metrics**: Total P&L, Sharpe ratio, maximum drawdown, number of trades.


## Results
On the example universe (financial stocks, 2019–2024), the best cointegrated pair (`stock1`–`stock2`) achieved:
- **Total P&L: $39393.65
- **Sharpe Ratio (annualised): 0.56
- **Maximum Drawdown: $-19534.45
- **Number of trades (one-way): 22

<img width="1017" height="541" alt="image" src="https://github.com/user-attachments/assets/f40a277e-731c-4db4-a67b-e2c58c1f8935" />

<img width="1130" height="601" alt="image" src="https://github.com/user-attachments/assets/752837df-2728-41ce-a62e-858010c7d8ce" />



