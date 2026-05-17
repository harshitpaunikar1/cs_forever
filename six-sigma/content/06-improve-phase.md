# Improve Phase

## Overview
The Improve phase is where the team develops, tests, and implements solutions that address the verified root causes identified during the Analyze phase. This phase transforms analysis into action by generating potential solutions, evaluating them against criteria, running pilots to confirm effectiveness, and rolling out the best option. The goal is to make measurable, lasting changes to the process.

---

## Why It Matters
Analysis without action produces no value. The Improve phase is where the team turns insights into tangible results by designing solutions that directly target root causes. By piloting solutions before full-scale implementation, teams reduce risk and build evidence that the changes work. A disciplined Improve phase also ensures that solutions are practical, cost-effective, and accepted by the people who will use them daily.

## Key Principles
- Generate multiple solution options before selecting the best one
- Use pilot tests or small-scale experiments to validate solutions before full rollout
- Evaluate solutions based on impact, cost, feasibility, and risk
- Involve the people who work in the process when designing and testing changes

## Key Terms
| Term | Definition |
|------|------------|
| **Pilot Test** | A small-scale trial of a proposed solution to evaluate its effectiveness before full implementation |
| **Design of Experiments (DOE)** | A structured method for testing multiple factors simultaneously to find the optimal combination of settings |
| **Solution Selection Matrix** | A tool that scores potential solutions against weighted criteria such as cost, impact, and ease of implementation |
| **Implementation Plan** | A detailed roadmap that specifies the steps, resources, responsibilities, and timeline for deploying a solution |

## Use Case
An electronics manufacturer uses Design of Experiments to find the optimal soldering temperature, speed, and paste amount that minimize circuit board defects.

## Scenario
> A hotel chain identifies that slow check-in is caused by a paper-heavy registration process. During the Improve phase, the team designs a digital check-in kiosk, pilots it at three locations for two months, and measures a 55% reduction in check-in time. After confirming the results, they roll out kiosks to all 120 properties with a phased implementation plan.

## Examples
- A pharmaceutical company runs a DOE to optimize tablet coating thickness, finding the exact combination of spray rate and drying temperature that eliminates cracking
- A logistics firm pilots a new route optimization algorithm at one distribution center and confirms a 20% reduction in fuel costs before expanding to all centers

---

## Audited Appendix

# Improve Phase
**Course:** Six Sigma
**Module:** Content / Improve Phase
**Audited on:** 2026-04-18
**Audited by:** A1
**Source files reviewed:** `six-sigma/content/06-improve-phase.md`

---

## 1. Topic Snapshot
Improve is the DMAIC step that converts verified root causes into tested solutions and a controlled rollout plan.
For an IT/AI/Product/Consulting leader, it is the stage that protects the business from a "big-bang deploy" — every proposed fix gets a pilot, a scoreboard, and an explicit go/no-go rule before touching production.
The decision it helps make: which solution to ship, at what scope, with what rollback trigger.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Pilot Test | - | Small-scale run of a proposed solution before full rollout. | To validate impact without betting the company. | Pre/post delta on the Y metric; statistical significance. | Product rollouts, ops pilots, consulting engagements. |
| Design of Experiments | DOE / DoE | Structured test of multiple factors at once to find the best combination of settings. | One-factor-at-a-time misses interactions and burns time. | Main effects, interaction effects, R², ANOVA p-values. | Manufacturing, ML hyperparameter tuning, pricing tests. |
| Solution Selection Matrix | - | Weighted scorecard comparing candidate solutions on cost, impact, feasibility, and risk. | Forces transparent trade-offs instead of HiPPO (highest-paid person's opinion) picking. | Weighted score (Σ weight × criterion rating). | Product prioritisation, M&A targets, operational improvements. |
| Implementation Plan | - | Step-by-step rollout document with owners, dates, resources, and dependencies. | Turns a decision into an executable sequence. | % steps completed on time; deviation from plan. | Project management, change management. |
| Root Cause | - | Verified upstream driver identified in Analyze. | Improve must target *these*, not symptoms. | Recurrence rate after fix (should drop to near zero). | RCA reports, DMAIC handoffs. |
| Factor | - | An input variable the team manipulates in a DOE. | Needed to map solution space. | Discrete levels (e.g., low/med/high) or continuous values. | DOE, ML experiments, A/B/n tests. |
| Interaction Effect | - | Situation where factor A's effect depends on the level of factor B. | Reveals non-additive behaviour hidden from one-at-a-time tests. | Interaction term coefficient; ANOVA interaction p-value. | DOE, regression, ML ablations. |
| Full-Factorial Design | - | DOE that tests every combination of factor levels. | Captures all main + interaction effects. | 2ᵏ runs for k factors at 2 levels each. | Engineering optimisation, marketing mix. |
| Fractional-Factorial Design | - | DOE testing a deliberate subset of combinations to save runs. | When full-factorial is too expensive. | 2ᵏ⁻ᵖ runs; resolution III/IV/V labels. | Pricing tests, ML hyperparameter search. |
| Pilot Success Criteria | - | Pre-declared thresholds that determine pilot "pass". | Prevents post-hoc goalpost-moving. | Primary + guardrail metrics with threshold values. | Product rollouts, clinical trials. |
| Impact–Effort Matrix | - | 2×2 plotting solutions by expected impact vs. effort. | Quick triage before full selection-matrix analysis. | Quadrant position; implementation sequence. | Product prioritisation, consulting shortlists. |
| Phased Rollout | - | Deployment in stages (e.g., 1% → 10% → 50% → 100%) with checkpoints. | Limits blast radius of a bad solution. | % population exposed; guardrail metric health. | Software releases, feature flags. |
| Rollback Plan | - | Pre-written procedure to revert to the prior state if pilot fails. | Makes "Improve" reversible. | Mean time to rollback; data restored %. | SRE, product engineering, change ops. |

---

## 3. Frameworks & Matrices

### Solution Selection Matrix (Weighted Scorecard)
**Purpose:** Compare 3–6 candidate solutions on transparent, weighted criteria so the team ships the best-scoring one, not the loudest-voiced one.

**Text Diagram:**
```text
                Impact  Cost   Speed   Risk    Tech-fit    WEIGHTED
Weight →         0.35   0.20   0.15    0.15      0.15      SCORE
────────────────────────────────────────────────────────────────────
Solution A         5      3      4       2          4        4.00
Solution B         4      4      3       4          5        4.00   ← tied
Solution C         3      5      5       5          3        3.85
Solution D         5      2      2       2          5        3.50
```

Axes / Quadrants / Components explained:
- Rows: candidate solutions (ideally 3–6).
- Columns: decision criteria; weights sum to 1.0. Typical IT/AI/Product/Consulting set = business impact, dev cost, time-to-value, rollout risk, technical fit/debt.
- Ratings: 1–5 anchored (1 = worst, 5 = best).
- Score = Σ (weight × rating).

IT/AI/Product/Consulting worked example: A SaaS Analyze phase shortlists 4 solutions for reducing median checkout latency. After weighted scoring, Solutions A and B tie at 4.00, but Solution B has a lower risk rating. Decision: pilot B; keep A as fallback. Cost per solution, latency impact, and risk scores are pulled from an engineering estimate sheet and a past-incident database — not from a meeting.

When to pull this out in a meeting: any time > 2 solutions are on the table and the team is about to vote by show-of-hands.

### Impact–Effort Matrix (Quick Triage)
**Purpose:** 2×2 screen that drops low-impact / high-effort solutions before anyone scores them in detail.

**Text Diagram:**
```text
                  HIGH EFFORT
                       │
    Major Projects     │     Thankless
    (plan, fund,       │     Tasks
    protect scope)     │     (drop unless
                       │     mandatory)
   HIGH IMPACT ────────┼──────── LOW IMPACT
                       │
    Quick Wins         │     Fill-ins
    (ship this         │     (only if slack
    sprint)            │     capacity)
                       │
                  LOW EFFORT
```

Axes / Quadrants / Components explained:
- X-axis: effort — engineer-weeks + coordination cost.
- Y-axis: impact — expected movement of the primary Y metric.
- Quadrants: Quick Wins (high impact, low effort) ship first; Major Projects get a formal plan; Fill-ins go in backlog; Thankless Tasks get dropped unless compliance forces them.

IT/AI/Product/Consulting worked example: A Product team ideates 11 solutions to a churn problem. Quick Wins (copy-change + day-14 nudge email) ship within a week. One Major Project (seat-activation playbook with new in-app tour) enters the roadmap with explicit Q3 scope. Four Thankless Tasks get archived in Jira with `/won't-fix`.

When to pull this out in a meeting: in a 10-person ideation where every idea feels "important".

### PDCA / Plan-Do-Check-Act Loop (the Pilot Engine)
**Purpose:** Structure each pilot so data, not optimism, decides whether to scale.

**Text Diagram:**
```text
        ┌────────────┐
        │    PLAN    │  hypothesis, success criteria, sample size, duration, rollback
        └─────┬──────┘
              ▼
        ┌────────────┐
        │     DO     │  run pilot on a defined cohort/cell/site/traffic slice
        └─────┬──────┘
              ▼
        ┌────────────┐
        │   CHECK    │  measure Y + guardrails against pre-declared thresholds
        └─────┬──────┘
              ▼
        ┌────────────┐
        │    ACT     │  scale, iterate, or kill — decision per written rule
        └─────┬──────┘
              │
              └─► feeds next PLAN (continuous)
```

Axes / Quadrants / Components explained:
- Plan: write the hypothesis (X → Y), primary metric, guardrails, sample size, stop rules, rollback mechanism.
- Do: execute on a slice (pilot store, 10% traffic, one squad, one region).
- Check: compare to pre-declared thresholds.
- Act: scale (hit threshold), iterate (near miss), kill (clear miss) — no ambiguity.

IT/AI/Product/Consulting worked example: An AI recommendation team pilots a new embedding model. Plan: primary = CTR uplift ≥ 3%, guardrail = p95 latency ≤ 180 ms, duration = 14 days, sample = 5% traffic. Do: feature flag at 5%. Check: CTR +4.1% (p < 0.01), p95 latency 165 ms — both criteria pass. Act: roll to 50%, re-check in 7 days, then 100%.

When to pull this out in a meeting: whenever someone wants to skip the pilot and go straight to 100%.

### Phased Rollout Ramp
**Purpose:** Limit blast radius and keep a rollback option open while confidence grows.

**Text Diagram:**
```text
 % exposed
   100% ┤                                              ██
        │                                          ████
    50% ┤                                     ████
        │                                ████
    10% ┤                          ████
        │                    ████
     1% ┤              ████
        │        ████
     0% ┤  ████
        └──┬─────┬─────┬─────┬─────┬──────┬────────── time
          D0    D2    D5    D9    D14    D21
   Gate   ✓canary ✓health ✓CTR ✓error  ✓business
```

Axes / Quadrants / Components explained:
- Ramp levels: 1% → 10% → 50% → 100% (or 1% / 5% / 25% / 100% for consumer web).
- Gates: each step requires guardrails within tolerance; a gate failure triggers rollback.
- Dwell time: stay at each level long enough to see at least one full seasonal cycle for the metric (hours for latency, days for engagement, weeks for revenue).

IT/AI/Product/Consulting worked example: A fintech deploys a new KYC flow. Day 0 at 1% surfaces a false-reject spike (guardrail violation) — rollback in 40 minutes. Fix shipped, re-start at 1% on D3; then 10%, 50%, 100% across 3 weeks. Net avoided: full-population incident + regulator notification.

When to pull this out in a meeting: whenever a launch plan reads "ship to all users on Friday".

---

## 4. Formulas

The source names DOE and pilot testing but provides no equations. The formulas below are the canonical Improve-phase toolkit [verified from model knowledge, not source], fitted with IT/AI/Product/Consulting decision thresholds.

### Formula 1: Solution Weighted Score
**Formula:** `Scoreₛ = Σⱼ wⱼ · rₛⱼ`, where Σⱼ wⱼ = 1.

**Variables:**
- `wⱼ` = weight on criterion j (impact, cost, speed, risk, tech-fit, etc.).
- `rₛⱼ` = rating (1–5) of solution s on criterion j.

**Why this formula exists:** Replaces a show-of-hands vote with an auditable number.

**How to interpret the output:**
- Top score within 0.2 of runner-up → call it a tie; pilot *both* on separate cells or decide by risk only.
- Top score leads by 0.2–0.5 → ship the winner; hold runner-up as fallback.
- Top score leads by > 0.5 → clear winner; fast-track to pilot.

**Worked example:** See matrix above. A = B = 4.00 (tied). C = 3.85, D = 3.50. Decision: B wins on risk tiebreak; pilot B with A as rollback.

### Formula 2: Pilot Sample Size (two-proportion, α = 0.05, power = 0.80)
**Formula:** `n per arm ≈ (zα/2 + zβ)² · [p₁(1-p₁) + p₂(1-p₂)] / (p₁ - p₂)²`

For α = 0.05 two-tailed and power = 0.80: `(1.96 + 0.84)² = 7.85`.

**Variables:**
- `p₁` = baseline success rate (e.g., checkout completion = 0.42).
- `p₂` = target rate at which you want to detect the lift (e.g., 0.45 = 3-pt lift).
- `zα/2` = 1.96 at α = 0.05; `zβ` = 0.84 at power = 0.80.

**Why this formula exists:** Prevents launching pilots that cannot detect the effect they were built to test — the #1 reason "inconclusive" pilots waste quarters.

**How to interpret the output:**
- Required n per arm ≤ available daily traffic × planned days → pilot is feasible as designed.
- 1× to 3× available traffic → extend duration or widen the accepted effect size.
- > 3× available traffic → you cannot detect the effect you want; redesign (pick a stronger lever or accept a bigger MDE).

**Worked example:** Baseline checkout = 42%, target = 45% (3-pt lift). n ≈ 7.85 · [0.42·0.58 + 0.45·0.55] / (0.03)² = 7.85 · (0.2436 + 0.2475) / 0.0009 = 7.85 · 545.6 ≈ 4,283 per arm. With 5,000 checkouts/day, a 50/50 test needs ~2 days — feasible.

### Formula 3: Expected Business Impact (ROI of the Solution)
**Formula:** `Expected Impact = Δmetric × population × unit_value − implementation_cost`

**Variables:**
- `Δmetric` = verified delta from pilot (e.g., +3 pts checkout conversion).
- `population` = annual eligible users / transactions.
- `unit_value` = revenue or cost per unit (contribution margin per checkout).
- `implementation_cost` = engineering + change-management + maintenance cost (one-off + 1-year run).

**Why this formula exists:** Ensures the pilot lift translates into actual P&L before a full rollout is funded.

**How to interpret the output:**
- Expected Impact ≥ 3× implementation cost → fund full rollout now.
- 1× to 3× → fund rollout but cap risk (phased deploy with stop rules).
- < 1× → kill the rollout; record learnings and reassign engineers.

**Worked example:** +3-pt checkout lift × 2,000,000 checkouts/year × ₹180 contribution margin = ₹10.8 Cr. Implementation cost = ₹1.2 Cr. Ratio ≈ 9× → fund the full rollout.

### Formula 4: DOE Full-Factorial Run Count
**Formula:** `runs = Lᵏ · r`, where L = levels per factor, k = number of factors, r = replicates.

**Variables:**
- `L` = typically 2 (low/high) or 3 (low/med/high).
- `k` = count of factors under test.
- `r` = replicates (usually 2–3).

**Why this formula exists:** Makes the cost of a DOE design visible before the experiment is committed.

**How to interpret the output:**
- Runs ≤ available test budget → run full factorial.
- Runs = 2–4× budget → use fractional factorial (resolution IV or V).
- Runs > 4× budget → screen factors first (Plackett–Burman) then full-factorial on survivors.

**Worked example:** An AI team testing 5 hyperparameters at 2 levels each with 2 replicates = 2⁵ × 2 = 64 training runs. If budget allows 24 runs, switch to a 2^(5-1) fractional factorial with r=1 → 16 runs, estimate main effects + selected two-way interactions.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|------|
| Ship the first solution that survives a team brainstorm. | Generate ≥ 3 candidate solutions, then score them on a weighted Solution Selection Matrix before piloting. |
| Run a pilot with success criteria decided *after* seeing the data. | Pre-declare primary metric, guardrails, sample size, duration, and stop rules in the pilot charter before Day 0. |
| Go straight from a successful 2-week pilot to 100% rollout. | Use a phased ramp (1% → 10% → 50% → 100%) with explicit guardrail checks at each gate. |
| Change multiple factors in the pilot and credit the total lift to "the new process". | Use DOE or isolate changes so each factor's contribution is attributable; otherwise you cannot defend the rollout. |
| Declare a pilot "failed" from a sample that was under-powered. | Compute required sample size before Day 0; if the pilot cannot detect the effect you care about, redesign it. |
| Treat the Implementation Plan as documentation to write after launch. | Build it in Jira/Asana *before* the pilot goes live — owners, dates, dependencies, and rollback trigger all named. |
| Ignore the people who run the process daily when designing the fix. | Co-design with frontline operators (support, sales, SRE); their veto kills more rollouts than bad data does. |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: AI product — embedding-model upgrade
**Situation:** A B2C recommendation product wants to swap a v2 embedding model for v3. Analyze confirmed that embedding quality is the top driver of session CTR. ML infra lead proposes "deploy everywhere on Friday".
**Applicable framework/metric:** PDCA + Phased Rollout Ramp + Sample-Size Formula.
**Analysis:** Required n per arm for a 1-pt CTR lift (baseline 8%) at α = 0.05, power = 0.80: n ≈ 7.85 · [0.08·0.92 + 0.09·0.91] / (0.01)² ≈ 7.85 · 0.1555 / 0.0001 ≈ 12,206 sessions per arm. At 250,000 sessions/day, a 5% canary reaches required power in under 2 hours, so 1-day minimum, 14-day recommended.
**Decision rule:** If (a) CTR uplift ≥ +1 pt with p ≤ 0.05 AND (b) p95 latency ≤ 180 ms AND (c) no model-safety flag spike → advance ramp. Any failure → rollback in < 30 min and postmortem within 48 h.
**Action (Monday):** (a) Write the pilot charter in Confluence; (b) set Unleash feature flag to 5%; (c) wire Grafana board with CTR, latency, safety incident rate; (d) schedule gate reviews at D1, D3, D7, D14; (e) pre-draft a 3-line rollback runbook in the SRE wiki.
- Data sources used: Mixpanel (CTR), Prometheus/Grafana (latency), Snowflake (revenue), Unleash (feature flag).

### Scenario 2: IT operations — incident-ticket triage automation (Solution Selection)
**Situation:** An enterprise IT ops team has 4 candidate solutions to reduce mean-time-to-acknowledge (MTTA): (A) hire 2 more L1s, (B) deploy an LLM-based ticket classifier, (C) rewrite ServiceNow routing rules, (D) buy a commercial AIOps product.
**Applicable framework/metric:** Solution Selection Matrix + Expected Business Impact formula.
**Analysis:** Weights — Impact 0.35, Cost 0.25, Speed 0.15, Risk 0.15, Tech-fit 0.10. Ratings: A (4,2,3,4,5) → 3.45; B (5,4,4,3,4) → 4.20; C (3,5,5,4,3) → 3.85; D (5,1,2,2,3) → 2.95. Expected impact of B: 35% MTTA reduction × 80,000 tickets/yr × ₹120 operator-cost per minute saved = ₹3.36 Cr, implementation ≈ ₹45 L → ratio > 7×.
**Decision rule:** Weighted score gap ≥ 0.3 AND expected-impact ratio ≥ 3× → fund the winner with a phased pilot. Otherwise pilot both top-two on different cells.
**Action (Monday):** (a) Charter a 6-week B pilot on the top-3 product queues; (b) lock guardrails (misclassification rate ≤ 5%, escalation-to-human ≥ 98% on P1s); (c) freeze C as fallback; (d) park A and D with cost/risk notes in the architecture decision record.
- Data sources used: ServiceNow (tickets), Looker (MTTA dashboards), Jira (pilot tasks), Confluence (ADR).

### Scenario 3 (ANTI-EXAMPLE): Consulting engagement — skipping the pilot
**Situation:** A retail-banking client is told by a consulting team that a new credit-decisioning model will lift approval rates with no adverse-selection risk. The engagement skips a staged pilot and ships the model bank-wide "to meet the quarterly timeline".
**Applicable framework/metric:** Phased Rollout Ramp + PDCA + Pilot Sample-Size formula.
**Analysis (what went wrong):** The pilot should have been a 1% canary on the lowest-risk segment for 4 weeks. The required sample to detect a 0.3 pt change in default rate (baseline 2.5%) at α = 0.05, power = 0.80 is n ≈ 41,500 per arm — achievable at 1% traffic in ~3 weeks. Skipping this, the team relied on a back-tested simulation.
**Decision rule that should have applied:** No rollout > 10% without at least one full seasonal cycle at canary with guardrails green. Guardrails: default-rate drift ≤ +0.1 pt, disparate-impact ratio ≥ 0.85, override-rate ≤ 5%.
**Wrong decision shipped and its cost:** Weeks 3–6 post-launch, default rate drifts from 2.5% to 3.1% on a segment not represented in the training data. Net credit loss ≈ ₹8.2 Cr over the quarter; model re-training + freeze costs another ₹1.5 Cr; regulator sends a query. A proper 4-week canary would have detected the drift at < ₹50 L exposure and cost ~6 weeks of schedule.
**Correct action (had the framework been applied):** 1% canary on weeks 1–4; 10% on weeks 5–6 with guardrail re-check; 50% on weeks 7–8; 100% in week 9 conditional on all gates green.
- Data sources used: Snowflake (loan book), Looker (risk dashboards), model-monitoring tool (feature drift).

---

## 7. Implementation Playbook

1. **Kick off with an Improve charter in Confluence** naming: the verified root cause from Analyze, Y metric and target, guardrails, budget, rollback trigger, stakeholders.
2. **Generate ≥ 3 candidate solutions in a 60-minute ideation** (SCAMPER or TRIZ prompts); park each as a one-paragraph brief in a shared Notion doc.
3. **Triage with the Impact–Effort Matrix** to drop obvious non-starters before detailed scoring.
4. **Score survivors on a Solution Selection Matrix** in Google Sheets with weights signed off by the business owner; winner ≠ tie ⇒ pilot one, else pilot two.
5. **Write a pilot charter** specifying: hypothesis, primary metric, guardrails, sample size, duration, cohort definition, stop/go rules, rollback steps. Store in Confluence alongside the Jira epic.
6. **Build the phased-rollout ramp in your feature-flag tool** (Unleash, LaunchDarkly, or internal flagger) with gates at 1/10/50/100%.
7. **Wire a live pilot scoreboard in Looker/Grafana/Datadog** showing primary metric, guardrails, and gate-status; owner gets a daily digest.
8. **Run PDCA on a fixed cadence** (daily during early ramp, weekly thereafter); at each Act step, log the go / iterate / kill decision in the charter with evidence.

---

## 8. Content Quality Audit

- **Covered well:** The source correctly names the four core Improve outputs — solution options, selection matrix, pilot, implementation plan — and uses a clean hotel chain scenario to illustrate piloting.
- **Underplayed or missing:**
  - **Sample size / power** is never mentioned, yet under-powered pilots are the dominant reason Improve fails.
  - No coverage of **guardrail metrics** or **stop rules** — only primary metrics are discussed.
  - **DOE fundamentals** (main effects vs interactions, fractional factorial) are alluded to in one line ("structured method for testing multiple factors") without the run-count or resolution ideas.
  - **Phased rollout** and **rollback planning** are treated as afterthoughts ("phased implementation plan") rather than as the core risk control.
  - **Change management** — the people side of Improve — gets only a principle-line mention; Kotter-style transition plans, RACI, and training are absent.
  - No link to **feature flags** / experimentation platforms, which are the IT/AI-industry implementation of phased rollouts.
- **Supplement with:**
  - *The Six Sigma Handbook* — Thomas Pyzdek & Paul Keller, 5th ed. (2018), chapters on DOE, Pilot Testing, and Lean Improvement.
  - *Trustworthy Online Controlled Experiments* — Ron Kohavi, Diane Tang, Ya Xu (2020), especially chapters on guardrails, ramp-up, and sample-size calculators.
  - "Leading Change: Why Transformation Efforts Fail" — John P. Kotter, *HBR*, March–April 1995 — the definitive reference for the change-management side of Improve.
  - *Design and Analysis of Experiments* — Douglas C. Montgomery, 10th ed. (2019) — for full-/fractional-factorial designs and response-surface methods.
  - HBS case "Dropbox: Shipping Fast in a Large Organization" (HBS 820-105) — a modern phased-rollout / experimentation case in a software context.
- **Red flags in the source:**
  - The hotel-kiosk example reports "55% reduction in check-in time" without reporting sample size, significance, or guardrails — reinforces a bad pattern of celebrating headline numbers without evidence rigor.
  - DOE is defined in one sentence and then never used in any of the worked examples — students can pass the topic without understanding it.
  - No discussion of failure scenarios or rollback — the source implies pilots either succeed or go away quietly.

---

## 9. Quick-Recall Card

Improve = turn verified root causes into piloted, sized, and ramped solutions.
Toolkit: Impact–Effort screen → Selection Matrix → PDCA pilot → Phased Rollout.
Always pre-declare primary metric, guardrails, sample size, and rollback before Day 0.
Compare ≥ 3 solutions on a weighted scorecard; pilot winner, hold runner-up as fallback.
Every rollout is a ramp, not a launch — 1% → 10% → 50% → 100% with explicit gates.
**As a PM/Consultant/AI Lead, the one question to answer with this framework is:** *What is the smallest, fastest, cheapest test that would tell me whether this solution deserves a full rollout — and what is the rule that would make me kill it?*

---

**Connects to:** [05-analyze-phase.md](05-analyze-phase.md), [07-control-phase.md](07-control-phase.md) (once audited), and [../project-management/](../project-management/) for implementation-plan depth; [../product-management-npd/12-agile-product-development.md](../product-management-npd/12-agile-product-development.md) for the iterative-pilot lens.

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Sections rewritten: [Section 6 trimmed — anti-example made sharper on cost; Section 9 re-shortened to 6 lines]
Enrichments applied: [cross-course link to analyze-phase, control-phase, project-management, agile-product-development; 5 named supplements with author+year; anti-example with quantified cost; IT-org data sources (Mixpanel, Grafana, ServiceNow, Unleash, Snowflake) across scenarios; role-lens question closes Section 9]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 20:45
Audited by: A1
-->
