# Operations Analytics

## Overview
Operations analytics uses data-driven methods to improve the efficiency, quality, and reliability of business processes. It covers areas such as supply chain management, production scheduling, inventory control, and workforce planning. The goal is to reduce waste, lower costs, and increase throughput without sacrificing quality or customer satisfaction.

---

## Why It Matters
Operational inefficiencies directly erode profit margins and customer experience. Even small improvements in cycle time, defect rate, or inventory turnover can translate into significant financial gains when applied at scale across an organization's operations.

## Key Principles
- Map end-to-end processes before optimizing so you understand where bottlenecks and waste actually occur
- Use real-time data collection to monitor operations continuously rather than relying on periodic reviews
- Balance efficiency with resilience by maintaining appropriate safety stock and capacity buffers
- Apply continuous improvement frameworks that use data to identify, test, and validate process changes

## Key Terms
| Term | Definition |
|------|------------|
| **Throughput** | The rate at which a system produces output, typically measured in units per time period |
| **Cycle Time** | The total elapsed time from the start to the completion of a single unit of work or process step |
| **Safety Stock** | Extra inventory held as a buffer against uncertainty in demand or supply lead times |
| **Bottleneck** | The step in a process that limits overall throughput because it has the lowest capacity or highest processing time |

## Use Case
A fulfillment center uses operations analytics to redesign its warehouse pick paths, reducing average order processing time by 22 percent during peak season.

## Scenario
> A food manufacturer notices inconsistent delivery times to retailers. An operations analytics project maps the entire supply chain and identifies that a single packaging line is the bottleneck. By adding a second shift on that line, the company reduces average delivery delays from three days to less than one day.

## Examples
- Analyzing machine sensor data to predict equipment failures and schedule preventive maintenance before breakdowns occur
- Optimizing staff scheduling at a call center by modeling call volume patterns across days of the week and times of day

---

## Audited Appendix

# Operations Analytics
**Course:** Business Analytics
**Module:** Content / Operations Analytics
**Audited on:** 2026-04-18
**Source files reviewed:** `business-analytics/content/10-operations-analytics.md`

---

## 1. Topic Snapshot
Operations analytics = applying data methods to processes, inventory, scheduling, and workforce to move throughput up and waste/cost down. For an IT/AI/Product/Consulting leader, the same laws that govern factories govern software teams, AI inference pipelines, support queues, and SLA-bound services — Little's Law, bottlenecks, WIP limits, and queue theory are universal. Decision it helps make: *"Which step of my process is actually limiting throughput, and what is the cheapest intervention to unlock it?"*

Cross-reference: deeper coverage of these topics in the full Operations Management course (Topics 01–24 in `operations-management/`). This file is the analytics-focused subset.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Throughput | — | Output per unit time | Primary operations measure | units / hour | Ops, eng |
| Cycle Time | — | Time to complete one unit | Single-unit latency | seconds / minutes / days | Software, mfg |
| Lead Time | — | Total time from order to delivery | Customer-facing time metric | days / hours | Supply chain, support |
| Takt Time | — | Available production time / demand | Paces production to demand | time / unit | Lean, Toyota Production System |
| WIP | Work in Progress | Units currently in system | Inventory-in-flight | count or $ | Lean, Kanban |
| Little's Law | — | WIP = Throughput × Lead Time | Universal flow law | — | OR, Lean, Agile |
| Utilisation | — | % of capacity used | Too high creates queueing explosion | % | Queue theory |
| Bottleneck | — | Lowest-capacity step | Limits overall throughput | Identify via capacity audit | TOC |
| Theory of Constraints | TOC | Goldratt: identify and exploit bottleneck | Focuses improvement effort | Throughput per constraint | OR |
| OEE | Overall Equipment Effectiveness | Availability × Performance × Quality | Single number for mfg equipment | 0–1 | Manufacturing |
| Availability | — | Uptime / planned production time | Component of OEE | % | Mfg |
| Performance | — | Actual rate / standard rate | Component of OEE | % | Mfg |
| Quality | — | Good units / total units | Component of OEE | % | Mfg |
| DPMO | Defects Per Million Opportunities | Quality scale | Six Sigma standard | count | Quality |
| Sigma Level | — | Sigmas away from spec | 3.4 DPMO ≡ Six Sigma | σ level | Quality |
| Safety Stock | — | Buffer inventory | Guards against stockout | Z × σ × √L | Inventory |
| Reorder Point | ROP | Trigger level to reorder | Prevents stockout | Average demand × Lead time + safety stock | Inventory |
| EOQ | Economic Order Quantity | Optimal order size | Balances order + holding costs | √(2DS/H) | Inventory |
| Service Level | — | % of demand satisfied on time | Inventory-policy KPI | 90, 95, 99% | Inventory, SRE |
| Queueing Theory | — | Math of waiting lines | Explains why 80% utilisation ≈ 4× wait at 50% | M/M/1, M/M/s models | OR, SRE |
| M/M/1 | — | Single-server queue with Poisson arrivals | Foundational queue model | λ, μ, ρ | Queue theory |
| Poka-yoke | — | Mistake-proofing | Lean quality | Defect rate change | Lean |
| Just-in-Time | JIT | Produce / deliver exactly when needed | Reduces inventory | Cycle time, WIP | Toyota |
| Kanban | — | Pull-system signal | Limits WIP | Board with columns | Lean, Agile |
| DMAIC | Define-Measure-Analyze-Improve-Control | Six Sigma improvement framework | Structured problem-solving | Cycle completion per project | Six Sigma |
| Value Stream Map | VSM | End-to-end process visualisation | Exposes waste | Activity cycle times, handoffs | Lean |
| Shingo Seven Wastes | — | TIMWOODS: Transport, Inventory, Motion, Waiting, Over-production, Over-processing, Defects, Skills under-used | Taxonomy of waste | Waste events by category | Lean |
| Predictive Maintenance | — | Sensor-driven maintenance scheduling | Avoids unplanned downtime | Failure predictions, uptime | IoT, mfg, cloud |
| Digital Twin | — | Real-time virtual replica of physical asset | Simulate interventions | Model fidelity | Industry 4.0 |
| SRE | Site Reliability Engineering | Google's discipline for running services reliably | Apply ops analytics to software | Error budget, SLO | Software ops |
| SLO / SLA / SLI | Service Level Objective / Agreement / Indicator | Targets, commitments, measurements | Reliability contracts | % targets met | SRE, cloud |

> All extensions beyond source-named four (`Throughput`, `Cycle Time`, `Safety Stock`, `Bottleneck`) are standard. `[verified from model knowledge, not source]`.

---

## 3. Frameworks & Matrices

### Framework 1: Theory of Constraints (TOC) Improvement Loop
**Purpose:** Focus all improvement effort on the bottleneck — other improvements have zero throughput impact.

**Text Diagram:**
```
   ┌────────────────────────┐
   │ 1. IDENTIFY the        │  Where does queue build up? 
   │    CONSTRAINT          │  Where is utilisation > 90%?
   └────────────┬───────────┘
                │
   ┌────────────▼───────────┐
   │ 2. EXPLOIT the         │  Squeeze more capacity out of existing
   │    CONSTRAINT          │  bottleneck (overtime, automation)
   └────────────┬───────────┘
                │
   ┌────────────▼───────────┐
   │ 3. SUBORDINATE         │  Everyone else runs at bottleneck pace —
   │    everything else     │  don't overproduce upstream
   └────────────┬───────────┘
                │
   ┌────────────▼───────────┐
   │ 4. ELEVATE if needed   │  Add capacity (new equipment, new shift,
   │                        │  parallel lane)
   └────────────┬───────────┘
                │
   ┌────────────▼───────────┐
   │ 5. REPEAT              │  Constraint moves; start at step 1
   └────────────────────────┘
```

Components:
- Every system has one constraint at any time
- Improvement of non-bottlenecks = 0 throughput gain

**IT/AI/Product/Consulting worked example:** An AI inference pipeline has GPU, CPU pre-processing, and network egress stages. Utilisation: GPU 90%, CPU 45%, Network 20%.
- Identify: GPU is bottleneck
- Exploit: batch requests more aggressively, use speculative decoding, quantise
- Subordinate: reduce upstream pre-processing complexity; don't flood GPU queue
- Elevate: add GPU capacity (buy H100, spot instances, or shift to cheaper regions)
- Repeat: new bottleneck may be network egress

**When to pull this out in a meeting:** Ops improvement programs; software platform scaling; SRE review.

---

### Framework 2: OEE Decomposition
**Purpose:** Decompose equipment/service effectiveness into its three drivers — so improvement effort is well-directed.

**Text Diagram:**
```
   OEE = AVAILABILITY × PERFORMANCE × QUALITY

      Availability = Run time / Planned production time
                     (downtime: maintenance, breakdowns, changeovers)
      ×
      Performance  = Actual output rate / Standard rate
                     (slow cycles, micro-stops)
      ×
      Quality      = Good units / Total units
                     (defects, rework)

   Example: 0.90 × 0.85 × 0.95 = 0.73 (73% OEE)
   World-class benchmark: 85%
```

Components:
- Each factor has its own intervention levers
- Multiplicative → small gains in each compound

**IT/AI/Product/Consulting worked example:** A SaaS platform's "service OEE":
- Availability (uptime vs target SLO): 99.5% (down 0.5%)
- Performance (p95 latency vs target): 85% of requests under target
- Quality (error-free responses): 99.2%
- Service OEE = 0.995 × 0.85 × 0.992 = **0.839**

Biggest lever: performance. Action: optimise p95 (CDN tuning, query optimisation, caching).

**When to pull this out in a meeting:** Service-health reviews; SRE quarterly; factory performance reviews.

---

### Framework 3: Little's Law Diagnostic
**Purpose:** Relate the three universal flow variables — use to diagnose any queue.

**Text Diagram:**
```
   ┌─────────────────────────────────────────┐
   │          LITTLE'S LAW                    │
   │                                          │
   │          L = λ × W                       │
   │                                          │
   │   L = avg work in system (WIP / queue)   │
   │   λ = avg arrival rate                   │
   │   W = avg time in system (lead time)     │
   └─────────────────────────────────────────┘

   Use cases:
   • Want lower W? Reduce L or raise λ capacity.
   • Want higher throughput? Either raise capacity or reduce W.
   • If L and λ known, W = L / λ.
```

Components:
- Universal — holds for any queue in steady state
- Link L, λ, W → change any one and know the other's direction

**IT/AI/Product/Consulting worked example:** A support queue has L = 120 tickets open, λ = 40 tickets/day. → W = 3 days average age. Goal: get to 2 days. Two levers:
- Reduce L to 80 tickets (aggressive closure push): W = 2 days ✓
- Raise throughput to 60/day (more agents or automation): W = 2 days ✓

**When to pull this out in a meeting:** Any queue debate — support tickets, sales pipeline, code review backlog, build jobs.

---

## 4. Formulas

### Formula 1: Little's Law
**Formula:** `L = λ × W`

**Variables:**
- L = average WIP in system
- λ = arrival rate (per time)
- W = average time in system

**Why this formula exists:** Universal flow law. If you know any two, the third is determined. Works for any queue in steady state — manufacturing, software, people.

**How to interpret the output:**
- Gives target leverage point; lets you set cap on WIP to hit desired W
- "Stop starting, start finishing" — cap WIP via Kanban to reduce W

**Worked example:** A DevOps team completes 5 tickets/day (λ). WIP 25 (L). → Lead time W = 5 days.
- Goal W = 2 days → WIP cap must be 10.
- Impact: fewer items in progress; finish rate the same; individual lead time drops dramatically.

**Data source:** Work tracking in Jira/Linear/Asana; dashboarded in flow-metrics tools (ActionableAgile, Plandek).

---

### Formula 2: Economic Order Quantity (EOQ)
**Formula:** `EOQ = √(2DS / H)`

**Variables:**
- D = annual demand
- S = ordering cost per order
- H = holding cost per unit per year

**Why this formula exists:** Balances the tradeoff between frequent-small-orders (high S) vs infrequent-large-orders (high H).

**How to interpret the output:**
- EOQ = economic reorder quantity; minimises total cost
- Real-world factors (volume discounts, storage constraints) may push away from strict EOQ

**Worked example:** Cloud-commodity purchasing: D = 100,000 GPU-hours/yr, S = $200 per contract, H = $20/GPU-hour/yr.
- EOQ = √(2 × 100,000 × 200 / 20) = √(2,000,000) = **~1,414 GPU-hours per order**
- ~70 orders / year

**Data source:** D from usage telemetry; S from procurement cycle time × team hourly rate; H from finance cost of capital + storage.

---

### Formula 3: Safety Stock
**Formula:** `Safety Stock = Z × σ_LTD × √L` (lead-time demand variability version) or simpler: `Z × σ_demand`

**Variables:**
- Z = service-level z-score (90%→1.28, 95%→1.65, 99%→2.33)
- σ_LTD = standard deviation of demand during lead time
- L = lead time (periods)

**Why this formula exists:** Quantifies buffer needed to hit desired service level given demand variability.

**How to interpret the output:**
- Higher service level → exponentially larger safety stock
- Reducing lead-time variability is often cheaper than raising safety stock

**Worked example:** An e-commerce fulfilment centre: daily demand μ=200 units, σ=40, lead time 4 days. Target 95% service level.
- σ_LTD = 40 × √4 = 80
- Safety stock = 1.65 × 80 = **132 units**

**Data source:** Demand history from ERP; variability computed in warehouse; reorder-point rules stored in inventory system.

---

### Formula 4: Queue Utilisation Impact (M/M/1)
**Formula:** `Avg Wait Time W_q = ρ / (μ − λ)`, where ρ = utilisation = λ/μ

**Variables:**
- λ = arrival rate
- μ = service rate
- ρ = utilisation (must be < 1 for stability)

**Why this formula exists:** Shows that waiting time explodes as utilisation approaches 100%. Lesson: never run systems at "max efficiency."

**How to interpret the output:**
- ρ = 0.5 → wait 1 service time
- ρ = 0.8 → wait 4 service times
- ρ = 0.9 → wait 9 service times
- ρ = 0.95 → wait 19 service times
- ρ ≥ 1 → infinite queue

**Worked example:** Call centre with 1 agent, arrival rate 10 calls/hour, service rate 12 calls/hour. ρ = 0.83; wait time = 0.83 / (12 − 10) = **0.417 hours = 25 min**. Add a second agent (M/M/2 model): wait drops dramatically.

**Data source:** Arrival and service rates from call-centre software (Zendesk, Five9, Genesys).

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|-------|
| Optimise non-bottlenecks and expect throughput gains | Identify and attack the bottleneck per TOC |
| Run any system at > 85% utilisation | Keep buffer; use queue theory to set utilisation caps |
| Aggregate cycle time; lose the distribution tail | Report p50, p90, p99 of cycle time; set SLOs on tail |
| Treat every defect equally | Weight by cost: defects escaping to customer × blast radius |
| Rely on scheduled preventive maintenance alone | Implement predictive (sensor-driven) maintenance for critical assets |
| Set safety stock by gut | Use Z × σ formula tied to service-level target |
| Ignore lead-time variance | Variance often matters more than mean for service level |
| Add capacity without exploiting existing | TOC: exploit before elevate |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: AI Platform Optimising Inference Pipeline
**Situation:** An AI platform serves inference requests; p99 latency violates SLA; costs are rising.

**Applicable framework/metric:** TOC + Little's Law + Queue Theory.

**Analysis:**
- Utilisation: GPU 92%, CPU 40%, Network 30%.
- Little's Law: λ = 1,000 req/sec; L = 280 in flight; W = 0.28 sec.
- Target W = 0.15 sec. Keeping λ constant → need L = 150.
- Queue theory: at 92% utilisation, tail is 12×. Target 75% → tail 3×.

**Decision rule:** If utilisation > 85%, add capacity or reduce arrival rate before optimising elsewhere.

**Action (Monday morning):** Add GPU capacity (spot instances) to drop utilisation to 75%. Cap request queue depth. Measure p99 after 48 hrs.

---

### Scenario 2: Consulting Firm Redesigning Client Support Operations
**Situation:** A SaaS client's support team has 3-day avg resolution time; target 1 day.

**Applicable framework/metric:** Little's Law + Service Level.

**Analysis:**
- Current: WIP 180 tickets, λ = 60 tickets/day → W = 3 days.
- Target W = 1 day → WIP cap 60 OR λ raised to 180/day.
- WIP cap requires strict prioritisation + closing long-pending; λ raise requires 3× throughput (unrealistic without automation).

**Decision rule:** Attack the larger lever (3× WIP cut is operational; 3× throughput requires capacity or AI).

**Action:** Install WIP cap 60 via Kanban. Deploy AI triage for Tier-1 tickets (automates ~30% of volume). Combined: lead time to 1.2 days; refine from there.

---

### Scenario 3 (Anti-example): Chasing Utilisation as a KPI
**Situation:** An ops manager sets KPI "machine utilisation > 95%" across manufacturing lines.

**Applicable framework/metric:** Queue Theory + Bottleneck pacing.

**Analysis (what goes wrong):**
- At 95% utilisation, queue times explode exponentially
- Downstream customers experience erratic lead times
- WIP balloons; defects rise; changeover costs ignored
- "Utilisation up, throughput down" paradox

**Cost of this mistake:** Customer complaints, late deliveries, quality drop, higher overall cost — exactly opposite of intent.

**Decision rule:** Never set utilisation > 85% as a KPI; use throughput and lead time instead.

**Action:** Rewrite ops KPIs: throughput, lead time (p50 and p90), OEE. Utilisation becomes input, not output.

---

## 7. Implementation Playbook

1. **Map the end-to-end process** — Value Stream Map on Miro or Lucidchart; include cycle time, waiting time, handoffs for each step.
2. **Instrument each step with real-time metrics** — sensor data / log-derived cycle-time and throughput; export to Prometheus / Snowflake.
3. **Identify the current bottleneck** — look for highest utilisation AND highest queue; validate with production data.
4. **Set TOC loop as a standing review** — monthly; track constraint as it moves.
5. **Define OEE or Service-OEE** — decomposed into availability / performance / quality; owner per component.
6. **Implement WIP caps via Kanban tooling** — Linear, Jira, or ActionableAgile — across software and ops teams.
7. **Deploy predictive maintenance on critical assets** — sensor + classifier model; alert 24–72 hours before predicted failure.
8. **Establish SLO + error-budget culture for software** — Google SRE book as playbook; review weekly.

---

## 8. Content Quality Audit

**Covered well:**
- Names throughput, cycle time, safety stock, bottleneck.
- Notes real-time monitoring and continuous-improvement frameworks.
- Mentions predictive maintenance.

**Underplayed or missing:**
- No Little's Law.
- No TOC / Goldratt logic operationalised.
- No OEE decomposition.
- No queue theory / utilisation-tail relationship.
- No EOQ, reorder point, service-level math.
- No DMAIC / Six Sigma quality toolkit connection.
- No reference to Goldratt, Womack/Jones, Ohno, or Google SRE book.
- Zero AI/software examples (fulfilment center, food manufacturer). Misses the modern observation that every SaaS/AI service is a factory.

**Supplement with:**
- *The Goal* — Eliyahu M. Goldratt (1984, North River Press). Theory of Constraints origin novel.
- *Factory Physics* — Wallace Hopp & Mark Spearman (3rd ed 2011). Queue theory + ops analytics.
- *Lean Thinking* — James Womack & Daniel Jones (1996, revised 2003). Foundational Lean.
- *Toyota Production System* — Taiichi Ohno (1988, Productivity Press).
- *Site Reliability Engineering* — ed. Betsy Beyer, Chris Jones, Jennifer Petoff, Niall Richard Murphy (2016, O'Reilly, free online). Google's operations playbook applied to software.
- *The Phoenix Project* — Gene Kim, Kevin Behr, George Spafford (2013). TOC applied to IT ops (novel).
- *Accelerate* — Nicole Forsgren, Jez Humble, Gene Kim (2018). Operations metrics for software (DORA metrics).
- HBR: "Turning Great Strategy into Great Performance" — Michael Mankins & Richard Steele, *HBR*, 2005.
- HBR: "Reinventing Supply Chains with AI" — various HBR briefings.
- HBS case: "Toyota Motor Manufacturing USA" — TPS in practice.
- HBS case: "Benihana of Tokyo" — restaurant as operations study.
- IIMA case: "Asian Paints: Supply Chain Analytics" — Indian manufacturing ops analytics.

**Red flags in the source:**
- "Balance efficiency with resilience" — correct direction but no math (Z-score safety stock, service level, etc).
- "Use real-time data collection to monitor operations continuously" — table-stakes; no guidance on alerting thresholds, SLOs, or anomaly detection.
- Example "warehouse pick paths redesign" is a real technique (travelling salesman / routing) but source never names optimisation algorithms.
- Machine-sensor predictive maintenance mentioned without pipeline discussion (features, training, false-positive cost tradeoff).

**Connects to:**
- `audit_management_course/business-analytics/02-descriptive-analytics.md` (metric dashboards)
- `audit_management_course/business-analytics/04-predictive-analytics.md` (predictive maintenance modelling)
- `audit_management_course/business-analytics/05-prescriptive-analytics.md` (routing / scheduling optimisation)
- `audit_management_course/operations-management/01-what-is-operations-management.md` through `24-technology-in-operations.md` (full ops course)
- `audit_management_course/six-sigma/*` (quality discipline)
- `audit_management_course/supply-chain-management/*` (SCM-specific analytics)
- `audit_management_course/project-management/10-schedule-management.md` (schedule optimisation)
- `audit_management_course/ai-ml-business/15-ai-in-operations.md` (AI-driven ops)

---

## 9. Quick-Recall Card

```
Topic: Operations Analytics
Core idea: Flow laws (Little's Law) + bottleneck focus (TOC) beat local optimisation every time.
Key metric/formula: L = λW; OEE = A×P×Q; EOQ; Safety Stock = Z×σ√L; queue wait ~ ρ/(μ−λ).
Framework trigger: Capacity planning, cycle-time SLA work, inventory policy, support queue design.
Watch out for: Utilisation > 85% as a target; optimising non-bottlenecks; aggregate-only cycle times.
Monday action: Compute Little's Law on 3 key queues; identify current bottleneck; set WIP cap.
As a PM/Consultant/AI Lead, the one question to answer with this framework is:
"Where is the real bottleneck, and what one intervention relaxes it fastest?"
```

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Pass 1 average: 4.8
Sections rewritten: none (no criterion <4/5)
Enrichments applied: [cross-course links to business-analytics/02, 04, 05; operations-management/01-24; six-sigma; supply-chain-management; project-management/10; ai-ml-business/15. Goldratt 1984, Hopp/Spearman 2011, Womack/Jones 1996, Ohno 1988, Beyer/Jones/Petoff/Murphy 2016 (Google SRE), Kim/Behr/Spafford 2013, Forsgren/Humble/Kim 2018, Mankins/Steele HBR 2005. HBS Toyota + Benihana, IIMA Asian Paints. Anti-example Scenario 3 (utilisation-as-KPI). Data sources: Prometheus, Jira/Linear, ActionableAgile, Zendesk, Genesys. Decision-maker view in Quick-Recall.]
Final scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] — average 5.0
Pass 2 completed: 2026-04-18 01:40
-->
