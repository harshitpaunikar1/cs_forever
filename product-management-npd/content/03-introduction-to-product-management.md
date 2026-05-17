# Introduction to Product Management

## Overview

Product management is the discipline of deciding what to build and guiding it from idea to launch and beyond. It blends business strategy, customer empathy, and technical judgment. A product manager is not a project manager — project management tracks tasks, product management owns outcomes.

---

## Why It Matters

Companies that practice real product management ship fewer features but more that customers love. This reduces engineering waste, speeds up learning, and builds a stronger brand. Without the discipline, teams drift — building whatever the loudest voice in the room wants.

## Key Principles

- Outcome over output: success is measured by customer and business impact.
- Discovery before delivery — understand the problem before designing the solution.
- Small bets, fast feedback: ship, measure, adjust.
- Align the team around a shared vision and clear priorities.
- Keep a long-term view but work in short cycles.

## Key Terms

| Term | Definition |
|------|------------|
| **Discovery** | The work of validating a problem and solution before building. |
| **Delivery** | The work of building, shipping, and iterating on the chosen solution. |
| **MVP** | Minimum Viable Product — the smallest version that delivers real value. |
| **Product Vision** | A clear picture of where the product is headed in 2-5 years. |
| **Prioritization** | Choosing what to do now, next, and never. |

## Use Case

A logistics SaaS company has a strong engineering team but no PM function. Sales promises features to close deals, engineers burn out building one-offs, and churn rises. Hiring a head of product who introduces discovery, prioritization, and roadmap discipline turns the ship within two quarters.

## Scenario

> A mobility startup had 14 features in flight and shipped none on time. A new product lead froze all work, ran a one-week prioritization exercise with leadership, and chose three bets for the next 90 days. Delivery predictability rose from 20% to 85% and the team's NPS jumped.

## Examples

- A fintech PM cancels a "crypto wallet" feature after discovery shows core users want faster bank transfers instead.
- A healthcare app PM ships an MVP appointment-reminder feature in two weeks, validates demand, then invests in a full scheduling redesign.

---

## Audited Appendix

# Introduction to Product Management
**Course:** Product Management and New Product Development
**Module:** Content / Introduction
**Audited on:** 2026-04-18
**Source files reviewed:** `product-management-npd/content/03-introduction-to-product-management.md`

---

## 1. Topic Snapshot
The PM discipline: deciding what to build and guiding it end-to-end. For an IT/AI/Product/Consulting leader, this frames the operating model that ships fewer features, learns faster, and produces less waste than a ticket-factory. Decision it helps make: *"Given a portfolio of asks, which belong in 'Now', which in 'Next', which to kill — and how do I create a system that makes those choices repeatable?"*

Cross-reference: role definition, RICE, and outcome hierarchy in `product-management-npd/01-role-of-product-managers.md`. Continuous discovery in `04-product-ideation-techniques.md`. Agile in `12-agile-product-development.md`.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Discovery | — | Validate problem + solution before building | Reduces delivery waste | # problems validated per quarter | Cagan, Torres |
| Delivery | — | Build, ship, iterate | Core engineering output | Velocity, quality | Agile |
| MVP | Minimum Viable Product | Smallest version delivering real value | Enables learning cheaply | First-ship scope | Lean startup |
| MMP | Minimum Marketable Product | Smallest version fit for paid use | Commercial-readiness threshold | Feature completeness | Enterprise product |
| MLP | Minimum Lovable Product | Smallest scope with delightful UX | Counterweight to feature-thin MVPs | NPS, qualitative love | Consumer product |
| Product Vision | — | 2-5 year directional picture | Anchors strategy | Memorability; employee recall | Strategy |
| North Star | — | One metric that captures user value delivered | Operational anchor | Value (user, not revenue) | PLG, SaaS |
| Prioritisation | — | Choosing Now / Next / Never | Core PM skill | Roadmap discipline | PM practice |
| Now-Next-Later | — | Horizon roadmap | Communicates without false precision | Horizon coverage | Modern PM |
| Outcome | — | Measurable user/business result | Vs output (features shipped) | OKR attainment | PM |
| Build-Measure-Learn | — | Lean-startup loop | Hypothesis-driven product dev | Loop cycle time | Lean startup (Ries) |
| Hypothesis | — | Testable "we believe X will cause Y" | Structures learning | Test framed | Lean, product |
| Validated Learning | — | Knowledge gained from a test | Lean startup output | Learnings documented | Lean |
| Pivot | — | Significant change in direction after learning | When hypothesis fails | # pivots / cycle | Lean, startup |
| Persevere | — | Continue current strategy | Alternative to pivot | — | Lean |
| Kill Criteria | — | Pre-committed thresholds for killing | Objectivity on sunk cost | Explicit criteria | Lean, portfolio |
| Feature Factory | — | Shipping output without measuring outcomes | Anti-pattern | Output-focused KPIs | Perri |
| Product-Market Fit | PMF | Product serves a strong market demand | Gate for scaling | Sean Ellis 40% test; retention curves | Startup |
| Sean Ellis Test | — | "Very disappointed if product disappeared" ≥ 40% | PMF proxy | Survey % | Startup |
| Scope Creep | — | Uncontrolled expansion of scope | Kills delivery predictability | % scope delta | Project |
| Product Strategy | — | Choices to win in chosen market | Links vision to execution | Strategy coherence | Product leadership |
| Product Principle | — | Guardrail for decisions (e.g., "simplicity over features") | Makes tradeoffs repeatable | # decisions using principle | Product teams |

> `MMP`, `MLP`, `Now-Next-Later`, `Build-Measure-Learn`, `Hypothesis`, `Validated Learning`, `Pivot/Persevere`, `Kill Criteria`, `Feature Factory`, `PMF`, `Sean Ellis Test`, `Product Principle` are standard extensions. `[verified from model knowledge, not source]`.

---

## 3. Frameworks & Matrices

### Framework 1: Discovery → Delivery Loop (with Kill Gate)
**Purpose:** Ensure ideas earn their way into delivery via validated discovery; provide explicit off-ramps.

**Text Diagram:**
```
     ┌──────────────────┐       ┌──────────────────┐
     │ IDEA / REQUEST    │──────►│  DISCOVERY        │
     │ (from anywhere)   │       │  (interviews,    │
     │                   │       │   prototypes,    │
     │                   │       │   market check)  │
     └──────────────────┘       └──────┬──────────┘
                                        │
                       pass kill gate? ─┴─ NO ─► KILL (document learnings)
                          (validated
                           problem +
                           viable solution?)
                                        │ YES
                                        ▼
                                  ┌──────────────────┐
                                  │  DELIVERY         │
                                  │  (build, ship,   │
                                  │   iterate)       │
                                  └──────┬───────────┘
                                         │
                                         ▼
                                  ┌──────────────────┐
                                  │  POST-LAUNCH     │
                                  │  MEASURE (30/60/ │
                                  │  90 day review)  │
                                  └──────┬───────────┘
                                         │
                                         │  outcome vs predicted
                                         ▼
                                  learn → next discovery
```

Components:
- **Kill gate:** explicit criteria; no feature enters delivery without passing
- **Post-launch review:** 30/60/90-day impact check; results feed next discovery

**IT/AI/Product/Consulting worked example:** A SaaS PM receives "add AI summarisation" request. Discovery: 10 interviews reveal users don't want summarisation — they want semantic search. Kill the summarisation ask; pivot to search. Ship MVP in 8 weeks. 60-day review: 25% engagement lift; validated. Next discovery: expand search to cross-document scope.

**When to pull this out in a meeting:** Any "why did we build that?" moment; kickoff of new quarter.

---

### Framework 2: MVP vs MMP vs MLP Decision Grid
**Purpose:** Pick the right "minimum" for your context — "viable" isn't always enough.

**Text Diagram:**
```
                          MARKET CONTEXT
                   Early stage / learning      Mature market / competitive
              ┌────────────────────────┬──────────────────────────────┐
  AUDIENCE    │                         │                              │
  Enterprise  │  MVP                     │  MMP                         │
              │  (learn + few customers) │  (marketable; won't ship to  │
              │                          │   paying enterprise without  │
              │                          │   baseline functionality)    │
              ├────────────────────────┼──────────────────────────────┤
  Consumer    │  MVP                    │  MLP                          │
              │                          │  (emotional connection,      │
              │                          │   delightful UX differentiate│
              │                          │   in crowded market)         │
              └────────────────────────┴──────────────────────────────┘
```

Components:
- **MVP:** learning-focused; small user base; acceptable rough edges
- **MMP:** enterprise-grade baseline (SSO, audit logs, SLA) needed to sell
- **MLP:** consumer context; emotional appeal matters

**IT/AI/Product/Consulting worked example:** A GenAI startup for code review debates scope.
- B2B enterprise → MMP required: SSO, SOC-2, audit trails, role-based access, contractual SLA. "MVP without these" won't sell.
- Consumer-free-tier → MLP: strong UX, emotional delight (GitHub-Copilot-level polish), otherwise users don't switch.

**When to pull this out in a meeting:** MVP-scope debates; enterprise vs SMB release planning.

---

### Framework 3: Pivot/Persevere/Kill Decision Matrix
**Purpose:** Force an objective decision when the learning is in.

**Text Diagram:**
```
                  METRIC vs TARGET
              < 50%          50-80%          80-120%        > 120%
         ┌───────────────┬────────────────┬───────────────┬────────────────┐
 TIME    │               │                │               │                │
 SPENT   │   KILL        │    PIVOT       │  PERSEVERE    │   SCALE UP     │
 < 50%   │   (fast fail  │   (tweak        │  (on track)   │  (over-perform;│
  of     │    saves      │    approach;   │               │   invest more) │
 runway  │    capital)   │    2nd try)    │               │                │
         ├───────────────┼────────────────┼───────────────┼────────────────┤
 > 50%   │   KILL        │    KILL OR     │  PERSEVERE    │   SCALE        │
 of      │    (cannot    │    PIVOT HARD  │  (validate    │                │
 runway  │    recover)   │    (last       │   with        │                │
         │               │    chance)     │   confidence) │                │
         └───────────────┴────────────────┴───────────────┴────────────────┘
```

Components:
- Pre-commit thresholds: % of target AND time/capital spent
- Removes ego from the decision

**IT/AI/Product/Consulting worked example:** A B2B feature launched; target 25% adoption in 60 days. At day 30: adoption 9%. Time spent 50% of budget → Kill-or-pivot-hard cell. Team chooses pivot: ship an opinionated default-on variant. Day 60: adoption 22%. Persevere.

**When to pull this out in a meeting:** 30/60/90-day launch reviews; budget-approval gates.

---

## 4. Formulas

### Formula 1: Sean Ellis Test for PMF
**Formula:** `PMF Signal = (% users "very disappointed" if product disappeared)`

**Variables:**
- Ask current active users: "How would you feel if you could no longer use [product]?"
- Options: Very disappointed / Somewhat disappointed / Not disappointed / N/A

**Why this formula exists:** Simple, cheap PMF proxy. Widely adopted.

**How to interpret the output:**
- \> 40% very disappointed → PMF signal
- 30–40% → almost; investigate segment heterogeneity
- < 30% → not yet PMF; don't scale

**Worked example:** 200 active users surveyed: 95 very disappointed, 55 somewhat, 40 not, 10 N/A.
- % very disappointed = 95/200 = 47.5% → PMF signal.

**Data source:** Typeform or in-product survey; filtered to active users; quarterly cadence.

---

### Formula 2: Time-to-Ship-MVP (Cycle Time)
**Formula:** `MVP Cycle Time = (Ship Date − Idea Date)` in days

**Variables:**
- Ship Date = first real user exposure
- Idea Date = hypothesis documented

**Why this formula exists:** Measures discovery + delivery velocity. Shorter = faster learning.

**How to interpret the output:**
- < 30 days → highly experimental (good for early-stage)
- 30–90 days → typical for SaaS features
- \> 90 days → likely over-scoped; check if you're shipping MMP when MVP was fine

**Worked example:** Team ships 6 MVPs in a year; median cycle time 45 days. 1 outlier at 180 days (over-scope) → identified; team restructured to cut scope on large projects.

**Data source:** Jira / Linear timestamps; dashboard in Metabase.

---

### Formula 3: Outcome Review Ratio
**Formula:** `Outcome Review Ratio = (# launches with 30/60/90 review) / (Total launches)`

**Variables:**
- Launches = shipped features/products
- Reviews = formal post-launch impact reviews

**Why this formula exists:** Proves whether the team is operating with an outcome mindset or a ship-and-forget mindset.

**How to interpret the output:**
- < 50% → feature factory; add discipline
- 50–90% → normal; improve
- \> 90% → outcome-first org

**Worked example:** Product team ships 40 launches this year, runs 22 post-launch reviews → Ratio 55%. Install process: every launch auto-creates a scheduled review in 30/60/90 days.

**Data source:** Launch tracker in Notion; review status per launch.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|-------|
| Launch features with no post-launch review | Schedule 30/60/90 reviews at launch time; cancel only on deliberate decision |
| Define MVP as "everything we can't cut" | Define MVP as "smallest thing that tests the hypothesis"; enterprise may need MMP |
| Skip kill criteria | Pre-commit kill thresholds at project kickoff |
| Call every course change a "pivot" | Define pivot vs persevere with data, not emotion |
| Confuse product management with project management | PM owns outcomes; project manager owns tasks/dates |
| Treat "discovery" as an afterthought | Institutionalise weekly customer touches |
| Sell features to close deals (sales-led roadmap) | Product commitments go through RICE + outcome-fit check |
| Manage roadmap by date commitments | Now/Next/Later horizons; commit dates only in Now |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: Startup Choosing MVP Scope for an Enterprise Sale
**Situation:** Seed-stage AI startup lands a $200k pilot with a large bank. Bank requires "enterprise basics." Team debates: ship pure MVP vs MMP.

**Applicable framework/metric:** MVP vs MMP + Time-to-Ship.

**Analysis:**
- Bank requires: SSO, audit logs, data-residency, role-based access. Non-negotiable.
- Pure MVP = 4 weeks; MMP = 10 weeks.
- Revenue risk if MVP shipped: deal falls through → $200k lost + reputation.

**Decision rule:** In enterprise B2B, ship MMP; in consumer, MVP often works.

**Action (Monday morning):** Commit to 10-week MMP plan. Break down into 2 sprints: security foundations (SSO, audit), then integration + residency. Keep UX minimal; don't gold-plate beyond MMP scope.

---

### Scenario 2: Consulting Firm Advising on Feature Factory Cleanup
**Situation:** A 2,000-person enterprise software client ships 60 features/year; retention flat; 40% of features used by < 5% of customers.

**Applicable framework/metric:** Discovery → Delivery Loop + Outcome Review Ratio.

**Analysis:**
- Outcome Review Ratio today: 18% (10 of 55 launches reviewed)
- 70% of features shipped with no predicted outcome metric
- Install: discovery gate, kill gate, 30/60/90 reviews, outcome-attached roadmap

**Decision rule:** After 12 months, target Outcome Review Ratio > 80% and feature-factory metric (features shipped with no outcome review) < 10%.

**Action:** Roll out processes; quarterly audits; retire dashboards that lack outcome ties. Pair each launch with a review auto-scheduled at 30/60/90 days.

---

### Scenario 3 (Anti-example): Sales-Led Roadmap Kills PMF
**Situation:** A 40-person SaaS lets sales promise features to close each deal. 18 months later: retention flat, roadmap full of one-offs, core product diluted.

**Applicable framework/metric:** Product Strategy + Outcome Hierarchy.

**Analysis (what goes wrong):**
- 70% of quarterly engineering went to bespoke commitments for 12 customers
- Core product hasn't advanced meaningfully in 18 months
- Customers renewing out of inertia; new logos struggle to see the value
- PMF signal dropped from 44% to 29%

**Cost of this mistake:** 18 months wasted; 15 engineer-years on one-off work; $8M of missed core-product investment.

**Decision rule:** Customer commitments go through a RICE + outcome-fit check; commitments that don't roll up to the roadmap are declined.

**Action:** Freeze custom-feature commitments for 60 days. Audit pipeline: can we renew without the bespoke? (Usually yes.) Re-align team on core product; reintroduce Now/Next/Later roadmap with outcome commitments.

---

## 7. Implementation Playbook

1. **Institutionalise the Discovery → Delivery → Review loop** — kickoff template with kill gate; launch template with 30/60/90 review.
2. **Pre-commit kill criteria at project start** — template: "kill if [metric] < [threshold] by [date]."
3. **Adopt a launch tracker** — Notion DB; status for each launch including review dates and outcomes.
4. **Run quarterly PMF surveys per segment** — Sean Ellis test; track trend.
5. **Publish an outcome review dashboard** — % of launches with review; outcome-vs-predicted gaps.
6. **Train team on MVP vs MMP vs MLP mental model** — context matters; not all "minimum" is equal.
7. **Use Now/Next/Later roadmap** — commit dates in Now only.
8. **Establish product principles** — 3–5 guardrails (e.g., "simplicity over configurability") codified; referenced in decisions.

---

## 8. Content Quality Audit

**Covered well:**
- Distinguishes PM from project management.
- Notes outcome-over-output.
- Introduces MVP, discovery, delivery, prioritisation, vision.
- Scenario (mobility startup freezing & reprioritising) is realistic.

**Underplayed or missing:**
- No MMP / MLP distinction.
- No Sean Ellis / PMF measurement.
- No kill criteria or pivot/persevere formalism.
- No Build-Measure-Learn operationalisation.
- Ried/Christensen/Perri absent.
- No product-principle concept.

**Supplement with:**
- *The Lean Startup* — Eric Ries (2011, Crown). Build-Measure-Learn; pivot taxonomy.
- *Escaping the Build Trap* — Melissa Perri (2018, O'Reilly). Feature factory → outcome org.
- *Inspired* — Marty Cagan (2017). Modern PM discipline.
- *Product-Led Growth* — Wes Bush (2019). PMF and PLG mechanics.
- Sean Ellis' blog on PMF + 40% test (growthhackers.com).
- David Skok on metric-driven SaaS (forentrepreneurs.com).
- *Intercom on Product Management* — free ebook (intercom.com).
- HBR: "Why Most Product Launches Fail" — Joan Schneider & Julie Hall, *HBR*, Apr 2011.
- HBR: "What Makes a Great Product Manager" — various *HBR* essays.
- HBS case: "Dropbox: It Just Works" — MVP to scale.
- HBS case: "Warby Parker: Vision of a 'Good' Company" — product principles in practice.
- IIMA case: "Swiggy's Product Strategy" — Indian-context product decisions.

**Red flags in the source:**
- Defines MVP correctly but not MMP/MLP — leaves reader thinking MVP is always right.
- "Ship, measure, adjust" — aspirational without review discipline (no 30/60/90).
- No kill criteria — classic source of feature-factory behaviour.
- Scenario uses "delivery predictability rose from 20% to 85%" but doesn't show the prioritisation mechanism behind it.

**Connects to:**
- `audit_management_course/product-management-npd/01-role-of-product-managers.md` (role definition)
- `audit_management_course/product-management-npd/04-product-ideation-techniques.md` (ideation)
- `audit_management_course/product-management-npd/11-product-lifecycle-management.md` (PLC)
- `audit_management_course/product-management-npd/12-agile-product-development.md` (Agile method)
- `audit_management_course/product-management-npd/15-time-to-market-reduction.md` (TTM)
- `audit_management_course/startup-strategy/04-lean-startup-methodology.md` (lean startup)
- `audit_management_course/startup-strategy/06-product-market-fit.md` (PMF)
- `audit_management_course/strategic-management/10-strategy-execution.md` (execution discipline)

---

## 9. Quick-Recall Card

```
Topic: Introduction to Product Management
Core idea: Ship fewer, learn more. Discovery before delivery. Outcomes over outputs.
Key metric/formula: Sean Ellis PMF > 40%; MVP Cycle Time; Outcome Review Ratio > 80%.
Framework trigger: New initiative kickoff; launch; 30/60/90 review; PMF evaluation.
Watch out for: Feature factory, sales-led roadmap, MVP where MMP is required.
Monday action: Install 30/60/90 review per launch; pre-commit kill criteria at kickoff.
As a PM/Consultant/AI Lead, the one question to answer with this framework is:
"For every feature on the roadmap, can I state the hypothesis, the kill criterion, and the review date?"
```

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Pass 1 average: 4.8
Sections rewritten: none (no criterion <4/5)
Enrichments applied: [cross-course links to product-management-npd/01, 04, 11, 12, 15; startup-strategy/04, 06; strategic-management/10. Ries 2011, Perri 2018, Cagan 2017, Bush 2019, Ellis PMF blog, Skok SaaS, Intercom ebook. HBS Dropbox + Warby Parker, IIMA Swiggy. Anti-example Scenario 3 (sales-led roadmap kills PMF). Data sources: Typeform PMF surveys, Jira/Linear cycle time, Notion launch tracker. Decision-maker view in Quick-Recall.]
Final scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] — average 5.0
Pass 2 completed: 2026-04-18 02:05
-->
