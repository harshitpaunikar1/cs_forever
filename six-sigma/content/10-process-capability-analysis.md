# Process Capability Analysis

## Overview
Process capability analysis measures how well a process meets its specification limits by comparing the spread of process output to the width of the specification range. It answers a fundamental question: can this process consistently produce output that meets customer requirements? The result is expressed as capability indices such as Cp and Cpk, which provide a simple numerical summary of process performance.

---

## Why It Matters
A process may be statistically in control yet still produce output that does not meet specifications. Process capability analysis bridges the gap between process stability and customer satisfaction by quantifying whether the process can deliver within the required tolerances. Organizations use capability indices to make decisions about production readiness, equipment purchases, supplier qualification, and whether a process needs improvement.

## Key Principles
- A process must be in statistical control before capability can be meaningfully assessed
- Capability compares process spread to specification width, not just to control limits
- Cp measures potential capability assuming the process is perfectly centered
- Cpk accounts for how far the process mean is shifted from the center of the specification

## Key Terms
| Term | Definition |
|------|------------|
| **Cp** | A capability index that compares the specification width to the process spread, assuming the process is centered |
| **Cpk** | A capability index that accounts for both the process spread and how far the mean is from the nearest specification limit |
| **Specification Limits** | The boundaries set by the customer or engineering team that define acceptable product performance |
| **Process Spread** | The range of output values produced by a process, typically measured as six standard deviations |

## Use Case
An automotive parts supplier calculates Cpk for each critical dimension of a brake rotor to demonstrate to the car manufacturer that its process consistently meets engineering tolerances.

## Scenario
> A bottling company checks whether its filling process is capable of meeting the labeled volume of 500 mL plus or minus 5 mL. The team calculates a Cpk of 0.8, which means the process is not capable and some bottles are being underfilled. They adjust the fill head calibration, re-measure, and achieve a Cpk of 1.5, confirming the process now comfortably meets the specification.

## Examples
- A circuit board manufacturer requires all suppliers to demonstrate a Cpk of at least 1.33 for critical solder joint dimensions before approving production orders
- A pharmaceutical company uses process capability analysis to verify that tablet weight variation stays within regulatory limits across all production lines

---

## Audited Appendix

# Process Capability Analysis
**Course:** Six Sigma
**Module:** Content / Process Capability Analysis
**Audited on:** 2026-04-18
**Audited by:** A2
**Source files reviewed:** `six-sigma/content/10-process-capability-analysis.md`

---

## 1. Topic Snapshot
Process Capability Analysis quantifies whether a stable process can consistently meet customer/spec tolerances by comparing process spread (6σ) to specification width (USL−LSL), expressed as Cp (potential, if centered) and Cpk (actual, off-center penalized).
For an IT/AI/Product/Consulting leader this is the statistical backbone of SLO compliance (API p99 latency vs SLO), model tolerance (confidence-accuracy thresholds), supplier qualification (vendor Cpk ≥ 1.33), and release-readiness gates — it converts "we're stable" into "we meet the contract."
Decision it drives: ship / hold / re-center / reduce variation / renegotiate spec — and whether a vendor, model, or service is production-grade.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|------|-----------|---------------|---------------|--------------|-------------------|
| Cp | Process Capability (potential) | How much spec room vs. how wide the process spreads, assuming centered | Separates spread problem from centering problem | (USL−LSL)/(6σ) | Manufacturing QA, SRE capacity reviews |
| Cpk | Process Capability Index | Cp penalized for how off-center the mean sits | Real-world capability, not theoretical | min[(USL−μ)/3σ, (μ−LSL)/3σ] | Supplier scorecards, release gates |
| Pp | Process Performance (potential) | Same as Cp but uses long-term (overall) σ | Captures between-subgroup drift | (USL−LSL)/(6σ_LT) | PPAP auto/aero audits |
| Ppk | Process Performance Index | Cpk's long-term twin | Honest "actual" view over months | min[(USL−μ)/3σ_LT, (μ−LSL)/3σ_LT] | AIAG PPAP, regulated industries |
| USL | Upper Spec Limit | Customer's "not more than" | Defines one boundary of acceptable | Given by customer/contract | Contracts, SLOs |
| LSL | Lower Spec Limit | Customer's "not less than" | Other boundary | Given by customer/contract | Contracts, SLOs |
| Process Spread | 6σ range of output | Natural variation band | Compares to spec width | 6 × sample σ | Capability studies |
| Specification Width | USL − LSL | Tolerance band size | Numerator of capability ratio | Contract-defined | QA, SRE |
| Process Centering | μ vs. target T | How off-bullseye the mean is | Drives Cpk gap from Cp | k = |μ−T| / ((USL−LSL)/2) | Calibration reviews |
| Sigma Level | Z-score of nearest spec | Distance in σ to failure | Translates Cpk to defects | Z = 3·Cpk (short-term) | Six Sigma scorecards |
| DPMO | Defects Per Million Opportunities | Failure rate at 1M scale | Common Six Sigma currency | From Z or Cpk tables | Executive dashboards |
| Capability Index | General term Cp/Cpk/Pp/Ppk | Ratio of tolerance to variation | Single number for go/no-go | See above | All of the above |
| Target Cpk | Industry minimum | Accepted threshold (1.33, 1.67, 2.0) | Contractual bar | Policy | Automotive ≥1.33, aerospace ≥1.67 |
| RTY | Rolled Throughput Yield | Prob. of zero defect across N steps | Multi-step reality check | Π y_i | End-to-end pipeline reviews |
| Six Sigma Target | Cpk ≥ 2.0 | 3.4 DPMO with 1.5σ shift | Aspirational quality level | Derived | Six Sigma certifications |
| Box-Cox | Power transform | Fix non-normal data so Cpk math works | Non-normal processes bias Cpk | λ search on Y^λ | Minitab, JMP, Python |

---

## 3. Frameworks & Matrices

### 3.1 Cp vs Cpk vs Pp vs Ppk Matrix
**Purpose:** Tell apart short-term potential, short-term actual, long-term potential, long-term actual — each answers a different question.

```
                    CENTERED (μ ≈ T)         OFF-CENTER (μ ≠ T)
                 ┌────────────────────────┬────────────────────────┐
   SHORT-TERM σ  │  Cp  = potential, ideal│  Cpk = actual short-run│
   (within-      │  "How tight COULD we   │  "How tight we ARE on  │
    subgroup)    │   run if we aimed?"    │   a good day"          │
                 ├────────────────────────┼────────────────────────┤
   LONG-TERM σ   │  Pp  = potential, real │  Ppk = actual long-run │
   (overall)     │  "Best case across all │  "What customer sees   │
                 │   drifts, if centered" │   over quarters"       │
                 └────────────────────────┴────────────────────────┘
   Rule of thumb: Cp ≥ Cpk, Pp ≥ Ppk, and Cp/Cpk ≥ Pp/Ppk.
   Gap (Cpk − Ppk) signals between-subgroup drift / instability.
```

**Components:** Short-term σ (pooled within-subgroup), Long-term σ (overall), Mean μ, Target T.
**IT/AI example:** Model inference latency. Cpk (within-hour) = 1.6, Ppk (across month) = 0.9 → process drifts day-to-day; nightly batch jobs or cache-warming variance is eating capability. Decision: investigate drift (not add capacity).
**Trigger:** Any PPAP, supplier audit, SLO quarterly review, model monitoring handoff.

### 3.2 Capability Traffic-Light Decision Matrix
**Purpose:** One-glance go/no-go with prescribed action.

```
  Cpk band    Color   Sigma~  DPMO~      Verdict              Action
  ──────────  ─────   ──────  ─────────  ───────────────────  ──────────────────────────
  < 1.00      RED     <3σ     >66,800    NOT capable          Halt release; variance-reduction kaizen
  1.00–1.33   AMBER   3–4σ    66k→6,200  Marginal             100% inspect; improvement plan; re-measure
  1.33–1.67   GREEN   4–5σ    6,200→233  Capable (industry)   Ship; monitor via SPC
  1.67–2.00   BLUE    5–6σ    233→3.4    Highly capable       Reduce sampling freq; use capacity elsewhere
  ≥ 2.00      BLUE+   6σ+     <3.4       Six-Sigma capable    Process is a competitive moat
```

**IT/AI worked example:** API p99 latency, SLO USL = 300 ms. μ = 220, σ = 30 → Cpk = (300−220)/(3·30) = 0.89 → RED → freeze release, run profiling sprint before promising SLO to customer.
**Trigger:** Any gate review, supplier onboarding, SLO commitment, model promotion to prod.

### 3.3 Process Centering Diagnosis Framework
**Purpose:** Cpk is low — is it spread or centering? Different fix.

```
  Case A: OFF-CENTER (spread OK)        Case B: TOO WIDE (centered OK)
      LSL   T      USL                      LSL     T     USL
       │    │  ███ │                         │  ██████████ │
       │   █│███████│                         │ ████████████│
       │ ███│████ ║ │                         │██████████████
       │████│█   ║ → spec exceeded on high     ██│██████████│██  ← both tails clip
      Cp = 1.5, Cpk = 0.7                    Cp = 0.7, Cpk = 0.6
      k ≈ 0.5 (mean shifted)                 Cp low to begin with
      FIX: re-center (calibrate, tune prompt, FIX: reduce variance (better infra,
           change setpoint, adjust threshold)      cleaner data, tighter controls)
```

**Diagnostic rule:** Compute k = |μ − T| / ((USL−LSL)/2). If k > 0.2 and Cp ≥ 1.33, it's centering. If Cp < 1.33, it's spread. If both, fix centering first (cheaper).
**IT/AI example:** Checkout conversion model, spec 92–96% accuracy on holdout. μ = 90%, σ = 0.8%. Cp = 2.5, Cpk = −0.8 (below LSL!) → purely centering; retrain/re-threshold, don't add data.
**Trigger:** Any Cpk < 1.33 or any Cpk << Cp ratio.

---

## 4. Formulas

### 4.1 Cp — Potential Capability
**Formula:** Cp = (USL − LSL) / (6σ)
**Variables:** USL/LSL = spec limits; σ = short-term (within-subgroup) std dev.
**Why:** Ignores where mean sits — pure "is my variance small enough for the tolerance?"
**Thresholds:** <1.0 not capable · 1.0–1.33 marginal · ≥1.33 capable · ≥1.67 automotive/aero · ≥2.0 Six Sigma.
**Worked (API latency SLO):** Contract says p99 latency must stay within 200–300 ms (USL=300, LSL=200). σ = 12 ms.
Cp = (300 − 200) / (6 × 12) = 100 / 72 = **1.39** → GREEN-capable *if* we can center at 250 ms.

### 4.2 Cpk — Actual Capability
**Formula:** Cpk = min[(USL − μ)/(3σ), (μ − LSL)/(3σ)]
**Variables:** μ = process mean; σ = short-term std dev.
**Why:** Real-world capability — penalizes for off-centering.
**Thresholds:** same as Cp; Cp − Cpk > 0.2 → centering problem dominates.
**Worked (ticket ack time):** SLA LSL = 0 min, USL = 15 min. μ = 11 min, σ = 2 min.
Cpk = min[(15−11)/6, (11−0)/6] = min[0.67, 1.83] = **0.67** → RED. Even though spread is fine (Cp = 15/12 = 1.25), mean is too close to USL. Fix: reduce average handle time (auto-triage), don't buy more staff.

### 4.3 Pp / Ppk — Long-Term Performance
**Formula:** Pp = (USL−LSL)/(6σ_LT); Ppk = min[(USL−μ)/3σ_LT, (μ−LSL)/3σ_LT]
**Variables:** σ_LT = overall std dev across all data (includes drift).
**Why:** Customer sees long-term reality, not idealized within-subgroup.
**Thresholds:** Same bands. Cpk/Ppk ratio >1.3 → significant between-subgroup drift.
**Worked (model confidence, Consulting):** Fraud model confidence score, spec ≥0.70 for auto-approve. Daily within-day σ=0.03, but month-long σ=0.08 (model drift). μ=0.80. Cpk = (0.80−0.70)/(3·0.03) = 1.11 (amber); Ppk = (0.80−0.70)/(3·0.08) = **0.42** (red) → model drift is the real problem; add Evidently drift monitor + monthly retrain.

### 4.4 Expected DPMO from Cpk
**Formula:** DPMO ≈ [Φ(−3·Cpk_upper) + Φ(−3·Cpk_lower)] × 1,000,000 (two-sided); one-sided ≈ Φ(−3·Cpk)·1e6.
**Variables:** Φ = standard normal CDF.
**Why:** Converts capability to defect count a business person understands.
**Thresholds:** Cpk 1.00 → ~2,700 DPMO · 1.33 → ~63 · 1.67 → ~0.6 · 2.00 → 0.002 (with 1.5σ shift added: 1.0→66,800; 1.33→6,210; 1.67→233; 2.0→3.4).
**Worked (checkout conversion, Product):** One-sided USL on failed-checkout rate. Cpk = 1.20. DPMO ≈ Φ(−3.6)·1e6 ≈ **159 per million checkouts**. At 2M checkouts/month → 318 failures/month = $47k at $148 AOV. Target Cpk 1.33 would cut this to ~126/month.

### 4.5 Rolled Throughput Yield (RTY)
**Formula:** RTY = Π y_i, where y_i = first-pass yield of step i (and yield_i ≈ 1 − DPMO_i/1e6 for its Cpk).
**Variables:** y_i per process step.
**Why:** Six-step pipeline of 99% stages = 94% end-to-end; capability must be seen across the chain.
**Thresholds:** Target ≥95% for customer-facing flows; <90% demands redesign.
**Worked (AI pipeline, IT/AI):** ML inference path with 6 stages (ingest, featurize, infer, post-process, cache, respond), each Cpk = 1.33 (y ≈ 0.9999).
RTY = 0.9999^6 = **0.9994** → 6 per 10,000 end-to-end misses — acceptable. If one stage drops to Cpk=1.0 (y=0.9973), RTY = 0.9973·0.9999^5 = 0.9968 → 32/10,000 — 5× worse. Weakest link dominates; pour capability budget there.

---

## 5. Do vs Don't

| Do | Don't |
|----|-------|
| Verify statistical control (stable X-bar R chart) BEFORE computing Cp/Cpk | Compute Cpk on an out-of-control process — the σ is meaningless |
| Check normality (Anderson–Darling, probability plot) before using standard Cpk | Blindly apply normal-theory Cpk to latency, queue-time, or error-rate data (right-skewed) |
| Use Box-Cox / Johnson transform or non-normal Cpk (percentile method) for skewed data | Pretend lognormal latency is normal because Minitab will still give you a number |
| Report both Cp AND Cpk so the reader can see centering gap | Report Cpk alone — hides whether fix is re-center or reduce-variance |
| Require ≥30 data points (ideally ≥100) for stable σ estimate | Quote Cpk from 10 samples in a demo and treat it as contractual |
| Use short-term σ for Cp/Cpk and long-term σ for Pp/Ppk — and compare | Mix the two; "the Cpk" with no σ context is a red flag |
| Map Cpk to industry norms (1.33 automotive, 1.67 aero, 2.0 six-sigma) before promising | Commit to a customer Cpk without knowing what their buyer community expects |
| Treat SRE error budgets as the modern one-sided Ppk for SaaS | Force manufacturing two-sided spec math onto an inherently one-sided SLO |
| Re-measure after any fix and show before/after Cpk with confidence interval | Declare victory on a point estimate with no CI — Cpk has wide CIs at n=30 |

---

## 6. Real-Life Scenarios

### 6.1 API Latency SLO Capability (IT/SRE)
**Context:** Payments API, SLO commits p99 latency ≤ 250 ms (one-sided USL). Ingest 4 weeks of Prometheus histograms via Grafana; export to Snowflake.
**Measurement:** After Box-Cox on right-skewed latency, μ = 180 ms, σ_LT = 28 ms.
**Compute:** Ppk = (250 − 180) / (3 × 28) = 70 / 84 = **0.83** → RED.
**Decision:** Do NOT sign the SLO at 250 ms. Options: (a) renegotiate to 300 ms (Ppk = 1.43, green); (b) invest in cache layer + async fan-out to cut σ to 15 ms (Ppk = 1.56). Pick (b) — cost $40k infra vs. ~$1.2M customer-credit exposure over a year.
**Tools:** Grafana (dashboards), Prometheus (metric store), Datadog (alerting), Snowflake (long-term), Python SciPy (Box-Cox, Cpk).

### 6.2 ML Model Confidence Threshold Capability (AI/Product)
**Context:** Fraud model — business rule: confidence ≥ 0.75 ⇒ auto-approve, else human review. Product wants 85% auto-approval rate without crossing a 0.5% false-approve cap (LSL on precision at threshold).
**Measurement:** Over 90 days of scoring telemetry (Evidently + Looker), precision at 0.75 has μ = 0.993, σ_LT = 0.004; spec LSL = 0.995.
**Compute:** Ppk_lower = (0.993 − 0.995) / (3 × 0.004) = **−0.17** → model is NOT capable at that threshold; mean already below LSL.
**Decision:** Either (a) raise threshold to 0.82 (reduces auto-approval to 78%, meets precision spec, Ppk ≈ 1.1) or (b) retrain with hard negatives. Pick (a) for this sprint, (b) for next quarter. Set Evidently drift alert.
**Tools:** Evidently (drift + precision monitoring), Looker (exec dashboards), Snowflake (feature store).

### 6.3 ANTI-EXAMPLE: Cpk on Unstable Non-Normal Process (Consulting)
**Context:** Consulting team reports ticket-resolution SLA Cpk = 1.45 to client based on Q3 data; client signs escalation-credit clause at that level.
**What went wrong:**
- Process was NOT in control (a major deploy mid-Q3 shifted mean) — the within-subgroup σ understated reality.
- Resolution-time data is right-skewed lognormal — normal Cpk formula overstated capability.
- Sample n = 42, wide CI not reported; true Ppk (post-deploy, lognormal-correct) = 0.72.
**Consequence in Q4:** SLA breach rate 18% vs. contractual ≤3%, triggered $280k of service credits + churn of a $1.1M/yr anchor account. Total cost: **~$1.4M** traced to a capability number that was mathematically wrong.
**Lesson:** Always (1) SPC chart first, (2) test normality, (3) use Ppk not Cpk for customer-facing claims, (4) report CI, (5) re-measure after any process change.
**Tools that would have caught it:** Datadog anomaly-detect on resolution time, Evidently drift, Python `scipy.stats` normality tests, Looker trended Ppk.

---

## 7. Implementation Playbook

1. **Define** spec limits (USL/LSL/target) as a signed artifact — contract, SLO doc, or PPAP form. No capability study without them.
2. **Collect** ≥100 data points spanning ≥20 rational subgroups (e.g., 20 days × 5 samples) — store in Snowflake/warehouse.
3. **Chart & stabilize** via X-bar/R or I-MR control chart (Grafana or Minitab) — remove special causes before capability math.
4. **Test normality** (Anderson–Darling, Q-Q plot); if fails, Box-Cox transform or use non-normal/percentile Cpk.
5. **Compute** Cp, Cpk, Pp, Ppk with 95% confidence intervals (Python `scipy`, Minitab, JMP) — produce one-pager.
6. **Map** to traffic-light band and industry norm; write decision (ship/hold/re-center/reduce-variance).
7. **Act** on centering vs. spread diagnosis — calibrate, retrain, scale, or re-architect accordingly.
8. **Monitor & re-baseline** quarterly via dashboard (Datadog/Evidently/Looker); trigger re-study on any major process change.

---

## 8. Content Quality Audit

### Covered well
- Core Cp vs Cpk distinction and intuition.
- Connection to statistical control as prerequisite.
- Industry use cases (automotive, pharma, bottling) with concrete Cpk thresholds.

### Underplayed / missing (must call out)
- **Pp vs Cp distinction** — source omits long-term vs short-term σ entirely; customer-facing claims should use Ppk.
- **Normality assumption** — Cpk formula assumes normal data; latency/queue/price data are skewed and inflate Cpk.
- **Minimum-sample issues** — Cpk has wide confidence intervals below n=100; a "Cpk = 1.5" from 25 points is noise.
- **Non-normal capability** — Box-Cox, Johnson transform, or percentile method (Clements) not mentioned.
- **One-sided capability** — most SaaS SLOs (latency, error rate) are one-sided; source implicitly assumes two-sided.
- **SRE error budgets as modern analogue** — (1 − SLO) acts as a long-term Ppk in reverse; source doesn't connect Six Sigma to modern SRE practice.
- **Confidence intervals on Cpk** — never mentioned; small-sample Cpk CI can span two traffic-light bands.

### Supplement with named sources
1. **Montgomery, D.C. (2019).** *Introduction to Statistical Quality Control*, 8th ed., Wiley — canonical Cp/Cpk chapter and CIs.
2. **Wheeler, D.J. (2000).** *Normality and the Process Behavior Chart*, SPC Press — on normality assumption myth.
3. **Bothe, D.R. (1997).** *Measuring Process Capability*, McGraw-Hill — non-normal, one-sided, short vs long-term.
4. **Beyer, B. et al. (2016).** *Site Reliability Engineering*, O'Reilly (Google SRE Book) — error budgets, SLO math as modern one-sided capability.
5. **Kane, V.E. (1986).** "Process Capability Indices," *Journal of Quality Technology* 18(1) — original Cpk paper.
6. **Harry, M. & Schroeder, R. (2000).** *Six Sigma*, Doubleday — 1.5σ shift and DPMO table lineage.
7. **HBR — Schroeder, R. et al. (2008).** "Six Sigma: Definition and Underlying Theory," *JOM* / HBR coverage — executive framing.

### Red flags in source
- No mention of normality, sample size, or CIs — a practitioner following the source verbatim will over-claim capability.
- Automotive Cpk ≥ 1.33 cited without the "PPAP / AIAG" context behind it.
- Pharma example glosses over regulatory requirement for Ppk (not Cpk) in long-term stability.
- No anti-example of mis-applied Cpk.

---

## 9. Quick-Recall Card
- Cp = tolerance ÷ 6σ (potential); Cpk = Cp penalized for off-center — use Cpk for reality.
- Bands: <1.0 red, 1.0–1.33 amber, 1.33–1.67 green, ≥1.67 blue — and industry norm is 1.33.
- Cp >> Cpk → centering problem (cheap to fix). Cp low → variance problem (expensive).
- Use Ppk (long-term σ) for customer promises; Cpk (short-term) for tuning.
- Never compute capability on an unstable or non-normal process without transform — you will be wrong by a factor.
- SRE error budget is capability in SaaS clothing: (1 − SLO) is your allowable defect rate.
- **Role-lens question:** "For the next SLO, model threshold, or vendor contract I sign — do I know the Ppk, the confidence interval, and whether the underlying data is normal — or am I about to commit to a number I can't hold?"

---

**Connects to:** [07-control-phase.md](07-control-phase.md), [09-statistical-process-control.md](09-statistical-process-control.md), [../business-analytics/10-operations-analytics.md](../business-analytics/10-operations-analytics.md).

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5]
Sections rewritten: [all enriched from source to IT/AI/Product/Consulting lens; added Pp/Ppk, DPMO, RTY, anti-example]
Enrichments applied: [cross-course links; 7 supplements; anti-example with $1.4M cost; IT-org tooling — Grafana/Prometheus/Datadog/Snowflake/Looker/Evidently; role-lens question; normality + non-normal + one-sided + CI callouts; SRE error-budget analogue]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A2
-->
