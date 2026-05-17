# Prescriptive Analytics

## Overview
Prescriptive analytics recommends specific actions by combining predictive models with optimization and simulation techniques. It answers the question "what should we do?" rather than just "what will happen?" This makes it the most actionable tier of analytics, directly linking data insights to decision-making.

---

## Why It Matters
Knowing what is likely to happen is valuable, but knowing the best course of action is even more powerful. Prescriptive analytics closes the gap between insight and execution by providing concrete, data-backed recommendations that account for constraints, trade-offs, and business objectives.

## Key Principles
- Define clear objective functions that reflect what the business is trying to maximize or minimize
- Incorporate real-world constraints such as budgets, capacity limits, and regulatory requirements into the model
- Use scenario analysis and simulation to evaluate the impact of different decisions before committing resources
- Automate routine decisions where the prescriptive model has demonstrated consistent accuracy

## Key Terms
| Term | Definition |
|------|------------|
| **Optimization** | The mathematical process of finding the best solution from a set of feasible alternatives given defined objectives and constraints |
| **Simulation** | A technique that models the behavior of a system under various conditions to estimate probable outcomes |
| **Decision Variable** | A controllable factor in an optimization model that the decision-maker can adjust, such as price or staffing level |
| **Constraint** | A limitation or requirement that must be satisfied within an optimization model, such as budget caps or delivery deadlines |

## Use Case
A logistics company uses prescriptive analytics to determine the optimal delivery routes each morning, minimizing fuel costs while meeting all customer time windows.

## Scenario
> A hospital network needs to allocate nursing staff across 12 units for the upcoming quarter. A prescriptive model considers patient volume forecasts, nurse skill levels, labor regulations, and overtime costs to generate a staffing schedule that reduces overtime spending by 18 percent while maintaining care quality standards.

## Examples
- Recommending the optimal marketing budget allocation across channels to maximize return on ad spend within a fixed budget
- Determining the best product mix for a factory to produce each week based on demand forecasts, raw material availability, and machine capacity

---

## Audited Appendix

# Prescriptive Analytics
**Course:** Business Analytics
**Module:** Content / Prescriptive Analytics
**Audited on:** 2026-04-18
**Source files reviewed:** `business-analytics/content/05-prescriptive-analytics.md`

---

## 1. Topic Snapshot
Prescriptive analytics = "what should we do?" via optimisation, simulation, recommendation, and RL. Top rung of the ladder — the point where analytics becomes an automated decision asset. For an IT/AI/Product/Consulting leader this is where you decide to let a model run the budget allocation, pricing, routing, or staffing. Decision it helps make: *"Within our constraints, which action maximises the objective we've chosen — and is the recommendation trustworthy enough to automate?"*

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Optimisation | — | Finding best action within constraints | Converts objectives to decisions | Optimal value of objective | OR, pricing, routing |
| Objective Function | — | What we're maximising/minimising | Must be a single scalar | $ revenue, $ cost, $ profit, time | OR problems |
| Decision Variable | — | Variable we control | Defines action space | Continuous / integer / binary | OR formulation |
| Constraint | — | Rule the solution must satisfy | Reflects reality (budget, capacity, regulation) | Equality / inequality | OR formulation |
| Feasible Region | — | Set of solutions satisfying all constraints | Where we're allowed to operate | Region geometry | OR theory |
| Linear Programming | LP | Linear objective + linear constraints | Most tractable optimisation class | Solve time; optimality gap | OR, pricing, blending |
| Integer Programming | IP | Variables must be integer | For count-based decisions (open/close stores) | Same; harder to solve | Network design |
| Mixed Integer LP | MILP | Combination of LP + IP | Common real-world form | Gurobi / CPLEX solver output | Ops research |
| Nonlinear Programming | NLP | Nonlinear objective or constraints | Required for real-world pricing, demand | Convergence, local vs global optimum | Advanced OR |
| Stochastic Optimisation | — | Variables are random — optimise over distributions | Handles uncertainty | Expected objective; VaR | Finance, supply chain |
| Simulation | — | Run a model of the system under many scenarios | Estimates distributions when analytic solutions fail | Mean + SD of outcomes | Risk, ops |
| Monte Carlo | — | Simulation via random sampling | Converges to true distribution with enough runs | # simulations; CI width | Risk, finance |
| Discrete-Event Simulation | DES | Simulates systems that change at events | Queueing, manufacturing | Throughput, wait time | Ops research |
| Scenario Analysis | — | Evaluate pre-defined scenarios | Qualitative framing | Scenario count | Strategy |
| Sensitivity Analysis | — | How output changes as input varies | Diagnoses robust vs fragile recs | Partial derivatives / one-at-a-time | OR, finance |
| Heuristic | — | Rule of thumb giving good-enough answer | When optimal is infeasible to compute | Quality vs optimal | Routing, scheduling |
| Metaheuristic | — | Higher-level heuristic framework (GA, simulated annealing) | Escapes local optima in hard problems | Solution quality | Advanced OR |
| Greedy Algorithm | — | Locally optimal choice each step | Simple, fast, sometimes optimal | Performance vs benchmark | Scheduling |
| Recommendation System | — | Ranks items for a user | Core ML application of prescription | Uplift@K, CTR, revenue/session | E-commerce, media |
| Collaborative Filtering | — | Recommends via user-item similarity | "People like you liked X" | Ranking metrics | Recsys |
| Content-Based Filtering | — | Recommends via item-feature similarity | Cold-start friendly | Ranking metrics | Recsys |
| Reinforcement Learning | RL | Agent learns via interaction + reward | When action loops and data generate themselves | Cumulative reward | Robotics, games, ads |
| Multi-armed Bandit | MAB | Online RL for choice among known options | Balances explore vs exploit in production | Regret; lift | Ad tech, UX |
| Uplift Modeling | — | Predicts treatment effect, not outcome | Optimises causal lift, not prediction accuracy | Qini, AUUC, Uplift@K | Marketing, retention |
| Policy | — | Mapping from state → action | Output of RL or prescriptive model | Performance under policy | RL |
| Counterfactual | — | "What would have happened under alternative action?" | Required for policy evaluation | Inverse-propensity estimates | Causal, off-policy eval |

> All extensions beyond source-named four (`Optimization`, `Simulation`, `Decision Variable`, `Constraint`) are standard. `[verified from model knowledge, not source]`.

---

## 3. Frameworks & Matrices

### Framework 1: Optimisation Problem Structure
**Purpose:** Force a clean formulation of any "what should we do?" question into Objective + Variables + Constraints.

**Text Diagram:**
```
┌────────────────────────────────────────────────────────┐
│ OBJECTIVE FUNCTION      (max or min — one scalar)       │
│   e.g., max  Σ price_i × units_i − cost                 │
├────────────────────────────────────────────────────────┤
│ DECISION VARIABLES                                       │
│   x_i = units produced of product i                      │
│   y_j = binary: open warehouse j?                        │
├────────────────────────────────────────────────────────┤
│ CONSTRAINTS                                              │
│   Σ material_i × x_i ≤ material_available                │
│   x_i ≥ demand_i                                         │
│   y_j ∈ {0, 1}                                           │
│   x_i ≥ 0                                                │
├────────────────────────────────────────────────────────┤
│ → SOLVER (Gurobi, CPLEX, OR-Tools, CVXPY)                │
│ → Optimal variables + shadow prices (sensitivity)        │
└────────────────────────────────────────────────────────┘
```

Components:
- **Objective:** single scalar; often $ but can be latency, satisfaction index, etc.
- **Decision variables:** continuous, integer, or binary
- **Constraints:** capacity, budget, regulation, feasibility

**IT/AI/Product/Consulting worked example:** A SaaS company's marketing budget allocation. Objective: maximise conversions. Variables: spend per channel (Google, LinkedIn, podcast, events). Constraints: total budget ≤ $2M; each channel ≥ minimum viable spend; each channel ≤ saturation point. Solve with linear programming (assuming linear response) or convex optimisation (for diminishing returns). Output: channel spend allocation + shadow prices (value of loosening each constraint).

**When to pull this out in a meeting:** Any "where should we allocate X?" question with multiple decisions and shared constraint.

---

### Framework 2: Optimisation vs Simulation Choice Matrix
**Purpose:** Pick the right tool — optimisation finds the best solution analytically; simulation explores the outcome distribution.

**Text Diagram:**
```
                UNCERTAINTY IN INPUTS
                 LOW                    HIGH
            ┌─────────────────────┬─────────────────────┐
 DECISION   │                     │                     │
 SPACE      │  Deterministic      │  Stochastic         │
 SMALL      │  Optimisation       │  Optimisation       │
 (<100      │  (LP / MILP /       │  or Scenario LP     │
  options)  │   convex)           │                     │
            ├─────────────────────┼─────────────────────┤
 LARGE      │                     │                     │
 / COMPLEX  │  Heuristics +       │  Simulation         │
            │  Metaheuristics     │  (Monte Carlo /     │
            │  (GA, SA)           │  DES) + optimisation│
            │                     │  over scenarios     │
            └─────────────────────┴─────────────────────┘
```

Components:
- **Low-uncertainty + small decision space:** classical LP / MILP (Gurobi, CPLEX, OR-Tools)
- **Low-uncertainty + complex decisions:** heuristics / metaheuristics
- **High-uncertainty + small decision space:** stochastic LP, scenario-based optimisation
- **High-uncertainty + large decision space:** simulation (Monte Carlo, DES) or RL

**IT/AI/Product/Consulting worked example:** An AI consulting firm decides between:
- Marketing allocation (small decisions, low uncertainty) → LP
- Hiring plan over next 12 quarters (medium decisions, high uncertainty about demand) → stochastic LP or scenario modelling
- Agent-workflow design in a complex multi-step product (large decision space, high uncertainty) → RL or MAB

**When to pull this out in a meeting:** Pre-kickoff of any optimisation project — prevents misuse of tooling (e.g. solving a queueing problem with LP or a pricing problem with MAB when A/B is fine).

---

### Framework 3: Recommender / RL Sophistication Ladder
**Purpose:** Escalate from simple popularity-based recommenders to RL only when justified by data and business impact.

**Text Diagram:**
```
 Sophistication / Complexity
    │
    │    ┌──────────────────────────┐
    │    │  RL / Contextual Bandits  │  ← when action affects future rewards
    │    │  (LinUCB, Thompson)       │    or action loops exist
    │    └──────────────────────────┘
    │    ┌──────────────────────────┐
    │    │  Uplift Modeling          │  ← when causal lift matters,
    │    │  (S-learner, T-learner)   │    not just prediction
    │    └──────────────────────────┘
    │    ┌──────────────────────────┐
    │    │  Collab + Content Hybrid  │  ← standard state-of-the-art
    │    │  (matrix factorisation,   │    for large catalogues
    │    │   neural recsys)          │
    │    └──────────────────────────┘
    │    ┌──────────────────────────┐
    │    │  Content-Based Filtering  │  ← cold start; new items/users
    │    └──────────────────────────┘
    │    ┌──────────────────────────┐
    │    │  Collaborative Filtering  │  ← "people like you bought"
    │    └──────────────────────────┘
    │    ┌──────────────────────────┐
    │    │  Rule / Popularity-Based  │  ← baseline — always ship first
    │    └──────────────────────────┘
    │
    └─────────────────────────────────────► Data + engineering needed
```

Components:
- Start with rules; measure lift; climb only when lift justifies engineering
- RL is the final rung — never the first

**IT/AI/Product/Consulting worked example:** A B2B SaaS wants in-product recommendations for next-best action. Start with rules (if feature X used < 3 times, show tutorial). Measure. Then content-based recommender on feature-similarity. Measure. Then collaborative+content hybrid. Only after 6–9 months, consider contextual bandit if action loop exists.

**When to pull this out in a meeting:** When someone proposes building "an RL system" for a problem that a rule would solve. Prevents 6-month rabbit holes.

---

## 4. Formulas

### Formula 1: Linear Program Canonical Form
**Formula:**
Maximise: `c^T x`
Subject to: `Ax ≤ b`, `x ≥ 0`

**Variables:**
- x = decision vector (n × 1)
- c = objective coefficients (n × 1)
- A = constraint matrix (m × n)
- b = constraint RHS (m × 1)

**Why this formula exists:** The workhorse of prescriptive analytics. If you can force a problem into this shape, commercial solvers will find global optimum in seconds for millions of variables.

**How to interpret the output:**
- Optimal value of objective
- Values of each decision variable (the prescription)
- Shadow prices: marginal value of loosening each constraint by 1 unit

**Worked example:** Marketing budget allocation across 4 channels with $2M total.
- c = [CPA Google, CPA LinkedIn, CPA podcast, CPA events] → optimise conversions per $
- Constraints: Σ x_i ≤ 2,000,000; x_i ≥ min_i; x_i ≤ max_i (saturation)
- Solver output: Google $800k, LinkedIn $600k, Podcast $400k, Events $200k → 18k conversions vs 15k under current naive split.
- Shadow price on total budget = 0.008 conversions/$; meaning +$100k budget → +800 conversions.

**Data source:** Coefficients from marketing measurement (Nielsen MMM, internal attribution models). Solver: OR-Tools (free), Gurobi / CPLEX (commercial).

---

### Formula 2: Monte Carlo Convergence
**Formula:** `CI_95 half-width ≈ 1.96 × σ / √N`

**Variables:**
- σ = standard deviation of simulated outcome
- N = number of simulations

**Why this formula exists:** Tells you how many simulations are enough to estimate a metric within desired precision.

**How to interpret the output:**
- Quadruple N to halve CI width
- Stop when CI width < business-meaningful threshold

**Worked example:** Simulating 5-year ARR under uncertain churn, CAC, expansion. σ of annual ARR = $8M. Want CI ± $500k. N ≥ (1.96 × 8 / 0.5)² = **≈985** simulations. Run 1,000 Monte Carlo simulations.

**Data source:** Simulation code in Python (NumPy, simpy), R, or commercial tools (AnyLogic, Arena). Outputs stored in a parquet file or warehouse for exec review.

---

### Formula 3: Uplift@K
**Formula:** `Uplift@K = P(Y=1 | T=1, top K) − P(Y=1 | T=0, top K)`, where T = treated, Y = outcome

**Variables:**
- K = number of top-ranked customers
- P = probability of success (conversion, retention)

**Why this formula exists:** Regular model quality (AUC, accuracy) doesn't tell you if treating the top-ranked customers actually moves the outcome. Uplift does.

**How to interpret the output:**
- Uplift@10% > 0.05 → worth treating top 10%
- Uplift@10% ≈ 0 → model not capturing causal effect; rework targeting
- Uplift decaying past K → treatment saturates; don't chase the long tail

**Worked example:** An uplift model for retention campaigns. Top-10% uplift = 0.08 (8 percentage-point lift in retention from treatment). Target = these 10%. Avoid treating the "sure thing" and "lost cause" segments where uplift < 0.01.

**Data source:** From an RCT-trained uplift model (S-learner, T-learner, X-learner) using scikit-uplift or EconML. Evaluation via Qini curve.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|-------|
| Jump to RL when a rule + dashboard solves it | Start at the lowest rung of the recommender ladder; measure lift; escalate only on evidence |
| Hide uncertainty in a single "optimal answer" | Report sensitivity analysis + scenario outcomes alongside recommendations |
| Optimise without including real constraints | Every optimisation formulation has explicit capacity, regulatory, and budget constraints |
| Confuse prediction accuracy with prescriptive lift | Evaluate prescriptive models on business outcome (A/B test) not on AUC |
| Deploy recommendations without feedback loops | Track what users do with recommendations; feed back into the model (closed-loop) |
| Run Monte Carlo until "result looks right" | Stop based on CI convergence criterion, not eyeballing |
| Build a solver-based system without a rule fallback | Always have a deterministic fallback for solver failures or degraded mode |
| Automate the recommendation before validating | Start with human-in-the-loop; automate once accuracy and trust are established |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: AI SaaS Optimising Inference Cost Across Cloud Regions
**Situation:** An AI SaaS incurs $4M/year in GPU inference cost across 3 clouds; latency targets vary by customer.

**Applicable framework/metric:** Optimisation Problem Structure + MILP.

**Analysis:**
- Objective: minimise cost
- Variables: requests routed to region i = x_i
- Constraints: latency ≤ customer SLA; regional capacity; data residency (EU data → EU region)
- Solver: MILP in Gurobi

Current split: naive round-robin. Optimised split: 45% AWS us-east (cheapest on-demand), 25% GCP eu-west (residency), 20% Azure on spot (fallback), 10% burst to cheapest available.

Cost saving: $850k/year. Latency maintained within SLA at 99.5%.

**Decision rule:** Deploy if (a) model respects all hard constraints, (b) cost savings > 10% of annual spend, (c) regression test in staging passes.

**Action (Monday morning):** Prototype in OR-Tools; run on last month's traffic; compare against naive routing. Deploy gradually, shifting 10% of traffic per week.

---

### Scenario 2: Consulting Firm Advising Retailer on Dynamic Pricing
**Situation:** A 200-store retailer wants to move from manual weekly prices to dynamic pricing.

**Applicable framework/metric:** Recommender Ladder + Uplift.

**Analysis:**
- Rung 1 (rules): if inventory > 120% of target AND 2 weeks to expiry, reduce price 15% → $6M margin uplift (measured in pilot)
- Rung 2 (demand model): regression-based price-elasticity per SKU → $11M uplift
- Rung 3 (RL bandit): LinUCB per store × category → $14M uplift but 9 months engineering effort

**Decision rule:** Climb the ladder only when expected lift from next rung > 3× cost. Rung 1 → 2: easy yes (already at rung 2 lift, engineering modest). Rung 2 → 3: borderline; pilot in one category first.

**Action:** Ship rung 1 across all stores in 60 days (highest ROI). Start rung 2 dev in parallel. Evaluate rung 3 only after rung 2 is stable for 3 months.

---

### Scenario 3 (Anti-example): Automating Recommendations Before Building Trust
**Situation:** A B2B SaaS auto-applies "next-best-offer" discount recommendations generated by an ML model to customer-facing email, without human review. Several recommendations are absurd (wrong tier, wrong product).

**Applicable framework/metric:** Human-in-the-Loop + Uplift validation.

**Analysis (what goes wrong):**
- Model was predictive (high AUC) but not prescriptive (no uplift measurement).
- Recommendations went to customers without a review layer.
- A few public errors on LinkedIn; customer trust takes a hit.
- Sales team refuses to trust the system; manual overrides reach 80%.

**Cost of this mistake:** Revenue loss ~$1M; brand/PR cost higher; model retired and rebuilt with human review from scratch.

**Decision rule:** No prescriptive system auto-executes before (a) uplift is validated in an RCT, and (b) a 3-month human-in-the-loop phase.

**Action:** Roll back automation. Re-launch with explicit human approval step. Instrument uplift measurement via holdout group. Only re-automate after Uplift@K > 0.05 and model-agreement with human > 85% for 3 months.

---

## 7. Implementation Playbook

1. **Write every optimisation problem in canonical form** — Objective + Variables + Constraints — before writing any code. One-page template in Confluence.
2. **Default to open-source OR-Tools** — Gurobi / CPLEX only when problem scale demands; licence cost real.
3. **Install sensitivity-analysis output on every optimisation deliverable** — shadow prices, one-at-a-time sensitivity, scenario table.
4. **Maintain a recommender-ladder template per product** — every recommendation use case documents current rung + next-rung plan + expected lift.
5. **Require RCT / holdout group for prescriptive deployments** — never deploy without a way to measure causal uplift.
6. **Set up human-in-the-loop for new prescriptive systems** — manual review for first 1–3 months; track agreement rate; automate when > 90% agreement.
7. **Monitor policy drift** — treat the recommender/optimisation model like a ML model: monitor data drift, uplift decay, business-impact drift.
8. **Publish the prescriptive-analytics backlog with business-impact estimates** — prioritise by (Uplift × Reach) / Cost.

---

## 8. Content Quality Audit

**Covered well:**
- Introduces optimisation, simulation, decision variable, constraint.
- Mentions scenario analysis and automation.
- Notes the link from insight to execution.

**Underplayed or missing:**
- No LP canonical form; optimisation is discussed but not formalised.
- No distinction between LP, MILP, NLP, stochastic.
- No recommendation-system ladder.
- No RL, bandits, uplift — modern prescriptive vocabulary.
- No human-in-the-loop discipline.
- Sensitivity analysis mentioned only once (shallow).
- No references to Hillier/Lieberman (OR), Sutton/Barto (RL), Gutin/Punnen (routing), or Gurobi/CPLEX ecosystem.
- Zero IT/AI/Product examples; logistics, hospital, and factory dominate.

**Supplement with:**
- *Introduction to Operations Research* — Frederick Hillier & Gerald Lieberman (11th ed 2020, McGraw-Hill). Canonical OR textbook.
- *Optimisation Models* — Giuseppe Calafiore & Laurent El Ghaoui (2014, Cambridge). Modern treatment.
- *Reinforcement Learning: An Introduction* — Richard Sutton & Andrew Barto (2nd ed 2018, MIT Press). Free PDF. Canonical RL text.
- *Bandit Algorithms* — Tor Lattimore & Csaba Szepesvári (2020, Cambridge). Free PDF. Bandit theory + practice.
- *Recommender Systems: The Textbook* — Charu Aggarwal (2016, Springer).
- *Simulation Modeling and Analysis* — Averill Law (5th ed 2014, McGraw-Hill). Canonical simulation text.
- HBR: "Algorithms Need Managers, Too" — Michael Luca, Jon Kleinberg, Sendhil Mullainathan, *HBR*, Jan–Feb 2016. Decision-automation tradeoffs.
- HBR: "Building the AI-Powered Organization" — Tim Fountaine, Brian McCarthy, Tamim Saleh, *HBR*, Jul–Aug 2019. Scaling prescriptive.
- McKinsey: "The real-world potential and limits of prescriptive analytics" (2023).
- HBS case: "Cisco's Cost-to-Serve Optimization" — classic supply-chain prescriptive.
- HBS case: "UPS: Orion Route Optimization" — canonical routing case.
- IIMA case: "Flipkart's Pricing Algorithm" — Indian-context dynamic pricing.

**Red flags in the source:**
- "Incorporate real-world constraints such as budgets, capacity limits, and regulatory requirements" — correct but without formal structure (objective + variables + constraints).
- "Automate routine decisions where the prescriptive model has demonstrated consistent accuracy" — missing human-in-the-loop and uplift-validation pre-steps.
- Recommendation/personalisation — one of the biggest prescriptive use cases — absent.
- RL / bandits — entire field absent.
- Hospital-staffing example is good but lacks the model-formulation detail that makes prescriptive actionable.

**Connects to:**
- `audit_management_course/business-analytics/01-introduction-to-business-analytics.md` (ladder context)
- `audit_management_course/business-analytics/04-predictive-analytics.md` (feeds prescription)
- `audit_management_course/business-analytics/10-operations-analytics.md` (OR for operations)
- `audit_management_course/operations-management/08-improving-processes-lean.md` (ops optimisation)
- `audit_management_course/operations-management/10-facility-layout-for-flow.md` (facility LP)
- `audit_management_course/strategic-pricing/05-ai-and-ml-in-predictive-pricing-models.md` (ML-driven dynamic pricing)
- `audit_management_course/strategic-pricing/07-dynamic-pricing.md` (dynamic pricing mechanics)
- `audit_management_course/supply-chain-management/10-network-planning.md` (network design optimisation)
- `audit_management_course/ai-ml-business/13-predictive-and-prescriptive-analytics.md` (ML-side prescription)
- `audit_management_course/business-analytics/12-ethics-governance-analytics.md` (automation ethics)

---

## 9. Quick-Recall Card

```
Topic: Prescriptive Analytics
Core idea: Recommend (or automate) actions via optimisation, simulation, recsys, RL.
Key metric/formula: LP canonical form; Monte Carlo CI; Uplift@K.
Framework trigger: Budget allocation, routing, pricing, staffing, personalisation.
Watch out for: Skipping rungs (going straight to RL), auto-executing without uplift validation.
Monday action: Write canonical optimisation formulation for top prescriptive use-case; pilot rule-based rung first.
As a PM/Consultant/AI Lead, the one question to answer with this framework is:
"Does the prescribed action beat the current policy in an RCT, and is the system trustworthy enough to remove the human?"
```

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Pass 1 average: 4.8
Sections rewritten: none (no criterion <4/5)
Enrichments applied: [cross-course links to business-analytics/01, 04, 10, 12; operations-management/08, 10; strategic-pricing/05, 07; supply-chain-management/10; ai-ml-business/13. Hillier/Lieberman 2020, Calafiore/El Ghaoui 2014, Sutton/Barto 2018, Lattimore/Szepesvári 2020, Aggarwal 2016, Law 2014. Luca/Kleinberg/Mullainathan HBR 2016, Fountaine/McCarthy/Saleh HBR 2019, McKinsey 2023. HBS Cisco + UPS Orion, IIMA Flipkart. Anti-example Scenario 3 (auto-executing recs without uplift validation). Data sources: OR-Tools, Gurobi, CPLEX, CVXPY, scikit-uplift, EconML, LinUCB/Thompson. Decision-maker view in Quick-Recall.]
Final scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] — average 5.0
Pass 2 completed: 2026-04-18 01:15
-->
