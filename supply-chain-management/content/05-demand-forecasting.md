# Demand Forecasting in Supply Chains

## Overview

Demand forecasting is predicting how much customers will buy so you can plan production, inventory, and deliveries.

---

## Why It Matters

Forecasting helps avoid stockouts (lost sales) and overstock (waste and high storage cost). Better forecasts = smoother operations.


## Key Principles

- Use past sales + current trends
- Forecast more frequently for fast-moving items
- Separate “baseline demand” from “promotion demand”
- Improve forecasts using feedback (learn from errors)


## Key Terms

| Term | Definition |
|------|------------|
| **Forecast** | A demand estimate for the future |
| **Forecast Error** | Difference between forecast and actual demand |
| **Seasonality** | Patterns like weekends/festivals/summers |
| **Moving Average** | Simple method using average of recent periods |


## Use Case

A clothing retailer forecasts winter jacket demand before placing factory orders months in advance.


## Scenario

> A company forecasts low demand for umbrellas. Unexpected early rains hit. Stores run out quickly. If they had included weather patterns, they would have stocked more.


## Examples

- Ice cream sales rise in summer—forecasting increases production in advance.
- Electronics demand spikes during festivals—forecasting prevents last-minute shortages.

---

## Audited Appendix

# Demand Forecasting in Supply Chains
**Course:** Supply Chain Management  
**Module:** Content / Demand Forecasting  
**Audited on:** 2026-04-19  
**Audited by:** A3  
**Source files reviewed:** `supply-chain-management/content/05-demand-forecasting.md`

---

## 1. Topic Snapshot
Demand forecasting is the practice of predicting how much customers will buy so production, inventory, and delivery plans are not built on guesswork.  
It matters because forecast quality directly shapes stockouts, overstock, markdown risk, and service levels in IT/AI/Product/Consulting decisions.  
For a decision-maker, the key question is whether the forecast is separating baseline demand from promotion demand well enough to drive the next planning cycle.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Forecast | - | An estimate of future demand | To plan production and inventory before demand arrives | Forecast units by period | Demand planning, S&OP |
| Forecast Error | - | The difference between forecast and actual demand | To show how far the plan missed reality | Absolute error, percentage error, bias | Forecast reviews, analytics dashboards |
| Seasonality | - | Repeatable demand patterns such as weekends or festivals | To avoid mistaking seasonal spikes for true growth | Seasonal indices, pattern comparison | Retail, CPG, capacity planning |
| Moving Average | - | A simple forecast using the average of recent periods | To smooth noise in stable demand streams | Rolling average over n periods | Planning meetings, ERP rules |
| Baseline Demand | - | Normal demand without special promotions | To isolate the steady-state signal | Historical non-promo demand | Forecasting, replenishment |
| Promotion Demand | - | Extra demand caused by a price promotion or campaign | To keep spikes from contaminating the baseline forecast | Promo lift, incremental units | Marketing, trade planning |
| Weather Pattern | - | Weather-linked demand movement | To improve forecasts for weather-sensitive products | Weather-adjusted forecast error | Retail planning, seasonal goods |
| Stockout | - | Running out of inventory | To show the cost of under-forecasting | Lost sales, stockout days | Store operations, customer service |
| Overstock | - | Holding too much inventory | To show the cost of over-forecasting | Excess units, days of supply, markdowns | Warehousing, finance |
| Feedback | - | Learning from forecast misses and updating the model | To improve the next forecast cycle | Error trend, model revision cadence | Planning, BI, AI ops |

## 3. Frameworks & Matrices

### Demand Decomposition Loop
**Purpose:** Break total demand into baseline, seasonality, promotion, and error so teams do not forecast on a noisy aggregate.

**Text Diagram:**
```text
Actual demand = baseline demand + seasonality + promotion demand + random error
                     |                     |               |
                     v                     v               v
               planning forecast <----- model update <----- forecast error
```

Axes / Quadrants / Components explained:
Component 1: Baseline demand, the non-promo core demand that should drive long-run planning.  
Component 2: Seasonality, the repeatable calendar pattern that should be adjusted for rather than chased.  
Component 3: Promotion demand, the temporary lift that should not become the new normal.  
Component 4: Forecast error, the residual miss that tells you whether the model is improving or drifting.

IT/AI/Product/Consulting worked example: An AI demand model learns from POS history, the product manager marks promo weeks separately, the IT team feeds weather data into the planning pipeline, and the consultant explains why the forecast must be decomposed before inventory is set.  
When to pull this out in a meeting: When the team is arguing whether a sales spike is a trend, a promotion, or just noise.

### Forecast Method Selection Matrix
**Purpose:** Match the forecast method to demand behavior instead of using one method for every SKU.

**Text Diagram:**
```text
                    Demand variability
                Low                         High
Horizon   ------------------------------------------------
Short     | Moving average / simple rules  | Fast updates + judgment
Long      | Trend + seasonality model      | Segmentation + scenarios
```

Axes / Quadrants / Components explained:
Demand variability: how volatile the item is from period to period.  
Planning horizon: how far ahead the decision must be made.  
Low variability, short horizon: a moving average is often enough.  
High variability, short horizon: the team needs faster updates and human review.  
Low variability, long horizon: trend and seasonality models usually work well.  
High variability, long horizon: use segmentation, scenarios, and frequent refreshes.

IT/AI/Product/Consulting worked example: A product analytics team uses a lightweight moving average for stable staples, but a scenario-driven model for festival products. The decision produced is whether to automate the same forecast rule everywhere or segment the portfolio.  
When to pull this out in a meeting: When someone proposes one universal model for every product.

## 4. Formulas

Formula: MAPE = average of absolute percentage errors [verified from model knowledge, not source]  
Variables:  
Actual = real demand observed in the market  
Forecast = predicted demand for the same period  
Absolute percentage error = |Actual - Forecast| / Actual x 100  
Why this formula exists: It answers how large the forecast miss is relative to demand size.  
How to interpret the output:  
Value < 10% -> strong forecast -> keep the model and monitor.  
Value 10%-20% -> acceptable but improvable -> tune features or segmentation.  
Value > 20% -> weak forecast -> change the model or data inputs.  
Worked example with numbers: If actual demand is 1,000 units and forecast is 850 units, the absolute percentage error is 15%. If a forecast has errors of 5%, 12%, and 18% across three periods, the average is 11.7%, which says the model is usable but not yet strong.

Formula: Bias % = average of (Actual - Forecast) / Actual x 100 [verified from model knowledge, not source]  
Variables:  
Actual = real demand observed in the market  
Forecast = predicted demand for the same period  
Bias = direction of the miss, not just its size  
Why this formula exists: It answers whether the team systematically overforecasts or underforecasts.  
How to interpret the output:  
Value < -10% -> systematic overforecasting -> reduce forecast level or adjust safety stock.  
Value -10% to +10% -> roughly balanced -> keep the method and review by segment.  
Value > +10% -> systematic underforecasting -> raise the forecast or improve responsiveness.  
Worked example with numbers: If actual demand is 1,200 and the forecast is 1,000, the bias is +16.7%, which means the plan is consistently too low. The response is to update the baseline forecast and check whether the model is missing weather or seasonality.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Forecast all demand as if it were one pattern | Separate baseline demand from promotion demand |
| Use last month's spike as the new normal | Check seasonality and whether a special event caused the spike |
| Ignore forecast error after the model is published | Review error and bias every cycle |
| Use one method for every SKU | Match the method to volatility and planning horizon |
| Ship inventory plans directly from raw forecast output | Translate forecast into replenishment and capacity decisions |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: Winter jackets with seasonal demand  
Situation: A fashion retailer sees jacket sales jump during an early cold spell. The IT dashboard shows actual demand of 18,000 units versus a forecast of 12,000, and the product team must decide whether the gap is a permanent trend or seasonal noise.  
Applicable framework/metric: MAPE and demand decomposition.  
Analysis: The absolute percentage error is 33.3%. Because weather and seasonality are obvious drivers, the team should not treat the spike as baseline growth.  
Decision rule: If MAPE > 20%, retrain or redesign the forecast. If 10%-20%, improve the model. If < 10%, keep the current approach.  
Action: Add weather inputs, separate seasonal lift from baseline demand, and adjust replenishment for the cold-wave window.

Scenario 2: Umbrella sales after unexpected rain  
Situation: A consumer goods company forecasts 2,000 umbrellas but actual demand reaches 3,000 when early rains arrive. The consulting lead wants to know whether the model simply missed a weather pattern or whether the forecast process itself is broken.  
Applicable framework/metric: Bias %.  
Analysis: Bias is +33.3%, which means the forecast was too low. The issue is not just noise; the model missed a driver that should have been included.  
Decision rule: If bias is below -10%, the model is overforecasting. If between -10% and +10%, keep and monitor. If above +10%, increase forecast sensitivity.  
Action: Add weather data, shorten forecast review cycles, and set emergency replenishment rules for rain-sensitive SKUs.

Scenario 3: Promotion lift on a beverage launch  
Situation: A product manager runs a promotion that lifts orders from a baseline of 5,000 units to 8,500 units for one week. The operations team must decide whether to scale plant output or treat the uplift as promotional demand.  
Applicable framework/metric: Baseline vs promotion demand split.  
Analysis: The promo lift is 3,500 units, or 70% above baseline. That is large enough to distort the forecast if it is not separated.  
Decision rule: If promo lift is material and temporary, keep it out of the baseline. If it persists for multiple periods, investigate whether the baseline has truly shifted.  
Action: Lock the baseline forecast, plan promo inventory separately, and brief supply partners before the next campaign.

## 7. Implementation Playbook
1. Create a demand calendar that tags each period as normal, seasonal, or promotional.  
2. Build a forecast file that separates baseline demand from promotion demand for every major SKU.  
3. Choose a forecast method by demand pattern, not by personal preference.  
4. Track MAPE and bias every cycle and publish the numbers in the planning review.  
5. Add weather, festival, and campaign inputs where demand is clearly event-driven.  
6. Translate forecast output into replenishment, capacity, and labor plans instead of stopping at the number.  
7. Revisit the forecast after each promotion or weather shock so the next cycle learns from the error.  

## 8. Content Quality Audit
Covered well: The source explains the business purpose of forecasting and the main idea that better forecasts reduce stockouts and overstock.  
Underplayed or missing: It does not explain forecast evaluation metrics, model selection, decomposition of demand drivers, or how forecast error feeds inventory and capacity decisions.  
Supplement with: Hyndman and Athanasopoulos, *Forecasting: Principles and Practice* [verified from model knowledge, not source]; Armstrong, *Principles of Forecasting* [verified from model knowledge, not source]; Makridakis et al. (2018), the M4 forecasting competition paper [verified from model knowledge, not source]; a useful case is Zara's fast-fashion demand sensing and responsiveness [verified from model knowledge, not source].  
Red flags in the source: It is intentionally simplified, so a reader could miss the difference between baseline and promotional demand, or assume a moving average is enough for every product.

## 9. Quick-Recall Card
```text
Topic: Demand Forecasting in Supply Chains
Core idea: Forecasts turn messy market signals into inventory, production, and delivery plans.
Key metric/formula: MAPE = average of absolute percentage errors [verified from model knowledge, not source].
Framework trigger: Use it when demand has seasonal or promotional swings and the team needs a planning baseline.
Watch out for: Mixing promo spikes into the baseline forecast.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What is the real baseline demand after removing seasonality and promotions?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [baseline-vs-promotion framing, demand decomposition, MAPE and bias formulas, IT/AI/Product/Consulting examples, forecast governance playbook] Final scores: all 5/5 Pass 2 completed: 2026-04-19 10:40 Audited by: A3 -->
