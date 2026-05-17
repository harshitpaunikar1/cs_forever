# Analyzing Economic Problems


## Overview

This topic teaches you how to break a business problem into choices, constraints, and outcomes. You learn a few core tools to predict what will happen when something changes.


## Why It Matters

Managers constantly face “if we change X, what happens to Y?” questions. These tools help you make decisions that are logical, measurable, and less guess-based.


## Key Principles

- Think in trade-offs (you can’t maximize everything).
- Use constrained optimization (best choice within limits).
- Use equilibrium analysis (where forces balance).
- Use comparative statics (how results change when inputs change).
- Separate positive (what is) from normative (what should be).


## Key Terms

| Term | Definition |
|------|------------|
| **Constrained Optimization** | Best decision given limits (budget, capacity, time). |
| **Equilibrium** | A stable point where no one wants to change behavior. |
| **Comparative Statics** | Studying how equilibrium changes when conditions shift. |
| **Positive Analysis** | Describes reality (facts/predictions). |
| **Normative Analysis** | Value-based recommendations. |


## Use Case

Choosing the best product mix when you have limited machine hours and limited labor.


## Scenario

> A factory has 1,000 machine-hours and 500 labor-hours. The manager must decide how many units of Product A and B to produce to maximize profit.


## Examples

- Comparative statics: “If wages rise by 10%, what happens to hiring?”
- Positive vs normative: “A tax will raise prices” (positive) vs “The tax is unfair” (normative).

---

## Audited Appendix

# Analyzing Economic Problems
**Course:** Microeconomics for Managers  
**Module:** Content / Analyzing Economic Problems  
**Audited on:** 2026-04-19  
**Audited by:** A5  
**Source files reviewed:** `microeconomics-for-managers/content/01-analyzing-economic-problems.md`

---

## 1. Topic Snapshot
An economic problem is a choice under limits: a manager must pick the best option when resources, demand, or time are constrained.
For IT, AI, Product, and Consulting leaders, this is the decision discipline behind prioritization, pricing, capacity allocation, and trade-off management.
The decision it helps make is which option maximizes value while staying inside the real constraint.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Constrained Optimization | - | Finding the best choice within limits. | It turns a vague problem into a solvable one. | Objective value, constraint slack, binding limits. | Operations, pricing, resource planning. |
| Equilibrium | - | A stable point where no one wants to change behavior. | It explains market or system stability. | Price, quantity, utilization, adoption stability. | Markets, game theory, operations. |
| Comparative Statics | - | Studying how the outcome changes when an input changes. | It helps managers predict direction and magnitude. | Sensitivity, delta in output, scenario results. | Economics, forecasting, policy analysis. |
| Positive Analysis | - | Describing what is happening or what will happen. | It separates facts from opinions. | Observed data, model estimates, forecasts. | Research, dashboards, executive reviews. |
| Normative Analysis | - | Recommending what should happen based on values or goals. | It makes the value judgment explicit. | Target choice, policy preference, trade-off weighting. | Strategy, policy, leadership decisions. |
| Binding constraint [verified from model knowledge, not source] | - | The limit that is actually stopping better performance. | It tells you what to fix first. | Slack = 0, bottleneck utilization, shortage count. | Capacity planning, pricing, project management. |
| Opportunity cost [verified from model knowledge, not source] | - | What you give up when you choose one option over another. | It makes trade-offs visible. | Foregone profit, time, or capacity. | Strategy, product prioritization, finance. |
| Marginal analysis [verified from model knowledge, not source] | - | Comparing the extra benefit to the extra cost of one more unit. | It supports incremental decisions. | Marginal revenue, marginal cost, contribution per unit. | Pricing, production, portfolio decisions. |

## 3. Frameworks & Matrices

### Constraint-Objective Map
**Purpose:** Convert a business problem into one objective and one or more limits.

**Text Diagram:**
```text
objective -> maximize / minimize
constraints -> budget, capacity, time, demand, policy
decision -> choose the best feasible option
```

Axes / Quadrants / Components explained:
Component 1: objective - what the team is trying to maximize or minimize.
Component 2: constraints - the limits that cannot be violated.
Component 3: decision variables - the controllable levers, such as price, headcount, or product mix.
Component 4: feasibility - whether the proposed plan actually fits inside the limits.

IT/AI/Product/Consulting worked example: A product team wants to maximize feature impact but has only two engineers and one quarter to ship. The map forces the team to choose the highest-value scope instead of pretending everything can be delivered [verified from model knowledge, not source]. The decision is to cut low-value work before execution starts.

When to pull this out in a meeting: When everyone wants more than the budget, time, or headcount can support.

### Comparative Statics Response Matrix
**Purpose:** Predict how a decision changes when an input changes.

**Text Diagram:**
```text
input change -> model response -> decision adjustment
```

Axes / Quadrants / Components explained:
Component 1: input change - wages, tax, demand, capacity, or price.
Component 2: response direction - up, down, or no change.
Component 3: response size - small, medium, or large movement.
Component 4: managerial action - adjust price, hiring, production, or policy.

IT/AI/Product/Consulting worked example: A consulting team models what happens if wages rise 10% and sees that hiring softens but automation becomes more attractive. The decision is not to guess but to test the sensitivity of the plan before locking it in [verified from model knowledge, not source].

When to pull this out in a meeting: When a stakeholder asks, "What happens if we change X?"

### Positive vs Normative Filter
**Purpose:** Separate facts from preferences so debate stays clean.

**Text Diagram:**
```text
positive: what is / what happens
normative: what should we do
```

Axes / Quadrants / Components explained:
Component 1: positive claims - testable statements about the world.
Component 2: normative claims - value-based recommendations.
Component 3: evidence - data that supports the positive claim.
Component 4: values - the business or policy preference behind the normative claim.

IT/AI/Product/Consulting worked example: "A tax will raise prices" is positive, while "the tax is unfair" is normative. A product manager uses the same filter when separating conversion data from the decision to raise or lower price [verified from model knowledge, not source]. The decision is to stop arguments from mixing evidence and preference.

When to pull this out in a meeting: When the room is mixing data analysis with ideology or personal preference.

## 4. Formulas

### Formula 1: Profit
Formula: `Profit = Revenue - Cost`
Variables:
Revenue = money earned from sales
Cost = total cost of producing and delivering the output
Why this formula exists: It answers whether the chosen plan creates value or destroys it.
How to interpret the output:
Value < 0 -> loss -> redesign the plan
Value = 0 -> break-even -> improve pricing or cost
Value > 0 -> value created -> scale carefully
Worked example with numbers: If a product line earns 2,000,000 and costs 1,650,000, profit is 350,000. Decision: keep the line only if it also fits strategic and capacity goals.

### Formula 2: Contribution per Constraint Unit [verified from model knowledge, not source]
Formula: `Contribution per Constraint Unit = contribution margin / constrained resource used`
Variables:
contribution margin = revenue minus variable cost
constrained resource used = machine hours, labor hours, or budget consumed
Why this formula exists: It answers which product or project should get the scarce resource first.
How to interpret the output:
Value low -> low priority
Value medium -> possible filler
Value high -> should be allocated first
Worked example with numbers: If Product A contributes 40 per unit and uses 2 machine-hours, its contribution per constraint unit is 20 per hour. If Product B gives 30 per unit and uses 1 hour, it is stronger at 30 per hour. Decision: produce B first if machine time is the bottleneck.

### Formula 3: Comparative Statics Change Ratio [verified from model knowledge, not source]
Formula: `Change Ratio = (new outcome - old outcome) / old outcome`
Variables:
new outcome = result after the input changes
old outcome = result before the input changes
Why this formula exists: It answers how sensitive the system is to a change in a key driver.
How to interpret the output:
Value near 0 -> weak response -> the input is not very influential
Value moderate -> meaningful response -> plan for adjustment
Value large -> strong response -> the input is critical
Worked example with numbers: If forecasted demand rises from 10,000 to 12,000, the change ratio is 20%. Decision: revisit capacity, staffing, and inventory before the change lands.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Try to optimize everything at once. | Pick one objective and the binding constraints first. |
| Make decisions without naming the trade-off. | State the cost, benefit, and opportunity cost clearly. |
| Treat a forecast as a fact. | Use positive analysis for what is likely and normative analysis for what should happen. |
| Allocate scarce resources by politics. | Rank options by marginal value per constraint unit. |
| Change one driver without checking the downstream effect. | Run comparative statics before changing price, capacity, or policy. |

## 6. Real-Life Scenarios (Metric-Driven)
### Scenario 1: Product mix with machine and labor limits
Situation: A factory has 1,000 machine-hours and 500 labor-hours. The product team wants to maximize profit from two products, but one product is machine-heavy and the other is labor-heavy.
Applicable framework/metric: Constraint-Objective Map and Contribution per Constraint Unit.
Analysis: If Product A gives 20 per machine-hour and Product B gives 30 per machine-hour, B should get priority if machine time is the binding limit. The team then checks whether labor becomes the new constraint [verified from model knowledge, not source].
Decision rule: If one resource is binding, rank products by contribution per unit of that resource. If no resource binds, the problem is not yet truly constrained.
Action: Build a simple resource table, rank products by contribution per machine-hour, and reallocate capacity weekly.

### Scenario 2: Wage rise and hiring plan
Situation: A consulting-backed operations team expects wages to rise by 10%. Leadership wants to know whether staffing should be cut, automated, or held steady.
Applicable framework/metric: Comparative Statics Response Matrix.
Analysis: If wages rise 10% and labor-intensive output falls by 6%, the change ratio is -6% for that output measure. That tells the team to test automation or process redesign before the change arrives [verified from model knowledge, not source].
Decision rule: If the response is large, change the plan. If the response is moderate, stage the adjustment. If the response is near zero, keep the current design.
Action: Run a sensitivity table for wages, demand, and automation payback before finalizing the workforce plan.

### Scenario 3: Tax and price debate
Situation: A product leader wants to raise prices after a tax change, while the sales team argues the brand will lose volume. The room is mixing data, policy, and opinion.
Applicable framework/metric: Positive vs Normative Filter and Profit.
Analysis: "Tax will raise prices" is a positive claim and can be tested with the model. "The tax is unfair" is a normative claim and belongs in policy or ethics discussion. If profit rises from 350,000 to 420,000 after the change but churn also rises, the decision must weigh both [verified from model knowledge, not source].
Decision rule: If the data show clear profit improvement and demand remains stable, adjust price. If the change hurts trust or volume beyond the gain, redesign the offer.
Action: Separate the analysis slide from the recommendation slide, then decide with both economics and brand risk visible.

## 7. Implementation Playbook
1. State the objective in one sentence: maximize profit, minimize cost, or improve service within a limit.
2. List the binding constraints and verify which one actually stops better performance.
3. Quantify the trade-off with profit, contribution, or sensitivity analysis.
4. Separate facts from preferences so data review and recommendation do not get mixed.
5. Build a simple scenario table for price, demand, wages, or capacity changes.
6. Rank options by value per scarce resource before asking for more budget or headcount.
7. Review the plan after any major input change and update the constraint picture.

## 8. Content Quality Audit
Covered well: The source correctly gives the basic microeconomic toolkit: constrained optimization, equilibrium, comparative statics, and the positive-versus-normative split.
Underplayed or missing: It does not show how to turn those concepts into a product-mix, pricing, or staffing decision, or how to measure the impact of changing one driver at a time.
Supplement with: Varian, *Intermediate Microeconomics* [verified from model knowledge, not source]; Nicholson & Snyder, *Microeconomic Theory: Basic Principles and Extensions* [verified from model knowledge, not source]; Pindyck & Rubinfeld, *Microeconomics* [verified from model knowledge, not source]; HBR cases on capacity, pricing, and trade-offs [verified from model knowledge, not source]; and standard operations-research treatments of constrained optimization [verified from model knowledge, not source].
Red flags in the source: It is conceptually correct but abstract. Without a resource table, a sensitivity test, and a positive/normative filter, the learner may understand the vocabulary without being able to use it in management decisions.

## 9. Quick-Recall Card
```text
Topic: Analyzing Economic Problems
Core idea: Choose the best option under constraints and separate facts from value judgments.
Key metric/formula: Profit = Revenue - Cost; Contribution per Constraint Unit = contribution margin / constrained resource used; Change Ratio = (new outcome - old outcome) / old outcome.
Framework trigger: Use it when a decision has limits, trade-offs, or sensitivity to one or two key inputs.
Watch out for: Mixing normative opinions with positive analysis.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What is the best feasible choice, and what input change would most alter that choice?
```
<!-- Self-Audit Report Pass 1 scores: [1:5/5, 2:4/5, 3:4/5, 4:4/5, 5:5/5, 6:5/5, 7:5/5, 8:4/5, 9:5/5, 10:5/5] Sections rewritten: [2, 3, 4, 6, 8] Enrichments applied: [source-term glossary; constraint-objective map; comparative statics response matrix; positive-versus-normative filter; profit, contribution-per-constraint-unit, and change-ratio formulas; product-mix, wage, and tax scenarios; economics references; IT/AI/Product/Consulting framing] Final scores: all 5/5 Pass 2 completed: 2026-04-19 11:22 IST Audited by: A5 -->
