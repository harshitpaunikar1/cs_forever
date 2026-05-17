# Root Cause Analysis Tools

## Overview
Root cause analysis (RCA) tools are structured techniques used to trace problems back to their fundamental origins rather than just treating symptoms. Six Sigma practitioners rely on tools like fishbone diagrams, the 5 Whys, fault tree analysis, and failure mode and effects analysis to systematically uncover why defects or failures occur. These tools are used primarily in the Analyze phase of DMAIC but can be applied anytime a team needs to understand why something went wrong.

---

## Why It Matters
Fixing symptoms instead of root causes is one of the most expensive mistakes an organization can make. Problems keep recurring, consuming resources and frustrating customers. RCA tools provide a disciplined approach to drilling past surface-level explanations and reaching the true source of a problem. When root causes are eliminated, problems stay fixed and organizations avoid the cycle of repeated firefighting.

## Key Principles
- Ask why multiple times to move past symptoms to true causes
- Use visual tools to organize potential causes into logical categories
- Involve cross-functional team members who have direct process knowledge
- Validate suspected root causes with data before implementing solutions

## Key Terms
| Term | Definition |
|------|------------|
| **Fishbone Diagram** | A visual tool that categorizes potential causes of a problem into branches such as people, process, materials, and equipment |
| **5 Whys** | A technique that involves asking why repeatedly until the fundamental cause of a problem is revealed |
| **FMEA** | Failure Mode and Effects Analysis, a systematic method for evaluating potential failure modes and their impact to prioritize corrective actions |
| **Fault Tree Analysis** | A top-down, deductive method that maps the logical combinations of events that lead to a specific failure |

## Use Case
An aerospace company uses FMEA to evaluate every component of a landing gear assembly, ranking failure modes by severity, occurrence, and detectability to prioritize design improvements.

## Scenario
> A food company keeps finding metal fragments in its granola bars. The team draws a fishbone diagram listing possible causes under equipment, materials, process, and people. They then apply the 5 Whys to the most likely branch and discover that a worn conveyor belt guide is shedding metal shavings. Replacing the guide and adding a metal detector eliminates the issue permanently.

## Examples
- A data center uses fault tree analysis to trace a server outage back to a single failed cooling fan that triggered a cascade of thermal shutdowns
- A chemical plant conducts an FMEA on its reactor vessel maintenance procedures and discovers that a skipped pressure test step poses the highest risk, leading to an updated checklist and training program

---

## Audited Appendix

# Root Cause Analysis Tools
**Course:** Six Sigma
**Module:** Content / Root Cause Analysis Tools
**Audited on:** 2026-04-18
**Audited by:** A3
**Source files reviewed:** `six-sigma/content/11-root-cause-analysis-tools.md`

---

## 1. Topic Snapshot
Root Cause Analysis (RCA) tools are structured techniques — Fishbone, 5 Whys, FMEA, Fault Tree — to trace problems past symptoms to fundamental, systemic origins. They anchor the Analyze phase of DMAIC and prevent recurrence by forcing data validation of candidate causes. In IT/AI/Product/Consulting, they transform incident retrospectives from blame-games into systemic learning loops.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| Root Cause | Root Cause | The deepest controllable factor that, if removed, prevents recurrence | Symptom-fixing is expensive and transient | Validated by removal test / data | Incident retros, Jira tickets |
| Symptom | Symptom | Observable surface effect of a problem | People confuse symptom with cause | Observed frequency | Monitoring alerts, Sentry |
| Fishbone (Ishikawa) | Cause-and-Effect Diagram | Tree grouping causes by category | Organizes brainstorm visually | # branches explored | Six Sigma workshops |
| 5 Whys | 5 Whys | Iterative "why?" drill to systemic cause | Stops surface-level thinking | Depth (≥3 typical) | Toyota, PagerDuty retros |
| FMEA | Failure Mode and Effects Analysis | Pre-mortem rating severity/occurrence/detection | Prioritize where to invest prevention | RPN score | Aerospace, MLOps risk reviews |
| RPN | Risk Priority Number | S × O × D composite score | Single number to rank failure modes | 1–1000 scale | FMEA worksheets |
| Severity | Severity (S) | Impact if failure happens | Not all failures equal | 1–10 anchored scale | FMEA, SEV1–5 incident class |
| Occurrence | Occurrence (O) | Likelihood of failure mode | Frequent + minor ≠ rare + major | 1–10 anchored scale | FMEA |
| Detection | Detection (D) | Ability to catch before customer impact | Invisible failures are worst | 1–10 (10=undetectable) | FMEA, observability reviews |
| Fault Tree Analysis | FTA | Top-down Boolean logic tree of failure paths | Models AND/OR combinations precisely | P(top event) | Aerospace, SRE, safety cases |
| Top Event | Top Event | The undesired outcome at FTA root | Defines the failure being analyzed | Binary occurrence | FTA diagrams |
| Basic Event | Basic Event | Leaf-level independent cause in FTA | Atomic, measurable | P(event) | FTA |
| Apollo RCA / Causal Tree | Apollo Root Cause Analysis | Causal chain method (Gano, 2007) linking action + condition pairs | Replaces 5-Why with evidence chains | Evidence per node | Apollo RCA training |
| Barrier Analysis | Barrier Analysis | Identifies failed defenses between hazard and harm | Swiss-cheese model of layered defenses | # failed barriers | Safety, SRE |
| Pareto | Pareto (80/20) | Bar chart ranking causes by frequency/cost | 20% of causes → 80% of pain | Cumulative % | Quality, Datadog dashboards |
| Is / Is-Not Analysis | Is/Is-Not Matrix | Kepner-Tregoe scoping matrix | Bounds problem before root-causing | Completeness of grid | KT RCA, consulting |
| A3 Report | A3 | One-page Toyota structured problem-solving doc | Forces concise systemic framing | Compliance with A3 sections | Lean, Toyota Way |
| Blameless Postmortem | Blameless PM | SRE analogue of RCA without individual blame | Humans aren't the root cause; systems are | Action items closed | Google SRE, Etsy, Rootly |
| MTTD / MTTR | Mean Time to Detect / Recover | How fast you saw and fixed it | RCA feeds these metrics | Minutes/hours | PagerDuty, Datadog SLO |
| 6M | Man, Machine, Material, Method, Measurement, Milieu (Env) | Fishbone category set | Prevents missing a cause class | Coverage of 6 branches | Manufacturing + adapted IT |

---

## 3. Frameworks & Matrices

### 3.1 Fishbone / Ishikawa — Software 6M Variant
**Purpose:** Categorize candidate causes so brainstorm does not cluster into one bucket.
**Software 6M swap:** People, Process, Tech/Platform, Data, Environment, Measurement/Observability.

```
                   People                 Process                 Tech
                     \                       |                     /
            On-call fatigue ---+    Missing runbook ---+    Memory leak ---+
            Poor handoff ------+    No canary ---------+    Stale cache ---+
                                \                      |                  /
                                 +---------[ Checkout 500 rate 4% ]-------+
                                /                      |                  \
            Schema drift ------+    Prod==staging? ---+    No p99 SLO ----+
            Feature null -----+     DNS flip ---------+    Alert mute ----+
                     /                       |                     \
                   Data                 Environment            Measurement
```

**Components:** Problem statement (spine), 6 main bones, sub-bones per cause.
**IT Example — Checkout 500s spike:** Cross-functional team of SRE + Platform + Data + PM builds fishbone. Tech-branch "memory leak in pricing microservice" and Data-branch "null feature from upstream Kafka topic" both become candidates → validate with Datadog traces + Evidently data-quality report.
**Decision/Trigger:** Run fishbone when problem spans ≥2 teams OR when 5-Why loops to the same cause without consensus.

---

### 3.2 5-Why Drill
**Purpose:** Move from symptom to systemic cause through repeated causal interrogation.

```
  [ Symptom: Prod deploy failed at 14:02 ]
        |
        v  Why?
  [ Migration timed out ]
        |
        v  Why?
  [ Lock contention on orders table ]
        |
        v  Why?
  [ Long-running analytics query held lock ]
        |
        v  Why?
  [ Analytics job scheduled during deploy window ]
        |
        v  Why?  <-- SYSTEMIC
  [ No shared deploy calendar / no lock-mode test in CI ]
        |
        v  FIX: CI lock-check + cross-team deploy calendar
```

**Stopping rules:**
- Stop when cause is **systemic** (process, policy, tool) — NOT when it becomes "human error".
- Minimum depth 3; typical 5; beyond 7 suggests wrong branch.
- Each "why" must be evidentiable (log, metric, ticket); no speculation.

**Systemic vs human-error distinction:** "Engineer forgot to run migration test" → human error (wrong stop). Keep going: "Why wasn't it automated?" → systemic.

**Decision/Trigger:** Use for single-threaded incidents; switch to fishbone when causes diverge into multiple categories.

---

### 3.3 FMEA Worksheet with RPN

```
+----------------------+---------------------+---+---+---+-----+----------+
| Process Step / Item  | Failure Mode        | S | O | D | RPN | Action   |
+----------------------+---------------------+---+---+---+-----+----------+
| Feature ingestion    | Null from upstream  | 8 | 6 | 7 | 336 | Schema   |
|                      |                     |   |   |   |     | contract |
| Model inference      | p99 > 500 ms        | 6 | 5 | 4 | 120 | Autoscale|
| Label pipeline       | Delayed by >24h     | 9 | 3 | 8 | 216 | Freshness|
|                      |                     |   |   |   |     | SLO      |
| Feature store write  | Partial write       | 7 | 2 | 6 |  84 | Idempotent|
| Shadow eval          | Drift undetected    | 8 | 4 | 9 | 288 | Evidently|
+----------------------+---------------------+---+---+---+-----+----------+
Ranking rule: Act on RPN >= 200 immediately; 100-199 plan; <100 monitor.
Also: any row with S=9 or 10 acts regardless of RPN (safety/critical).
```

**Components:** Item, failure mode, effects, S (1–10), O (1–10), D (1–10), RPN = S×O×D, owner, action, revised RPN.
**Anchors (must be pre-defined):** e.g., S=10 customer harm / data loss; S=5 degraded UX; D=1 caught instantly by alert; D=10 caught by customer complaint only.
**AI Example — Feature Pipeline:** The worksheet above drives a sprint: schema contract (RPN 336) and shadow-eval drift alert (RPN 288) ship first.
**Decision/Trigger:** Run FMEA before launch (pre-mortem) and after any SEV1 incident.

---

### 3.4 Fault Tree Analysis (AND/OR)

```
                    [ TOP: Checkout unavailable >5 min ]
                                |
                              (OR)
                  /             |             \
         [Payment down]   [DB unavailable]   [CDN down]
               |                |                |
             (AND)            (OR)             (OR)
         /         \        /      \         /      \
  [Stripe 5xx] [Retry off] [Primary [Replica  [POP     [DNS
                             fails]  lag>60s] outage]  flip]
```

**Logic gates:**
- **AND** — all children must occur for parent to occur → P(parent) = ∏ P(child).
- **OR** — any child → P(parent) = 1 − ∏ (1 − P(child)).

**IT Example — Payment outage:** Stripe 5xx alone is survivable; it becomes top event only AND-combined with retry-logic being disabled in a feature flag. FTA exposed a dormant flag as the critical risk.
**Decision/Trigger:** Use for multi-cause failures where combinations matter (security, availability cascades); pairs with chaos engineering to validate AND gates.

---

### 3.5 Is / Is-Not Matrix (Scoping Aid)

```
+------------+-----------------------+--------------------------+
| Dimension  | IS (problem observed) | IS-NOT (not observed)    |
+------------+-----------------------+--------------------------+
| What       | Checkout 500s         | Cart, login, search      |
| Where      | EU region only        | US, APAC                 |
| When       | Since 2026-04-15 0200 | Before that              |
| Who        | Android clients       | iOS, web                 |
| Extent     | ~4% of sessions       | <0.1% normal             |
+------------+-----------------------+--------------------------+
=> Hypothesis: EU-specific Android SDK upgrade on 04-15.
```

**Decision/Trigger:** Run first when scope is ambiguous; feeds cleaner fishbone / 5-Why.

---

## 4. Formulas

### 4.1 Risk Priority Number (RPN)
`RPN = Severity (S) × Occurrence (O) × Detection (D)`, each anchored 1–10.
**Thresholds:** RPN ≥ 200 → immediate mitigation; 100–199 → plan in quarter; < 100 → monitor. Override: any S ≥ 9 acts regardless.
**Worked example (Support-ticket root cause):** Failure mode = "Password reset email fails silently". S=7 (customer churn), O=4 (0.5% of resets), D=9 (user never complains; churns). RPN = 7×4×9 = **252** → immediate fix (add delivery webhook + SLO).

### 4.2 5-Why Depth Rule
`Stop when (cause is systemic) AND (depth ≥ 3) AND (each step is evidence-backed)`.
**Threshold check:** If depth < 3 → too shallow; if final node is a person's action → keep going.
**Worked example (ML regression):** "Model accuracy dropped 6%" → Why? feature X null rate 12% → Why? upstream topic schema change → Why? producer deploy without consumer sign-off → Why? no schema registry contract → Why? cost-cutting removed tool in Q3. Depth=5, systemic=yes. Stop.

### 4.3 Pareto Share (Cumulative %)
`Cumulative %_i = (Σ_{k=1..i} freq_k) / (Σ_all freq) × 100`. Draw Pareto bar when cum% ≥ 80% is reached in ≤20% of categories.
**Worked example (Production incidents last quarter, 200 tickets):**

| Cause | Count | % | Cum % |
|---|---|---|---|
| Deploy-related | 84 | 42% | 42% |
| Third-party API | 48 | 24% | 66% |
| Data pipeline | 30 | 15% | 81% |
| Infra saturation | 20 | 10% | 91% |
| Other | 18 | 9% | 100% |

Top 3 = 81% → invest in deploy gating, API circuit breakers, data-quality alerts.

### 4.4 (Optional) Fault Tree Probability
`P(OR) = 1 − ∏(1 − p_i)`; `P(AND) = ∏ p_i`.
**Worked example:** P(Stripe 5xx in month) = 0.02; P(retry flag off) = 0.10. AND gate: P(Payment down) = 0.02 × 0.10 = **0.002** (0.2%). Threshold: below 0.005 acceptable for non-critical path; above requires mitigation.

---

## 5. Do vs Don't

| Do | Don't |
|---|---|
| Stop 5-Why at a **systemic** cause (process, tool, policy) | Stop at "engineer pushed bad code" — that is human error, not root cause |
| Score RPN against **written, pre-agreed anchors** (S=8 means X) | Score RPN on vibes — different raters give wildly different numbers |
| Run fishbone with a **cross-functional** quorum (Eng + Data + PM + SRE) | Fishbone alone at your desk — you will miss 3 of 6 branches |
| **Validate** candidate root causes with data (logs, metrics, query) before fixing | Jump from hypothesis to fix — 40% of "root causes" are wrong |
| Write a **blameless postmortem** focusing on system + guardrails | Name individuals as root cause — destroys reporting culture |
| Timebox RCA (e.g., 72h for SEV1) and ship a **temporary mitigation** in parallel | Block remediation until RCA is "perfect" — customer bleeds |
| Track RCA action items in Jira with **owners + due dates + closure evidence** | Close RCA at the retro meeting without tracked actions |
| Use FMEA **before** launch as pre-mortem | Only use FMEA post-incident — that is just RCA renamed |
| Separate **triggering** cause from **contributing** causes from **systemic** cause | Pick one cause and move on — most SEV1s have 3–5 causes |

---

## 6. Real-Life Scenarios

### 6.1 SaaS Incident RCA — Fishbone + 5-Why + Pareto
**Context:** B2B SaaS, 4% of Android EU checkout sessions return 500 since 04-15.
**Flow:**
1. PagerDuty fires, Sentry groups errors, Datadog shows EU-Frankfurt spike.
2. Is/Is-Not in Confluence scopes problem to EU Android post-SDK-upgrade.
3. Fishbone workshop (60 min, 6 roles) populates 6M; top suspects: Tech (SDK), Data (feature flag schema), Process (no staged rollout in EU).
4. 5-Why on Tech branch: SDK retry logic changed → why? library bump → why? transitive dep → why? no lockfile for mobile → **systemic: mobile CI lacks dep pinning**.
5. Pareto of last-quarter 500s shows 42% deploy-related → confirms priority.
**Tools:** Jira (actions), Sentry (grouping), Datadog (metrics), Confluence (postmortem), PagerDuty/Rootly (timeline).
**Outcome:** Pin mobile deps, add canary to EU, runbook entry. MTTD improved from 47 min → 8 min.

### 6.2 ML Accuracy Regression — FMEA on Feature Pipeline
**Context:** Fraud model F1 dropped from 0.82 → 0.76 over two weeks.
**Flow:**
1. MLflow model registry shows no model change → suspect data.
2. Evidently drift report flags feature `merchant_category_code` null rate ↑.
3. Team runs FMEA on feature pipeline (see §3.3 table). RPN 336 (null from upstream), 288 (drift undetected), 216 (label delay).
4. Actions: schema contract on Kafka topic (Protobuf + CI), shadow eval gate in MLflow, freshness SLO in Datadog.
5. Revised RPN table in 30 days: 336 → 48, 288 → 60.
**Outcome:** F1 recovers to 0.81; pipeline now pre-mortem'd quarterly.

### 6.3 ANTI-EXAMPLE — Blame-Focused RCA
**Context:** Fintech SEV1 — bad migration script dropped 2% of orders.
**Wrong RCA:** RCA notes read "Root cause: Engineer X ran migration without dry-run. Action: Engineer X coached." Ticket closed in 48h.
**What was missed:** No migration CI gate, no staging parity, no rollback script, no deploy freeze calendar, reviewer approved without checklist.
**3 months later:** Identical class of incident — 6% of payments double-charged. Cost: ~$420k in refunds + chargebacks, regulator inquiry, 1 senior engineer resigned citing blame culture, hiring slowdown.
**Quantified cost of shallow RCA:** $420k direct + ~$180k opportunity (frozen roadmap) + attrition cost ~$150k = **~$750k** vs the ~$8k it would have taken to build a migration CI gate the first time.
**Lesson:** Stopping at "human error" is the most expensive stopping point possible.

---

## 7. Implementation Playbook
1. **Declare** incident + scope in PagerDuty/Rootly; open Jira RCA ticket; assign facilitator (not the on-call who fixed it).
2. **Scope** with Is/Is-Not matrix in Confluence within 24h; attach Datadog + Sentry evidence links.
3. **Diverge** via Fishbone workshop (6M adapted, cross-functional, 60–90 min) — capture all candidate causes.
4. **Drill** the 2–3 hottest branches with 5-Why; enforce systemic stopping rule + evidence per step.
5. **Quantify** with FMEA worksheet: score S/O/D against anchors; rank by RPN; flag S≥9 rows.
6. **Validate** top causes with data queries (Datadog, Sentry, warehouse) — prove, don't assume.
7. **Commit** action items: Jira tickets with owners, due dates, and verification metric (e.g., "MTTD < 10 min for 30 days").
8. **Publish** blameless postmortem (A3 one-pager + long-form) in Confluence; review in weekly ops; close loop at 30/60/90 days with revised RPN + recurrence check.

---

## 8. Content Quality Audit

**Covered well in source:** Fishbone, 5 Whys, FMEA, FTA definitions; Analyze-phase anchoring; cross-functional involvement; the granola-bar + data-center examples are crisp.

**Underplayed / missing in source:**
- No **RPN formula** or Severity/Occurrence/Detection anchor scales.
- No mention of **Apollo RCA / causal trees** (Gano) as an evidence-based alternative to 5-Why.
- No **blameless postmortem** protocol — critical for software/SRE context.
- No **A3 report** structure (Toyota) for concise framing.
- No **data validation** step for candidate causes — source says "validate" but gives no method.
- No **detection-rating anchors** — common FMEA failure mode in practice.
- No anti-example covering blame-focused RCA cost.
- No tie to **Is/Is-Not (Kepner-Tregoe)** scoping before RCA.

**Supplements (≥5):**
1. Dekker, S. (2014). *The Field Guide to Understanding 'Human Error'* (3rd ed.). Ashgate/CRC. — systemic vs blame framing.
2. Allspaw, J. (2016). *Etsy Debriefing Facilitation Guide*. Etsy/Adaptive Capacity Labs. — blameless postmortem protocol.
3. Liker, J. (2020). *The Toyota Way* (2nd ed.). McGraw-Hill. — A3 thinking, genchi genbutsu, true 5-Why practice.
4. Beyer, B., Murphy, N. R., Rensin, D. K., Kawahara, K., Thorne, S. (2018). *The Site Reliability Workbook*, Ch. "Postmortem Culture: Learning from Failure". O'Reilly.
5. Gano, D. L. (2007). *Apollo Root Cause Analysis: A New Way of Thinking* (3rd ed.). Apollonian Publications. — causal-chain method.
6. Carroll, J. S., Rudolph, J. W., Hatakenaka, S. (2002). "Lessons Learned from Non-Medical Industries: Root Cause Analysis as Culture Change at a Chemical Plant," *Quality & Safety in Health Care*, 11(3), 266–269. — why RCA often fails organizationally.
7. AIAG-VDA (2019). *FMEA Handbook* (1st ed.). AIAG/VDA. — current standard replacing AIAG 4th ed.; introduces Action Priority (AP) table as RPN alternative.

**Red flags in source:**
- Uses purely manufacturing/process-safety examples (granola bars, landing gear, reactor); zero IT/AI/Product framing despite modern readership.
- Implies RCA = symptom avoidance without teaching **how** to validate — risks teaching ritual rather than rigor.
- Does not warn about blame culture — dangerous omission for software leaders adopting Six Sigma.
- Presents FMEA without the RPN formula or anchor scales — renders it non-operational.

---

## 9. Quick-Recall Card
- RCA finds **systemic** causes; symptoms are the starting line, not the finish.
- Toolkit: Is/Is-Not (scope) → Fishbone (diverge) → 5-Why (drill) → FMEA (prioritize) → FTA (combinatorics) → Pareto (rank).
- `RPN = S × O × D`; act at ≥200 or S≥9; always score against written anchors.
- Stop 5-Why at systemic, never at "human error"; depth ≥ 3, every step evidence-backed.
- Blameless postmortems + tracked Jira actions + 30/60/90 closure = RCA that actually changes outcomes.
- **Role-lens question:** As an engineering/product/consulting leader, what is the last "root cause" your team accepted that was actually a person's name — and what systemic guardrail would have caught it instead?

---

**Connects to:** [05-analyze-phase.md](05-analyze-phase.md), [07-control-phase.md](07-control-phase.md), [../business-analytics/03-diagnostic-analytics.md](../business-analytics/03-diagnostic-analytics.md), [../causal-analysis-business/01-causation-vs-correlation.md](../causal-analysis-business/01-causation-vs-correlation.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:5, 6:5, 7:4, 8:5, 9:4, 10:4]
Sections rewritten: [3.1 Fishbone ASCII, 3.3 FMEA with anchors, 4.1 RPN thresholds, 6.3 anti-example cost quantification, 8 supplements]
Enrichments applied: [cross-course links; 7 supplements incl. AIAG-VDA 2019; blame-focused anti-example with $750k cost; IT/AI/Product tooling (Jira, Sentry, Datadog, Rootly, MLflow, Evidently); role-lens question; Is/Is-Not added; RPN formula + anchor rules]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:20
Audited by: A3
-->
