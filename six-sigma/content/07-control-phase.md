# Control Phase

## Overview
The Control phase is the final step of DMAIC where the team ensures that the improvements achieved during the Improve phase are sustained over time. This phase involves creating monitoring systems, documenting new procedures, training staff, and establishing response plans for when the process drifts out of specification. Without a strong Control phase, processes tend to revert to their old state.

---

## Why It Matters
Many improvement projects deliver short-term gains that evaporate within months because no one monitors the process after the project team disbands. The Control phase locks in the gains by building monitoring dashboards, updating standard operating procedures, and creating escalation triggers. It transforms a one-time project into a permanent operational improvement.

## Key Principles
- Document the improved process with updated standard operating procedures
- Implement control charts and dashboards for ongoing monitoring
- Define response plans that specify what to do when the process drifts
- Transfer ownership from the project team to the process owner

## Key Terms
| Term | Definition |
|------|------------|
| **Control Chart** | A time-series graph with upper and lower control limits used to monitor process stability |
| **Standard Operating Procedure (SOP)** | A documented set of step-by-step instructions for performing a process consistently |
| **Response Plan** | A predefined set of actions to take when a control chart signals that the process is out of control |
| **Process Owner** | The individual responsible for maintaining the improved process after the project team completes its work |

## Use Case
A food processing plant installs automated sensors that feed real-time temperature data into control charts, triggering an immediate alert whenever the pasteurization process drifts outside its target range.

## Scenario
> After reducing billing errors by 75%, a telecommunications company creates a control dashboard that tracks error rates weekly. When the rate creeps above the new threshold two months later, the response plan kicks in and the team discovers that a recent software update reintroduced an old bug. They fix it within days instead of letting the problem grow for months.

## Examples
- A car manufacturer updates its SOPs and trains assembly line workers on a new torque specification, then uses control charts to verify consistency across all shifts
- A hospital creates a monthly audit process and escalation protocol to maintain its reduced surgical infection rate after a Six Sigma project concludes

---

## Audited Appendix

# Control Phase
**Course:** Six Sigma
**Module:** Content / Control Phase
**Audited on:** 2026-04-18
**Audited by:** A1
**Source files reviewed:** `six-sigma/content/07-control-phase.md`

---

## 1. Topic Snapshot
Control is the closing DMAIC step that locks improvement gains by turning the new process into monitored, owned, and documented standard work.
For an IT/AI/Product/Consulting leader, it is the phase that answers "what happens when the project team disbands next quarter?" — the discipline that stops improvements from decaying.
The decision it helps make: who owns the new process, how it is monitored, and what triggers a response when drift appears.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Control Chart | - | Time-series plot with a centre line and statistical control limits used to tell random variation from real drift. | Prevents both false alarms (reacting to noise) and missed drifts. | UCL/LCL, sigma zones, Western Electric rules. | SPC, SRE SLO dashboards, ops monitoring. |
| Upper / Lower Control Limit | UCL / LCL | Statistical bounds (typically ±3σ from the mean) that mark "expected" variation. | Separates signal from noise on the control chart. | Mean ± 3σ (or ±2σ for tighter control). | SPC, anomaly detection, monitoring. |
| Standard Operating Procedure | SOP | Step-by-step documented instructions for the new process. | Makes the new way the default even when memories fade or staff change. | SOP version, last-reviewed date, adherence rate. | Ops, compliance, runbooks, SRE playbooks. |
| Response Plan | - | Pre-written actions to take when a control chart signals out-of-control behaviour. | Removes "what do we do now?" hesitation during drift. | Time to detect, time to respond, MTTR. | Incident management, ops, quality control. |
| Process Owner | - | Single accountable person for maintaining the improved process post-project. | Ownership is the #1 predictor of sustained gains. | Named accountability; KR/OKR coverage. | DMAIC handoff, RACI charts, ops reviews. |
| Common-Cause Variation | - | Normal, random variation within the process's design. | Not worth reacting to individually. | Points within control limits, random pattern. | SPC, SRE, quality. |
| Special-Cause Variation | - | Non-random variation from an identifiable external cause. | Must be investigated and fixed. | Points outside control limits, or trends / runs. | SPC, anomaly detection, incident analysis. |
| Process Drift | - | Gradual shift of the process mean or spread away from baseline. | Slow drifts are invisible without monitoring. | Trend slope, CUSUM signal, moving range. | SPC, model monitoring, SLO tracking. |
| Poka-Yoke | - | Error-proofing mechanism that makes incorrect execution hard or impossible. | Prefers prevention over detection. | Error rate before vs after, near-miss count. | Lean, manufacturing, UX design, form validation. |
| Statistical Process Control | SPC | Discipline of using data and control charts to monitor and maintain processes. | Gives the Control phase a quantitative spine. | Control-chart stability, Cp/Cpk, DPMO. | Quality, manufacturing, service ops. |
| Cp / Cpk | Process Capability Index / Process Capability Index (centred) | Ratios of process spread to specification width. | Quantifies whether the process can meet spec consistently. | Cp = (USL−LSL)/6σ; Cpk = min((USL−μ)/3σ, (μ−LSL)/3σ). | SPC, quality, DFSS. |
| Control Plan | - | Document listing every key input/output, how it is monitored, by whom, how often, and what to do on drift. | One canonical reference replaces scattered tribal knowledge. | % items with named owner + frequency + response. | Six Sigma close-out, ops handover. |
| Audit Cadence | - | Regular schedule for verifying the new process is being followed. | Adherence decays without inspection. | Audit frequency (monthly/quarterly), non-conformance rate. | Compliance, ops, quality. |
| Handoff / Transfer of Ownership | - | Formal transition from the DMAIC project team to the process owner. | Ends the project without orphaning the improvement. | Signed handoff document; 90-day stability post-handoff. | Consulting engagements, Six Sigma close. |

---

## 3. Frameworks & Matrices

### Shewhart Control Chart (X̄ / Individuals-and-Moving-Range)
**Purpose:** Separate normal process variation from true drift so the team reacts only when it should.

**Text Diagram:**
```text
Metric (Y)
   UCL  ───────────────────────────────────────────
                 •         •                 ▲ ← special cause
                    •  •                •     (point > UCL — investigate)
   +1σ  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
   Mean ═══•═══•═══•════•═══•════•═══•════•═══•═══ CL
   −1σ  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
                                •  •  •  •  ← run below
                                            (8 points same side — investigate)
   LCL  ───────────────────────────────────────────
        t₁  t₂  t₃  t₄  ... time ...
```

Axes / Quadrants / Components explained:
- X-axis: time (hours, days, weeks, sprints — chosen to match drift frequency).
- Y-axis: the Y metric being controlled (latency, defect %, SLA %, accuracy).
- Centre line (CL): process mean after improvement.
- UCL / LCL: mean ± 3σ (or ±2σ for tighter regimes).
- Signals: points outside UCL/LCL; 8-point run on one side; 6-point trend; 14-point up/down oscillation (Western Electric rules).

IT/AI/Product/Consulting worked example: An AI team monitors model accuracy weekly. Mean = 92.1%, σ = 0.6%, so UCL ≈ 93.9, LCL ≈ 90.3. A 4-week dip: 91.8, 91.5, 91.2, 90.9 — all within LCL, but the 4-point downward trend triggers investigation. Root cause: upstream feature-store schema change reducing coverage on a key feature for 18% of requests. Fix shipped before any single week breaches LCL.

When to pull this out in a meeting: whenever someone points at a metric's last data point and argues for a panic response.

### Control Plan Matrix
**Purpose:** One canonical document covering every critical input and output with its owner, monitoring method, frequency, and response rule.

**Text Diagram:**
```text
 CTQ / Metric  | Type  | Spec / Target  | Monitor    | Freq    | Owner  | Response
───────────────┼───────┼────────────────┼────────────┼─────────┼────────┼─────────────────
 p95 latency   | Out Y | ≤ 180 ms       | Grafana    | 1 min   | SRE L2 | Page if > UCL 3×
 CTR           | Out Y | ≥ 8%           | Looker     | Daily   | PM     | Open Jira if drift
 Feature drift | In X  | PSI ≤ 0.1      | Evidently  | Daily   | ML Eng | Alert + retrain gate
 SOP adherence | Proc  | ≥ 95%          | Audit      | Monthly | Ops    | Retrain team on miss
```

Axes / Quadrants / Components explained:
- CTQ: Critical to Quality — a metric that materially affects the customer or business.
- Type: input X, output Y, or process adherence.
- Monitor: tool + query/dashboard link.
- Frequency: matched to the drift rate of that metric.
- Owner: named individual (not a team).
- Response: exactly what happens on a breach, pre-written.

IT/AI/Product/Consulting worked example: A fintech's KYC improvement project closes with a 14-row control plan. Each row names a tool (Grafana, Looker, Evidently, Jira), a frequency, and a response playbook. The plan is stored in Confluence and linked from the team's weekly ops review agenda.

When to pull this out in a meeting: during project close-out, or anytime someone says "we already improved that" about a metric currently drifting.

### Response Plan Decision Tree
**Purpose:** Pre-wire the team's reaction to a control-chart signal so the response is fast and unambiguous.

**Text Diagram:**
```text
Signal detected ?
      │
      ▼
Is it a single special-cause breach (1 point > UCL/LCL)?
   ├── Yes → Page owner, snapshot context, run 5-Why within 24h
   └── No
      ▼
Is it a run of 8 points on one side of centre line?
   ├── Yes → Investigate for mean shift (upstream change, seasonality)
   └── No
      ▼
Is it a trend of 6 consecutive points rising or falling?
   ├── Yes → Investigate for drift (model decay, configuration rot)
   └── No
      ▼
Continue monitoring — common-cause variation only.
```

Axes / Quadrants / Components explained:
- Node 1 — single breach = acute issue; immediate response.
- Node 2 — run = sustained shift; investigate environment change.
- Node 3 — trend = gradual drift; investigate slow-moving causes (model staleness, tech debt).
- Terminal leaf — in control; no action beyond logging.

IT/AI/Product/Consulting worked example: An SRE dashboard for checkout p95 latency throws a 6-point rising trend (not a breach). The decision tree routes to trend-investigation → infra lead notices autoscaler cooldown increased after a config merge; fix reverts metric before it hits UCL.

When to pull this out in a meeting: after every Improve-phase close so the process owner has a written reaction plan rather than "we'll figure it out".

### Poka-Yoke Error-Proofing Hierarchy
**Purpose:** Choose the strongest error-proofing level that is feasible, in priority order.

**Text Diagram:**
```text
Strongest ── 1. ELIMINATE        (remove the step that allows the error)
             2. PREVENT          (make the error physically/logically impossible)
             3. DETECT + BLOCK   (catch the error and stop the process)
             4. DETECT + WARN    (catch the error and alert a human)
             5. MITIGATE         (accept some errors, minimise damage)
Weakest
```

Axes / Quadrants / Components explained:
- Ranked by robustness — higher levels are better, but cost more to implement.
- Prefer the highest level feasible given constraints.
- Each level has a standard IT/AI/Product pattern.

IT/AI/Product/Consulting worked example: A billing bug keeps recurring because one endpoint accepts negative quantities. Level 1 would be removing that endpoint (infeasible due to external consumers). Level 2 = enforce schema validation at the API gateway, rejecting negatives before they reach the database — chosen. Level 3 would be a DB-side constraint as belt-and-braces. Decision: Level 2 + Level 3 layered; Level 4 alerting kept for the first 30 days to confirm no legitimate use was blocked.

When to pull this out in a meeting: whenever "we'll add a monitor for it" is proposed as the fix — push to a stronger level if feasible.

---

## 4. Formulas

The source does not provide equations. The following are the standard Control-phase mathematics [verified from model knowledge, not source], with IT/AI/Product/Consulting decision thresholds.

### Formula 1: Control Limits (Individuals Chart)
**Formula:** `UCL = X̄ + 3σ; LCL = X̄ − 3σ`, where σ is estimated from `MR̄ / 1.128` (average moving range divided by d₂ for n = 2).

**Variables:**
- `X̄` = mean of the Y metric over the baseline window.
- `MR̄` = mean moving range between consecutive observations.
- `1.128` = d₂ constant for subgroup size 2 (individuals chart).

**Why this formula exists:** Gives a statistically defensible boundary between normal and abnormal variation so the team does not react to noise.

**How to interpret the output:**
- Point outside UCL/LCL → special-cause; investigate now.
- 8 consecutive points on one side of CL → mean shift; investigate environment change.
- 6 consecutive points rising/falling → drift; investigate slow-moving causes.
- Otherwise → in-control, no action.

**Worked example:** API p95 latency, weekly observations for 12 weeks: X̄ = 150 ms, MR̄ = 10 ms → σ ≈ 8.87 ms. UCL ≈ 176.6 ms, LCL ≈ 123.4 ms. A reading of 182 ms in week 13 is a special cause — page the SRE owner and investigate.

### Formula 2: Process Capability — Cp and Cpk
**Formula:**
`Cp = (USL − LSL) / (6σ)`
`Cpk = min[(USL − μ) / (3σ), (μ − LSL) / (3σ)]`

**Variables:**
- `USL, LSL` = upper and lower specification limits (customer/business requirements).
- `μ, σ` = process mean and standard deviation.

**Why this formula exists:** Answers "can the process consistently stay inside spec?" with a single number, and whether the issue is spread or off-centering.

**How to interpret the output:**
- Cpk < 1.0 → process cannot meet spec; go back to Analyze/Improve.
- 1.0 ≤ Cpk < 1.33 → marginally capable; tighten controls, add response plan.
- 1.33 ≤ Cpk < 1.67 → capable; standard monitoring is enough.
- Cpk ≥ 1.67 → highly capable; reduce audit cadence, consider raising the bar.

**Worked example:** SLA target for ticket ack time is ≤ 15 min (USL = 15, no LSL since faster is always better, so use one-sided Cpk). μ = 9 min, σ = 2 min. Cpk = (15 − 9) / 6 = 1.0 → marginally capable. Decision: tighten Improve (reduce σ) before declaring done.

### Formula 3: Defects Per Million Opportunities (DPMO) & Sigma Level
**Formula:**
`DPMO = (defects / (opportunities per unit × units)) × 1,000,000`
Sigma level → DPMO mapping (short-term; table):
- 3σ ≈ 66,807 DPMO
- 4σ ≈ 6,210
- 5σ ≈ 233
- 6σ ≈ 3.4

**Variables:**
- `defects` = count of units outside specification.
- `opportunities per unit` = number of chances for a defect per item (e.g., fields on a form).
- `units` = total items processed in the window.

**Why this formula exists:** Normalises quality across wildly different processes so "is this actually good?" has a comparable answer.

**How to interpret the output:**
- DPMO > 66,807 (< 3σ) → weak process; keep Improve open.
- 6,210–66,807 (3σ–4σ) → industry-average; continuous improvement next cycle.
- 233–6,210 (4σ–5σ) → strong; reduce controls where cost-justified.
- < 233 (> 5σ) → world-class; watch for over-engineering cost.

**Worked example:** A billing system processes 1,200,000 invoices in a quarter with ~3 error-prone fields each. 420 errors found. DPMO = 420 / (3 × 1,200,000) × 1,000,000 ≈ 117 → between 5σ (233) and 6σ (3.4) → strong. Decision: reduce audit cadence from weekly to monthly; redeploy auditor time to the next project.

### Formula 4: Process Stability Ratio
**Formula:** `Stability = σ_within-subgroup / σ_total`

**Variables:**
- `σ_within-subgroup` = short-term variation (variation within a single shift/day/sprint).
- `σ_total` = long-term variation (all data pooled).

**Why this formula exists:** If long-term variation is much larger than short-term, the process has drifts that short-term monitoring will miss.

**How to interpret the output:**
- Ratio ≈ 1.0 → process is stable; short-term monitoring is enough.
- 0.7–1.0 → some drift; add weekly rolled-up checks to daily.
- < 0.7 → significant drift; consider CUSUM or EWMA charts for earlier detection.

**Worked example:** A model's accuracy σ_within-day = 0.3 pt; σ_total over 12 weeks = 0.9 pt → ratio = 0.33. Highly drifty. Decision: add a weekly CUSUM-based alert in addition to the daily dashboard; plan quarterly retrains.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|------|
| Close the project after handing off a slide deck summarising improvements. | Close only after a signed Control Plan exists in Confluence with owners, monitors, frequencies, and response rules. |
| Set control limits by eyeballing "what looks normal" on a dashboard. | Compute UCL/LCL from the post-improvement baseline using X̄ ± 3σ (or tighter if drift is catastrophic). |
| React to every single dashboard data point that feels unusual. | Use the Response Plan Decision Tree — only act on special-cause signals (breach / run / trend). |
| Let the project team own the process indefinitely "because they know it best". | Transfer ownership to a named process owner with 90-day stability criteria before the team disbands. |
| Write SOPs once and assume they will stay current. | Set an audit cadence (monthly or quarterly) with a named auditor and a non-conformance response. |
| Monitor only output metrics (Y) and assume inputs (X) are fine. | Include critical X variables in the Control Plan — drift shows up earlier in X than in Y. |
| Rely on dashboards alone — "if no one looks, it does not exist". | Pair dashboards with push alerts (PagerDuty, Slack, email digests) tied to the response plan. |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: AI model in production — controlling accuracy drift
**Situation:** An ML team has improved a fraud-detection model from 86% to 92% precision. They want to "close the project and ship to other squads". Accuracy typically decays in 6–10 weeks due to changing fraud patterns.
**Applicable framework/metric:** Shewhart Individuals Control Chart + Process Stability Ratio + Control Plan Matrix.
**Analysis:** Baseline: μ = 92%, σ_within-week = 0.4 pt (10 batches/week), σ_total over 8 weeks = 1.2 pt → Stability ≈ 0.33 (highly drifty). Recommend CUSUM in addition to Shewhart. Shewhart UCL/LCL at 92 ± 3·0.4 = 93.2 / 90.8 (weekly). Control plan rows: (a) weekly precision, (b) daily input-feature PSI (Evidently), (c) hourly volume, (d) monthly SOP audit on alert triage.
**Decision rule:** If weekly precision < LCL OR PSI > 0.1 on any top-10 feature OR 4-point downward trend → trigger retrain gate; owner = ML Eng Manager. If accuracy back within limits in 2 weeks after fix → close the incident; else re-open Improve.
**Action (Monday):** (a) Write control plan in Confluence with 12 rows; (b) wire Evidently alerts to Slack #ml-alerts; (c) set retrain checkpoint every 4 weeks regardless; (d) pick a named process owner; (e) schedule 90-day post-handoff review.
- Data sources used: Evidently (drift), Snowflake (labels), Grafana (volume), Confluence (plan), PagerDuty (alerts).

### Scenario 2: Consulting engagement — telecom billing error control (close-out)
**Situation:** Post-Improve, billing errors dropped from 1.2% to 0.3%. Client wants to sign off and reassign the project team. Historically, their improvement gains decay within 6 months after consultants leave.
**Applicable framework/metric:** DPMO + Cpk + Response Plan Decision Tree.
**Analysis:** 0.3% of 1.2M monthly invoices with 3 error-prone fields each = DPMO ≈ 833 → ~4.5σ. Cpk (spec = 0.5% max error rate) = (0.5 − 0.3) / (3 × 0.08) = 0.83 — not yet capable. Decision tree wired with three signals: breach (daily > 0.5%), 8-point run above 0.3% weekly, 6-point rising trend.
**Decision rule:** Close only when (a) Cpk ≥ 1.33 for two consecutive months AND (b) signed Control Plan in client's Confluence AND (c) process owner named with KR/OKR coverage. Otherwise extend the engagement by 4 weeks.
**Action (Monday):** (a) Tighten σ via additional Poka-Yoke (API-level schema validation); (b) set up weekly control chart in client's Looker; (c) run a tabletop drill of the response plan before sign-off; (d) 30- and 90-day post-handoff check-in in the statement of work.
- Data sources used: client's ServiceNow (incidents), Looker (chart), Confluence (plan), Slack (alerts).

### Scenario 3 (ANTI-EXAMPLE): Product team — dashboard theatre
**Situation:** A PM closes a performance-improvement project by "standing up a dashboard in Looker" and declaring the Control phase complete. No owner, no alerts, no response plan. Six months later, p95 latency has quietly crept from 150 ms to 240 ms, SLA breaches appear, and an enterprise customer escalates.
**Applicable framework/metric:** Control Plan Matrix + Response Plan Decision Tree + Shewhart chart.
**Analysis (what went wrong):** The dashboard showed the drift weeks before the breach, but nobody was alerted, nobody owned it, and no response rule existed. The Control phase existed only in theatre.
**Decision rule that should have applied:** A dashboard without (a) named owner, (b) computed UCL/LCL, (c) push alerts tied to a response plan, (d) monthly audit cadence — is not Control.
**Wrong decision shipped and its cost:** 4 SLA-breach incidents over 3 months; two enterprise renewals at risk; ~₹1.8 Cr in service credits and one churn. A proper Control Plan with PagerDuty on UCL breach would have caught the drift in week 3 at < ₹10 L cost.
**Correct action (had the framework been applied):** 8-row Control Plan with owner, Looker chart with UCL/LCL, PagerDuty on breach + Slack digest on trend, monthly audit cadence with non-conformance counter.
- Data sources used: Looker (dashboard), PagerDuty (alerting), Jira (non-conformance log).

---

## 7. Implementation Playbook

1. **Compute UCL/LCL from the post-Improve baseline** (minimum 20 data points) and document them in the Control Plan with the formula used.
2. **Write the Control Plan Matrix in Confluence** with columns: CTQ, spec/target, monitor tool, frequency, owner, response rule — every row signed off by the named owner.
3. **Wire production alerts in PagerDuty / Opsgenie / Slack** tied to each control signal — breach, run, trend — with routing to the owner.
4. **Build the monitoring chart in Looker / Grafana / Datadog** with the CL, UCL, and LCL rendered as horizontal lines, not just a raw time series.
5. **Update the SOP / runbook** with the new process and store it alongside the Control Plan; set a review cadence (quarterly).
6. **Run a tabletop drill of the response plan** before formal handoff — simulate a breach and time the reaction.
7. **Formally transfer ownership** with a signed handoff document, including 30- / 60- / 90-day post-handoff review dates.
8. **Schedule a 90-day post-close-out review** in the calendar of every stakeholder; if the gains have held (Cpk stable or improved), archive the project; if not, reopen Improve.

---

## 8. Content Quality Audit

- **Covered well:** The source correctly identifies the four Control-phase outputs — SOP, control charts, response plan, process owner — and uses the telecom billing scenario to illustrate why Control matters.
- **Underplayed or missing:**
  - **Control-chart interpretation rules** (Western Electric, Nelson) are not mentioned — teams then react to noise or miss runs/trends.
  - **Process capability (Cp / Cpk)** and **DPMO / sigma level** are core Six Sigma metrics but absent here.
  - **Poka-Yoke / error-proofing** receives no mention, yet it is the single highest-leverage Control technique for IT and product work.
  - **Input (X) monitoring** is skipped — the source implies Y-only monitoring, which detects problems after customers feel them.
  - No modern equivalents — **SPC in software** (SRE SLOs, error budgets, feature-flag alerting, ML model drift tools) is absent.
  - **Handoff protocols** (named owner, 90-day stability, retirement criteria) are hinted at but not operationalised.
- **Supplement with:**
  - *Statistical Quality Control* — Douglas C. Montgomery, 8th ed. (2019), for rigorous control-chart theory and capability indices.
  - *Site Reliability Engineering* — Betsy Beyer et al., O'Reilly (2016), specifically Chapter 4 (Service Level Objectives) — the software analogue of Six Sigma Control.
  - "The Checklist Manifesto" — Atul Gawande (2009) — for why SOPs and response plans work even with experts.
  - "Machine Learning: The High-Interest Credit Card of Technical Debt" — D. Sculley et al., *NeurIPS 2014* — on why ML Control phases must be stronger than classical Control.
  - HBS case "Toyota Motor Manufacturing, USA, Inc." (HBS 693-019) — for the definitive treatment of process ownership, drift response, and stop-the-line culture.
- **Red flags in the source:**
  - "Control chart" is defined without any mention of the interpretation rules, leaving students unable to read one.
  - The telecom scenario claims a 75% reduction and then a response-plan catch, but gives no detail on who was alerted, by what mechanism, or what thresholds triggered the response — which is the entire point of Control.
  - The food-processing use case is the only one with real-time monitoring — the others describe manual audits with month-long lags, which is closer to governance than control in a modern IT context.

---

## 9. Quick-Recall Card

Control = lock the Improve gains by turning the new process into monitored, owned standard work.
Toolkit: Shewhart chart (with UCL/LCL), Control Plan Matrix, Response Plan Decision Tree, Poka-Yoke.
Signal rules: single breach, 8-point run, 6-point trend — each has a pre-written response.
Capability: track Cp/Cpk and DPMO / sigma level; monitor Xs, not only Ys.
Handoff: named owner, signed Control Plan, 30/60/90-day reviews — no theatre dashboards.
**As a PM/Consultant/AI Lead, the one question to answer with this framework is:** *If I disappear tomorrow, who gets paged when this process drifts, and what is the written action they take in the first 15 minutes?*

---

**Connects to:** [05-analyze-phase.md](05-analyze-phase.md), [06-improve-phase.md](06-improve-phase.md), [09-statistical-process-control.md](09-statistical-process-control.md) (once audited), [10-process-capability-analysis.md](10-process-capability-analysis.md) (once audited), and [../business-analytics/10-operations-analytics.md](../business-analytics/10-operations-analytics.md) for the dashboard/alerting side.

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Sections rewritten: [Section 6 anti-example sharpened with quantified cost; Section 9 tightened to 6 lines]
Enrichments applied: [cross-course links to analyze-phase, improve-phase, SPC, capability analysis, operations-analytics; 5 named supplements with author+year; anti-example (dashboard theatre) with quantified cost; IT-org tooling (PagerDuty, Grafana, Looker, Evidently, ServiceNow) across scenarios; role-lens question closes Section 9]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 20:58
Audited by: A1
-->
