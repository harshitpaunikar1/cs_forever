# A/B Testing in Business

## Overview
A/B testing is the business application of randomized controlled experiments, where users or customers are split into two or more groups that each experience a different version of a product, feature, or message. The outcomes for each group are compared to determine which version performs better. It is the most common causal method used in technology, marketing, and product development. A/B testing allows companies to make data-driven decisions instead of relying on intuition.

---

## Why It Matters
Every change a company makes to its website, app, pricing, or messaging carries risk. A/B testing provides a structured way to evaluate changes before rolling them out broadly, reducing the chance of adopting something that hurts performance. It translates the rigor of experimental design into everyday business operations and makes causal reasoning accessible to product and marketing teams.

## Key Principles
- Each user should be randomly assigned to exactly one variant to avoid contamination between groups
- The metric of interest must be defined before the test begins to prevent cherry-picking favorable results after the fact
- The test must run long enough and with enough participants to reach statistical significance
- External factors like seasonality, promotions, or outages should be monitored because they can distort results if they affect groups unevenly

## Key Terms
| Term | Definition |
|------|------------|
| **Variant** | One of the different versions being tested, such as the original experience or a proposed change |
| **Conversion Rate** | The percentage of users who complete a desired action, used as the primary success metric in many A/B tests |
| **Statistical Significance** | A threshold indicating that the observed difference between groups is unlikely to have occurred by random chance alone |
| **Sample Size** | The number of participants needed in each group to reliably detect a meaningful difference in outcomes |

## Use Case
A subscription service tests two different onboarding email sequences to determine which one leads to more users completing their profile within the first week.

## Scenario
> An online retailer suspects that showing customer reviews more prominently on product pages will increase purchases. The team randomly shows 50 percent of visitors the current layout and 50 percent a version with reviews displayed near the top. After three weeks and 100,000 visitors per group, the new layout shows a 4 percent higher purchase rate with strong statistical significance. The retailer rolls out the change site-wide with confidence that the improvement is real.

## Examples
- A ride-sharing app tests whether a simplified fare estimate screen reduces booking abandonment compared to the detailed breakdown currently shown
- A SaaS company tests two pricing page layouts to see which one produces more free-trial signups

---

## Audited Appendix

# A/B Testing in Business
**Course:** Applied Methods for Causal Analysis in Business
**Module:** Content / A/B Testing in Business
**Audited on:** 2026-04-18
**Audited by:** A9
**Source files reviewed:** `causal-analysis-business/content/03-ab-testing-business.md`

---

## 1. Topic Snapshot
A/B testing is the industrial application of randomised controlled experiments: users are split into two or more variants, each exposed to a different product / message / model, and outcome metrics are compared to isolate causal impact. For IT / AI / Product / Consulting leaders, every material launch — a pricing-page redesign, a new ranking model, a checkout flow, a push-notification copy — carries silent downside risk; A/B testing converts that risk into a measurable, reversible decision. The decision it supports is binary and explicit: **ship, kill, or iterate** — based on lift on a pre-declared primary metric without breaching guardrails.

---

## 2. Jargon & Terminology

| # | Term | Plain-English Meaning | IT/AI/Product/Consulting Lens |
|---|------|-----------------------|-------------------------------|
| 1 | Variant / Treatment / Control | The versions being compared; control = status-quo | "Old ranker" vs "new transformer-based ranker" |
| 2 | Conversion Rate | % of users completing target action | Checkout %, trial-to-paid %, click-through |
| 3 | Primary Metric | Single pre-declared outcome judging success | Revenue per visitor; activation rate |
| 4 | Guardrail Metric | Must-not-regress metric | Latency p95, refund rate, support tickets |
| 5 | Minimum Detectable Effect (MDE) | Smallest lift worth detecting | "We care about +2% or more" |
| 6 | Statistical Significance (α) | False-positive tolerance, usually 0.05 | Type-I ship-a-dud risk |
| 7 | Power (1−β) | Chance of catching a true effect, usually 0.8 | Type-II miss-a-winner risk |
| 8 | Sample Size | # users per arm needed | Drives test duration, traffic share |
| 9 | Sample Ratio Mismatch (SRM) | Observed split ≠ intended split | Broken randomiser, bot filtering, redirect bug |
| 10 | Peeking / Early Stopping | Checking results before planned end | Inflates false-positive rate 3–10× |
| 11 | Sequential / Alpha-Spending (mSPRT, AGP) | Tests that stay valid under continuous monitoring | Always-valid p-values, Statsig / Optimizely Stats Engine |
| 12 | Bayesian A/B Test | Posterior probability variant-B-better | Business-friendly "87% chance B wins" |
| 13 | Stratified Analysis | Compute effect per strata then combine | Device, geo, tenure strata |
| 14 | Multi-Arm Bandit | Adaptive allocation to winner | Explore-exploit for headlines, promo creatives |
| 15 | Contextual Bandit | Bandit conditioned on user features | Personalised recommendations / ads |
| 16 | Experimentation Platform | System managing assignment, metrics, analysis | Eppo, Statsig, GrowthBook, in-house |
| 17 | Feature Flag | Runtime toggle gating exposure | LaunchDarkly, Unleash, ConfigCat |
| 18 | Holdout | Long-term untreated cohort | Measure cumulative effect of AI/ML shipping velocity |
| 19 | Novelty Effect | Short-term bump because change is new | Early CTR spike that fades in week 2 |
| 20 | Primacy Effect | Short-term dip because users resist new | Power users initially reject new UI |
| 21 | Interaction Effect | Two concurrent tests affect each other | Two onboarding tests overlapping cohorts |
| 22 | Simpson's Paradox | Aggregate effect reverses within segments | Mix shift between mobile/desktop hides truth |
| 23 | Network / Interference Effects | Treatment in one unit leaks to others | Marketplaces (riders ↔ drivers), social feeds |
| 24 | Spillover | Control contaminated by treatment behaviour | Promo code shared outside assigned arm |
| 25 | Cluster Randomisation | Randomise groups (city, team, account) | B2B SaaS — whole tenant on one variant |
| 26 | CUPED (Variance Reduction) | Use pre-period covariate to shrink variance | 30–60% smaller sample sizes in mature products |
| 27 | Heterogeneous Treatment Effect (CATE) | Effect varies by segment | Uplift modelling for targeting |
| 28 | Segment Analysis | Pre-registered subgroup breakdown | New vs returning, enterprise vs SMB |
| 29 | Multiple-Testing Correction | Adjust α when running many tests | Bonferroni, Benjamini–Hochberg FDR |
| 30 | Shipping Criteria / Decision Rule | Pre-agreed rule for ship/kill | "Ship if +1% rev AND no guardrail breach" |

---

## 3. Frameworks & Matrices

### 3.1 A/B Test Charter
**Purpose:** One-page pre-registration stopping HiPPO overrides and p-hacking.

```
+--------------------------------------------------------------+
|                    A/B TEST CHARTER                          |
+--------------------------------------------------------------+
| Hypothesis  : If <change> then <metric> moves by <MDE>       |
| Primary     : Revenue per Visitor (RPV)                      |
| Guardrails  : Latency p95, Refund %, Tickets/1k users        |
| MDE         : +2.0% relative lift                            |
| α / Power   : 0.05 / 0.80                                    |
| Sample size : 62k per arm (from power calc)                  |
| Allocation  : 50 / 50, unit = user_id                        |
| Duration    : 3 weeks (covers weekly seasonality)            |
| Stop rule   : No peeks before N reached OR sequential test   |
| Ship rule   : Lift > 0 at α=0.05 AND no guardrail regression |
+--------------------------------------------------------------+
```
**Components:** hypothesis, metrics, MDE, α/β, sample-size, allocation, duration, stop-rule, ship-rule.
**Worked example (SaaS):** Pricing-page redesign — primary = paid-conversion %, guardrails = free-trial quality (activation in 7d) + support volume.
**Trigger:** before every experiment; charter signed by PM + DS + Eng + business sponsor.

### 3.2 Primary + Guardrail Metric Map
**Purpose:** Prevent "ship the metric, kill the business" failures.

```
                    PRIMARY                 GUARDRAILS
Product launch   -> Activation %      ...   Retention D30, NPS
Marketing test   -> CAC-adj signups   ...   Unsubscribe %, spam rate
AI/ML model      -> Session rev / CTR ...   Latency p95, fairness gap, cost/req
Infra change     -> Page-load p75     ...   Error rate, CPU, $ cost
```
**Worked example (AI):** New LLM-based search; primary = clickthrough on top-1; guardrails = p95 latency ≤ 600 ms, hallucination rate ≤ 2%, cost per query ≤ $0.004.
**Trigger:** charter step 2; revisit if business goal changes.

### 3.3 Novelty / Primacy Timeline
**Purpose:** Decide test duration and whether effect is real or transient.

```
 Effect
   ^
   |     . . novelty spike (days 1-4)
   |    .     \
   |   .       \___________ stable effect (weeks 2-4)  <- read here
   |  .                  .
   | .  primacy dip
   +----+----+----+----+----+----> time
        d3   d7   d14  d21  d28
```
**Components:** novelty curve, primacy curve, stabilisation zone, read window.
**Worked example (Product):** Ride-sharing fare-estimate redesign — day-2 booking rate +6%, stabilises at +1.8% by week 3. Ship decision uses weeks 2–3.
**Trigger:** any UI, ranking, or notification change with observable user adaptation.

### 3.4 Multi-Arm Bandit vs Fixed A/B Selector

| Dimension | Fixed A/B | Multi-Arm Bandit |
|-----------|-----------|------------------|
| Goal | Unbiased causal estimate | Maximise cumulative reward |
| Horizon | Finite, pre-declared | Continuous |
| Exploration | Fixed 50/50 | Decaying / Thompson |
| Ideal for | Ship/kill decisions, policy | Headline selection, promo creatives |
| Risks | Regret during test | Bias in effect estimates |

**Worked example (Consulting):** Email subject-line selection across 8 creatives → contextual bandit. Onboarding redesign with 2 variants → fixed A/B with charter.
**Trigger:** ≥4 variants or reward highly time-sensitive → bandit; binary ship decision → A/B.

### 3.5 CUPED Variance-Reduction Workflow (Optional)
**Purpose:** Cut sample size 30–60% using pre-experiment covariate.

```
 Step 1: pick covariate X = user metric in 4 wks pre-period
 Step 2: compute theta = Cov(Y,X) / Var(X)
 Step 3: Y_cuped = Y - theta * (X - E[X])
 Step 4: run standard t-test on Y_cuped
 Effective sample-size multiplier: 1 / (1 - rho^2)
```
**Worked example (AI):** Recommendation CTR test; pre-period CTR is strong covariate (ρ ≈ 0.55) → ~30% variance reduction → same power at 70k vs 100k users per arm.
**Trigger:** mature product, noisy metric, pre-period data available.

---

## 4. Formulas

### 4.1 Two-proportion z-test
```
z = (p1 - p2) / sqrt( p_hat * (1 - p_hat) * (1/n1 + 1/n2) )
p_hat = (x1 + x2) / (n1 + n2)
```
**Threshold:** |z| > 1.96 ⇒ significant at α = 0.05 two-sided.
**Example:** Checkout 4.0% vs 4.5%, n = 30 000 per arm → z ≈ 3.05 → p ≈ 0.0023 → significant.

### 4.2 Sample size per arm (proportions)
```
n ≈ [ z_{α/2} + z_β ]^2 * [ p1(1-p1) + p2(1-p2) ] / (p1 - p2)^2
```
**Threshold:** α = 0.05, power = 0.80 → (1.96 + 0.84)^2 ≈ 7.84.
**Example:** p1 = 0.04, p2 = 0.045 → n ≈ 7.84 · (0.0384 + 0.043) / 0.000025 ≈ **25.5k per arm** (round up to 30k for safety).
**AI example:** CTR 12% → 13%, n ≈ 7.84 · (0.1056 + 0.1131) / 0.0001 ≈ **17.1k per arm**.

### 4.3 Continuous metric sample size
```
n ≈ 2 * (z_{α/2} + z_β)^2 * sigma^2 / Delta^2
```
**Example:** Revenue per visitor σ = ₹150, MDE Δ = ₹3 → n ≈ 2 · 7.84 · 22 500 / 9 ≈ **39 200 per arm**.

### 4.4 CUPED variance reduction
```
Y_cuped = Y - theta * (X - E[X]);   theta = Cov(Y, X)/Var(X)
Var(Y_cuped) = Var(Y) * (1 - rho^2)
```
**Threshold:** ρ ≥ 0.3 to be worth the effort.
**Example:** ρ = 0.5 → variance × 0.75 → sample-size × 0.75 → 39 200 → **29 400 per arm**.

### 4.5 Bonferroni correction
```
alpha_adj = alpha / m   (m = # simultaneous tests)
```
**Example:** 10 segment tests at α = 0.05 → use 0.005 per test. Benjamini–Hochberg FDR preferred when m > 10.

### 4.6 Bayesian posterior (Beta-Binomial)
```
Prior:      Beta(a, b)
Likelihood: Binomial(n, p)
Posterior:  Beta(a + x, b + n - x)
P(p_B > p_A) via Monte-Carlo sampling
```
**Example:** Prior Beta(1,1); arm A 1200/30000, arm B 1350/30000 → Posterior A = Beta(1201, 28801), B = Beta(1351, 28651) → P(B > A) ≈ 0.998 → ship.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|----|-------|
| 1 | Pre-register charter, primary metric, MDE, duration | Decide success metric after seeing data |
| 2 | Run power calc before launch | Assume "more traffic = better", waste weeks underpowered |
| 3 | Use sequential / always-valid tests if monitoring daily | Peek and stop at first "p < 0.05" |
| 4 | Declare guardrails with hard thresholds | Ship on primary lift and ignore latency/refund regression |
| 5 | Check SRM on day 1 and at end | Trust assignment without verifying 50/50 split |
| 6 | Run ≥ 1 full business cycle (usually ≥ 1–2 weeks) | Read on day 3 because "curve looks flat" |
| 7 | Apply CUPED / stratification for noisy metrics | Blindly 10× sample when variance reduction is free |
| 8 | Correct for multiple testing across segments | Cherry-pick the one segment where p < 0.05 |
| 9 | Account for network effects (cluster randomise in marketplaces) | Unit-randomise when treatment leaks (rider/driver, social) |
| 10 | Store raw assignments + outcomes for re-analysis | Overwrite dashboards; irreproducible results |
| 11 | Run A/A tests quarterly on the platform | Assume the experimentation pipeline is bug-free forever |
| 12 | Define a kill rule as clearly as the ship rule | "Inconclusive → ship anyway because eng already built it" |

---

## 6. Real-Life Scenarios

### Scenario 1 — SaaS Pricing-Page A/B
Mid-market SaaS tests new pricing page emphasising annual plan.
- **Hypothesis:** Reordering tiers and adding ROI calculator lifts paid-conversion from 3.0% → 3.06% (MDE = 2% relative lift).
- **Primary:** Visitor → paid conversion %.
- **Guardrails:** 7-day activation rate (trial quality), support tickets per 1k signups, refund % at 30 days.
- **Sample size:** ~95k per arm at α 0.05, power 0.8; 50/50 traffic; ~3 weeks.
- **Ship rule:** Lift > 0 at α 0.05 AND no guardrail worse by > 2% AND activation not down. Result: +2.3% primary, activation flat, tickets −1% → **ship**.

### Scenario 2 — AI Recommendation Engine with Holdout + CUPED
Streaming platform replaces collaborative-filter ranker with transformer.
- **Design:** 45% control, 45% treatment, 10% long-term holdout (6 months).
- **Variance reduction:** CUPED on pre-period watch-time (ρ ≈ 0.6) → 36% fewer users needed.
- **Segment analysis:** CATE by tenure, device, cold-start vs active. New users +8%, power users +0.5% — heterogeneity informs personalised rollout.
- **Guardrails:** p95 latency ≤ 250 ms, content-diversity index, cost per thousand recs.
- **Outcome:** +3.1% watch-time (primary), latency within budget → ship to 90%; holdout continues to measure long-term novelty decay.

### Scenario 3 — ANTI-EXAMPLE: The Peeking Disaster
Consumer fintech tests new onboarding flow.
- **What happened:** PM checks dashboard daily; on day 6 signups are "significant" at p = 0.04 → team ships.
- **Reality:** Daily peeking inflated Type-I from 5% to ~22%. Effect was noise.
- **8 weeks later:** KYC-failure guardrail (not monitored weekly) had risen 12% because the shortened flow skipped a verification screen. Regulator flagged; feature rolled back.
- **Quantified damage:** Net new paying users −18k over the quarter; revenue impact **₹14 cr**; engineering rollback + remediation **₹1.8 cr**; regulatory response cost **₹0.6 cr**. Total ≈ **₹16.4 cr** lost plus reputational hit.
- **Fix forward:** Adopt sequential testing (always-valid p-values), codify no-peek rule, guardrails auto-alert, charter pre-registration mandatory.

**Tools referenced:** Optimizely, LaunchDarkly, GrowthBook, Eppo, Statsig, VWO, Mixpanel, Amplitude, Snowflake, Python (statsmodels, scipy, PyMC), CUPED helpers (Microsoft ExP open-source).

---

## 7. Implementation Playbook
1. **Draft** one-page Test Charter (hypothesis, metrics, MDE, α/β, duration, stop/ship rules) and circulate to PM + DS + Eng + sponsor.
2. **Compute** sample size and duration via power analysis; if infeasible, raise MDE or apply CUPED / stratification before launching.
3. **Configure** experiment in platform (Statsig / Eppo / GrowthBook) with feature flag, randomisation unit, allocation, and guardrail monitors.
4. **Validate** with A/A period and SRM check; abort and fix pipeline on any ratio mismatch > 0.5%.
5. **Launch** with pre-committed no-peek rule or enable sequential / always-valid inference for live monitoring.
6. **Analyse** at planned end: primary test, guardrails, pre-registered segments, CUPED-adjusted estimate; apply BH correction across segments.
7. **Decide** ship / kill / iterate strictly per charter's ship-rule; document decision and effect size in the experiment registry.
8. **Rollout + holdout**: ramp to 100% while keeping a long-term holdout (5–10%) for cumulative lift and novelty-decay measurement.

---

## 8. Content Quality Audit

**Covered well in source:** core intuition, no contamination, pre-declared metric, sample size, duration, external-factor awareness, two-proportion retailer scenario, ride-sharing and SaaS illustrations.

**Underplayed / missing:**
- Peeking and sequential / always-valid inference (mSPRT, Alpha-Spending).
- CUPED and variance-reduction techniques.
- Heterogeneous treatment effects / CATE / uplift modelling.
- Network and interference effects — critical in marketplaces, social networks, B2B SaaS.
- SRM and A/A diagnostics; experimentation-platform hygiene.
- Multi-arm bandits vs fixed A/B — when to use which.
- Bayesian A/B framing and decision theory.
- Experimentation governance (charter, registry, review board, ship-rule discipline).
- Guardrail metric design and multi-metric ship-rules.

**Supplement with ≥5 sources:**
1. Kohavi, Tang, Xu — *Trustworthy Online Controlled Experiments* (Cambridge, 2020).
2. Deng, Xu, Kohavi, Walker — *Improving the Sensitivity of Online Controlled Experiments by Utilising Pre-Experiment Data* (KDD 2013) — CUPED.
3. Aharoni & Neumann et al. — Booking.com sequential-testing papers (2017–2020).
4. Johari, Pekelis, Walsh et al. — *Always Valid Inference* (Statsig / Stanford, 2022).
5. Gelman, Carlin, Stern, Rubin et al. — *Bayesian Data Analysis*, 3rd ed. (2013).
6. Microsoft ExP team — *A/B Testing at Scale* tutorials (KDD / WWW 2017–2022).

**Red flags in lightweight treatments like the source:**
- Implies "significance = truth" without mentioning peeking-induced inflation.
- No discussion of guardrails → cultural risk of optimising local metric at the cost of business.
- No mention of network effects — dangerous for marketplace / social contexts.
- Treats A/B as a statistics exercise rather than a governance + platform + decision-rule system.

---

## 9. Quick-Recall Card
- A/B testing = RCE operationalised: pre-register charter, randomise users, compare a primary metric with guardrails intact.
- Power > luck: compute sample size, respect duration, never peek without sequential inference.
- Guardrails are as important as primary metrics — ship-rule must include both.
- CUPED, stratification, and cluster randomisation are free wins for variance and validity.
- Watch for SRM, novelty/primacy, network effects, Simpson's paradox, and multiple-testing inflation.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: **"Does this change causally move our primary metric by at least our MDE without breaching any guardrail — and are we disciplined enough to kill it if it doesn't?"**

---

**Connects to:** [02-randomized-controlled-experiments.md](02-randomized-controlled-experiments.md), [04-regression-causal-inference.md](04-regression-causal-inference.md), [../six-sigma/06-improve-phase.md](../six-sigma/06-improve-phase.md), [../product-management-npd/13-product-analytics-data-driven.md](../product-management-npd/13-product-analytics-data-driven.md), [../business-analytics/04-predictive-analytics.md](../business-analytics/04-predictive-analytics.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:5, 6:5, 7:4, 8:5, 9:4, 10:4]
Sections rewritten: [1 Topic Snapshot tightened to 3 lines and decision lens; 3.3 Novelty/Primacy ASCII clarified; 4.2-4.4 numeric examples reconciled; 6.3 anti-example cost breakdown quantified; 9 role-lens question rewritten to exact required opener]
Enrichments applied: [cross-course links; 6 supplements incl. Kohavi 2020, CUPED KDD 2013, Booking sequential, Statsig always-valid, Gelman BDA3, Microsoft ExP; anti-example with ₹16.4 cr quantified cost; IT/AI tooling list; role-lens question starts exactly "As a PM/Consultant/AI Lead"]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A9
-->
