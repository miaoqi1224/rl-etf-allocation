# Risk-Sensitive Reinforcement Learning for Multi-Asset ETF Allocation

Daily dynamic allocation across ETFs using a custom risk-sensitive RL framework — coded from scratch, no black-box RL library.

## Results (out-of-sample)

| Strategy | Total Return | Annualized Return | Sharpe | Max Drawdown |
|---|---|---|---|---|
| **RL (ours)** | **63.3%** | **28.6%** | — | — |
| Inverse-volatility | — | — | **1.51** | — |
| Minimum-variance | — | — | — | **-5.9%** |

The RL allocator achieved the **highest total and annualized returns** on the out-of-sample test set. The honest trade-off, documented in the report: traditional risk-controlled benchmarks (inverse-volatility, minimum-variance) delivered higher Sharpe ratios and smaller drawdowns. RL proved valuable for adaptive timing and allocation — best evaluated alongside classical methods, not as a replacement.

## Approach

- **Universe**: SPY, TQQQ, TLT, GLD — ~10 years of daily adjusted closes (Mar 2016 – Mar 2026)
- **Custom RL, built from first principles**: policy, reward function, and iterative update rule all coded explicitly in R — no off-the-shelf RL package, so every penalty term has transparent economic meaning
- **Risk-sensitive reward**: drawdown penalty (φ), turnover penalty, transaction costs; long-only constraint
- **Features**: rolling returns, volatility, downside risk, drawdown, cross-asset correlations, current drawdown state
- **Validation**: Sharpe − 0.5 × |Max Drawdown| for hyperparameter selection; epoch-wise Sharpe tracking

## Files

- `rl_project_final_report.Rmd` — full analysis source (R Markdown)
- `rl_project_final_report_1.pdf` — rendered report
- `STAT_GR5291_Final_Project.pdf` — course submission version

## Run it

```r
# Requires: quantmod, xts, zoo, quadprog, ggplot2, dplyr, readr, knitr, rmarkdown
rmarkdown::render("rl_project_final_report.Rmd")
```
