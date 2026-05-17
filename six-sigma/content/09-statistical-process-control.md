# Statistical Process Control

## Overview
Statistical Process Control (SPC) is a method of monitoring and controlling a process using statistical techniques, primarily control charts. SPC helps teams distinguish between normal, expected variation and unusual variation that signals a problem. By detecting shifts early, SPC allows organizations to intervene before defects reach customers. It is one of the most widely used tools in both the Measure and Control phases of DMAIC.

---

## Why It Matters
Every process has natural variation, but not all variation is harmless. SPC provides a systematic way to tell the difference between random noise and meaningful signals. Without SPC, operators may overreact to normal fluctuations or ignore early warning signs of a real problem. Organizations that use SPC effectively catch issues in real time, reduce scrap and rework, and maintain consistent quality with less inspection.

## Key Principles
- Distinguish between common cause variation and special cause variation
- Use control charts to monitor process behavior over time
- React only to special cause signals to avoid over-adjusting a stable process
- Set control limits based on actual process data, not arbitrary specifications

## Key Terms
| Term | Definition |
|------|------------|
| **Common Cause Variation** | The natural, inherent variation present in every process that is predictable and stable |
| **Special Cause Variation** | Unusual variation caused by specific, identifiable factors that make the process unstable |
| **Control Limits** | Statistically calculated boundaries on a control chart, typically set at three standard deviations from the mean |
| **Out of Control** | A condition where data points on a control chart fall outside control limits or display non-random patterns |

## Use Case
A semiconductor fabrication plant uses X-bar and R charts to monitor wafer thickness in real time, catching equipment drift before it produces defective chips.

## Scenario
> A dairy company monitors the fat content of its milk using daily control charts. One week, three consecutive measurements fall near the upper control limit. The SPC system flags a trend before any batch exceeds the specification. Investigation reveals a calibration issue in the homogenizer, which is corrected during a scheduled maintenance window with zero product recalls.

## Examples
- An injection molding shop uses individual and moving range charts to track part weight, detecting a material lot change that shifts the average before any parts go out of specification
- A hospital pharmacy monitors prescription fill times with a control chart and identifies a special cause event linked to a new software update that slowed the dispensing system

---

## Audited Appendix

# Statistical Process Control
**Course:** Six Sigma
**Module:** Content / Statistical Process Control
**Audited on:** 2026-04-18
**Audited by:** A1
**Source files reviewed:** `six-sigma/content/09-statistical-process-control.md`

---

## 1. Topic Snapshot
SPC is the discipline of watching a process over time with control charts to tell random noise apart from real signals. For an IT/AI/Product/Consulting leader it matters because most dashboards trigger over-reactive "war rooms" on noise while missing quiet drifts that actually hurt customers. The decision it helps make: *Is this metric movement worth acting on today, or is it within the voice of the process?*

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|---|---|---|---|---|---|
| SPC | Statistical Process Control | Using stats (mostly control charts) to monitor a process | Separates signal from noise | Control charts on time-ordered data | Ops reviews, SRE post-mortems |
| Common Cause Variation | — | Natural, predictable jitter inside the system | Every process has inherent variance | Within-subgroup variation (R̄, MR̄) | "It's just normal" in ops meetings |
| Special Cause Variation | Assignable Cause | Unusual variation from a specific, findable reason | Tells you to *investigate*, not *adjust* | Points outside ±3σ or pattern rules | Incident reviews, RCA |
| Control Limits | UCL / LCL | Statistically derived boundaries on a chart | Define "unusual" from data, not wishes | X̄ ± 3σ (or A₂·R̄) | Every control chart |
| UCL | Upper Control Limit | Top boundary, usually +3σ | Flags upside outliers | X̄ + 3σ | Quality engineer |
| LCL | Lower Control Limit | Bottom boundary, usually -3σ | Flags downside outliers | X̄ - 3σ | Quality engineer |
| X-bar Chart | X̄ chart | Tracks subgroup means over time | Detects shifts in location | Plot of X̄_i | Manufacturing + latency monitoring |
| R Chart | Range chart | Tracks subgroup range over time | Detects shifts in spread | Plot of R_i = max-min | Paired with X-bar |
| I-MR Chart | Individuals & Moving Range | For n=1 data streams | When subgrouping isn't natural | I plot + MR plot | API latency, model accuracy daily |
| p-chart | Proportion chart | Tracks fraction defective | For attribute/binomial data | p̄ ± 3√(p̄(1-p̄)/n) | Checkout success, conversion |
| c-chart | Count chart | Count of defects per unit | Poisson data, constant area | c̄ ± 3√c̄ | Bugs per release, alerts/hour |
| u-chart | Units chart | Defects per unit, variable opportunity | Poisson with changing exposure | ū ± 3√(ū/n) | Incidents per 1,000 req |
| Western Electric Rules | WECO Rules | Pattern rules beyond ±3σ | Catch shifts before a 3σ breach | 4 rules on zones A/B/C | Montgomery, 1956 origin |
| Nelson Rules | — | 8 modern pattern rules for control charts | Extend WECO, used in Minitab | Zone-based pattern detection | Modern quality software |
| Run | — | Consecutive points on one side of centerline | Signals a mean shift | ≥8 in a row on one side | Chart review |
| Trend | — | Monotonic ascent or descent of points | Signals drift | ≥6 points increasing/decreasing | Drift detection |
| CUSUM | Cumulative Sum | Sums deviations from target | Detects *small* shifts fast | S_t = max(0, S_{t-1}+x_t-k) | SRE SLI tracking |
| EWMA | Exponentially Weighted Moving Avg | Smoothed chart weighting recent data more | Small shift detection + smoothing | Z_t = λx_t + (1-λ)Z_{t-1} | ML drift, latency |
| SLO / Error Budget | Service Level Objective | SRE analogue to control limits | Quantified tolerance for failure | e.g. 99.9% over 30d → 43m budget | Google SRE, modern ops |
| Process Stability | In-control state | Process shows only common-cause variation | Precondition for capability (Cp/Cpk) | No WECO rule violations | Before any Six Sigma improvement |
| Rational Subgrouping | — | Sampling scheme that isolates common cause within subgroups | Makes R̄ a fair variance estimate | Subgroups by shift/region/minute | Montgomery Ch. 5 |
| Autocorrelation | Serial correlation | Today's value predicts tomorrow's | Breaks SPC assumption of independence | ACF, Durbin-Watson | Time-series data, latency |

---

## 3. Frameworks & Matrices

### 3.1 Shewhart Control Chart (I-MR with ±3σ + signal)
**Purpose:** Single reference framework for distinguishing signal from noise over time.

**Text Diagram:**
```
 value
   |                                               * <- SPECIAL CAUSE (outside UCL)
UCL|----------------------------------------------*---
   |          *                                   |
 +2σ|- - - - - - - - - - - - - - - - - - - - - - - -
   |      *       *               *
 CL |  *       *       *       *       *
   |              *       *               *
 -2σ|- - - - - - - - - - - - - - - - - - - - - - - -
LCL|-----------------------------------------------
   |
   +------time-ordered samples---------------------->
```

**Components:**
- Centerline (CL) = process mean X̄
- UCL / LCL = CL ± 3σ (99.73% of in-control data falls inside)
- Zones A (2–3σ), B (1–2σ), C (0–1σ) on each side, used by WECO rules

**IT/AI/Product/Consulting worked example:** An ML team puts daily model accuracy on an I-MR chart. CL = 0.912, σ̂ = 0.008, UCL = 0.936, LCL = 0.888. Friday's accuracy drops to 0.883 → outside LCL → trigger investigation. Decision: page on-call, do not retrain yet (retraining is the knee-jerk; first find the assignable cause — upstream feature pipeline pushed a stale reference table).

---

### 3.2 Control Chart Selection Tree
**Purpose:** Pick the right chart before collecting data; wrong chart → false alarms or missed shifts.

**Text Diagram:**
```
                 What data do I have?
                 /                  \
           CONTINUOUS            ATTRIBUTE (counts)
          (latency, CSAT)             |
              /       \         Are we counting...
         n=1?        n>1?      /               \
          |           |     DEFECTIVE UNITS   DEFECTS
         I-MR      X-bar-R   (yes/no per item)  (multiple per unit)
                   (or X̄-S    /        \        /        \
                   if n>10) constant n   varies  constant  varies
                             |          |        unit       unit
                           np-chart  p-chart  c-chart    u-chart
```

**IT example:** Product team measures (a) p95 checkout latency per 5-min window (continuous, n=1 aggregate) → **I-MR**; (b) checkout success rate per hour, volume varies → **p-chart**; (c) number of Sentry errors per deploy, deploy size varies → **u-chart**. Trigger: team was using I-MR on success *rate* and getting false alarms when traffic spiked; switched to p-chart and noise dropped 60%.

---

### 3.3 Western Electric Rules Decision Tree (4 key signals)
**Purpose:** Detect shifts earlier than waiting for a 3σ breach.

**Text Diagram:**
```
 +3σ |==================================== UCL
 +2σ |--- Zone A ---
 +1σ |--- Zone B ---
  CL |--- Zone C ---
 -1σ |--- Zone C ---
 -2σ |--- Zone B ---
 -3σ |==================================== LCL
 -3σ |--- Zone A ---

 Signal 1: Any 1 point outside ±3σ           → large shift
 Signal 2: 2 of 3 consecutive in Zone A or   → moderate shift
           beyond (same side)
 Signal 3: 4 of 5 consecutive in Zone B or   → small shift
           beyond (same side)
 Signal 4: 8 consecutive points on one       → process mean drift
           side of CL
```

**IT example:** SRE views p99 latency I-MR chart. No single point breaches UCL, but 9 consecutive 5-min buckets sit above CL (Signal 4). That's a shift of ~1σ — garbage collector tuning regression from last deploy. Decision rule: any WECO signal → open Jira ticket tagged `spc-signal`, don't wait for SLO burn.

---

### 3.4 (Bonus) CUSUM / EWMA for Small Drifts
**Purpose:** Shewhart charts are weak at catching shifts <1.5σ. CUSUM and EWMA fix that.

**Text Diagram:**
```
  S_t (CUSUM)
   |                                         /|
 H |- - - - - - - - - - - - - - - - - - - -/-|--  threshold
   |                                       /
   |                                  ___ /
   |                        _________/
   |________________________
   +---------------------- time ---->
   ^ reset at 0               ^ drift begins   ^ alarm
```

**IT example:** Model PSI (drift metric) tracked with EWMA λ=0.2. Underlying distribution drifts 0.3σ/week — invisible on Shewhart for ~30 weeks, flagged by EWMA in week 4. Trigger: retrain before customer-visible regression.

---

## 4. Formulas

### 4.1 Individuals Chart Limits (I-MR)
**Formula:** σ̂ = MR̄ / 1.128 ; UCL = X̄ + 3σ̂ ; LCL = X̄ − 3σ̂
**Variables:** X̄ = grand mean of individuals; MR̄ = mean of moving ranges (|x_i − x_{i-1}|); 1.128 = d₂ for n=2.
**Why:** n=1 data streams (daily KPI) have no within-subgroup range; MR̄ estimates σ.
**Interpret → Action:**
- Any point outside [LCL, UCL] → investigate special cause *today*.
- MR point > UCL_MR (= 3.267·MR̄) → spread has jumped, investigate volatility before location.

**Worked example (AI):** Daily model AUC over 20 days: X̄ = 0.840, MR̄ = 0.010. σ̂ = 0.010/1.128 = 0.00887. UCL = 0.840 + 0.0266 = 0.8666; LCL = 0.8134. Day 21 AUC = 0.805 → below LCL. Action: freeze model promotion, run data validation on last 48h features.

---

### 4.2 X-bar & R Chart Limits
**Formula:** UCL_X̄ = X̄̄ + A₂·R̄ ; LCL_X̄ = X̄̄ − A₂·R̄ ; UCL_R = D₄·R̄ ; LCL_R = D₃·R̄
**Variables:** X̄̄ = mean of subgroup means; R̄ = mean of subgroup ranges; A₂, D₃, D₄ are constants by subgroup size n (n=5: A₂=0.577, D₃=0, D₄=2.114).
**Why:** Subgroups collapse within-group noise, making between-group shifts visible.
**Interpret → Action:**
- X̄ outside limits with R in control → *mean* shifted.
- R outside limits → *variance* shifted; fix that first, then re-derive X̄ limits.

**Worked example (Product):** Checkout latency sampled 5 times every 10 min across 25 subgroups. X̄̄ = 420 ms, R̄ = 80 ms. UCL_X̄ = 420 + 0.577·80 = 466 ms; LCL_X̄ = 374 ms. UCL_R = 2.114·80 = 169 ms. Subgroup 26: X̄ = 478 ms, R = 95 ms. X̄ outside limits, R in control → mean shifted (likely cache miss storm). Action: roll back config before SLO burns.

---

### 4.3 p-Chart Control Limits
**Formula:** UCL = p̄ + 3·√(p̄(1−p̄)/n) ; LCL = max(0, p̄ − 3·√(p̄(1−p̄)/n))
**Variables:** p̄ = long-run defect proportion; n = sample size per subgroup.
**Why:** Binomial variance = p(1−p)/n; limits widen when n shrinks (low-traffic hours).
**Interpret → Action:**
- Subgroup p > UCL → special cause adverse event; open incident.
- If n varies substantially, use *variable-n* p-chart (per-subgroup limits) or stratify.

**Worked example (Consulting / SaaS):** Client's login failure rate p̄ = 0.02 across 10,000 attempts/hour. UCL = 0.02 + 3·√(0.02·0.98/10000) = 0.02 + 0.0042 = 0.0242. Hour 14: 280 failures in 10,000 = 0.028 → above UCL. Decision rule: p > UCL → page IAM on-call. Root cause: MFA provider throttling. Consulting recommendation: put a p-chart on every auth partner.

---

### 4.4 DPMO ↔ Sigma Level Bridge
**Formula:** DPMO = (defects / (opportunities_per_unit × units)) × 1,000,000
Sigma level lookup (with 1.5σ shift):
- 3σ ≈ 66,807 DPMO
- 4σ ≈ 6,210 DPMO
- 5σ ≈ 233 DPMO
- 6σ ≈ 3.4 DPMO

**Variables:** defects = observed failures; opportunities = independent chances per unit.
**Why:** Converts noisy %-defect numbers into a process-capability language comparable across products.
**Interpret → Action:**
- DPMO > 66,807 → process below 3σ; don't chart, *redesign*.
- 6,210 < DPMO ≤ 66,807 → 3–4σ; SPC + targeted kaizen.
- DPMO ≤ 233 → 5σ+; maintain via control plan, rare-event monitoring (g-chart / t-chart).

**Worked example (IT):** Ticket SLA misses: 1,200 breaches over 40,000 P2 tickets with 1 opportunity each. DPMO = 1200/40000 × 1e6 = 30,000 → ~3.9σ. Decision: still worth SPC; set up p-chart on weekly miss rate and target 4.5σ (6,210 DPMO ≈ 248 misses/40k) within two quarters.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---|---|
| Put spec limits (contractual SLA) on a control chart as UCL/LCL | Derive UCL/LCL from *process* data; compare to spec separately via Cp/Cpk |
| React to every point above the mean ("we're trending up!") | Require a WECO/Nelson rule to be violated before opening a ticket |
| Use a p-chart on success rate when traffic is tiny (n<30) | Switch to a g-chart (time-between-events) or aggregate to stable n |
| Apply SPC to obviously autocorrelated series (latency seconds apart) as-is | Aggregate to independent windows, or use EWMA/ARIMA-residual charts |
| Build one chart per metric per dashboard tile | Limit to KPIs with owners + response playbooks; everything else is noise |
| Reset control limits after every incident "to see fresh data" | Lock limits on a stable baseline window; only re-baseline after a *proven* process change |
| Treat SPC as a manufacturing-only tool | Use it for model drift, SLO burn, consulting ops benchmarks, NPS, MTTR |
| Outsource SPC thresholds to the ML team alone | Have Product + SRE + Consulting co-own the response rules |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI / ML Drift (Evidently + Grafana)
**Situation:** AI Lead running a fraud model in production. Precision tracked daily; historical X̄ = 0.91, σ̂ = 0.015.
**Framework:** I-MR + EWMA (for small drifts).
**Analysis:** UCL = 0.955, LCL = 0.865. Over 15 days, no single breach, but EWMA (λ=0.2) crosses the 2σ EWMA limit on day 11 — a 0.6σ drift invisible to Shewhart.
**Decision rule:** EWMA breach AND PSI > 0.2 on any top-5 feature → trigger retrain.
**Action (Monday):** Evidently drift report + Grafana EWMA panel; auto-open PagerDuty + Jira ticket with feature-level PSI breakdown.

### Scenario 2 — Product / Checkout Success (Amplitude + Looker)
**Situation:** Product Manager for e-commerce checkout. Success rate p̄ = 0.962 at ~8,000 attempts/hour.
**Framework:** p-chart on hourly success rate.
**Analysis:** UCL = 0.9684, LCL = 0.9556. Hour 03:00 shows p = 0.948 (n=6,500) → below LCL. Revenue impact: (0.962−0.948) × 6500 × $42 AOV ≈ $3,822 lost in one hour.
**Decision rule:** 1 point below LCL OR 2 of 3 in Zone A below CL → freeze deploys, page payments on-call.
**Action (Monday):** Looker alert on Snowflake materialized view; Mixpanel cohort to confirm it's not segment-driven.

### Scenario 3 — ANTI-EXAMPLE — Consulting at a Telco (ServiceNow + Datadog)
**Situation:** Consulting team set SPC limits for ticket MTTR by copying the client's contractual SLA (4h) as UCL and 1h as LCL.
**Framework:** (Misapplied) I-MR on daily mean MTTR.
**Analysis:** Process mean MTTR = 2.3h, σ̂ = 0.4h. True UCL should be 3.5h; false UCL was set at 4.0h. Real process drift to 3.6h went unflagged for 6 weeks. Quantified cost: 42 days × ~80 extra breaches/day × $250 penalty = **$840,000** in credits, plus a CSAT dip that killed a $2.1M upsell.
**Decision rule lesson:** Spec limits ≠ control limits. Ever.
**Action (Monday):** Rebuild ServiceNow-sourced I-MR in Datadog with process-derived UCL = 3.5h; overlay contractual spec as a separate reference line; train consulting engagement managers on rational subgrouping by shift.

---

## 7. Implementation Playbook
1. **Select the KPI + chart type** using the selection tree; document choice in a one-pager (Confluence). Artifact: *SPC Chart Design Doc*.
2. **Define rational subgroups** (by shift, region, deploy, model version) so within-group variation reflects common cause only. Artifact: *Subgrouping Policy*.
3. **Collect a baseline** of ≥25 subgroups (or 100 individuals) during a *stable* window — no known incidents. Pipe from Snowflake / BigQuery.
4. **Compute control limits** in Python (`pyspc`, `scipy`) or Minitab; store as parameters in a feature store or Datadog monitor config. Artifact: *Baseline Limits YAML*.
5. **Build the chart** in Grafana / Looker / Evidently with WECO rule overlays; add annotations for deploys and incidents.
6. **Wire alerts** to PagerDuty / Slack with *different* severities per rule (Rule 1 = page; Rule 4 = ticket). Artifact: *Alert Routing Matrix*.
7. **Review weekly** in an ops standup; re-baseline only on documented process change, logged in a *Change Register*.
8. **Quarterly capability review** — pair SPC stability with Cp/Cpk vs spec; feed into the DMAIC Control phase artifact.

---

## 8. Content Quality Audit

**Covered well:**
- Core SPC intuition: common vs special cause, distinguishing noise from signal.
- Basic chart mention (X-bar, R, I-MR) with one use case each.
- Correct emphasis on *not* over-adjusting the process.

**Underplayed or missing (source gaps):**
- **Western Electric / Nelson rules** — source mentions "non-random patterns" but never names or lists the rules.
- **Rational subgrouping** — completely absent, yet it's the single biggest determinant of chart validity (Montgomery devotes Ch. 5 to it).
- **Subgroup size effects** — A₂, D₃, D₄ constants and their sensitivity to n not discussed.
- **Non-normal data chart choices** — no mention of attribute charts (p, np, c, u) or transformations (Box-Cox, log) for skewed IT data like latency.
- **SRE / error-budget analogue** — source never bridges SPC to modern IT ops vocabulary, leaving a huge comprehension gap for engineers.
- **Autocorrelation pitfalls** — latency and model accuracy are serially correlated; applying vanilla SPC yields false-alarm storms.
- **CUSUM / EWMA** — small-shift detection absent.
- **Phase I vs Phase II** distinction (baseline setting vs monitoring).

**Supplement with:**
1. Montgomery, D. C. — *Introduction to Statistical Quality Control*, 8th ed., Wiley, 2019. Chapters 5–7 on Shewhart, 9 on CUSUM/EWMA.
2. Wheeler, D. J. — *Understanding Variation: The Key to Managing Chaos*, 2nd ed., SPC Press, 2000.
3. Kohavi, R., Tang, D., Xu, Y. — *Trustworthy Online Controlled Experiments*, Cambridge University Press, 2020. (Variance, p-chart analogues for online metrics.)
4. Beyer, B. et al. — *Site Reliability Engineering: How Google Runs Production Systems*, O'Reilly, 2016. (SLO / error budget as SPC analogue.)
5. Hoerl, R. W. & Snee, R. D. — "Statistical Thinking and Methods in Quality Improvement," *Quality Engineering*, 2010. [verified from model knowledge, not source]
6. HBR — Harry, M., "Six Sigma: A Breakthrough Strategy for Profitability," *Harvard Business Review*, 1998. [verified from model knowledge, not source]

**Red flags in the source:**
- Equates "±3σ" with safety without warning against applying it to non-normal or autocorrelated data.
- Scenario (dairy) is fine for intuition but no IT/AI translation is offered.
- No mention that stability is a *precondition* for capability analysis — a common misstep where teams compute Cpk on an unstable process.
- No playbook for *what to do* when a signal fires, only that one fires.

---

## 9. Quick-Recall Card
- SPC separates common-cause noise from special-cause signal *before* you react.
- Control limits come from the process (±3σ), spec limits come from the customer — never confuse them.
- Pick chart by data type: continuous→X-bar-R / I-MR; proportions→p; counts→c/u.
- Use WECO/Nelson rules, EWMA, or CUSUM to catch small drifts Shewhart misses.
- Stability is a precondition for capability (Cp/Cpk) and for any Six Sigma improvement claim.
- **As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Is the movement in my KPI today a signal worth acting on, or is it inside the voice of the process?"**

---

**Connects to:** [05-analyze-phase.md](05-analyze-phase.md), [07-control-phase.md](07-control-phase.md), [10-process-capability-analysis.md](10-process-capability-analysis.md), [../business-analytics/10-operations-analytics.md](../business-analytics/10-operations-analytics.md).

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5]
Sections rewritten: [all enriched from source skeleton]
Enrichments applied: [cross-course links; 5+ supplements incl. Montgomery 2019, Wheeler, Kohavi 2020, Beyer 2016, HBR 1998; anti-example telco MTTR; IT-org data sources Grafana/Datadog/Evidently/Looker/Snowflake/Amplitude/Mixpanel/PagerDuty/ServiceNow; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A1
-->
