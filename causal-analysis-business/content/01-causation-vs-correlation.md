# Causation vs Correlation

## Overview
Correlation means two things tend to move together, but causation means one thing actually makes the other happen. In business, confusing the two can lead to costly decisions based on patterns that have no real cause-and-effect link. Understanding this distinction is the foundation of all causal analysis. Every method in this course exists because simply observing that two metrics move together is not enough to prove one drives the other.

---

## Why It Matters
Businesses constantly observe patterns in their data, such as higher ad spending coinciding with higher revenue or employee satisfaction rising alongside productivity. Acting on correlation alone can waste resources or create harmful policies. Only by establishing true causation can leaders confidently invest in strategies that actually produce desired outcomes.

## Key Principles
- Correlation describes a statistical relationship between two variables, but says nothing about which causes which
- Causation requires demonstrating that a change in one variable directly produces a change in another
- Confounding variables are hidden factors that can create the illusion of a causal link between two unrelated things
- Reverse causality occurs when the assumed direction of cause and effect is actually backwards

## Key Terms
| Term | Definition |
|------|------------|
| **Correlation** | A statistical measure showing how strongly two variables move together, without implying one causes the other |
| **Causation** | A relationship where a change in one variable directly produces a change in another variable |
| **Confounding Variable** | A third factor that influences both the supposed cause and the supposed effect, creating a misleading association |
| **Spurious Correlation** | A statistical relationship between two variables that appears meaningful but is actually coincidental or driven by a hidden third factor |

## Use Case
A retail chain notices that stores playing classical music have higher sales and wants to know if the music itself drives purchases or if those stores simply happen to be in wealthier neighborhoods.

## Scenario
> A streaming platform observes that users who watch documentary content also have longer subscription lifespans. The marketing team proposes pushing documentaries to all users to reduce churn. However, analysis reveals that documentary viewers tend to be older, more educated users who are already less likely to cancel regardless of what they watch. The correlation between documentaries and retention is driven by a confounding demographic factor, not the content itself.

## Examples
- Ice cream sales and drowning incidents both rise in summer, but ice cream does not cause drowning; warm weather drives both
- Companies with more diverse boards often have higher profits, but the relationship may reflect that larger, better-managed companies both pursue diversity and generate strong returns

---

## Audited Appendix

# Causation vs Correlation
**Course:** Applied Methods for Causal Analysis in Business
**Module:** Content / Causation vs Correlation
**Audited on:** 2026-04-18
**Audited by:** A7
**Source files reviewed:** `causal-analysis-business/content/01-causation-vs-correlation.md`

---

## 1. Topic Snapshot
Correlation measures whether two variables move together; causation asserts that changing X actually changes Y, and conflating the two is the single most expensive analytical error in modern enterprises.
For an IT/AI/Product/Consulting leader, correlation-based decisions silently mis-allocate budget in product roadmaps (feature = retention?), hiring (training = promotion?), marketing (channel = conversion?), and ML models (spurious feature = prediction?), because observational data is riddled with confounders, reverse causality, and selection bias.
The decision this topic enables: *before any investment, policy, or ML feature ships, ask "would Y change if we intervened on X?" and require evidence beyond a Pearson coefficient.*

---

## 2. Jargon & Terminology

| # | Term | Plain-English Definition | IT/AI/Product/Consulting Example |
|---|------|--------------------------|----------------------------------|
| 1 | Correlation (Pearson r) | Linear association between two continuous variables, range [−1, 1] | NPS vs MRR = 0.42 |
| 2 | Spearman ρ | Rank-order correlation; captures monotonic, non-linear ties | Plan-tier rank vs usage rank |
| 3 | Kendall τ | Concordance-based rank correlation; robust to ties | A/B ranking consistency across cohorts |
| 4 | Causation | Intervention on X produces a change in Y (do-operator, P(Y\|do(X))) | Turning feature flag ON lifts retention |
| 5 | Confounder (Common Cause) | A variable that drives both X and Y, inflating apparent link | Tenure drives both feature-use and retention |
| 6 | Spurious Correlation | Statistical association with no causal link | Ice-cream sales ↔ drownings |
| 7 | Reverse Causality | Y causes X, not X causes Y | Revenue drives ad-spend, not the reverse |
| 8 | Selection Bias | Sample non-representative of target population | Only power users complete the NPS survey |
| 9 | Simpson's Paradox | Aggregate trend reverses within subgroups | Conversion up overall but down per segment |
| 10 | DAG (Directed Acyclic Graph) | Graph encoding assumed causal structure | Pearl-style DAG of onboarding → activation → retention |
| 11 | Counterfactual | "What would have happened if…" outcome for same unit | User retention had they *not* seen feature X |
| 12 | Potential Outcomes (Rubin) | Y(1) and Y(0) per unit; only one observed | Treated vs untreated customer's revenue |
| 13 | Treatment / Control | Group receiving intervention vs not | A/B variant vs holdout |
| 14 | Instrumental Variable (IV) | Variable affecting X but not Y directly | Random coupon lottery as IV for price change |
| 15 | Randomisation | Random assignment breaks confounding | 50/50 experiment split |
| 16 | Observational Data | Non-experimental, naturally occurring data | Clickstream logs, CRM, warehouse tables |
| 17 | Natural Experiment | Real-world event mimicking randomisation | Region rollout delay due to regulation |
| 18 | Ecological Fallacy | Inferring individual behaviour from group averages | "Country X uses AI more" → "this user does" |
| 19 | Post-Hoc Ergo Propter Hoc | "After, therefore because" fallacy | Launched campaign Monday → revenue up Tuesday |
| 20 | Collider | Variable caused by both X and Y; conditioning opens bias | Conditioning on "got promoted" when studying skill→tenure |
| 21 | Mediator | Variable on the causal path X → M → Y | Activation as mediator from signup → retention |

---

## 3. Frameworks & Matrices

### 3.1 Correlation → Causation Ladder (5 Rungs)
**Purpose:** Decide how much evidence you have before committing budget or policy.

```
Rung 5 | Causal Inference (DoWhy/EconML, IV, DiD, Synthetic Control) --> ship with confidence
Rung 4 | Controlled Experiment (A/B, MAB, switchback)               --> gold standard
Rung 3 | Hypothesis Test + Confounder Control (regression, PSM)     --> defensible
Rung 2 | Statistical Correlation (Pearson/Spearman, p-value)        --> signal, not proof
Rung 1 | Visual Pattern (scatter, dashboard)                        --> hypothesis only
```
**Components:** evidence grade, assumptions required, decision weight.
**Worked example:** PM sees "users of feature F churn less" (Rung 1) → computes r = −0.38 (Rung 2) → regresses churn on F controlling for tenure/plan (Rung 3) → runs hold-out experiment (Rung 4) → estimates heterogeneous CATE via EconML for rollout targeting (Rung 5).
**Trigger:** any dashboard insight that could lead to ≥ ₹50L spend or a policy change.

### 3.2 DAG Basics (ASCII)
**Purpose:** Make causal assumptions explicit before modelling.

```
Chain:       X --> M --> Y              (M is a mediator; test mechanism)
Fork:        X <-- C --> Y              (C is a confounder; MUST adjust)
Collider:    X --> K <-- Y              (K is a collider; DO NOT condition)
Direct:      X --> Y                    (target effect)
```
**Components:** nodes = variables, arrows = assumed direction, back-door vs front-door paths.
**Worked example:** Studying "training hours (X) → promotion (Y)" with ambition (C) as fork; conditioning on "manager nomination (K)" opens collider bias.
**Trigger:** any observational analysis where randomisation is impossible.

### 3.3 Confounder Checklist
**Purpose:** Rapid pre-mortem on every correlation claim.

```
[ ] Age / demographics
[ ] Tenure / cohort
[ ] Seasonality (week, month, quarter)
[ ] Time-of-day / day-of-week
[ ] Region / geography / timezone
[ ] User type / plan / segment
[ ] Device / platform / OS
[ ] Prior test or campaign exposure
[ ] Data-collection change / instrumentation drift
```
**Components:** variable, hypothesised direction, available in warehouse? (Y/N), adjustment method.
**Worked example:** Consultant auditing churn model finds "support ticket volume" correlated with churn; checklist reveals tenure + plan + device confound — effect collapses after adjustment.
**Trigger:** any correlation > 0.2 used in a business case.

### 3.4 (Optional) Simpson's Paradox Warning Pattern
**Purpose:** Catch aggregate-vs-segment reversals before they mis-steer strategy.

```
Aggregate:    Variant B > Variant A      (ship B?)
Segment 1:    Variant A > Variant B
Segment 2:    Variant A > Variant B
Segment 3:    Variant A > Variant B      --> DO NOT ship B
```
**Trigger:** any A/B result with skewed traffic across segments, or pre/post launches with mix-shift.

---

## 4. Formulas

### 4.1 Pearson r
r = Cov(X, Y) / (σ_X · σ_Y), range [−1, 1].
**Thresholds (business rule-of-thumb):** |r| < 0.1 trivial; 0.1–0.3 weak; 0.3–0.5 moderate; >0.5 strong — none imply causation.
**Numeric example:** feature-usage minutes vs 90-day retention r = 0.46 (looks strong) — after controlling for tenure the partial r drops to 0.08.

### 4.2 Spearman ρ
ρ = Pearson r computed on ranks; robust to non-linearity and outliers.
**Threshold:** same bands as Pearson.
**Example:** plan-tier rank vs NPS rank ρ = 0.31; monotonic but weak.

### 4.3 Observed Effect Decomposition
Observed Association = Causal Effect + Confounding Bias + Selection Bias + Measurement Error
**Example:** Observed churn lift from "onboarding email opens" = −6 pp. Decomposition: −1 pp causal (from RCT), −4 pp confounded by engaged-user type, −1 pp selection (opt-in sample).

### 4.4 Conditional Independence Check
X ⊥ Y | Z  ⇔  P(X, Y | Z) = P(X | Z) · P(Y | Z)
**Use:** if X and Y become independent once Z is held fixed, Z is likely the confounder.
**Example:** feature-usage ⊥ churn | tenure — so tenure, not feature-usage, is the causal lever.

**Thresholds for "controlled":** partial r drop > 50% OR effect not significant at α = 0.05 after adjustment ⇒ original correlation was confounded.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|----|-------|
| 1 | Draw a DAG before running the regression | Start with the regression and back-fit a story |
| 2 | List ≥ 5 plausible confounders upfront | Assume "controls in the model" handles everything |
| 3 | Demand an experiment (or quasi-experiment) for decisions > ₹50L | Escalate a dashboard correlation to CXO as proof |
| 4 | Use DoWhy / EconML refutation tests (placebo, random common cause) | Report a point estimate without sensitivity analysis |
| 5 | Segment results before averaging (Simpson check) | Trust aggregate lift on skewed traffic |
| 6 | State the counterfactual explicitly | Use vague language like "drives", "boosts", "leads to" |
| 7 | Flag reverse-causality candidates (revenue↔ad-spend, satisfaction↔productivity) | Assume chronology proves causation |
| 8 | Audit ML model features for confounding / leakage | Ship model features chosen by correlation to target |

---

## 6. Real-Life Scenarios

### Scenario 1 — Product Analytics (PM lens)
Growth PM claims "users of the collaboration feature retain 2.3× longer; let's make it default for all." Audit: collaboration users are mostly workspace-owners on 12+ month tenure (confounder) AND only surviving cohorts are measured (survivorship). After matched-cohort analysis + 2-week holdout, true causal lift = 11%, not 130%. Decision: ship with targeted onboarding, not universal default. Tools: Amplitude (behavioural segments), Mixpanel (funnels, with sampling caveats), Python statsmodels / pingouin, DoWhy for refutation, Snowflake for event backfill.

### Scenario 2 — HR / People Analytics (Consulting lens)
Client's HR dashboard shows "employees with >40 hrs training/yr are 3× more likely to be promoted." Consultant diagnoses selection bias: ambitious employees self-select into voluntary training, and managers nominate the same employees (collider on nomination). Recommendation: run a randomised lottery for the next training cohort OR use IV based on manager rotation. Deliverable: revised causal estimate + policy memo. Tools: DAGitty (DAG), Python EconML (DR-learner), Looker governed model.

### Scenario 3 — ANTI-EXAMPLE: Marketing Scale-Up (AI Lead lens)
Marketing team observes r = 0.72 between "influencer-campaign impressions" and "weekly signups"; CMO approves ₹8 cr expansion. Data team later runs a geo-holdout A/B: causal lift = 0.4%, not the implied ~40%. Confounder: brand-search burst from concurrent PR cycle. Quantified waste: ~₹6.2 cr of the ₹8 cr was not causally attributable; payback period slipped from 4 to 19 months. Lesson: gate scale-up decisions on Rung 4+ evidence. Tools: GeoLift (Meta OSS), DoWhy, Snowflake + dbt for exposure logs.

---

## 7. Implementation Playbook

1. **Draft** a DAG (Miro / DAGitty) of the proposed causal claim with ≥ 3 confounders and ≥ 1 collider.
2. **Inventory** data sources (Snowflake / BigQuery tables) covering treatment, outcome, and confounders; flag missingness.
3. **Compute** Pearson, Spearman, and partial correlations (pingouin) as a baseline diagnostic.
4. **Test** conditional independence using regression adjustment or propensity matching (statsmodels, scikit-learn).
5. **Run** refutation tests in DoWhy (placebo treatment, random common cause, data subset) and report sensitivity.
6. **Design** an A/B, switchback, or geo-holdout if the claim survives observational scrutiny; power-calc with MDE.
7. **Decide** using the Ladder: only claims at Rung 4 or 5 proceed to rollout; document the counterfactual.
8. **Publish** a one-page causal-memo (claim, DAG, evidence grade, decision, monitoring plan) to the relevant Slack / Confluence channel.

---

## 8. Content Quality Audit

**Covered well (in source):** basic definitions, retail classical-music example, streaming documentary confounder, ice-cream/drowning spurious correlation, diverse-boards example.

**Underplayed / missing:**
- DAG-based thinking (Pearl's do-calculus, back-door / front-door criteria).
- Simpson's paradox and mix-shift in A/B tests.
- Collider bias (conditioning on post-treatment variables).
- Potential-Outcomes framework (Rubin) and formal counterfactuals.
- Modern practitioner toolkits: DoWhy, EconML, CausalML, DoubleML, GeoLift.
- ML-specific confounding: spurious features, target leakage, shortcut learning, distribution shift.
- Quantitative sensitivity analysis (E-value, Rosenbaum bounds).

**Supplementary sources (≥5):**
1. Pearl, J. *Causality: Models, Reasoning, and Inference*, 2nd ed., Cambridge Univ. Press, 2009.
2. Pearl, J. & Mackenzie, D. *The Book of Why*, Basic Books, 2018.
3. Angrist, J. & Pischke, J-S. *Mostly Harmless Econometrics*, Princeton, 2008.
4. Imbens, G. & Rubin, D. *Causal Inference for Statistics, Social, and Biomedical Sciences*, Cambridge, 2015.
5. Hernán, M. & Robins, J. *Causal Inference: What If*, Chapman & Hall / online, 2020.
6. Microsoft Research — DoWhy & EconML documentation (2024 releases).

**Red flags in the source:**
- Uses "drives" ambiguously without distinguishing association from intervention.
- No mention of colliders — practitioners can create bias by over-controlling.
- No quantified anti-example (cost of acting on correlation).
- No role-specific guidance for PM / Consultant / AI Lead.
- Tooling omitted: the modern causal stack (DoWhy, EconML, DAGitty) is absent.

---

## 9. Quick-Recall Card
- Correlation = moves together; Causation = intervention on X changes Y.
- Always draw a DAG and list confounders, colliders, mediators.
- Climb the Ladder: visual → stats → adjusted → experiment → causal inference.
- Simpson's paradox + collider bias are the two silent killers of dashboard insights.
- Modern toolkit: DoWhy, EconML, DAGitty, pingouin, GeoLift.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: **"Would our outcome metric change if we intervened on this driver, holding everything else equal — and what evidence rung on the Correlation-to-Causation Ladder am I actually standing on?"**

---

**Connects to:** [02-randomized-controlled-experiments.md](02-randomized-controlled-experiments.md), [03-ab-testing-business.md](03-ab-testing-business.md), [04-regression-causal-inference.md](04-regression-causal-inference.md), [../business-analytics/08-regression-analysis-business.md](../business-analytics/08-regression-analysis-business.md), [../six-sigma/05-analyze-phase.md](../six-sigma/05-analyze-phase.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4]
Sections rewritten: [1, 2, 3, 4, 6, 8, 9]
Enrichments applied: [cross-course links; 5+ supplements; anti-example w/ ₹6.2 cr waste; IT tooling (DoWhy, EconML, DAGitty, pingouin, GeoLift, Snowflake, Amplitude); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A7
-->
