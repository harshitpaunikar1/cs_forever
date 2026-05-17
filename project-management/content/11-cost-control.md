# Cost Control

## Overview

Cost control is the ongoing work of keeping project spend within the approved budget. It covers estimating, tracking actual spend, forecasting what's left, and deciding what to do when costs drift. It is done throughout the project, not only at the end.

---

## Why It Matters

Running over budget destroys margin, breaks customer contracts, and can get projects cancelled mid-flight. Tight cost control gives the team room to respond to problems without surprising the finance team. It also builds the PM's credibility with leadership.

## Key Principles

- Break the budget into categories small enough to manage.
- Track commitments, not just paid invoices.
- Compare forecast-at-completion to budget every week.
- Require approval for any variance beyond a set threshold.
- Separate scope changes from overruns in your reporting.

## Key Terms

| Term | Definition |
|------|------------|
| **Budget** | The approved total funding for the project. |
| **Cost Variance** | The difference between planned cost and actual cost. |
| **Burn Rate** | How fast the project is spending money, usually per month. |
| **Estimate at Completion (EAC)** | The expected final cost based on current performance. |

## Use Case

A research lab runs a 12-month grant-funded project. The PM splits the budget into salaries, equipment, travel, and contingency, and reviews burn rate monthly with the finance officer to avoid end-of-grant surprises.

## Scenario

> A construction project reported 70% budget spent at 50% progress and raised no flag. The new PM introduced weekly EAC reviews; the overrun was spotted early enough to renegotiate one subcontract and the project closed within 4% of original budget.

## Examples

- A software PM tracks cloud-compute spend daily and alerts on any 20% day-over-day jump.
- An event PM freezes all non-essential spend once 85% of the budget is committed.

---

## Audited Appendix

# Cost Control
**Course:** Project Management
**Module:** Content / Cost Control
**Audited on:** 2026-04-18
**Source files reviewed:** `project-management/content/11-cost-control.md`

---

## 1. Topic Snapshot
Cost control = ongoing budget stewardship: estimate → track → forecast → respond. For an IT/AI/Product/Consulting leader, this is the discipline that prevents "70% spent at 50% progress" silent disasters. Decision it helps make: *"At this moment, can I say — with EAC math — what the project will actually cost, and which line items are driving the variance?"*

Cross-reference: EVM in `01-project-management-principles.md`; financial analytics in `business-analytics/11`; reserves in `07-risk-management.md`.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Budget / BAC | Budget at Completion | Approved total | Anchor | $ | PMBOK |
| Cost Baseline | — | Time-phased approved budget | Measurement anchor | $ over time | PMBOK |
| Cost Variance | CV | EV − AC | Over/under | $ | EVM |
| Cost Performance Index | CPI | EV / AC | Efficiency ratio | > 1 under-budget | EVM |
| Schedule Performance Index | SPI | EV / PV | Schedule efficiency | > 1 ahead | EVM |
| Burn Rate | — | Spend per period | Pace | $ / month | Finance |
| Run Rate | — | Annualised burn | Extrapolation | $ / year | Startups |
| Estimate at Completion | EAC | Forecast final cost | Forward-looking | Multiple methods | EVM |
| Estimate to Complete | ETC | Remaining cost | Forward | $ | EVM |
| To-Complete Performance Index | TCPI | Efficiency needed to meet budget | Diagnostic | Ratio | EVM |
| Variance at Completion | VAC | BAC − EAC | Final surplus/deficit | $ | EVM |
| Contingency Reserve | — | For known risks | See Topic 07 | % of budget | PMBOK |
| Management Reserve | — | For unknown unknowns | Exec-controlled | % of budget | PMBOK |
| Commitment | — | Signed PO before invoice | Includes future pay | $ | Procurement |
| Actual Cost | AC | Cost incurred | Invoiced + paid | $ | EVM |
| Earned Value | EV | Budgeted cost of completed work | Progress in $ | $ | EVM |
| Planned Value | PV | Budgeted cost of scheduled work | Plan | $ | EVM |
| Cost of Delay | CoD | $ lost per period of delay | See `product-management-npd/15` | $ / period | Lean |
| FinOps | — | Cloud-cost management discipline | Modern SW | $ per service | DevOps |
| Cost Account | — | WBS-level cost tracking unit | Aggregation | $ per account | PMBOK |
| Accrual vs Cash | — | Accounting method differences | Reporting | Accounting standard | Finance |
| Zero-Based Budgeting | ZBB | Rebuild from zero | Cost discipline | % re-justified | Finance |
| Variance Approval Threshold | — | $ / % limit above which approval needed | Change control | Threshold | PM |

> Most extensions beyond source-named four are standard. `[verified from model knowledge, not source]`.

---

## 3. Frameworks & Matrices

### Framework 1: EVM Forecasting Cube
**Purpose:** Multiple EAC formulas for different assumptions about how the rest of the project will behave.

**Text Diagram:**
```
 Assumption                       │ EAC Formula
 ─────────────────────────────── ─┼──────────────────────────────
 Atypical variance (one-off)      │ EAC = AC + (BAC − EV)
                                  │ (remaining work at planned rate)
 Typical variance continues        │ EAC = BAC / CPI
                                  │ (cost-performance stays the same)
 Both cost AND schedule pressure  │ EAC = AC + (BAC − EV) / (CPI × SPI)
                                  │ (worst case)
 Bottom-up re-estimate             │ EAC = AC + new ETC
                                  │ (most reliable but most work)

 Report all 3 EAC variants when CPI or SPI < 0.9.
```

Components:
- 4 EAC formulas
- Atypical = best case; ongoing = typical; combined = worst
- Bottom-up re-estimate is gold standard when in trouble

**IT/AI/Product/Consulting worked example:** BAC $5M; month 3: PV $1.5M, EV $1.3M, AC $1.7M. CPI 0.76; SPI 0.87.
- Atypical: EAC = 1.7 + (5 − 1.3) = $5.4M
- Typical: EAC = 5 / 0.76 = **$6.6M**
- Combined: EAC = 1.7 + (5−1.3)/(0.76×0.87) = 1.7 + 5.6 = **$7.3M**

Recommendation to exec: plan for $6.6M baseline; reserve $800k for worst-case. Bottom-up re-estimate at next milestone.

**When to pull this out in a meeting:** Monthly cost reviews; board updates on struggling projects.

---

### Framework 2: Cost Variance Categorisation
**Purpose:** Separate scope changes, price changes, volume changes, and pure overruns — each has different remediation.

**Text Diagram:**
```
 Variance type     │ Cause                                    │ Response
 ────────────────┼──────────────────────────────────────────┼──────────────
 Scope change       │ Added scope (through CCB)                │ Update baseline
 Price change       │ Input cost ↑ (vendor raise, FX)          │ Re-negotiate or absorb
 Volume change     │ More units than planned                  │ Investigate + adjust
 Productivity       │ Team slower than estimated                │ Unblock or add resource
 Quality rework     │ Defects found late                       │ Apply QC lessons
 Risk materialised │ Known risk from register                  │ Use contingency reserve
 Unknown unknown   │ Surprise                                  │ Use management reserve
```

Components:
- Variance decomposition → right remediation
- Separates "we underestimated" from "the world changed"

**IT/AI/Product/Consulting worked example:** Software project $200k over budget. Breakdown:
- Scope change (CCB-approved): $80k (rebase budget)
- Vendor price increase: $40k (absorb with reserve)
- Team productivity: $50k (unblock dep)
- Rework: $30k (QC process fix)

Not all $200k is "bad" — 40% is scope; 20% external; 15% vendor pricing.

**When to pull this out in a meeting:** Every cost-variance report; avoiding the "why are we over budget" blame game.

---

### Framework 3: Variance Response Ladder
**Purpose:** Graded response based on variance severity.

**Text Diagram:**
```
 Cumulative Variance         │ Response
 ──────────────────────────┼───────────────────────────────────
 < 5%                         │ Monitor; no action                
 5–10%                        │ PM investigates; log causes       
 10–15%                       │ Report + action plan; team review
 15–20%                       │ Steering committee briefing      
 > 20%                        │ Re-baseline OR kill consideration
```

Components:
- Thresholds for escalation
- Discipline against "we'll catch up"

**IT/AI/Product/Consulting worked example:** Variance 14% at month 4. Threshold triggers steering briefing. PM presents EAC forecast, causes, and proposed plan: two-week replan + additional contractor. Steering approves; re-baseline scheduled.

**When to pull this out in a meeting:** Monthly cost reviews; whenever variance is creeping.

---

## 4. Formulas

### Formula 1: TCPI (To-Complete Performance Index)
**Formula:** `TCPI = (BAC − EV) / (BAC − AC)` — performance needed to finish at BAC
Alternate: `TCPI = (BAC − EV) / (EAC − AC)` — performance needed to finish at EAC

**Why this formula exists:** Tells you how efficient the remaining work must be.

**How to interpret the output:**
- TCPI > 1.1 → cost-efficiency needs to improve significantly
- TCPI > 1.5 → likely impossible; accept overrun or re-baseline

**Worked example:** BAC $5M; EV $1.3M; AC $1.7M. TCPI = (5 − 1.3)/(5 − 1.7) = 3.7/3.3 = **1.12**. Remaining work must be 12% cheaper than planned — tough but possible.

**Data source:** Project accounting + schedule data.

---

### Formula 2: Typical EAC (most-used forecast)
**Formula:** `EAC = BAC / CPI`

**Why this formula exists:** Assumes cost performance continues — conservative but realistic.

**How to interpret the output:**
- Compare to BAC → overrun $
- Use as baseline forecast unless strong evidence of atypical variance

**Worked example:** BAC $10M; CPI 0.85. EAC = 10/0.85 = **$11.76M**. Forecast overrun: $1.76M.

**Data source:** EVM metrics from project accounting.

---

### Formula 3: Burn Rate Projection
**Formula:** `Projected Total = Burn Rate × Remaining Duration + AC-to-date`

**Why this formula exists:** Simple extrapolation; independent of EVM.

**How to interpret the output:**
- Compare to BAC + reserve
- If > 110% of BAC → escalate

**Worked example:** Project spent $2M in 10 weeks = $200k/week. 20 weeks remaining → projected $2M + $4M = $6M total. If BAC is $5M → $1M (20%) overrun projected.

**Data source:** Finance weekly burn report.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|-------|
| Track only paid invoices | Track commitments (signed POs) — forward view |
| Report variance without categorising | Use Variance Category matrix |
| Use single EAC formula | Report multiple EAC variants when in trouble |
| Wait for month-end to react | Weekly cost reviews; daily for cloud-compute |
| Hide bad news until you "figure it out" | Early transparency beats late surprises |
| Dip into management reserve casually | Reserve requires exec approval |
| Treat cloud costs as "ops problem" | FinOps = shared engineering + finance responsibility |
| Lump scope changes with overruns | Separate reporting lines |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: Construction Project 70% Spent at 50% Progress
**Situation:** Construction PM reports 70% budget spent at 50% progress; no flag raised.

**Applicable framework/metric:** EVM + EAC Typical + Response Ladder.

**Analysis:**
- PV 50%; EV 50%; AC 70% → CPI 0.71
- EAC Typical = BAC / 0.71 = 141% of BAC → 41% overrun
- Variance 40% breaches all thresholds → steering committee now

**Decision rule:** CPI < 0.9 for 2 periods = mandatory intervention.

**Action (Monday morning):** Weekly EAC tracking; renegotiate largest subcontract; steering briefing within 48 hours.

---

### Scenario 2: Consulting Client with Cloud Cost Blowup
**Situation:** SaaS client cloud-compute bill 3× forecast after ML feature launch.

**Applicable framework/metric:** FinOps + Variance Categorisation.

**Analysis:**
- Volume change (usage up); productivity (inefficient models); vendor pricing (reserved capacity not used)
- Install daily cost dashboards + alert on 20% day-over-day jumps
- Right-size; use spot; commit to reserved capacity

**Decision rule:** Cost variance > 20% triggers FinOps review within 48 hours.

**Action:** FinOps review; model right-sizing; reserved-capacity commitments; alerts in Datadog.

---

### Scenario 3 (Anti-example): Single EAC Formula Misleads
**Situation:** PM uses only atypical EAC (assumes one-off variance) and reports $10.4M. Reality uses typical: $12.6M. Exec blindsided.

**Analysis (what goes wrong):**
- One-off atypical assumption invalid (variance is systemic)
- Forecast understated ~$2M
- Planning built on wrong number

**Cost of this mistake:** Budget overrun not provisioned; painful mid-year reset.

**Decision rule:** When CPI < 0.9, report all 3 EAC variants with the recommended one flagged.

**Action:** Re-forecast; present three scenarios to exec; escalate appropriately.

---

## 7. Implementation Playbook

1. **Weekly EVM + multiple EAC variants** — especially when CPI < 0.9.
2. **Variance category breakdown** — every report; show root causes.
3. **Threshold-based escalation ladder** — defined upfront.
4. **Commitment tracking** — includes signed POs + approved contracts.
5. **FinOps for cloud-heavy products** — daily cost alerts.
6. **Monthly finance-PM sync** — reconcile burn + EVM.
7. **Reserve drawdown discipline** — track usage; management reserve requires exec.
8. **Post-project cost retro** — what was over / under / on.

---

## 8. Content Quality Audit

**Covered well:**
- Names budget, variance, burn rate, EAC.
- Notes weekly reviews, approval thresholds.
- Good construction scenario.

**Underplayed or missing:**
- No EAC formula variants.
- No TCPI.
- No variance categorisation.
- No FinOps reference.

**Supplement with:**
- PMBOK — Cost chapter.
- *Earned Value Management* — Quentin Fleming & Joel Koppelman (3rd ed 2010).
- *Cloud FinOps* — Storment & Fuller (2nd ed 2023).
- HBR: "A Short Guide to Earned Value" — various.
- HBS case: "Sydney Opera House" — cost-overrun classic.
- HBS case: "Big Dig Boston" — megaproject cost.
- IIMA case: "Bangalore Metro Cost Management" — Indian-context.

**Red flags in the source:**
- EAC named but not formula-operationalised.
- No variance category.
- No FinOps for modern software.

**Connects to:**
- `audit_management_course/project-management/01-project-management-principles.md`
- `audit_management_course/project-management/07-risk-management.md`
- `audit_management_course/project-management/09-performance-tracking.md`
- `audit_management_course/business-analytics/11-financial-analytics.md`
- `audit_management_course/product-management-npd/15-time-to-market-reduction.md`

---

## 9. Quick-Recall Card

```
Topic: Cost Control
Core idea: Weekly EVM + multiple EAC variants + variance categorisation beats month-end surprises.
Key metric/formula: EAC variants; TCPI = (BAC−EV)/(BAC−AC); Typical EAC = BAC/CPI.
Framework trigger: Monthly cost review; cloud blowup; variance > 10%.
Watch out for: Paid-invoice-only tracking; single EAC; uncategorised variance.
Monday action: Compute multi-variant EAC; install weekly EVM; categorise current variance.
As a PM/Consultant/AI Lead, the one question to answer with this framework is:
"What's my honest EAC — and which slice of the variance do I attack first?"
```

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Pass 1 average: 4.8
Sections rewritten: none
Enrichments applied: [cross-course links; PMBOK, Fleming/Koppelman 2010, Storment/Fuller FinOps 2023. HBS Sydney Opera House + Big Dig, IIMA Bangalore Metro. Anti-example (single EAC misleading). Decision-maker view.]
Final scores: all 5/5 — average 5.0
Pass 2 completed: 2026-04-18 04:05
-->
