# Time Series Analysis

## Overview

Time series analysis studies data points collected at regular intervals over time to spot patterns, trends, and cycles. It helps businesses understand how a metric like sales or website traffic behaves historically so they can project it into the future. The core idea is that past behavior contains clues about what comes next.

---

## Why It Matters

Every business decision about inventory, staffing, and budgeting depends on knowing what demand or revenue will look like next month or next quarter. Time series analysis turns raw historical data into actionable forecasts, reducing guesswork and cutting the cost of over- or under-preparation.

## Key Principles

- Collect data at consistent intervals — gaps or irregular spacing distort patterns
- Decompose the series into trend, seasonal, and residual components before forecasting
- Stationarity matters — most models assume the statistical properties of the data do not change over time
- Always validate your model on a holdout period before trusting its predictions

## Key Terms

| Term | Definition |
|------|------------|
| **Time Series** | A sequence of data points recorded at successive, equally spaced time intervals |
| **Stationarity** | A property where the mean, variance, and autocorrelation of the series do not change over time |
| **Autocorrelation** | The correlation of a signal with a delayed copy of itself, revealing repeating patterns |
| **Lag** | The time gap between an observation and a previous observation used for comparison |

## Use Case

A retail chain tracks weekly sales for the past three years and uses time series analysis to forecast demand for the upcoming holiday season, allowing them to order the right amount of stock and schedule enough staff.

## Scenario

> A regional grocery chain noticed that its manual demand estimates were off by 20% each quarter, leading to spoilage on some items and empty shelves on others. After implementing time series analysis on two years of point-of-sale data, the chain reduced forecast error to 7% and cut food waste costs by 30%.

## Examples

- An airline analyzes five years of daily booking data to predict seat demand for each route next summer
- A streaming platform tracks hourly viewer counts to anticipate server load spikes on Friday evenings

---

## Audited Appendix

# Time Series Analysis
**Course:** Business Forecasting  
**Module:** Content  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** `business-forecasting/content/01-time-series-analysis.md`

---

## 1. Topic Snapshot
Time series analysis studies values collected at regular intervals to expose trend, seasonality, and noise.  
For IT, AI, product, or consulting decisions, it helps answer whether demand, traffic, bookings, or usage will rise, fall, or swing predictably.  
Use it to decide inventory, staffing, capacity, budget, and launch timing.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Time Series | N/A | A sequence of observations captured over time at regular intervals | To track how a business metric evolves | Date-stamped values by day, week, month, or hour | Forecasting, analytics, ops reviews |
| Stationarity | N/A | The series does not change its mean, variance, or autocorrelation structure over time | Many models assume stable behavior | Statistical tests, rolling summaries, plots | Model selection, validation discussions |
| Autocorrelation | N/A | Today’s value is related to earlier values | To detect repetition and momentum | Correlation at lagged intervals | Pattern analysis, model diagnostics |
| Lag | N/A | A previous time step used for comparison | To compare current behavior with the past | Lag-1, lag-7, lag-12, etc. | Feature engineering, forecasting |
| Trend | N/A | Long-run upward or downward movement | To separate growth from noise | Slope, moving averages, decomposition | Strategy, planning, forecasting |
| Seasonality | N/A | Repeating pattern tied to a calendar cycle | To capture weekly, monthly, or yearly effects | Seasonal indices, decomposition | Retail, SaaS, staffing, demand planning |
| Residual | N/A | What remains after trend and seasonality are removed | To isolate unexplained variation | Error term from decomposition or model fit | Model diagnostics, forecast review |
| Holdout Period | N/A | A chunk of historical data kept for testing | To check whether the forecast generalizes | Backtest error on unseen dates | Validation, model governance |
| Forecast Error | N/A | Difference between predicted and actual values | To judge forecast quality | MAE, MAPE, RMSE, bias | Planning reviews, S&OP, analytics |

## 3. Frameworks & Matrices

### Time-Series Decomposition
**Purpose:** Split a series into trend, seasonality, and residuals before choosing a forecast method.

**Text Diagram:**
```text
Observed series = Trend + Seasonality + Residual
```

Axes / Quadrants / Components explained:
Component 1: Trend, the long-run direction of the metric.
Component 2: Seasonality, the repeating calendar pattern.
Component 3: Residual, the unexplained noise after removing the first two components.

IT/AI/Product/Consulting worked example: A SaaS product team sees weekly sign-ups rise over 12 months, spike every Monday after weekend campaigns, and bounce around from one promotion to another. Decomposing the series tells the team that the real decision is not "is growth up?" but "how much of next week’s volume is structural versus campaign-driven?"
When to pull this out in a meeting: When a chart looks messy and the team needs to separate growth, cycle, and noise.

### Lag Analysis
**Purpose:** Test whether previous periods explain current demand or usage.

**Text Diagram:**
```text
Current value <- Lag 1 <- Lag 2 <- Lag 3
```

Axes / Quadrants / Components explained:
Component 1: Short lags, which capture immediate carryover.
Component 2: Medium lags, which capture weekly or monthly repetition.
Component 3: Long lags, which show whether older history still matters.

IT/AI/Product/Consulting worked example: A consulting firm's proposal volume this week depends heavily on the last two weeks of pipeline activity. Lag analysis shows that a lag-2 input improves the forecast more than a broad average, so the team keeps the model simple and actionable.
When to pull this out in a meeting: When you need to know how much history to feed into a forecast.

### Holdout Backtest
**Purpose:** Check whether a forecast works on unseen historical periods.

**Text Diagram:**
```text
Train period | Holdout period
-------------|--------------
Fit model    | Test forecast
```

Axes / Quadrants / Components explained:
Component 1: Training window, where the model learns the pattern.
Component 2: Holdout window, where the model is judged.
Component 3: Error comparison, which shows if the forecast is trustworthy.

IT/AI/Product/Consulting worked example: An AI platform forecasts daily API calls using the first 20 months of data and checks the last 4 months as holdout. If the model misses holiday spikes badly, the product team rejects it before planning server capacity.
When to pull this out in a meeting: When someone wants to deploy a forecast without proving it on recent unseen dates.

## 4. Formulas

[verified from model knowledge, not source]

Formula: Simple moving average forecast = (x1 + x2 + ... + xn) / n
Variables:
x = observed values from the last n periods
n = number of periods included in the average
Why this formula exists: It smooths short-term noise so the next planning value is based on recent history.
How to interpret the output:
Value < recent actuals -> demand may be accelerating -> raise inventory or capacity
Value near recent actuals -> stable run rate -> keep current plan
Value > recent actuals -> slowdown possible -> avoid overcommitting
Worked example with numbers: A product team averages the last 4 weekly sign-ups: 120, 140, 130, 150. Forecast = 135. The team uses 135 as next week’s baseline for campaign planning.

Formula: MAPE = (1/n) * Σ(|actual - forecast| / actual) * 100
Variables:
actual = observed value
forecast = predicted value
n = number of forecasted periods
Why this formula exists: It measures average forecast error in percentage terms, which is easy to compare across products or channels.
How to interpret the output:
Value < 5% -> very strong forecast -> automate with light oversight
Value 5%–15% -> usable forecast -> monitor and refresh regularly
Value > 15% -> weak forecast -> revisit features, seasonality, and model choice
Worked example with numbers: If three monthly forecasts miss by 4, 8, and 12 units against actuals of 100, 200, and 300, MAPE = (4/100 + 8/200 + 12/300)/3 * 100 = 4.0%. That is typically good enough for a product or consulting planning deck.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Forecast from a single noisy month | Use multiple periods and smooth short-term noise |
| Trust a model without a holdout test | Backtest on a recent unseen period before decisioning |
| Ignore recurring calendar spikes | Model seasonality explicitly for weekly, monthly, or yearly cycles |
| Treat irregular timestamps as normal data | Clean the timeline so intervals are consistent |
| Read a trend line as a full explanation | Separate trend from seasonality and residuals before acting |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: SaaS usage planning
Situation: A product ops team needs to forecast daily API calls for a new release and avoid overload during launch week. The team has 18 months of usage history and sees repeated Monday spikes plus a slow upward trend.
Applicable framework/metric: Time-series decomposition plus holdout backtest.
Analysis: Trend explains most growth, seasonality explains the Monday spike, and residuals capture launch noise. On the last 30 days of holdout, MAPE is 6.8%, so the forecast is usable for capacity planning.
Decision rule: "If MAPE < 5%, automate the plan. If between 5% and 10%, use it with manual review. If above 10%, redesign the model."
Action: Raise server headroom for Mondays, keep a rollback threshold, and refresh the forecast after every release.

Scenario 2: IT staffing for service desk demand
Situation: A consulting-style internal IT service desk sees ticket volume surge at month-end and during software patch cycles. Leaders want to decide whether to add a contractor or just shift schedules.
Applicable framework/metric: Lag analysis and forecast error.
Analysis: Ticket volume correlates strongly with the prior two weeks of release activity and the current month-end calendar. A lag-based forecast cuts absolute error from 180 tickets to 110 tickets per month.
Decision rule: "If error reduction exceeds 25%, rebaseline staffing. If 10% to 25%, adjust shifts only. If below 10%, keep the current plan."
Action: Move one analyst to late-month coverage and create a patch-calendar tracker for forecasting input.

Scenario 3: Consulting pipeline planning
Situation: A consulting partner needs to estimate next quarter’s proposal volume and delivery load. The pattern is fairly stable, but one major client renewal every quarter creates a visible bump.
Applicable framework/metric: Simple moving average and seasonal adjustment.
Analysis: A 6-period moving average smooths random wins and losses, but a quarterly bump must be added back as a seasonality factor. The adjusted forecast supports headcount planning and partner utilization.
Decision rule: "If seasonal lift is above 10%, build it into the plan. If between 3% and 10%, flag it as a soft adjustment. If below 3%, treat it as noise."
Action: Set utilization targets, pre-book delivery bandwidth, and review the renewal calendar with sales.

## 7. Implementation Playbook
1. Build a dated data table for the metric you care about, with no missing intervals.
2. Plot the series and mark obvious trend, seasonality, and spike periods.
3. Split the history into training and holdout windows.
4. Test a simple baseline forecast before trying a more complex model.
5. Measure forecast error with MAPE or another clear metric.
6. Add lag features only where prior periods actually improve accuracy.
7. Document the business action tied to each forecast band so the number changes a decision, not just a chart.
8. Refresh the model after major process or product changes.

## 8. Content Quality Audit
Covered well: regular-interval data, business value of forecasting, stationarity, autocorrelation, lag, and holdout validation.
Underplayed or missing: explicit forecast formulas, error metrics, and practical backtesting workflow.
Supplement with: Hyndman and Athanasopoulos, *Forecasting: Principles and Practice* (online text, 2018); Hanke and Wichern, *Business Forecasting* (9th ed., 2014); Makridakis, Spiliotis, and Assimakopoulos, forecasting competition papers on model comparison.
Red flags in the source: The source is accurate but very high level, so it can overstate ease of forecasting if teams skip validation, seasonality, or data cleaning.

## 9. Quick-Recall Card
```text
Topic: Time Series Analysis
Core idea: Use historical patterns to forecast what comes next.
Key metric/formula: MAPE = average percentage forecast error.
Framework trigger: Use when a business metric is recorded at regular time intervals.
Watch out for: Treating a noisy series as if it were stable and stationary.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What part of the next period is predictable from past trend, seasonality, and lagged behavior?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [added labeled model-knowledge formulas for moving average and MAPE, added IT/Product/Consulting scenarios, expanded term coverage, tightened decision rules] Final scores: all 5/5 Pass 2 completed: 2026-04-20 11:59 Audited by: A2 -->
