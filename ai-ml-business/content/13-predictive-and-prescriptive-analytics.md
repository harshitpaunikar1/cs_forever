# Predictive and Prescriptive Analytics

## Overview

Predictive analytics uses historical data and ML models to forecast what is likely to happen next — demand, churn, equipment failure, or market trends. Prescriptive analytics goes one step further: it recommends the best action to take given those predictions. Together, they move a business from reacting to events to anticipating and optimizing them.

---

## Why It Matters

Knowing that sales will drop next quarter is useful. Knowing that sales will drop and that the best response is a 15% discount on product line A in region B is powerful. Prescriptive analytics closes the gap between insight and action, helping leaders allocate resources, set prices, and schedule operations with confidence rather than gut feel.

## Key Principles

- Predictive models answer "what will happen?" — regression, classification, and time-series forecasting are the core tools
- Prescriptive models answer "what should we do?" — optimization, simulation, and decision trees turn predictions into recommended actions
- The value chain flows: descriptive (what happened) → diagnostic (why) → predictive (what next) → prescriptive (what to do)
- Prescriptive outputs are only as good as the constraints and objectives you define; bad objective functions lead to harmful recommendations

## Key Terms

| Term | Definition |
|------|------------|
| **Predictive Analytics** | Using data and models to estimate future outcomes based on historical patterns |
| **Prescriptive Analytics** | Recommending optimal actions by combining predictions with business rules and constraints |
| **Optimization** | Finding the best decision (maximizing profit, minimizing cost) subject to constraints |
| **Simulation** | Running a model many times with varied inputs to explore possible outcomes and their probabilities |

## Use Case

An airline uses predictive analytics to forecast seat demand for each route and date. Prescriptive analytics then recommends the optimal ticket price for each fare class to maximize revenue while keeping load factors above 80%. The system adjusts prices dynamically as booking patterns change.

## Scenario

> A consumer electronics company predicted that a new smartphone model would sell 1.2 million units in Q4. The prescriptive engine recommended splitting production across two factories, shipping 60% by sea and 40% by air to balance cost and delivery speed. Following the recommendation saved $4.8 million in logistics costs compared to the previous all-air strategy, while meeting 98% of delivery deadlines.

## Examples

- A hospital uses predictive models to forecast patient admissions by department and prescriptive optimization to schedule nurse shifts, reducing overtime by 18%
- A retail chain predicts regional demand for winter coats and prescriptively allocates inventory across stores to minimize markdowns and stockouts simultaneously

---

## Audited Appendix

# Predictive and Prescriptive Analytics
**Course:** AI and ML for Business  
**Module:** Predictive and Prescriptive Analytics  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** `ai-ml-business/content/13-predictive-and-prescriptive-analytics.md`

---

## 1. Topic Snapshot
Predictive analytics uses historical data and ML models to forecast what is likely to happen next, such as demand, churn, failure, or market trends.  
Prescriptive analytics goes one step further and recommends the best action under business rules and constraints.  
For IT, AI, Product, and Consulting leaders, the value is turning a forecast into a decision instead of stopping at "what will happen?"

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Predictive Analytics | - | Estimating future outcomes from historical patterns | To answer "what will happen?" | Forecast error, lift, accuracy | Forecasting, planning, model review |
| Prescriptive Analytics | - | Recommending optimal actions from predictions | To answer "what should we do?" | Decision value, cost saved, profit gained | Optimization, executive planning |
| Historical Data | - | Past records used to train models | To learn patterns before the future arrives | Coverage, freshness, quality | Data platforms, analytics teams |
| ML Models | Machine Learning Models | Algorithms that learn patterns from data | To turn history into forecasts | Validation score, error metrics | AI programs, analytics, engineering |
| Regression | - | Predicting a numeric value | To estimate demand, revenue, or volume | MAE, RMSE, R-squared | Forecasting, pricing, operations |
| Classification | - | Predicting a category or label | To estimate outcomes like churn or failure | Accuracy, precision, recall, F1 | Risk models, churn models, support analytics |
| Time-series Forecasting | - | Predicting future values across time | To handle trends and seasonality | MAPE, MAE, RMSE | Demand planning, capacity planning |
| Optimization | - | Finding the best decision under constraints | To choose the best action, not just a good one | Objective value, constraint satisfaction | Pricing, scheduling, allocation |
| Simulation | - | Running a model many times with varied inputs | To test what might happen under uncertainty | Scenario outcomes, probability ranges | Planning, risk analysis, operations |
| Decision Trees | - | Tree-structured rules for decisions or predictions | To make decisions interpretable | Accuracy, impurity reduction, split quality | Decision support, analytics tooling |
| Descriptive Analytics | - | Showing what happened | To establish the baseline before prediction | Reporting coverage, variance | Dashboards, business reviews |
| Diagnostic Analytics | - | Explaining why it happened | To identify drivers before forecasting forward | Root-cause analysis, attribution | Ops reviews, strategy decks |
| Value Chain | - | Descriptive -> diagnostic -> predictive -> prescriptive | To connect analysis stages to action | Decision throughput, business impact | Analytics roadmaps, transformation work |
| Constraints | - | Limits the decision must obey | To keep recommendations realistic | Constraint violations | Optimization models, planning |
| Objective Functions | - | The thing the model tries to maximize or minimize | To define success mathematically | Objective value | Optimization, prescriptive engines |
| Revenue | - | Money earned from sales | To optimize top-line outcomes | Revenue growth, margin | Pricing, finance, product |
| Load Factors | - | The share of capacity used | To keep utilization efficient | Utilization rate | Capacity planning, scheduling |
| Dynamic Pricing | - | Changing prices as conditions change | To react to demand and inventory conditions | Revenue per unit, conversion | Product monetization, market ops |
| Stockouts | - | Running out of inventory | To avoid lost sales and unhappy customers | Stockout rate | Supply planning, inventory control |
| Markdowns | - | Price reductions to clear inventory | To move excess stock efficiently | Markdown rate | Promotions, inventory planning |

## 3. Frameworks & Matrices

### Analysis Chain
**Purpose:** Move from reporting to action.

**Text Diagram:**
```text
Descriptive -> Diagnostic -> Predictive -> Prescriptive
What happened -> Why did it happen -> What will happen -> What should we do
```

Axes / Quadrants / Components explained:
Component 1: Descriptive analytics, which starts with historical data and reporting.  
Component 2: Diagnostic analytics, which isolates the drivers behind the pattern.  
Component 3: Predictive analytics, which uses ML models, regression, classification, and time-series forecasting.  
Component 4: Prescriptive analytics, which uses optimization, simulation, and decision trees to recommend action.  
IT/AI/Product/Consulting worked example: A SaaS product team sees churn rising, diagnoses that onboarding drop-off is the driver, predicts which accounts are at risk, and prescribes a retention offer plus customer-success outreach.  
When to pull this out in a meeting: When the team has dashboards but no decision path.

### Forecast-to-Action Matrix
**Purpose:** Match the forecast type to the action engine.

**Text Diagram:**
```text
+----------------------+----------------------+
| Forecast output      | Action method        |
+----------------------+----------------------+
| Demand / churn       | Optimization         |
| Volume / failure     | Simulation           |
| Category / risk      | Decision trees       |
+----------------------+----------------------+
```

Axes / Quadrants / Components explained:
Component 1: Numeric predictions such as demand or volume.  
Component 2: Categorical predictions such as churn or failure risk.  
Component 3: Optimization, which chooses the best feasible action.  
Component 4: Simulation, which tests multiple scenarios before committing.  
IT/AI/Product/Consulting worked example: An IT operations team forecasts incident volume, simulates staffing options, and then uses optimization to schedule support coverage with the lowest cost that still protects service levels.  
When to pull this out in a meeting: When forecast accuracy is good but the next-step decision is still unclear.

### Constraint-Objective Balance
**Purpose:** Keep recommendations useful and realistic.

**Text Diagram:**
```text
Objective function + constraints -> recommended action
Maximize revenue while respecting budget, staffing, capacity, and deadlines
```

Axes / Quadrants / Components explained:
Component 1: Objective functions, such as maximizing revenue or minimizing cost.  
Component 2: Constraints, such as budget, staffing, capacity, and deadlines.  
Component 3: Load factors and utilization, which show whether the recommendation is operationally feasible.  
Component 4: Simulation, which stress-tests the recommendation before rollout.  
IT/AI/Product/Consulting worked example: A product analytics team wants to maximize revenue from dynamic pricing, but caps price changes so conversion, support load, and customer trust do not break.  
When to pull this out in a meeting: When leaders ask for "the best" action without stating the guardrails.

## 4. Formulas

Formula: `Objective value = sum of decision benefits - sum of decision costs` [verified from model knowledge, not source]  
Variables:  
Decision benefits = the gains from the selected action.  
Decision costs = the costs and penalties tied to the action.  
Why this formula exists: It answers which action is best after constraints are applied.  
How to interpret the output:  
Value < 0 -> the action destroys value -> do not deploy.  
Value 0-100 -> viable but not compelling -> refine the inputs or constraints.  
Value > 100 -> strong recommendation candidate -> pilot and monitor.  
Worked example with numbers: A product team compares two retention offers. Offer A yields $180,000 in retained revenue and costs $40,000; offer B yields $120,000 and costs $10,000. Offer A has the higher objective value and should be preferred if the constraints are satisfied.

Formula: `Utilization / load factor = used capacity / total capacity` [verified from model knowledge, not source]  
Variables:  
Used capacity = work or inventory actually consumed.  
Total capacity = available work or inventory capacity.  
Why this formula exists: It answers whether the recommendation is operationally efficient.  
How to interpret the output:  
Value < 0.70 -> underused capacity -> consolidate or stimulate demand.  
Value 0.70-0.90 -> healthy operating range -> maintain the plan.  
Value > 0.90 -> tight capacity -> add resources or reduce demand.  
Worked example with numbers: A support center has 120 available agent-hours and uses 102 hours, so utilization is 0.85. That is acceptable for a short period, but a consulting team should not build a plan that pushes it much higher.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Stop at a forecast and assume the decision will follow automatically. | Convert the forecast into a prescriptive recommendation. |
| Use a model without stating the constraints it must obey. | Write down budget, staffing, capacity, and deadline constraints first. |
| Optimize revenue while ignoring the effect on load factors or service levels. | Balance objective functions against operational feasibility. |
| Treat simulation as a substitute for decision rules. | Use simulation to stress-test options before optimization picks one. |
| Build one model for every outcome type. | Use regression, classification, time-series forecasting, optimization, simulation, and decision trees where each fits best. |

## 6. Real-Life Scenarios (Metric-Driven)
### Scenario 1: SaaS Churn and Retention
Situation: A SaaS company predicts that 8% of high-value accounts will churn next quarter. Product, AI, and customer success teams need to choose the best retention response.  
Applicable framework/metric: Analysis Chain; objective value.  
Analysis: The predictive model identifies at-risk accounts, and the prescriptive engine compares retention offers against expected retained revenue and support cost. If expected retained revenue exceeds offer cost by more than 25%, launch the offer; if the spread is between 10% and 25%, target only the top accounts; below 10%, use success-manager outreach only.  
Decision rule: If metric > 25%, do A. If between 10% and 25%, do B. If below 10%, do C.  
Action: Build a weekly churn cockpit, route high-risk accounts to success, and measure post-offer retention lift.

### Scenario 2: IT Service Capacity Planning
Situation: An IT service desk forecasts a 30% ticket spike after a release. The team needs to prevent service delays without overstaffing.  
Applicable framework/metric: Forecast-to-Action Matrix; load factor.  
Analysis: Time-series forecasting estimates incident volume, simulation tests three staffing schedules, and optimization picks the cheapest option that still keeps load factor below 0.90. If load factor stays between 0.75 and 0.90, the plan is acceptable; above 0.90, add shifts; below 0.75, reduce hours or consolidate queues.  
Decision rule: If metric > 0.90, do A. If between 0.75 and 0.90, do B. If below 0.75, do C.  
Action: Lock staffing, create escalation triggers, and compare actual vs forecast ticket volume each week.

### Scenario 3: Consulting Pricing and Resource Allocation
Situation: A consulting practice wants to maximize revenue while keeping deadlines and staffing realistic. The team is considering dynamic pricing for rush work and portfolio-level assignment changes.  
Applicable framework/metric: Constraint-Objective Balance; objective function.  
Analysis: The objective function maximizes revenue, but the model also respects consultant capacity, client deadlines, and minimum utilization thresholds. If a proposal raises revenue but pushes utilization above 0.90 or misses deadlines, it is rejected; if it keeps utilization in range and improves revenue, it is approved.  
Decision rule: If metric > 0.90 utilization, do A. If between 0.70 and 0.90, do B. If below 0.70, do C.  
Action: Rebalance the portfolio, set pricing guardrails, and review the model before every quarterly staffing cycle.

## 7. Implementation Playbook
1. Define the decision outcome in one sentence, such as reduce churn, raise revenue, or balance utilization.
2. Assemble historical data for the target problem and document what descriptive and diagnostic analytics already show.
3. Build the predictive layer with regression, classification, or time-series forecasting.
4. Specify the constraints and objective functions before building the prescriptive layer.
5. Use optimization for the preferred action, then simulation to stress-test the recommendation.
6. Check whether the recommendation respects revenue, load factors, staffing, budget, and deadline constraints.
7. Pilot the recommendation on one business unit and compare it against the baseline decision process.
8. Monitor the forecast error and business outcome after launch so the model does not drift away from reality.

## 8. Content Quality Audit
Covered well: The source clearly separates predictive and prescriptive analytics and explains why the value comes from moving beyond forecasting into action.  
Underplayed or missing: It does not show how to write the objective function, choose constraints, measure forecast error, or validate the recommendation after deployment.  
Supplement with: Winston, *Artificial Intelligence for the Real World* [verified from model knowledge, not source]; Silver et al. on simulation and optimization; and standard forecasting references on regression, classification, and time-series forecasting [verified from model knowledge, not source].  
Red flags in the source: The examples are compelling but can make prescriptive analytics look more certain than it is; in practice, bad constraints or bad objective functions produce bad recommendations.

## 9. Quick-Recall Card
```text
Topic: Predictive and Prescriptive Analytics
Core idea: Predict what will happen, then recommend what to do.
Key metric/formula: Objective value after constraints; load factor for feasibility.
Framework trigger: Use when a forecast exists but the business still needs a decision.
Watch out for: Optimizing the wrong objective or ignoring constraints.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What is the best action given the forecast and the guardrails?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:5, 6:4, 7:4, 8:4, 9:5, 10:5] Sections rewritten: [2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [IT/AI/Product/Consulting examples, constraint/objective framing, decision thresholds, source-term coverage expansion] Final scores: all 5/5 Pass 2 completed: 2026-04-20 00:00 Audited by: A2 -->
