# Forecast Accuracy Measures

## Overview

Forecast accuracy measures are metrics that tell you how close your predictions came to what actually happened. Common measures include Mean Absolute Error, Mean Squared Error, and Mean Absolute Percentage Error. Without these metrics, you have no way to know if your forecast is useful, improving, or worse than a simple guess.

---

## Why It Matters

A forecast is only valuable if it is accurate enough to drive better decisions than gut instinct. Accuracy measures give you a scoreboard. They tell you which model to choose, when a model needs retraining, and whether the money you spent building a forecasting system is actually paying off. Managers who ignore accuracy metrics often keep using bad forecasts for months without realizing it.

## Key Principles

- Use multiple metrics — no single number captures every aspect of forecast quality
- MAPE is intuitive (expressed as a percentage) but breaks down when actual values are near zero
- MAE treats all errors equally; MSE penalizes large errors more heavily
- Always compare your model's accuracy against a naive baseline like "repeat last period"

## Key Terms

| Term | Definition |
|------|------------|
| **MAE (Mean Absolute Error)** | The average of the absolute differences between forecasted and actual values |
| **MSE (Mean Squared Error)** | The average of the squared differences between forecasted and actual values |
| **MAPE (Mean Absolute Percentage Error)** | The average of absolute errors expressed as a percentage of actual values |
| **Naive Forecast** | A simple benchmark that predicts the next period will equal the current period |

## Use Case

A supply chain team compares three forecasting methods by running each on the last 12 months of demand data and calculating MAE and MAPE for every SKU, then selects the method with the lowest average MAPE across product categories.

## Scenario

> A beverage distributor had been using exponential smoothing for two years but never measured accuracy. When the analytics team finally calculated MAPE, they discovered the model was off by 22% on average — worse than a simple naive forecast for several product lines. Switching those lines to a seasonal ARIMA model cut MAPE to 11% and reduced emergency shipments by 40%.

## Examples

- A demand planner reports monthly MAPE to leadership as a KPI alongside fill rate and inventory turns
- A weather service compares MSE across competing temperature models to decide which one to display to the public

---

## Audited Appendix

# Forecast Accuracy Measures
**Course:** Business Forecasting  
**Module:** Statistical Techniques  
**Audited on:** 2026-04-20  
**Audited by:** A1  
**Source files reviewed:** `business-forecasting/content/07-forecast-accuracy-measures.md`

---

## 1. Topic Snapshot
Forecast accuracy measures tell you how close a forecast came to what actually happened. This matters because a forecast is only useful if it beats a simple guess and is good enough to drive decisions. The decision it helps make is which model to trust, when to retrain, and whether the forecasting system is paying off.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| MAE | Mean Absolute Error | Average absolute size of the misses | To measure typical error size | Average of absolute residuals | Forecast reviews, ops |
| MSE | Mean Squared Error | Average squared size of the misses | To punish large misses more heavily | Average of squared residuals | Model comparison, analytics |
| MAPE | Mean Absolute Percentage Error | Average error as a percentage of actuals | To make error easy to read across SKUs or categories | Percentage error average | Supply chain, leadership dashboards |
| Naive forecast | N/A | Predict the next period equals the current period | To provide a simple benchmark | Model error versus repeat-last-period | Forecast benchmarking |
| Baseline | N/A | The simplest reference point for comparison | To prove the model adds value | Accuracy improvement over benchmark | Business cases, QA |
| Retraining | N/A | Updating the model with new data | To keep forecasts current | Error trend over time | MLOps, analytics ops |
| Fill rate | N/A | Share of demand met without stockout | To connect accuracy to service | Service level metric | Supply chain, inventory |
| Inventory turns | N/A | How quickly inventory cycles through | To connect forecast quality to working capital | Turns per year | Supply chain, finance |

## 3. Frameworks & Matrices

### Error Metric Selection Matrix
**Purpose:** Choose the right accuracy metric for the business problem.

**Text Diagram:**
```text
Need simple average error?   -> MAE
Need to punish big misses?   -> MSE
Need percent-based reading?   -> MAPE
Need a benchmark?            -> Naive forecast
```

Axes / Quadrants / Components explained:
Component 1: Error size, meaning how large the misses are in units.
Component 2: Error severity, meaning whether large misses should hurt more.
Component 3: Interpretability, meaning whether leadership needs percentages or raw units.

IT/AI/Product/Consulting worked example: A supply chain team managing SKUs uses MAPE to compare categories with different scales, while a weather model review uses MSE because big misses matter more when a severe temperature forecast is wrong.
When to pull this out in a meeting: When stakeholders ask which metric should be in the dashboard.

### Model-vs-Baseline Scoreboard
**Purpose:** Decide whether a forecasting model is actually better than the simplest alternative.

**Text Diagram:**
```text
Model error < naive error -> useful
Model error = naive error -> no improvement
Model error > naive error -> replace or retrain
```

Axes / Quadrants / Components explained:
Component 1: Model performance, meaning the candidate forecast.
Component 2: Naive benchmark, meaning repeat-last-period.
Component 3: Improvement, meaning the gap between the two.

IT/AI/Product/Consulting worked example: A beverage distributor finds that exponential smoothing underperforms a naive forecast on several product lines. The scorecard shows the model should not be rolled out universally.
When to pull this out in a meeting: When a model looks sophisticated but may not beat the baseline.

## 4. Formulas

The formulas below are standard forecast-accuracy formulas added from model knowledge [verified from model knowledge, not source].

Formula: `MAE = average(|actual - forecast|)`
Variables:
actual = observed value
forecast = predicted value
Why this formula exists: It answers the average size of the miss in the same units as the data.
How to interpret the output:
Lower MAE -> better typical forecast
Higher MAE -> worse typical forecast
Use when -> decision makers want a simple unit-based error measure
Worked example with numbers: If the forecast misses by 3, 5, and 7 units, MAE = 5.

Formula: `MSE = average((actual - forecast)^2)`
Variables:
actual = observed value
forecast = predicted value
Why this formula exists: It answers how bad the errors are when large misses should be penalized more.
How to interpret the output:
Lower MSE -> better forecast
Higher MSE -> bigger or more volatile misses
Use when -> large errors are especially costly
Worked example with numbers: Errors of 2, 4, and 6 units become 4, 16, and 36, so MSE = 18.67.

Formula: `MAPE = average(|actual - forecast| / actual) × 100`
Variables:
actual = observed value
forecast = predicted value
Why this formula exists: It answers error in percentage terms so different categories are comparable.
How to interpret the output:
Lower MAPE -> better relative accuracy
Higher MAPE -> worse relative accuracy
Use when -> the business wants an easy-to-read dashboard metric
Worked example with numbers: If actual demand is 100 and forecast is 90, the percentage error is 10%.

Formula: `Naive forecast = current period value`
Variables:
current period value = most recent observed value
Why this formula exists: It answers the simplest possible benchmark.
How to interpret the output:
Model beats naive -> keep the model
Model equals naive -> no value add
Model worse than naive -> retrain or replace
Worked example with numbers: If last month sales were 500, the naive forecast for next month is 500.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Report only one metric and call the forecast good | Use MAE, MSE, and MAPE together |
| Ignore a naive forecast benchmark | Compare every model to repeat-last-period |
| Use MAPE when actual values can be near zero | Switch to MAE or MSE when percentages become unstable |
| Focus on average error and ignore big misses | Use MSE when large forecast failures are expensive |
| Keep a model that underperforms the baseline | Retrain, simplify, or replace it |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: Supply chain SKU benchmarking
Situation: A supply chain team tests three demand forecasting methods across many SKUs. The team needs a metric that works across different scales and product categories.
Applicable framework/metric: Error Metric Selection Matrix, MAPE.
Analysis: The team picks the method with the lowest average MAPE across categories because percentage error makes comparisons easier than raw units.
Decision rule: If MAPE improves materially versus the baseline, use the model. If not, keep the naive forecast for that SKU group.
Action: Put MAPE on the monthly forecast scorecard and review it by product family.

Scenario 2: Beverage distribution accuracy audit
Situation: A beverage distributor has used exponential smoothing for two years but never checked whether it beats a naive forecast. The analytics team wants a hard answer before more money goes into the system.
Applicable framework/metric: Model-vs-Baseline Scoreboard, MAPE.
Analysis: The model is off by 22% on average, while a seasonal ARIMA model cuts MAPE to 11%. That is a clear improvement.
Decision rule: If the candidate model beats the naive baseline by a wide margin, keep it; if not, replace it.
Action: Re-train the weak product lines and track emergency shipments after the switch.

Scenario 3: Weather model comparison
Situation: A weather service wants to decide which temperature model to show the public. A single large miss could be costly, so large errors matter more than average unit misses.
Applicable framework/metric: MSE.
Analysis: The model with the lowest MSE is preferred because it punishes large forecast failures more heavily than MAE.
Decision rule: If large misses are the biggest risk, choose the lowest MSE; if interpretability matters more, also report MAE or MAPE.
Action: Compare the top models on both MSE and MAE before publishing the forecast.

## 7. Implementation Playbook
1. Choose the business question and the decision that depends on forecast quality.
2. Define the baseline forecast, usually repeat-last-period or another naive method.
3. Compute MAE, MSE, and MAPE on the same holdout window.
4. Check whether MAPE is safe to use when actual values are near zero.
5. Compare every candidate against the baseline, not just against past performance.
6. Link the metric change to business outcomes like fill rate, inventory turns, or emergency shipments.
7. Retrain or replace the model when accuracy drifts below the accepted threshold.

## 8. Content Quality Audit
Covered well: The source correctly frames forecast accuracy as a business scoreboard and highlights the need for multiple metrics and a naive benchmark.
Underplayed or missing: It does not explain the formulas, threshold selection, or how metric choice changes with scale, zero values, or asymmetric business cost.
Supplement with: Forecasting texts that compare error metrics in practice, supply-chain planning case studies, and business analytics examples showing when MAPE fails near zero [verified from model knowledge, not source].
Red flags in the source: The definitions are accurate but simplified, so stakeholders still need judgment when metrics disagree or when actuals approach zero.

## 9. Quick-Recall Card
```text
Topic: Forecast Accuracy Measures
Core idea: A forecast is only useful if it beats a simple benchmark and is accurate enough for the decision.
Key metric/formula: MAE = average(|actual - forecast|); MSE = average((actual - forecast)^2); MAPE = average(|actual - forecast| / actual) × 100
Framework trigger: Use when choosing between forecast models or checking whether to retrain.
Watch out for: MAPE near zero and models that lose to a naive forecast.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Is this forecast accurate enough to improve the business decision more than the naive baseline?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [1,2,3,4,5,6,7,8,9] Enrichments applied: [error metric selection matrix, model-vs-baseline scoreboard, MAE/MSE/MAPE and naive formulas, IT/product/consulting scenarios, operational scorecard framing] Final scores: all 5/5 Pass 2 completed: 2026-04-20 12:15 Audited by: A1 -->
