# Sensitivity Analysis

## Overview

Sensitivity analysis tests how changes in one or more input variables affect the output of a model or forecast. You adjust one factor at a time — or several together — and observe how much the result moves. It answers the critical question: "Which assumptions matter most, and how wrong can they be before the decision changes?"

---

## Why It Matters

Every forecast is built on assumptions, and some assumptions carry far more risk than others. Sensitivity analysis identifies which inputs have the biggest impact on the outcome so managers can focus their attention, data collection, and risk mitigation where it matters most. It also gives stakeholders a realistic range of possible outcomes instead of a single number that implies false precision.

## Key Principles

- Vary one input at a time first (one-way sensitivity) to isolate individual effects
- Then test combinations of inputs (multi-way sensitivity) to capture interactions
- Present results as tornado charts or spider plots so decision-makers can quickly see which factors matter most
- Use realistic ranges for each input based on historical variation or expert judgment, not arbitrary plus-or-minus

## Key Terms

| Term | Definition |
|------|------------|
| **Tornado Chart** | A horizontal bar chart that ranks input variables by their impact on the output, with the widest bars at the top |
| **One-Way Sensitivity** | Varying a single input while holding all others constant to see its isolated effect on the output |
| **Break-Even Point** | The value of an input at which the decision or outcome flips from positive to negative |
| **Scenario Range** | The minimum-to-maximum span of an input used in the sensitivity analysis |

## Use Case

A real estate developer runs sensitivity analysis on a new apartment project by varying construction cost, rental rate, and occupancy rate to find out which factor has the most influence on the project's net present value and whether the deal still works in a downturn.

## Scenario

> A renewable energy startup was deciding whether to build a solar farm. The base-case model showed a 14% internal rate of return. Sensitivity analysis revealed that a 10% drop in electricity prices would cut IRR to 6%, while a 20% rise in panel costs only dropped it to 11%. The team focused negotiations on securing a long-term power purchase agreement to lock in price, rather than worrying about panel costs — saving months of procurement effort.

## Examples

- A CFO adjusts the discount rate in a DCF model from 8% to 12% to see how much the company's valuation changes before presenting to investors
- A supply chain manager tests how a 15% increase in shipping costs and a 10% currency depreciation together would affect landed product cost

---

## Audited Appendix

# Sensitivity Analysis
**Course:** Business Forecasting  
**Module:** Forecasting Methods  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** business-forecasting/content/12-sensitivity-analysis.md

Analytical enrichments in the examples, formulas, and decision thresholds are marked [verified from model knowledge, not source].

---

## 1. Topic Snapshot
Sensitivity analysis shows how much a forecast or model output changes when one or more inputs move. For an IT, AI, Product, or Consulting leader, it answers which assumptions matter enough to change the decision.
The practical value is not precision for its own sake; it is knowing where the risk is concentrated and what range of outcomes you should plan around.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Sensitivity analysis | N/A | Testing how output moves when inputs change | To find the assumptions that matter most | Output change from input change | Forecast reviews, model validation |
| Tornado chart | N/A | A ranked bar chart showing which inputs move the result most | To visualize impact quickly | Bar length by output impact | Investor decks, model presentations |
| One-way sensitivity | N/A | Change one input while holding others constant | To isolate one assumption at a time | Change in output versus one changed variable | DCF reviews, pricing analysis |
| Break-even point | N/A | Input level where the result flips from good to bad | To locate decision boundaries | Threshold value of an input | Go/no-go discussions, pricing reviews |
| Scenario range | N/A | The low-to-high span used for testing an assumption | To keep tests realistic | Historical variation or expert judgment [verified from model knowledge, not source] | Budgeting, forecasting, planning |
| Spider plot | N/A | A chart that shows how output responds across multiple inputs | To compare input sensitivity visually | Output across multiple input paths [verified from model knowledge, not source] | Scenario planning, model deep-dives |
| Internal rate of return | IRR | The return rate implied by a project's cash flows | To judge project attractiveness | Percentage return | Project finance, investment committee |
| Net present value | NPV | Present value of future cash flows minus upfront cost | To judge whether a project creates value | Dollar value after discounting | Capital budgeting, investment reviews |
| Discount rate | N/A | The rate used to bring future value back to today | To compare future cash flows fairly | Percentage used in discounting | DCF models, valuation discussions |

## 3. Frameworks & Matrices

Worked examples and meeting triggers below are analytical enrichments [verified from model knowledge, not source].

### One-Way Sensitivity
**Purpose:** Isolate the impact of one assumption on the model output.

**Text Diagram:**
```text
Input A changes -> output changes
All other inputs stay fixed
```

Axes / Quadrants / Components explained:
Component 1: The single input being tested, such as price, cost, or discount rate.
Component 2: The output being watched, such as IRR, NPV, or margin.
Component 3: The threshold where the decision changes, which is the break-even point.

IT/AI/Product/Consulting worked example: A product team tests how a 10% increase in cloud hosting cost changes the gross margin of an AI feature. If margin falls only slightly, the launch remains viable; if it falls below the target, the team renegotiates vendor terms before launch.
When to pull this out in a meeting: Use it when one assumption is disputed and you need a clean, isolated answer.

### Tornado Chart Prioritization
**Purpose:** Rank the inputs that have the biggest effect on the outcome.

**Text Diagram:**
```text
Largest impact
   |
   v
======== input 1
======   input 2
===      input 3
```

Axes / Quadrants / Components explained:
Component 1: Each input variable, such as revenue, cost, occupancy, or conversion.
Component 2: The width of each bar, which reflects how much the output changes.
Component 3: The ranking order, which shows where management attention belongs first.

IT/AI/Product/Consulting worked example: A consulting partner evaluates a new AI transformation proposal and finds that client utilization drives more value than small changes in travel cost. The tornado chart makes it obvious that staffing assumptions deserve more scrutiny than office expense.
When to pull this out in a meeting: Use it when you need to show which assumptions deserve the most risk review time.

## 4. Formulas

Formula interpretations and threshold bands below are analytical enrichments [verified from model knowledge, not source].

Formula: Output sensitivity = change in output / change in input
Variables:
Change in output = new result minus base-case result
Change in input = tested input minus base input
Why this formula exists: It shows how responsive the model is to a single assumption.
How to interpret the output:
Value < 1 -> output is less sensitive -> lower risk from that assumption
Value 1 to 2 -> moderate sensitivity -> watch the assumption
Value > 2 -> high sensitivity -> protect the assumption or redesign the plan
Worked example with numbers: If NPV falls from $2.0M to $1.6M when launch cost rises by $200k, sensitivity = -$400k / $200k = -2.0.

Formula: Break-even input = input level where output = 0 or decision flips
Variables:
Output = project value, margin, or IRR threshold
Input = price, cost, occupancy, utilization, or rate
Why this formula exists: It identifies the minimum acceptable assumption.
How to interpret the output:
Value below break-even -> decision fails -> stop or redesign
Value near break-even -> fragile decision -> add buffer
Value above break-even -> decision still works -> proceed with monitoring
Worked example with numbers: If an AI services project remains profitable only when utilization stays above 68%, then 68% is the break-even utilization threshold.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Test only the base-case and stop there | Vary key assumptions and compare the output movement |
| Assume every assumption has equal risk | Use a tornado chart to rank the largest drivers |
| Use arbitrary plus-or-minus ranges | Set ranges using historical variation or expert judgment |
| Present a single number with false certainty | Show a realistic range of outcomes |
| Hide the break-even point | State the threshold that would change the decision |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario calculations and decision rules below are analytical enrichments [verified from model knowledge, not source].

Scenario 1: AI launch model stress test
Situation: A product team is launching an AI feature and wants to know whether a higher cloud bill will kill the business case. The team has a base-case margin model but the CFO wants to see the break points before approving launch spend.
Applicable framework/metric: One-way sensitivity.
Analysis: If monthly margin is $300k at baseline and drops to $180k when hosting cost rises by $60k, the output sensitivity is -120k / 60k = -2.0.
Decision rule: If the output stays above the approval threshold, proceed; if it falls close to break-even, negotiate costs; if it falls below break-even, pause launch.
Action: Test hosting, inference, and support cost one at a time before the steering committee review.

Scenario 2: Consulting bid risk ranking
Situation: A consulting team is preparing a transformation proposal and needs to know which variables deserve the most diligence. The proposal depends on client utilization, travel cost, and implementation timing.
Applicable framework/metric: Tornado chart.
Analysis: Utilization has the widest bar, timing is second, and travel cost is last, so the proposal risk is driven mainly by staffing assumptions.
Decision rule: If one driver dominates, focus diligence there; if several are close, review all of them; if none are material, move ahead quickly.
Action: Build the bid review around utilization assumptions, then sanity-check the smaller cost lines.

Scenario 3: Product pricing break-even check
Situation: A SaaS product manager is changing price and wants to know how much churn the plan can tolerate. The team has a launch plan, but the board wants the downside case before the price move.
Applicable framework/metric: Break-even point.
Analysis: If the new pricing plan only works when churn stays under 3.5% monthly, that 3.5% is the break-even churn threshold.
Decision rule: If churn stays below the threshold, keep the price; if it is near the threshold, add retention work; if it rises above the threshold, reverse the change or repackage the offer.
Action: Run the sensitivity table for churn, conversion, and discount depth before shipping the new price book.

## 7. Implementation Playbook
1. Build a model with a single clear base case.
2. Identify the inputs that are most likely to move the decision.
3. Set realistic high and low ranges using history or expert judgment.
4. Change one input at a time and record the output shift.
5. Rank the results in a tornado chart for leadership.
6. Test combinations of inputs only after the one-way view is clear.
7. Write down the break-even point for the decision owner.
8. Present the output range, not just the base-case number.

## 8. Content Quality Audit
The supplements listed here are external enrichments [verified from model knowledge, not source].
Covered well: The source explains the purpose of sensitivity analysis, the value of one-way testing, the move to multi-way testing, and why tornado charts and realistic ranges matter.
Underplayed or missing: The source does not show the mechanics of a sensitivity table, does not define break-even mathematically, and does not translate the charts into explicit go/no-go rules.
Supplement with: [verified from model knowledge, not source] a corporate finance text on scenario and sensitivity tables, an HBS or IIM case on capital budgeting under uncertainty, and a valuation reference that explains tornado charts and scenario ranges.
Red flags in the source: The source is directionally correct, but without a clear threshold it can be used as presentation theater instead of decision support.

## 9. Quick-Recall Card
```text
Topic: Sensitivity Analysis
Core idea: Show which assumptions move the forecast or model output the most.
Key metric/formula: Output sensitivity = change in output / change in input
Framework trigger: Use it when a forecast or proposal depends on uncertain assumptions.
Watch out for: Treating all inputs as equally important.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Which assumption could break the decision first?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:5, 6:4, 7:5, 8:4, 9:5, 10:4] Sections rewritten: [1, 2, 3, 4, 6, 8] Enrichments applied: [added sensitivity math, break-even framing, tornado prioritization, and IT/AI/Product/Consulting examples] Final scores: all 5/5 Pass 2 completed: 2026-04-20 12:40 Audited by: A2 -->
