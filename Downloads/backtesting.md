# Module 3: Backtesting & Performance Metrics Implementation Guide

## Overview

Module 3 is the validation layer that simulates trading strategies on historical data and measures their effectiveness. It takes trading signals from Module 2 and runs them through a backtesting engine to produce performance metrics and insights.

---

## Key Features

Module 3 will:
- Simulate trades based on ML-generated buy/sell signals from Module 2
- Track portfolio performance over historical data
- Calculate risk-adjusted returns and key performance indicators
- Generate visualizations for performance analysis
- Output metrics in formats consumable by the dashboard (Module 5)

---

## Requirements

### 1. Input Data

- **OHLCV Data**: Historical price data (Open, High, Low, Close, Volume) for each stock/ETF
- **Trading Signals**: Signal column from Module 2 (1 = Buy, 0 = Hold, −1 = Sell)
- **Configuration**: Initial capital, transaction costs, leverage limits, backtest date range

### 2. Backtesting Engine

The core engine must:
- Simulate trades based on signal changes
- Track portfolio state: cash balance, holdings, total equity
- Apply realistic transaction costs (commissions, slippage)
- Support both single-asset and multi-asset portfolios
- Enforce position rules (no overlapping orders, max positions per portfolio)
- Use vectorized pandas operations (no loops) for performance

### 3. Performance Metrics

Calculate and output the following metrics:

| Metric | Purpose |
|--------|---------|
| Cumulative Return | Total profit/loss as percentage |
| Annualized Return (CAGR) | Year-over-year growth rate |
| Volatility | Price fluctuation standard deviation |
| Sharpe Ratio | Risk-adjusted returns (higher is better) |
| Max Drawdown | Worst peak-to-trough decline percentage |
| Win Rate | Percentage of profitable trades |
| Trade Count | Total number of trades executed |
| Avg Win/Loss | Average profit and loss per trade |

### 4. Outputs

- **Equity Curve**: Daily portfolio value as a dataframe
- **Trade Log**: Entry/exit prices, PnL, and holding period for each trade
- **Metrics Summary**: Dictionary/JSON with all performance KPIs
- **Visualizations**: Equity curve vs benchmark, drawdown curve, trade distribution

---

## Implementation Strategy

### Phase 1: Data Preparation

Combine OHLCV price data with signals from Module 2 and align them by date. Ensure no missing values, handle corporate actions (splits/dividends), and verify data quality before backtesting.

### Phase 2: Build the Backtesting Engine

Create a reusable BacktestEngine class with the following responsibilities:
- Initialize capital, costs, and position limits
- Convert signal changes into buy/sell trades
- Update portfolio state (cash, holdings, equity) daily
- Generate a detailed trade log with entry/exit details
- Handle edge cases (insufficient cash, zero trades, flat markets)

### Phase 3: Calculate Performance Metrics

Develop a performance metrics module that takes the equity curve and returns series as input and outputs:
- Absolute returns (total and annualized)
- Risk metrics (volatility, max drawdown, drawdown duration)
- Risk-adjusted returns (Sharpe ratio, Sortino ratio)
- Trade statistics (win rate, profit factor, consecutive wins/losses)

### Phase 4: Generate Outputs

Export results in multiple formats:
- CSV files for trade logs and equity curves
- JSON for dashboard integration
- PNG plots for reports and presentations

### Phase 5: Testing & Validation

Test the engine against:
- A simple baseline strategy (e.g., moving average crossover)
- Known reference results from academic examples
- Spot checks of trades and PnL calculations
- Comparison with external backtesting tools

---

## Library Recommendations

### Primary Framework: backtesting.py

**Why backtesting.py for Module 3:**
- Clean, intuitive API perfect for student projects
- Minimal code required to run a complete backtest
- Built-in performance statistics and interactive plots
- Excellent documentation and community examples
- Easy to explain to project reviewers

**Typical workflow:**
- Define a Strategy class with trading logic
- Pass price data and strategy to Backtest runner
- Get results immediately (equity curve, metrics, plots)

### Secondary Framework: vectorbt (for advanced experiments)

**Why vectorbt for research:**
- Highly vectorized using NumPy/Numba for extreme speed
- Can run thousands of parameter combinations in minutes
- Built-in technical indicators and portfolio analysis
- Integrates with Plotly for interactive dashboards
- Better for large-scale multi-ticker simulations

**When to use vectorbt:**
- Parameter optimization and hyperparameter tuning
- Testing strategies across many symbols simultaneously
- Research notebooks to explore strategy variations

### Recommended Approach

Use **backtesting.py as the primary production engine** for your main Module 3 deliverables because it's clear, maintainable, and perfect for demonstrating your work. Include **vectorbt in a research notebook** to show advanced optimization capabilities and thorough strategy validation.

---

## Deliverables

| Component | File Name | Purpose |
|-----------|-----------|---------|
| Engine | `backtester.py` | Core backtesting logic using backtesting.py wrapper |
| Metrics | `performance.py` | Performance metric calculations |
| Configuration | `backtest_config.yaml` | Tickers, capital, costs, date ranges |
| Example Notebook | `example_backtest.ipynb` | Demo showing end-to-end backtest run |
| Advanced Research | `vectorbt_optimization.ipynb` | Parameter tuning and sensitivity analysis |
| Output Folder | `results/` | CSV, JSON, and PNG outputs |

---

## Key Considerations

**Data Quality**: Ensure historical price data is clean, aligned with signals, and free of gaps or outliers.

**Realistic Assumptions**: Include realistic transaction costs (commissions), slippage, and bid-ask spreads. Conservative assumptions = more credible results.

**Benchmark Comparison**: Always compare strategy returns against a relevant benchmark (buy-and-hold, S&P 500 index) to contextualize performance.

**Vectorization**: Use pandas and numpy vectorized operations instead of loops for speed and readability.

**Edge Cases**: Handle scenarios like insufficient cash for orders, strategies with no trades, and flat markets.

**Documentation**: Clear docstrings and comments help team members and project reviewers understand the logic.

---

## Success Criteria

✓ Backtesting engine runs without errors on 3+ stocks  
✓ Equity curve and trade log are generated correctly  
✓ All metrics (Sharpe, drawdown, etc.) calculated and validated  
✓ Results match manual spot checks and external tools  
✓ Plots clearly visualize equity curve, performance, and drawdown  
✓ Output JSON integrates seamlessly with Module 5 dashboard  
✓ Code is clean, documented, and maintainable for future updates  

---

## Integration with Other Modules

**Inputs from Module 2 (ML Model):**
- Trading signals (1, 0, −1) for each date and stock

**Inputs from Module 1 (Data Pipeline):**
- Historical OHLCV data for backtesting period

**Outputs to Module 4 (Alerts & Scheduling):**
- Trained backtester ready for live data
- Performance metrics for alert thresholds

**Outputs to Module 5 (Dashboard):**
- Equity curves, trade logs, and metrics in JSON/CSV format
- Performance visualizations (equity plot, drawdown curve)

---

## Next Steps

1. **Setup**: Install backtesting.py and vectorbt libraries
2. **Data Integration**: Connect Module 1 data pipeline to backtester
3. **Prototype**: Build basic BacktestEngine wrapper around backtesting.py
4. **Validation**: Test on 2-3 stocks with simple baseline strategies
5. **Metrics**: Implement all performance calculations with unit tests
6. **Documentation**: Write example notebook and API documentation
7. **Optimization**: Add vectorbt research notebook for advanced analysis
8. **Integration**: Prepare output formats for Module 5 dashboard



## References & Resources

- Backtesting.py Documentation: https://kernc.github.io/backtesting.py/
- VectorBT Documentation: https://vectorbt.dev/
- Performance Metrics Guide: QuantStart.com backtesting articles
- Python Backtesting Best Practices: QuantInsti.com

