# Portfolio Risk Report: VaR, Expected Shortfall and Stress Tests

*A risk analysis of a hypothetical Rs 4.78 lakh portfolio of 8 Indian large caps, using daily data from January 2019 to October 2026. Built with Excel and Power BI.*

![Dashboard](image.png)

## Objective
How much could your portfolio lose in a single day? Which holdings drive the most risk, and how would your investments have survived the biggest market crashes?
This project uses Excel and Power BI to measure portfolio risk, identify the biggest risk contributors, and test how 8 Indian large-cap stocks performed during major market crashes using VaR, Expected Shortfall, and stress testing.

## Key findings
1. **Daily loss limit:** On 95% of days, the portfolio loses less than **1.48%** (about Rs 7,000). On the worst 5% of days the average loss is **2.49%** (about Rs 11,900).
2. **The tail is heavier than VaR shows:** expected shortfall is about 1.7 times VaR, and on 1 day in 100 the loss exceeds **2.91%**.
3. **The model is well calibrated:** the 95% VaR was broken on **5.05%** of days against 5% expected. Caveat: it was tested on the same data it was built from.
4. **Concentration:** Maruti Suzuki and L&T are about **39%** of the portfolio's value but about **48%** of its risk.
5. **Crash behaviour:** The portfolio fell less than the Nifty 50 in all three episodes, by a lot in 2022 (-8.1% vs -17%) and modestly in COVID (-33.9% vs -37%).
6. **Current state:** The drawdown chart ends about 21% below the peak.

## Results

| Measure | Result |
|---|---|
| Annualized volatility | 17.29% |
| 1-day VaR 95% | -1.48% (about Rs 7,058) |
| 1-day VaR 99% | -2.91% (about Rs 13,945) |
| Parametric VaR 95% | -1.74% |
| Expected shortfall (CVaR) 95% | -2.49% (about Rs 11,926) |
| 10-day VaR 95% | about Rs 22,318 |
| Backtest breach rate | 5.05% (expected 5%) |
| Maximum drawdown | -37.84% |

**Stress tests**

| Episode | Portfolio | Nifty 50 |
|---|---|---|
| COVID crash (Feb to Mar 2020) | -33.86% | -37% |
| 2022 rate-hike sell-off | -8.11% | -17% |
| 2024-25 correction | -14.00% | -16% |

**Weight vs share of risk**

| Stock | Weight | Share of risk | Beta |
|---|---|---|---|
| L&T | 20% | 24% | 1.10 |
| Maruti Suzuki | 19% | 24% | 1.01 |
| Reliance | 13% | 14% | 1.09 |
| Sun Pharma | 15% | 12% | 0.61 |
| HDFC Bank | 7% | 7% | 1.08 |
| Infosys | 8% | 7% | 0.85 |
| TCS | 9% | 7% | 0.73 |
| ITC | 8% | 6% | 0.68 |

## Data
- **Source:** Yahoo Finance daily adjusted closing prices (downloaded as a CSV file)
- **Assets:** Reliance, TCS, HDFC Bank, Infosys, ITC, Maruti Suzuki, Sun Pharma, L&T, plus the Nifty 50 as a benchmark.
- **Period:** January 2019 to October 2026.
- **Cleaning:** real date format, sorted, holiday gaps forward-filled, missing data checked before any rows were dropped.
- **Portfolio:** a hypothetical holding of 50 / 20 / 50 / 40 / 150 / 8 / 40 / 25 shares (Reliance, TCS, HDFC Bank, Infosys, ITC, Maruti Suzuki, Sun Pharma, L&T), worth about Rs 4.78 lakh at the last price.

## Method
- **Daily returns** for each stock, then a weighted **portfolio return** (SUMPRODUCT).
- **Portfolio index** (start = 100) and **drawdown** from the running peak.
- **Volatility:** standard deviation of daily returns times the square root of 252.
- **Value at Risk:** historical (5th and 1st percentile) and parametric (normal distribution).
- **Expected shortfall:** average of returns below the 95% VaR.
- **Backtest:** share of days that broke the 95% VaR line.
- **Beta** (slope against Nifty returns) and **risk contribution** (weight x covariance with the portfolio / portfolio variance).
- **Stress tests:** historical crash windows and hypothetical shocks (market -10%, IT -15%, banking -25%).
- **Power BI:** date table, one-to-many relationship, DAX measures for VaR 95, VaR 99, CVaR 95, volatility and maximum drawdown, all validated against the Excel results.

## Assumptions and limitations
- Today's holdings are applied to the whole history ("what if I had held this portfolio throughout?").
- No transaction costs, taxes or rebalancing.
- Prices are adjusted for splits and dividends; 252 trading days per year.
- Crash windows use approximate Nifty peak and trough dates.
- History may not repeat. VaR is a threshold, not a worst case. A normal distribution understates fat tails, and correlations rise in crashes.

## Files
- `Risk_Report.xlsx`: Excel workbook (returns, weights, risk metrics, stress tests)
- `Portfolio_Risk_Dashboard.pbix`: Power BI dashboard (needs Power BI Desktop)
- `prices_2019.csv`: price data
- `download_prices.py`: data download script

*This is an educational project on a hypothetical portfolio, not investment advice.*
