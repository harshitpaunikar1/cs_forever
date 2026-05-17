# Randomized Controlled Experiments

## Overview
A randomized controlled experiment assigns participants randomly to a treatment group or a control group, then measures the difference in outcomes between them. Random assignment ensures that, on average, the two groups are identical in every way except for the treatment itself. This eliminates confounding variables and provides the strongest evidence for causation. It is often called the gold standard of causal inference.

---

## Why It Matters
Without randomization, any observed difference between groups could be driven by preexisting differences rather than the treatment. Randomized experiments give businesses confidence that a new product feature, pricing strategy, or operational change actually causes the results they observe, rather than being an artifact of selection bias or hidden variables.

## Key Principles
- Random assignment balances both known and unknown confounders across groups, isolating the effect of the treatment
- The control group provides a baseline for comparison, showing what would have happened without the intervention
- Large sample sizes reduce the role of chance and increase statistical power to detect real effects
- Blinding participants or analysts to group assignments prevents bias from influencing behavior or interpretation

## Key Terms
| Term | Definition |
|------|------------|
| **Treatment Group** | The set of participants who receive the intervention or change being tested |
| **Control Group** | The set of participants who do not receive the treatment and serve as the baseline for comparison |
| **Random Assignment** | The process of allocating participants to groups using chance alone, so every individual has an equal probability of being in any group |
| **Statistical Power** | The probability that an experiment will detect a true effect when one actually exists, influenced by sample size and effect magnitude |

## Use Case
An e-commerce company randomly assigns half its customers to see a redesigned checkout page and the other half to see the original, then compares conversion rates to determine if the redesign genuinely increases purchases.

## Scenario
> A bank wants to know whether offering a financial literacy workshop reduces loan default rates. It randomly selects 2,000 new borrowers and invites half to attend the workshop while the other half receives no invitation. Six months later, the bank compares default rates between the two groups. Because assignment was random, any difference in defaults can be attributed to the workshop rather than to borrower characteristics.

## Examples
- A pharmaceutical company tests a new drug by randomly giving some patients the real medication and others a placebo, then comparing health outcomes
- A logistics firm randomly assigns half its delivery routes to a new scheduling algorithm and keeps the other half on the old system to measure whether on-time delivery improves

---

## Audited Appendix

# Randomized Controlled Experiments
**Course:** Applied Methods for Causal Analysis in Business
**Module:** Content / Randomized Controlled Experiments
**Audited on:** 2026-04-18
**Audited by:** A8
**Source files reviewed:** `causal-analysis-business/content/02-randomized-controlled-experiments.md`

---

## 1. Topic Snapshot
Randomized Controlled Experiments (RCEs) assign units randomly to treatment vs. control, making groups identical on average except for the intervention, which eliminates confounding and establishes causality. An IT/AI/Product/Consulting leader should treat them as the gold standard because they convert opinion-driven product, marketing, and ops decisions into evidence-based bets where the effect size is measurable, defensible, and replicable. The decision it enables: "Should we ship, kill, or iterate this change — and what is the expected lift with a known confidence interval?"

---

## 2. Jargon & Terminology

| # | Term | Plain Meaning | IT/AI/Product/Consulting Lens | Watch-out |
|---|------|---------------|-------------------------------|-----------|
| 1 | Treatment Group | Units that receive the intervention | Users served new checkout, new model | Must be randomly assigned |
| 2 | Control Group | Units that receive baseline/no change | Users on old checkout / current model | Keep stable through test |
| 3 | Random Assignment | Probabilistic allocation to arms | Hashing user_id mod N | Hash must be stable and uniform |
| 4 | Intention-to-Treat (ITT) | Analyse by assignment, not actual exposure | Counts users who were bucketed even if they never saw feature | Preserves randomisation guarantee |
| 5 | Average Treatment Effect (ATE) | Mean outcome difference treatment − control | Lift in conversion, revenue/user | Average can mask heterogeneity |
| 6 | Conditional ATE (CATE) | ATE for a sub-segment | Effect on mobile users vs desktop | Needs pre-specified segments |
| 7 | Local ATE (LATE) | Effect on compliers only | Effect on users who actually opened the email | Requires instrument (random assignment) |
| 8 | Statistical Power | P(detect effect if real) | Target 0.80 | Underpowered tests kill real wins |
| 9 | Type I Error (alpha) | False positive rate | Usually 0.05 | Inflates with peeking |
| 10 | Type II Error (beta) | False negative rate | Usually 0.20 | Rises with small n or small effect |
| 11 | Minimum Detectable Effect (MDE) | Smallest lift the test can catch | Pre-commit 2pt CTR lift | MDE smaller than business value = waste |
| 12 | Effect Size (Cohen's d) | Standardised difference | (mu1 − mu2)/pooled sd | Useful for cross-metric comparison |
| 13 | Blocking / Stratified Randomisation | Randomise within strata | By region, plan tier, seniority | Reduces variance |
| 14 | Cluster Randomisation | Randomise groups, not individuals | Randomise by manager, store, route | Needs ICC adjustment |
| 15 | Blinding (Single / Double) | Hide arm from user / analyst | UI-identical variants; blinded analyst | Prevents expectation bias |
| 16 | Blinded Analysis | Analyse before unblinding labels | Locked code + frozen dataset | Stops p-hacking |
| 17 | Pre-Registration | Commit hypotheses, metrics, stop rules | Document in Eppo / GrowthBook before launch | Prevents HARKing |
| 18 | Compliance / Crossover | Users don't follow assignment | Treatment user never logs in | Use ITT + LATE |
| 19 | Attrition | Units drop out mid-experiment | Churn before measurement | Check differential attrition |
| 20 | External Validity | Generalisability to real world | Canary cohort vs full population | Novelty can inflate lift |
| 21 | Internal Validity | Causal claim holds within experiment | No leakage, stable assignment | SRM checks |
| 22 | Hawthorne Effect | Behaviour changes because observed | Employees perform better when monitored | Blinding mitigates |
| 23 | Novelty Effect | Temporary lift from newness | New UI spikes, then regresses | Run long enough |
| 24 | Primacy Effect | Early users bias result | Power users dominate first week | Include ramp-up + steady-state |

---

## 3. Frameworks & Matrices

### 3.1 RCE Design Workflow
**Purpose:** Standardise end-to-end experiment lifecycle so every team ships with the same rigor.

```
+-------------+    +------+    +---------------+    +---------------+    +-----+    +-------------+    +--------+
| Hypothesis  | -> | MDE  | -> | Power / n     | -> | Randomisation | -> | Run | -> | Analyse ITT | -> | Report |
| (if X, Y)   |    |      |    | (alpha, beta) |    | (hash + SRM)  |    |     |    | + CATE      |    |        |
+-------------+    +------+    +---------------+    +---------------+    +-----+    +-------------+    +--------+
                                                          |                                               |
                                                          +--- Pre-registration (Eppo / GrowthBook) <-----+
```
**Components:** Hypothesis, MDE, sample size, randomisation unit, guardrail metrics, primary metric, run window, ITT + CATE analysis, decision memo.
**Worked example (AI Product):** New LLM ranker → MDE = 2% CTR lift → n = 63k/arm for alpha=0.05, beta=0.20 → hash-based assignment at session → 14-day canary → ITT shows +1.8% CTR (p=0.03) → ship at 50%, monitor for 7 days.
**Trigger:** Any user-visible change, model swap, pricing tweak, or process re-engineering with measurable KPI.

### 3.2 Randomisation Scheme Selector
**Purpose:** Pick the right unit of randomisation so results aren't contaminated or biased.

```
                  Contamination risk?
                   /           \
                  No            Yes
                  |              |
             Heterogeneity?   Cluster Randomisation
              /        \       (manager, store, route)
             Low       High
             |          |
          Simple     Blocking / Stratified
         (hash mod)  (by segment / seniority)
```
**Components:** Unit (user, session, cluster), stratification keys, contamination vector, ICC estimate.
**Worked example (Consulting):** Sales methodology training — reps in same team talk, so cluster-randomise at manager level; stratify by region and tenure.
**Trigger:** Whenever spillover between users is plausible (social features, B2B teams, shared queues).

### 3.3 Validity Threat Matrix

|  | Selection | Attrition | Hawthorne | Compliance |
|---|---|---|---|---|
| **Internal Validity** | Random assignment; SRM audit | Pre-commit attrition threshold; differential check | Blind UI; identical comms | ITT as primary; LATE as secondary |
| **External Validity** | Randomise over representative cohort | Follow-up measurement; steady-state window | Extended run past novelty | Report compliance rate transparently |

**Worked example (Product):** New onboarding flow — SRM passed, but 12% of treatment never completed signup (differential attrition) → report both ITT and per-protocol, flag bias.
**Trigger:** Any experiment readout before ship decision.

### 3.4 (Optional) ATE vs CATE vs LATE Diagnostic
- **ATE** — everyone assigned; headline number for ship decision.
- **CATE** — by segment; decides targeted rollout (e.g., mobile-only ship).
- **LATE** — for compliers; explains "true" effect when adoption is partial (e.g., opt-in AI assistant).

---

## 4. Formulas

### 4.1 Two-Proportion Sample Size (per arm)
`n ≈ [z_(α/2) + z_β]² · [p1(1 − p1) + p2(1 − p2)] / (p1 − p2)²`
**Thresholds:** alpha=0.05 (z=1.96), beta=0.20 (z=0.84). For alpha=0.05 two-sided + power 0.80, bracket ≈ 7.85.
**Example (AI product, 2-pt CTR lift):** Baseline p1 = 0.05, p2 = 0.07. Numerator = 7.85 × (0.0475 + 0.0651) = 7.85 × 0.1126 = 0.884. Denominator = (0.02)² = 0.0004. **n ≈ 2,210 per arm.** On a 5% canary with 50k DAU → 2,500 treated/day → reach n in ~1 day, but run 14 days to cover weekly seasonality and novelty.

### 4.2 Effect Size (Cohen's d)
`d = (μ1 − μ2) / pooled σ`
**Thresholds:** 0.2 small, 0.5 medium, 0.8 large.
**Example:** Revenue/user mu1=₹420, mu2=₹450, pooled sd=₹300 → d = 0.10. Small — needs large n; ~1,570 per arm for power 0.80.

### 4.3 Power
`Power = P(reject H0 | H1 true); target ≥ 0.80`
**Example:** With n=1,000/arm, MDE=2pt on 5% baseline → power ≈ 0.55 (underpowered). Either raise n, extend window, or accept larger MDE.

### 4.4 Intention-to-Treat (ITT)
`ITT effect = E[Y | assigned treatment] − E[Y | assigned control]`
**Threshold:** Report ITT as primary regardless of compliance rate; disclose compliance %.
**Example:** 100k assigned to new onboarding, only 60% actually saw it. ITT lift = +0.8pt signup; LATE (compliers) ≈ 0.8 / 0.6 = +1.33pt.

### 4.5 Cluster Adjustment (Design Effect)
`n_effective = n / (1 + (m − 1) · ICC)`
**Thresholds:** ICC 0.01–0.05 typical for employee/customer clusters.
**Example (HR training):** 50 managers × 20 reports = 1,000. ICC=0.05. Design effect = 1 + 19·0.05 = 1.95. n_effective = 1,000 / 1.95 ≈ 513. Plan for ~2× raw sample.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|----|-------|
| 1 | Pre-register hypothesis, primary metric, MDE, stop rule | Peek daily and stop when p<0.05 (alpha inflation) |
| 2 | Run SRM (sample ratio mismatch) check before analysis | Trust randomisation blindly — instrumentation bugs are common |
| 3 | Report ITT as primary | Use per-protocol only — reintroduces selection bias |
| 4 | Use cluster randomisation when spillover exists | Randomise individuals in features with network effects |
| 5 | Pre-commit segments for CATE | Data-mine subgroups post-hoc (HARKing) |
| 6 | Run past novelty window (≥1 full cycle) | Call ship at day 3 on a spike |
| 7 | Use alpha-spending / sequential tests for early stops | Run multiple one-sided tests informally |
| 8 | Document guardrail metrics (latency, churn, revenue) | Optimise one metric while silently harming another |
| 9 | Size to business-relevant MDE, not the smallest detectable | Chase statistical significance that's economically trivial |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI Product Canary
New GenAI summarisation feature. 5% treatment, 5% control, 90% holdout. Pre-registered MDE = 3% lift in task-completion rate; 14-day pilot; guardrails = p95 latency < 1.2s, cost/session < ₹0.40. Hash on user_id. Day 14: ITT +3.8% completion, p=0.02; latency +80ms (within guardrail); cost +₹0.11. **Decision:** ramp to 25% next sprint, re-run SRM.

### Scenario 2 — HR Training
Bank rolls out "credit risk workshop" to 2,000 new borrowers. Stratified by function (retail vs SME) and seniority (junior vs senior RM); cluster-randomised at branch manager level to avoid within-team contamination. 6-month default rate: treatment 3.1% vs control 4.2%; ITT diff = -1.1pt, p=0.04. Design effect applied (ICC=0.04). **Decision:** roll out firm-wide; expected ~₹8 cr reduction in annual defaults.

### Scenario 3 — ANTI-EXAMPLE (quantified)
Consulting team pushes a "new pricing page." Instead of randomising, they ship to early-adopter cohort for 2 weeks, then compare to a "laggard" cohort from last quarter. Report +18% conversion; leadership green-lights firm-wide rollout at ₹12 cr engineering + migration cost. Post-launch conversion drops 4% vs pre-launch baseline because the "lift" was a cohort artifact (early adopters always convert more). **Backfire: ₹12 cr sunk + ~₹6 cr annual revenue loss until rollback = ₹18 cr quantified cost.** Root cause: no random assignment → selection bias masqueraded as treatment effect.

**Tools:** Optimizely, LaunchDarkly, GrowthBook, Eppo, Statsig, Python (`statsmodels`, `scipy.stats`, `PyMC` for Bayesian), Snowflake, Looker, Evan Miller's sample-size calculators, CUPED variance-reduction libraries.

---

## 7. Implementation Playbook
1. **Draft** one-page hypothesis doc (change, primary metric, MDE, guardrails, segments).
2. **Compute** sample size + duration using two-proportion or t-test formula; include cluster adjustment if relevant.
3. **Pre-register** in Eppo/GrowthBook with locked metrics, stop rules, and analysis plan.
4. **Instrument** event logging and randomisation (stable hash on user_id/session_id); run A/A dry-run to verify SRM.
5. **Launch** on canary (5–10%) with feature flag; monitor guardrails daily via Looker dashboard.
6. **Freeze** data at pre-committed date; run blinded ITT analysis + pre-specified CATE.
7. **Decide** ship / iterate / kill via decision memo; attach SRM, attrition, guardrail results.
8. **Archive** experiment + learnings in a company-wide experiment registry for meta-analysis.

---

## 8. Content Quality Audit

**Covered well in source:** core definition, random assignment logic, treatment/control, blinding, statistical power, business use cases (e-commerce, banking, pharma, logistics).

**Underplayed / missing:**
- Cluster randomisation + ICC / design effect math.
- Pre-registration and alpha-spending / sequential testing.
- MDE rigor (business-relevant vs detectable).
- CATE / LATE and treatment-effect heterogeneity.
- Bayesian experimentation (priors, credible intervals, expected loss).
- Experiment-culture governance (registry, peer review, SRM checks).
- CUPED and variance-reduction techniques.
- Guardrail metrics and multi-metric trade-offs.

**Supplementary sources (≥5):**
1. Kohavi, Tang, Xu — *Trustworthy Online Controlled Experiments* (2020).
2. Angrist & Pischke — *Mostly Harmless Econometrics* (2008).
3. Duflo, Glennerster, Kremer — *Using Randomization in Development Economics Research: A Toolkit* (2008).
4. Gerber & Green — *Field Experiments* (2012).
5. Banerjee & Duflo — *Poor Economics* (2011).

**Red flags to watch in deployed RCEs:**
- SRM failure (observed/expected ratio off) → instrumentation bug, invalidates the test.
- Differential attrition between arms → report both ITT and sensitivity bounds.
- Peeking without alpha-spending → inflated false-positive rate.
- Post-hoc subgroup mining → treat as hypothesis-generating, not confirmatory.
- Novelty-driven spikes read as steady-state lift → require minimum run length.

---

## 9. Quick-Recall Card
- RCE = random assignment + control + measured outcome → causal effect, not correlation.
- Pre-register hypothesis, MDE, primary metric, and stop rule before launch.
- ITT is the default readout; disclose compliance and run LATE as secondary.
- Size for business-relevant MDE with 80% power and 5% alpha; adjust for clusters.
- Validate with SRM, attrition checks, and guardrail metrics — not just the primary p-value.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Does shipping this change cause a business-meaningful lift versus control — with a confidence level and effect size I am willing to stake budget on?"

---

**Connects to:** [01-causation-vs-correlation.md](01-causation-vs-correlation.md), [03-ab-testing-business.md](03-ab-testing-business.md), [../six-sigma/06-improve-phase.md](../six-sigma/06-improve-phase.md), [../product-management-npd/13-product-analytics-data-driven.md](../product-management-npd/13-product-analytics-data-driven.md), [../business-analytics/](../business-analytics/).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:5, 6:5, 7:4, 8:4, 9:4, 10:4]
Sections rewritten: [1 topic snapshot tightened; 3.3 validity matrix expanded; 4 formulas numeric-example added; 6 anti-example quantified; 9 role-lens question]
Enrichments applied: [cross-course links; 5 supplements; anti-example w/ cost; IT tooling; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A8
-->
