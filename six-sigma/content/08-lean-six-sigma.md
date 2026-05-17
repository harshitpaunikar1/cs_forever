# Lean Six Sigma

## Overview
Lean Six Sigma combines the waste-elimination focus of Lean manufacturing with the variation-reduction power of Six Sigma. Lean targets speed and efficiency by removing activities that do not add value, while Six Sigma targets quality by reducing defects and variation. Together they provide a comprehensive toolkit for making processes faster, cheaper, and more consistent.

---

## Why It Matters
Lean alone can make a process faster but may not reduce defects. Six Sigma alone can reduce defects but may not address inefficiency or waste. By combining both methodologies, organizations get the best of both worlds. Lean Six Sigma is especially valuable in complex environments where processes suffer from both excessive waste and high defect rates, such as healthcare, financial services, and supply chain operations.

## Key Principles
- Eliminate the eight types of waste to streamline process flow
- Reduce variation to improve quality and predictability
- Let customer value define which activities are necessary and which are waste
- Use value stream mapping to see the entire process before making changes

## Key Terms
| Term | Definition |
|------|------------|
| **Waste (Muda)** | Any activity in a process that consumes resources but does not add value from the customer's perspective |
| **Value Stream Mapping** | A visual tool that maps every step in a process to identify value-adding and non-value-adding activities |
| **Kaizen** | A philosophy of continuous, incremental improvement involving all employees |
| **5S** | A workplace organization method consisting of Sort, Set in Order, Shine, Standardize, and Sustain |

## Use Case
A distribution center applies Lean Six Sigma to reduce order fulfillment time by eliminating unnecessary handling steps and reducing picking errors simultaneously.

## Scenario
> A hospital emergency department suffers from both long patient wait times and frequent medication errors. The team uses value stream mapping to identify wasted steps in the triage process and Six Sigma tools to reduce prescription mistakes. Within four months, average wait time drops by 35% and medication errors fall by 60%.

## Examples
- An automotive supplier uses 5S to organize its shop floor and then applies Six Sigma to reduce dimensional variation in stamped parts, cutting rework costs by 45%
- A bank combines Lean process mapping with Six Sigma statistical analysis to reduce mortgage approval time from three weeks to five days while also cutting documentation errors

---

## Audited Appendix

# Lean Six Sigma
**Course:** Six Sigma
**Module:** Content / Lean Six Sigma
**Audited on:** 2026-04-18
**Audited by:** A1
**Source files reviewed:** `six-sigma/content/08-lean-six-sigma.md`

---

## 1. Topic Snapshot
Lean Six Sigma fuses two disciplines: Lean (remove waste, maximise flow) and Six Sigma (reduce variation, cut defects).
For an IT/AI/Product/Consulting leader, it is the toolkit used when a process is simultaneously slow *and* unreliable — a common pattern in incident response, ML pipelines, and multi-handoff service delivery.
The decision it helps make: where to cut waste first (Lean levers) versus where to chase variance (Six Sigma levers), and in what sequence.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Lean | - | A discipline focused on eliminating activities that do not add customer value (waste). | Processes accumulate waste silently; naming it surfaces it. | Lead time, cycle time, process efficiency %. | Manufacturing, software delivery, consulting. |
| Six Sigma | - | A discipline focused on reducing variation and defects using statistics. | Averages lie; variance is what customers feel. | DPMO, σ-level, Cp/Cpk. | Quality, manufacturing, service ops. |
| Waste (Muda) | - | Any activity that consumes resource but adds no customer value. | The primary target of Lean. | Categorised count and time per type. | Lean, TPS, process re-engineering. |
| DOWNTIME | - | Eight wastes acronym: Defects, Overproduction, Waiting, Non-utilised talent, Transportation, Inventory, Motion, Extra-processing. | A memorable list beats "find all waste". | Time/cost per waste category. | Lean training, kaizen events. |
| Value Stream Map | VSM | A visual, end-to-end picture of every step (value-add + non-value-add) in a process, usually with timings. | Seeing the whole prevents local optimisation. | Lead time, process time, % value-add, queue time. | Lean, consulting, operations. |
| Kaizen | - | Philosophy of small, continuous, everyone-included improvements. | Big-bang transformations fail more often than they succeed. | # of kaizen events; before/after metric deltas. | Lean, operations, SRE rituals. |
| 5S | - | Workplace organisation method: Sort, Set in Order, Shine, Standardise, Sustain. | Clean, ordered workspaces reduce errors and search time. | 5S audit score, time-to-find metric. | Manufacturing, labs, IT runbook hygiene. |
| Takt Time | - | Rate at which work must be completed to meet demand. | Aligns process pace with customer rate. | Takt = available time / customer demand. | Manufacturing, agile capacity, DevOps. |
| Cycle Time | - | Time to complete one unit from start to finish of the work step. | Reveals the actual pace of work. | Stopwatch, timestamps. | Manufacturing, software, SRE. |
| Lead Time | - | Total time from request to delivery, including queues. | The customer-experienced number. | Request-to-deliver timestamp delta. | Supply chain, software, consulting. |
| Process Cycle Efficiency | PCE | Share of lead time spent on value-add activity. | Tells you how bloated the process is. | PCE = value-add time / total lead time. | Lean, consulting diagnostics. |
| Pull System | - | Work is pulled by downstream demand rather than pushed by upstream producers. | Prevents overproduction and WIP pile-up. | WIP limits, pull signals (kanban cards). | Lean, agile, DevOps (CI/CD queues). |
| Kanban | - | Visual workflow board with WIP limits per column. | Operationalises pull and surfaces bottlenecks. | WIP per column, throughput, cycle time. | Agile, DevOps, marketing ops. |
| Poka-Yoke | - | Error-proofing mechanism that prevents mistakes by design. | Prefers prevention over inspection. | Error rate before/after; near-miss count. | Lean, UX, SRE tooling. |
| Jidoka | Autonomation | Automation with a human touch — machines stop when an abnormality is detected. | Prevents bad output from propagating downstream. | Stop-the-line events, time to detect anomaly. | TPS, manufacturing, SRE (circuit breakers). |
| Continuous Flow | - | Work moves one unit at a time with minimal queuing. | Reduces WIP, cycle time, and variability. | Batch size, WIP count, throughput. | Lean, DevOps, ML pipelines. |
| Gemba Walk | - | Go-and-see visit to the place where work actually happens. | Decisions based on the shop floor beat decisions from conference rooms. | Gemba frequency; # of observations logged. | Lean, consulting, ops reviews. |

---

## 3. Frameworks & Matrices

### The Eight Wastes (DOWNTIME)
**Purpose:** A checklist that forces teams to find every type of waste, not just the most visible one.

**Text Diagram:**
```text
D - DEFECTS                : rework, bug fixes, refunds, retries, re-approvals
O - OVERPRODUCTION         : building features/reports/models no one reads
W - WAITING                : queues, handoffs, approval delays, CI pipeline stalls
N - NON-UTILISED TALENT    : senior engineers doing manual triage; analysts copy-pasting
T - TRANSPORTATION         : passing data between systems/people repeatedly
I - INVENTORY              : backlog items, stale branches, unmerged PRs, WIP overload
M - MOTION                 : tool-switching, context-switching, hunting for info
E - EXTRA-PROCESSING       : over-engineering, redundant validations, gold-plating
```

Axes / Quadrants / Components explained:
- Each letter is a category of non-value-add activity the customer would refuse to pay for.
- Categories overlap — one root cause often creates waste in 3–4 categories.
- Goal is to reduce each category to the minimum feasible, not necessarily to zero.

IT/AI/Product/Consulting worked example: A product team audits its release process. Defects (5% hotfix rate), Overproduction (23% of shipped features have < 1% adoption at 90 days), Waiting (mean PR merge wait 4.2 days), Non-utilised talent (senior engineers doing release notes), Inventory (142 open PRs older than 14 days). Decision: attack Waiting first (highest customer-visible impact) with PR-review SLAs and automated reviewer assignment; attack Overproduction next by gating features behind an evidence-of-demand bar.

When to pull this out in a meeting: when someone argues the team is "too busy" — use DOWNTIME to show which category is consuming capacity.

### Value Stream Map (VSM)
**Purpose:** Put the entire process on one wall to see where time is actually spent, before any local optimisation.

**Text Diagram:**
```text
 Customer request                                                Customer delivery
       │                                                                   ▲
       ▼                                                                   │
  ┌────────┐   ┌─────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   │
  │ Intake │ ─▶│ Triage  │ ─▶│  Design  │ ─▶│   Build  │ ─▶│   Ship   │ ──┘
  └────────┘   └─────────┘   └──────────┘   └──────────┘   └──────────┘
  PT: 0.5 d     PT: 1 d        PT: 3 d         PT: 5 d        PT: 0.5 d     ← value-add time
  QT: 2 d       QT: 3 d        QT: 4 d         QT: 6 d        QT: 1 d       ← queue/wait time
                                                                             TOTAL LT = 26 d
                                                                             VA time = 10 d
                                                                             PCE = 38%
```

Axes / Quadrants / Components explained:
- Each box: a process step; PT = process time (value-add), QT = queue time (wait).
- Lead time (LT) = Σ(PT + QT); value-add time = Σ(PT); Process Cycle Efficiency = PT / LT.
- Arrows: flow and handoffs; each handoff is a risk for variation and waste.
- Symbols (in a full VSM): inventory triangles, push/pull arrows, information flows.

IT/AI/Product/Consulting worked example: A consulting firm maps a client's AI-use-case intake to delivery. Lead time 26 days, value-add time 10 days → PCE = 38%. Largest queue = Build step (6 days, due to shared GPU capacity). Decision: double GPU reservation for the top-2 use cases; target PCE 55% in 90 days.

When to pull this out in a meeting: before any sprint-level process change — always map the full stream first to avoid optimising a bottleneck into a new place.

### Lean vs Six Sigma Selector
**Purpose:** Decide which discipline's toolkit to reach for first, given the problem pattern.

**Text Diagram:**
```text
                        Variation / Defects (Y spread)
                               HIGH
                                │
                                │
          Six Sigma             │             Lean Six Sigma
       (hypothesis tests,       │           (VSM + SPC + DOE)
        regression, SPC)        │
                                │
   Waste / Flow ─────────────── +──────────────── Waste / Flow
      LOW                       │                      HIGH
                                │
           (Routine             │                 Lean
         monitoring)            │         (VSM, 5S, kanban,
                                │          pull, kaizen)
                                │
                               LOW
```

Axes / Quadrants / Components explained:
- Y-axis: magnitude of variation / defects in the output.
- X-axis: magnitude of waste / flow inefficiency.
- Quadrant choice tells you whether to open Lean tools, Six Sigma tools, or both.

IT/AI/Product/Consulting worked example: A SaaS incident-response process has mean MTTR = 47 min (target ≤ 30) AND σ(MTTR) = 22 min (target ≤ 8). Both waste and variance are high → Lean Six Sigma. Start with VSM to cut handoffs (Lean), then SPC and hypothesis tests to reduce variance within each retained step (Six Sigma). Target: MTTR 30 ± 6.

When to pull this out in a meeting: when a team debates whether to "Lean" or "Six Sigma" a problem — answer is usually "both, in sequence".

### 5S for Knowledge Work
**Purpose:** Apply workplace-organisation discipline to digital artefacts (repos, wikis, dashboards, runbooks).

**Text Diagram:**
```text
 1. SORT        — remove obsolete files, dashboards, runbooks, feature flags, branches
 2. SET IN ORDER — standard folder / naming / tagging scheme; one source of truth per artefact
 3. SHINE       — automated linters, dead-code removal, dashboard-usage audits
 4. STANDARDISE — templates (PR, RCA, ADR); shared style guides; pre-commit hooks
 5. SUSTAIN     — a named owner + cadence (quarterly repo hygiene sprint; monthly flag audit)
```

Axes / Quadrants / Components explained:
- Each step builds on the previous; skipping to Standardise without Sort is theatre.
- Each step has a measurable "after" state — number of flags retired, % dashboards with > 0 weekly viewers, mean PR template completion.

IT/AI/Product/Consulting worked example: A platform team runs a 2-week 5S on its monorepo: Sort removes 312 dead feature flags and 47 unused dashboards; Set in Order renames 23 services to `<domain>-<role>` standard; Shine retires 2.1M lines of unused code; Standardise introduces PR and RCA templates; Sustain assigns a hygiene owner and a quarterly sprint. Mean PR review time drops from 4.2 days to 1.6 days within a quarter.

When to pull this out in a meeting: when engineers complain "I can't find anything" or "we have five dashboards for the same metric".

---

## 4. Formulas

The source mentions VSM, 5S, kaizen, and DOWNTIME without equations. The formulas below are the standard Lean quantitative toolkit [verified from model knowledge, not source], with IT/AI/Product/Consulting decision thresholds.

### Formula 1: Process Cycle Efficiency (PCE)
**Formula:** `PCE = Value-Add Time / Total Lead Time × 100`

**Variables:**
- Value-Add Time = sum of step process times (customer would pay for these).
- Total Lead Time = Value-Add Time + Queue/Wait Time across all steps.

**Why this formula exists:** Quantifies bloat. High lead time with low PCE means the process is mostly waiting, not working — a Lean problem, not a Six Sigma one.

**How to interpret the output:**
- PCE < 10% → extremely waste-heavy; VSM and waiting-reduction are the first lever.
- 10–25% → typical for unoptimised office/service processes; Lean event will yield ~2× improvement.
- 25–50% → reasonable; squeeze waste further and pair with variance work.
- > 50% → well-optimised; next gain usually comes from Six Sigma variance reduction, not Lean.

**Worked example:** Mortgage approval process — PT = 3 hours, LT = 3 weeks = 120 hours. PCE = 3/120 = 2.5% → catastrophic. Decision: redesign the process around removing queues, not optimising any single step.

### Formula 2: Takt Time (Pace to Customer Demand)
**Formula:** `Takt = Available Work Time / Customer Demand`

**Variables:**
- Available Work Time = productive time in the window (e.g., 7.5 hr × 60 min = 450 min/day after breaks).
- Customer Demand = units needed in the same window.

**Why this formula exists:** Aligns team capacity with the rate at which demand arrives; exposes over- or under-capacity.

**How to interpret the output:**
- Cycle time > Takt → demand cannot be met; either reduce cycle time (Lean) or add capacity (expensive).
- Cycle time ≈ Takt → balanced; risky if variance is high.
- Cycle time < Takt by 10–20% → healthy buffer for variability.
- Cycle time << Takt → overcapacity; consider reassignment or scope expansion.

**Worked example:** Support team available 7.5 hr/day/agent × 6 agents = 2,700 min/day. Tickets/day = 300. Takt = 2,700/300 = 9 min/ticket. Actual mean cycle time = 11 min → under capacity. Decision: reduce cycle time via triage automation OR add a 7th agent; cost-compare.

### Formula 3: Little's Law
**Formula:** `Lead Time = WIP / Throughput`

**Variables:**
- WIP = work-in-progress items in the system.
- Throughput = units completed per time unit.

**Why this formula exists:** Proves mathematically that reducing WIP reduces lead time — the intuitive foundation of kanban and Lean.

**How to interpret the output:**
- WIP growing faster than throughput → lead time will blow up; set/lower WIP limits.
- Stable WIP and throughput → lead time is predictable; safe to commit SLAs.
- Throughput dropping at fixed WIP → bottleneck has emerged; VSM to locate.

**Worked example:** Engineering team has WIP = 40 open issues, throughput = 8/week. Lead time = 40/8 = 5 weeks. Leadership wants 2-week lead time. Options: cut WIP to 16 (hard), or raise throughput to 20/week (needs Lean + hiring). Decision: enforce WIP = 20 per engineer-pair via kanban; expect lead time ≈ 2.5 weeks within 4 weeks.

### Formula 4: Waste Cost (Translating Muda to Rupees)
**Formula:** `Waste Cost = Σ over waste categories (time_wasted × fully-loaded cost-rate)`

**Variables:**
- time_wasted = hours per category per period (from VSM or self-report).
- fully-loaded cost-rate = salary × overhead multiplier (typically 1.3–1.6).

**Why this formula exists:** Converts qualitative "waste" into a number a CFO responds to, unlocking budget for Lean projects.

**How to interpret the output:**
- Waste cost > 20% of the process's budget → fund a dedicated Lean event now; expected ROI > 5×.
- 10–20% → bundle waste-reduction into regular ops OKRs.
- < 10% → diminishing returns; reinvest capacity in variance reduction (Six Sigma).

**Worked example:** A 12-engineer team loses 4.5 hr/engineer/week to context-switching + tool churn. 12 × 4.5 × 50 weeks × ₹2,000/hr loaded = ₹54 L/year. Decision: fund a 3-week Lean sprint (₹8 L) to consolidate tooling and enforce focus-time blocks.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|------|
| Pick Lean OR Six Sigma by brand preference before diagnosing the problem. | Use the Selector: if both waste AND variance are high, sequence Lean → then Six Sigma. |
| Map a "happy path" when VSM-ing the process. | Map the actual observed process including every rework loop and handoff, with real queue times measured at the Gemba. |
| Remove a "waste" activity without checking whether it protects against a defect or a legal requirement. | Pair each waste-removal decision with a Six Sigma check — does removing this step increase variance or compliance risk? |
| Optimise the bottleneck until it is no longer the bottleneck, then stop. | Re-VSM after every material change — the bottleneck moves, and local optimisation past it is wasted effort. |
| Announce "we are doing Lean Six Sigma" without belts, charters, and named sponsors. | Staff projects with a trained lead (Green Belt+), a signed charter, a sponsor, and a 12-week timeline. |
| Chase a 6σ target on every metric. | Set sigma targets per business criticality — 3.5σ for internal tools, 4.5σ for customer-facing, 5σ+ for safety/regulated. |
| Treat a successful Lean event as a one-time win. | Add the improvement to the Control Plan and run quarterly Kaizen refreshers to prevent decay. |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: AI/ML delivery pipeline — both waste and variance
**Situation:** A data-science org ships ~8 models/quarter but 1-in-3 rework after deployment. Mean model-to-prod time = 9 weeks (target 4); variance σ = 3 weeks. Stakeholders debate "should we Lean the pipeline or Six Sigma the quality?".
**Applicable framework/metric:** Lean vs Six Sigma Selector + VSM + Little's Law.
**Analysis:** Both axes are high → Lean Six Sigma. VSM: PT = 15 days, LT = 45 days, PCE = 33%. Bottlenecks: (1) model-review queue = 8 days; (2) infra provisioning = 6 days. WIP = 24 models, throughput = 2.7/week; Little's Law gives LT = 8.9 weeks — confirms observed. Cutting WIP to 12 with an infra-provisioning template would move LT to ≈ 4.4 weeks.
**Decision rule:** If PCE < 40% AND variance ≥ 2× target → start with Lean (VSM + WIP reduction), then Six Sigma (hypothesis tests on rework causes). If PCE ≥ 40% → skip Lean, go straight to Six Sigma.
**Action (Monday):** (a) Run a 3-day VSM workshop with Data, ML Eng, SRE; (b) introduce WIP limit of 12 in the ML kanban; (c) automate infra provisioning via a Terraform template; (d) open a parallel Six Sigma project on the top-3 rework causes.
- Data sources used: Jira (tickets), Looker (throughput), MLflow (model lineage), Git/GitHub (PRs).

### Scenario 2: Consulting — service-ticket PCE diagnostic
**Situation:** A managed-services provider handles 18,000 tickets/month with mean resolution 6 days. Client asks for "efficiency improvement" without specifying Lean or Six Sigma.
**Applicable framework/metric:** VSM + PCE formula + Waste Cost formula.
**Analysis:** VSM of top-3 ticket types reveals PT = 1.8 hr, LT = 48 hr → PCE = 3.75%. 8 wastes analysis finds Waiting (40% of LT), Defects (15% rework), Motion (analysts tool-switch between 6 tools). Waste cost: 40 FTEs × 2 hr/day × ₹1,500/hr × 230 days = ₹2.76 Cr/year.
**Decision rule:** PCE < 10% → Lean-first engagement (3–5% points of PCE per wave expected). Pair with Six Sigma on Defects only after PCE hits ≥ 20%.
**Action (Monday):** (a) Propose 12-week Lean engagement with target PCE 20%+ and MTTR −30%; (b) deploy kanban with WIP = 1.5× weekly throughput; (c) consolidate the 6 tools to 2 by month 3; (d) lock savings into client Control Plan.
- Data sources used: ServiceNow (tickets), Looker (MTTR), client's HR system (loaded rates), Confluence (VSM artefact).

### Scenario 3 (ANTI-EXAMPLE): Product team — skipping VSM and 5S-ing a dashboard
**Situation:** A PM hears a keynote on Lean Six Sigma, skips the VSM, and launches a "kaizen week" that produces a new executive dashboard aggregating 14 metrics. Ten weeks later, nothing has improved; team morale dips.
**Applicable framework/metric:** VSM + Lean vs Six Sigma Selector + Eight Wastes.
**Analysis (what went wrong):** No diagnosis — the team did not map where time actually went, did not categorise waste, did not pick a target metric. A dashboard is an *observation* tool, not a *countermeasure*. Selector says the team's problem was flow-related (long lead times, few defects) — VSM would have pointed at the review queue and the WIP pile; no amount of metric visibility fixes those.
**Decision rule that should have applied:** No Lean Six Sigma activity without (a) a baseline VSM, (b) a named Y metric with target, (c) a selector check, (d) a charter with sponsor and timeline.
**Wrong decision shipped and its cost:** ~60 engineer-hours consumed; dashboard abandoned by week 12; the real bottleneck (review queue) remained, causing 2 missed quarterly commitments at ~₹45 L in delayed revenue each.
**Correct action (had the framework been applied):** (a) Map VSM first; (b) diagnose WIP with Little's Law; (c) enforce WIP limits + review SLAs as the kaizen output; (d) track Y = lead time, not "dashboard adoption".
- Data sources used: Jira (WIP, throughput), Looker (lead time), 1:1 Gemba observations.

---

## 7. Implementation Playbook

1. **Run the Lean vs Six Sigma Selector on a one-page diagnostic** (Google Doc) — rate waste and variance each on 1–5; screenshot the quadrant.
2. **Build a Value Stream Map in Miro** for the target process with PT and QT for every step; compute PCE.
3. **Categorise waste using DOWNTIME** in a Google Sheet — quantify hours and cost per category; compute Waste Cost formula.
4. **Shortlist 1–3 waste-reduction experiments**; write each as a 1-page kaizen card with baseline, target, timebox, and owner.
5. **Set WIP limits in the team's kanban** (Jira, Linear, GitHub Projects) calibrated via Little's Law to the target lead time.
6. **Run a 5S pass** on the team's digital workspace (repos, flags, dashboards, runbooks) with a written "after" state.
7. **Launch paired Six Sigma sub-projects** for any variance that survives Lean (use DMAIC Analyze/Improve steps).
8. **Embed the improvements into the Control Plan** from the DMAIC Control phase — every gain gets an owner, a monitor, and a response rule.

---

## 8. Content Quality Audit

- **Covered well:** Source correctly frames Lean and Six Sigma as complementary (speed vs quality) and names the four highest-leverage Lean tools (waste, VSM, kaizen, 5S). Hospital and bank examples are credible.
- **Underplayed or missing:**
  - **DOWNTIME / 8 wastes acronym** is not spelled out, though it is the #1 practical Lean checklist.
  - **Little's Law** is absent — the single most useful equation for knowledge-work Lean.
  - **Takt time** and **Process Cycle Efficiency** are missing — students cannot quantify waste without them.
  - **Pull systems / Kanban** and **WIP limits** are not discussed, despite being the software-industry-relevant Lean output.
  - No mention of **Gemba walks** or **Jidoka** (stop-the-line) — both have direct SRE analogues.
  - **Sequencing guidance** (Lean first, then Six Sigma) is implied but not stated; students may try to run them in parallel and confuse their teams.
- **Supplement with:**
  - *Lean Thinking* — James Womack & Daniel Jones, 2nd ed. (2003), for the canonical 5 Lean principles and VSM method.
  - *The Toyota Way* — Jeffrey Liker, 2nd ed. (2020), for Jidoka, Gemba, and the management-system view.
  - *Learning to See* — Mike Rother & John Shook (1999), the operational guide to Value Stream Mapping (still the standard).
  - "The Goal" — Eliyahu Goldratt (1984) — for the Theory of Constraints lens that pairs naturally with Lean bottleneck analysis.
  - HBR "Decoding the DNA of the Toyota Production System" — Steven Spear & H. Kent Bowen, September–October 1999 — a four-rule synthesis that is often quoted, rarely read.
  - HBS case "Toyota Motor Manufacturing, USA, Inc." (HBS 693-019) — the classic Lean case for line-stop culture.
- **Red flags in the source:**
  - "Combining both methodologies" sounds harmonious but glosses over the sequencing question — running Lean and Six Sigma simultaneously often confuses teams.
  - Scenario claims 35% wait-time reduction and 60% error reduction in 4 months without discussing how the team avoided re-introducing variance while cutting steps.
  - All examples are physical-process-heavy — students will not see how this applies to software delivery, ML pipelines, or consulting engagements unless supplemented.

---

## 9. Quick-Recall Card

Lean Six Sigma = Lean (remove waste) + Six Sigma (reduce variance) — used together when both are broken.
Start with the Selector: is the problem flow (Lean) or variation (Six Sigma) or both?
Lean toolkit: DOWNTIME, VSM, 5S, kanban + WIP, Little's Law, Takt.
Six Sigma toolkit: SPC, Cp/Cpk, hypothesis tests, regression, DMAIC.
Sequence: diagnose with VSM → cut waste → reduce variance → lock in via Control Plan.
**As a PM/Consultant/AI Lead, the one question to answer with this framework is:** *Is my target process slow, unreliable, or both — and which of Lean or Six Sigma should I open first to get the fastest measurable win?*

---

**Connects to:** [05-analyze-phase.md](05-analyze-phase.md), [06-improve-phase.md](06-improve-phase.md), [07-control-phase.md](07-control-phase.md), [09-statistical-process-control.md](09-statistical-process-control.md) (once audited), and [../operations-management/](../operations-management/) for the broader ops lens; [../project-management/](../project-management/) for kanban/WIP depth.

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Sections rewritten: [Section 6 anti-example tightened with quantified cost; Section 9 compressed to 6 lines]
Enrichments applied: [cross-course links to DMAIC phases, operations-management, project-management; 6 named supplements (author+year or HBS case); anti-example scenario with quantified cost; IT-org tooling (Jira, Linear, Miro, Looker, MLflow, ServiceNow, Terraform) across scenarios; role-lens question closes Section 9]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 22:22
Audited by: A1
-->
