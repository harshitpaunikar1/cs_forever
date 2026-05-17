# Inter-Group Relations and Role Relationships Management

## Overview

Inter-group relations are the interactions between different teams inside an organization, like sales and operations. Role relationships are the expectations each person holds about what others should do. When roles are unclear or groups compete, the business loses time and money.

---

## Why It Matters

Cross-team fights cost more than external competition for many companies. Deals stall because sales and credit disagree. Products slip because engineering and marketing work to different calendars. Managing these relationships is a core senior skill.

## Key Principles

- Name roles clearly. Use a tool like RACI so everyone knows who decides.
- Shared goals beat siloed metrics. If two teams have opposing KPIs, they will fight.
- Build bridges before you need them. Cross-team relationships are easier to use than to build in a crisis.
- Surface conflict early. Avoidance is not peace; it is a buildup of pressure.
- Leaders set the tone. If bosses compete, their teams will too.

## Key Terms

| Term | Definition |
|------|------------|
| **Inter-Group Relations** | The patterns of cooperation, conflict, and communication between teams. |
| **Role Clarity** | A shared understanding of what each person is responsible for. |
| **Role Conflict** | Tension that arises when a person faces mismatched expectations from different sources. |
| **RACI** | A chart that lists who is Responsible, Accountable, Consulted, and Informed on a task. |
| **Boundary Spanning** | The practice of working across team lines to share information and align action. |

## Use Case

A new head of operations at an e-commerce firm finds finance and operations blaming each other for missed cut-offs. She runs one joint workshop to map the end-to-end order flow and agree a single cut-off rule, ending months of friction.

## Scenario

> A pharma company's research and regulatory teams blamed each other for slow drug approvals. The new CEO paired a research lead with a regulatory lead on every project from day one. Approval times dropped by thirty percent and relationships improved visibly.

## Examples

- A bank introduces a weekly fifteen-minute standup between relationship managers and credit underwriters and cuts approval cycles by forty percent.
- A software firm defines a RACI for incident response and stops the usual cross-team finger-pointing during outages.

---

## Audited Appendix

# Inter-Group Relations and Role Relationships — Audit File

---

## 1. Jargon Buster

| # | Term | Plain-Language Definition | Why It Matters in Tech/Product/AI |
|---|------|--------------------------|-----------------------------------|
| 1 | **Inter-Group Relations** | The patterns of cooperation, competition, communication, and conflict that exist between two or more distinct teams or departments. | In tech orgs, this governs how Engineering, Product, Design, Data Science, and DevOps actually work together — or against each other — on shared deliverables. |
| 2 | **Role Clarity** | A shared, documented, and agreed understanding of what each person or team is responsible for — including decision rights, ownership, and boundaries. | Without it, two engineers both "own" the API contract, or no one does. Ambiguity = duplicated work or dropped balls. |
| 3 | **Role Conflict** | The tension experienced when expectations from two or more sources about how a role should behave are contradictory or mutually exclusive. | A Product Manager caught between a VP pushing rapid releases and an engineering lead demanding stability faces classic role conflict. |
| 4 | **RACI** | An acronym for Responsible (does the work), Accountable (single decision owner), Consulted (input before decision), Informed (notified after). A matrix format that maps these to tasks. | The most widely used tool in tech project management to eliminate "who decides?" arguments before they start. |
| 5 | **Boundary Spanning** | The act of an individual or role operating at the intersection of two or more teams, actively transferring information, translating norms, and aligning goals across group lines. | Technical Program Managers, Staff Engineers, and AI Product Owners routinely boundary-span between ML Research, Platform, and Business stakeholders. |
| 6 | **Silo Effect** | The tendency of groups to hoard information, optimize for their own metrics, and resist collaboration — resulting in fragmented output and misaligned priorities at the org level. | Sales chasing logo count while Delivery chases utilization rate is a classic silo producing failed client engagements. |
| 7 | **Realistic Conflict Theory (Sherif)** | Muzafer Sherif's finding that inter-group hostility arises naturally when groups compete for limited, incompatible resources or goals — and that it can be resolved by introducing superordinate goals both groups need. | When ML Platform and Data Engineering fight over GPU cluster access and headcount, Sherif predicts escalating hostility. The fix is a shared OKR (e.g., "model deployment time < 4 hours") both teams must hit together. |
| 8 | **Superordinate Goal** | A goal that is compelling to all groups involved, cannot be achieved by any single group alone, and therefore requires inter-group cooperation to accomplish. | "Ship the AI feature before competitor X" unifies PM, Eng, and Design when nothing else will. Must be genuine, not manufactured. |
| 9 | **DACI** | Driver (moves the work forward), Approver (has final say), Contributor (provides input/execution), Informed (kept in loop). An alternative to RACI preferred by some product-centric orgs (Atlassian, etc.). | Useful when RACI feels too linear — DACI emphasizes who is driving forward momentum, which is often the critical missing element in stalled cross-team work. |
| 10 | **Role Ambiguity** | A state where the scope, expectations, or success criteria of a role are unclear — distinct from role conflict in that the issue is absence of clarity rather than competing demands. | A newly formed "AI Governance Lead" role with no charter, no reporting line clarity, and no defined deliverables will underperform regardless of individual talent. |

---

## 2. Frameworks & Mental Models

### Framework 1: RACI Matrix — Worked IT Example

**Context:** A mid-size SaaS company is launching a new API rate-limiting feature affecting Engineering, Product, Security, and Customer Success.

| Task / Decision | Product Manager | Engineering Lead | Security Architect | Customer Success | Legal |
|----------------|----------------|------------------|--------------------|-----------------|-------|
| Define rate-limit thresholds | A | R | C | C | I |
| Design technical implementation | I | R | C | I | — |
| Security threat model review | I | C | R | — | I |
| Customer communication plan | C | I | I | R | A |
| Go/No-Go launch decision | A | C | C | C | C |
| Post-launch incident response | I | R | C | C | I |

**How to Read:** Only one A per row. R does the work. C must be consulted before the decision is made. I receives notice after.

**RACI Anti-Pattern Alert:**
- Multiple As in one row = accountability diffusion ("everyone is responsible" = no one is)
- R without A = orphaned work
- Too many Cs = decision paralysis by committee
- No Is = surprises at launch

**Rule:** If your RACI has more than 2 Cs per row, challenge whether all consulted parties are truly necessary or are there for political coverage.

---

### Framework 2: Sherif's Realistic Conflict Theory — Applied to Engineering vs. Product Conflict

**Sherif's Original Setup (Robbers Cave Experiment):**
1. Two groups form separate identities
2. Groups placed in competition for scarce resources
3. Inter-group hostility escalates — stereotyping, sabotage, refusal to cooperate
4. Introducing superordinate goals (shared water supply failure) dissolves hostility over time

**Applied to Eng-Product Conflict:**

| Sherif Stage | Eng-Product Manifestation |
|-------------|--------------------------|
| Separate identity formation | "Eng team" vs. "Product team" — distinct Slack channels, stand-ups, and success metrics |
| Resource competition | Sprint capacity: Product wants features; Eng wants tech debt reduction. Both cannot fully win. |
| Inter-group hostility | Engineers call PMs "unrealistic." PMs call engineers "obstructionist." Escalations to VPs become weekly. |
| Superordinate goal intervention | Company sets OKR: "Achieve 99.9% uptime while shipping 3 major features this quarter." Both teams must cooperate to hit it. |
| Hostility reduction | Shared retros, shared metrics dashboard, joint on-call rotations reduce us-vs-them framing. |

**Key Insight:** The conflict is not a personality problem. It is a structural one — misaligned resource claims without a shared goal large enough to override group self-interest.

---

### Framework 3: Superordinate Goal Framework

**Definition:** A goal that satisfies all of the following criteria:
1. Perceived as genuinely important by all groups involved
2. Attainable only through inter-group effort
3. Cannot be achieved by any single group acting alone
4. Clear and measurable enough to track progress jointly

**5-Step Implementation:**

1. **Diagnose the inter-group friction** — What resources are they fighting over? What metrics conflict?
2. **Identify the shared stake** — What outcome would hurt both groups equally if it failed? (e.g., product churn, regulatory rejection, customer SLA breach)
3. **Frame the superordinate goal** — Translate shared stake into a specific, metric-bound objective both groups sign onto
4. **Create joint accountability structures** — Mixed-team OKRs, shared retrospectives, co-owned dashboards
5. **Remove competing metrics** — If Engineering is rewarded for velocity and Product for feature count, the superordinate goal is undermined by incentive structures

**Pharma Case Application:** R&D and Regulatory paired from Day 1 on a shared goal of "submission-ready dossier within 18 months." Result: approval times -30% because regulatory requirements shaped R&D design early rather than being a late-stage audit.

---

### Framework 4: Thomas-Kilmann Conflict Mode Instrument (TKI)

**Two Dimensions:** Assertiveness (pursuing your own goals) × Cooperativeness (satisfying others' concerns)

| Mode | Assertiveness | Cooperativeness | When Appropriate in Tech/Product |
|------|--------------|-----------------|----------------------------------|
| **Competing** | High | Low | Security team enforcing non-negotiable compliance requirements |
| **Collaborating** | High | High | Eng + Product designing a system architecture that must meet both performance and UX goals |
| **Compromising** | Medium | Medium | Sprint capacity split between features and tech debt — neither team gets all they want |
| **Avoiding** | Low | Low | Tabling a low-stakes API naming debate until a more critical question is resolved |
| **Accommodating** | Low | High | PM deferring to Security on threat model — domain expertise asymmetry justifies it |

**PM Application:** When entering a conflict between Engineering and Design, first diagnose which mode both parties are currently using. If both are Competing, no resolution is possible without a superordinate goal or a process forcing Collaboration. If one is Avoiding, surface the conflict explicitly — avoidance is pressure buildup, not resolution.

---

## 3. Formulas / Thresholds / Decision Rules

### Formula 1: Role Conflict Index (RCI)

```
RCI = (Number of contradictory directives received in a given period) 
      ÷ (Total number of directives received in that period)
      × 100
```

**Interpretation:**
- RCI < 10%: Healthy — occasional tension, manageable
- RCI 10–25%: Warning zone — role definition review needed
- RCI > 25%: Crisis — the role structure is broken; escalate to leadership

**Example:** A Technical Program Manager receives 40 task directives in a quarter. 12 of them contradict each other (e.g., "accelerate timeline" from PM conflicts with "do not cut testing" from QA lead). RCI = (12/40) × 100 = 30% → Crisis level. Structural intervention required.

---

### Formula 2: Cross-Team Friction Score (CTFS)

```
CTFS = (Number of cross-team escalations in 90 days) 
       + (Number of missed cross-team SLA breaches × 2)
       + (Number of blame-shift incidents documented in retros × 3)
```

**Weighting Rationale:** Missed SLAs are weighted 2× because they have external customer impact. Blame-shift incidents are weighted 3× because they signal cultural corrosion, not just process failure.

**Thresholds:**
- CTFS 0–5: Green — teams working well
- CTFS 6–15: Amber — RACI review and superordinate goal workshop recommended
- CTFS > 15: Red — structural org design intervention; consider a boundary-spanning role (TPM, Integration Manager)

---

### Formula 3: RACI Coverage Check

```
Coverage Score = (Number of tasks with exactly one 'A' assigned)
                 ÷ (Total number of tasks in RACI)
                 × 100
```

**Minimum Acceptable Threshold:** 100%. Every task must have exactly one Accountable party. A Coverage Score below 100% means some tasks have either zero or multiple Accountable parties — both are failures.

**Secondary Check:**
```
Consult Overload Ratio = (Average number of 'C' entries per row)
```
If Consult Overload Ratio > 3, the RACI is being used for political coverage rather than efficiency. Challenge every C: "What specific input do they provide that changes the decision?"

---

### Formula 4: Escalation Threshold Rule

```
Escalate inter-group conflict when ANY ONE of the following is true:
  - The same conflict has recurred > 2 times without resolution
  - The conflict has caused a customer-facing delay or SLA breach
  - The conflict involves a resource decision > [org-defined spend threshold]
  - One or more parties has ceased direct communication (routing through third parties)
  - The Role Conflict Index for any individual involved exceeds 25%
```

**Decision Rule:** Do not escalate minor friction — it resolves naturally. Escalate structural conflicts early. The cost of late escalation grows exponentially: a conflict caught in week 2 requires a 30-minute conversation; the same conflict in week 8 requires a VP-level org redesign.

---

## 4. Do / Don't

### DO

1. **Do assign a single Accountable owner** for every cross-team decision before work begins — ambiguity at the start becomes a conflict at the deadline.

2. **Do create shared OKRs** that span Engineering, Product, and Design — when all three teams succeed or fail on the same metric, cooperation replaces competition.

3. **Do surface role conflicts openly in sprint planning** — bring contradictory directives to the table before they derail execution, not after.

4. **Do use RACI as a living document** — review and update it when scope changes, team membership changes, or when friction spikes.

5. **Do invest in boundary-spanning roles** (TPMs, Staff Engineers, AI Product Owners) proportional to the complexity of cross-team interdependencies.

6. **Do run inter-team retrospectives** after major incidents — not just within-team retros that allow blame to drift outward unchecked.

7. **Do involve downstream teams early** — Regulatory, Legal, and Customer Success should be in the room at design phase, not gate-review phase.

8. **Do quantify cross-team friction** using metrics (CTFS, escalation counts) — what gets measured gets managed.

9. **Do validate RACI coverage** with a Coverage Score check before any sprint or project kickoff.

10. **Do establish escalation protocols in advance** — agreeing on when and how to escalate before conflict occurs removes the political charge from doing so.

11. **Do conduct role clarity workshops** when new teams form, after reorgs, or when onboarding new senior hires who alter existing power dynamics.

12. **Do apply the Thomas-Kilmann lens** before entering any conflict mediation — know which mode each party is operating in before choosing your intervention.

---

### DON'T

1. **Don't assign accountability to a group** — "The Platform Team is accountable" means no individual will act, and everyone will point to the group when things go wrong.

2. **Don't allow opposing KPIs** to persist across teams that must collaborate — if Sales is measured on logos and Delivery on margin, you have a structural conflict factory.

3. **Don't treat avoidance as resolution** — two teams that have stopped fighting because they have stopped communicating are not aligned; they are a pressure vessel.

4. **Don't skip the 'Informed' column in RACI** — surprises at launch, especially for Customer Success or Legal, destroy trust and generate retaliatory friction in future projects.

5. **Don't let the same inter-group conflict recur three times** without a structural intervention — recurring conflict is a systems problem, not a people problem.

6. **Don't run inter-team conflict resolution in public Slack channels** — it creates audiences, encourages performative escalation, and makes resolution harder. Use a private, facilitated space.

7. **Don't assume co-location solves coordination problems** — physical proximity without shared goals and clear roles just makes the conflict louder.

8. **Don't use RACI for political coverage** — adding Cs to protect stakeholders from surprise is a symptom that trust is broken, not a fix for it.

9. **Don't let ML/AI team operate as an island** — AI teams that define success metrics without input from Product and Business create technically impressive models that solve the wrong problems.

10. **Don't escalate before documenting** — escalating a conflict without a written record of the specific clashes, dates, and impacts makes leadership resolution arbitrary and breeds resentment.

11. **Don't confuse role ambiguity with autonomy** — giving a team "freedom to operate" without defining their decision rights or boundaries produces chaos, not innovation.

12. **Don't ignore cross-vendor friction in consulting contexts** — when delivery involves multiple vendors or subcontractors, RACI must extend to them explicitly; role conflicts across organizational boundaries are the most expensive kind.

---

## 5. Metric-Driven Scenarios with Anti-Examples

### Scenario 1: PM-Engineering-Design Chronic Conflict

**Context:** A B2B SaaS company has experienced 14 escalations in one quarter between the Product, Engineering, and Design teams on a core dashboard feature. Velocity has dropped 40% from the previous quarter. Three designers have cited "constant rework requests" as a reason for attrition intentions.

**Root Cause Diagnosis:**
- No shared definition of "design complete" → Engineering begins implementation on mockups still under PM revision
- PM and Design both marking themselves as Accountable for UX decisions in RACI
- Engineering measured on velocity (story points/sprint); Design measured on craft score; PM measured on feature adoption — three independent metrics with no shared one

**Metric-Driven Intervention:**
- Introduce shared metric: "Feature Adoption Rate at 30 days post-launch" — all three teams' Q3 performance review includes it
- Revise RACI: PM = A on feature scope decisions; Design = A on UX decisions within approved scope; Engineering = A on technical feasibility decisions
- Define "design complete" as: Figma file with all states documented + Engineering sign-off on feasibility = locked for sprint
- Track RCI for PM role: reduced from 32% to 8% after RACI revision

**Results:** Escalations dropped from 14 to 2 the following quarter. Velocity recovered to 95% of baseline. Design attrition intentions resolved.

**Anti-Example:** The team runs a "culture workshop" focused on communication styles. No RACI changes, no shared metrics, no role definition revision. Escalations continue. Leadership concludes the individuals are incompatible and begins performance management of the PM — who leaves. The structural problem transfers to the next PM.

---

### Scenario 2: AI/MLOps vs. Platform Team Resource War

**Context:** An AI team building a fraud detection model requires 200 GPU hours per week for training runs. The Platform team that manages the cloud infrastructure is under a cost optimization mandate to reduce GPU spend by 30%. Both teams report to different VPs. Twelve sprint ceremonies have been partially or fully blocked by this resourcing conflict in six months.

**Metrics Surfacing the Problem:**
- Cross-Team Friction Score: 22 (Red zone)
- GPU cost overruns: $340K in two quarters
- Model retraining backlog: 6 weeks behind schedule
- Fraud losses attributable to stale model: $1.2M (estimated, surfaced by Risk team)

**Intervention:**
- Superordinate goal established by CTO: "Fraud detection model must be retrained within 72 hours of concept drift detection — both AI and Platform teams co-own this SLA"
- RACI revised to give AI team A on training schedule, Platform team A on cost optimization approach, shared C on GPU provisioning decisions
- Joint dashboard created: model freshness score + GPU cost per inference tracked by both teams weekly
- Platform team's cost optimization mandate revised: "30% cost reduction without increasing retraining latency beyond 72 hours"

**Results:** GPU spend reduced 22% through scheduling optimization (training during off-peak windows). Retraining backlog cleared in 6 weeks. Fraud losses declined 18% quarter-over-quarter.

**Anti-Example:** Platform team unilaterally implements GPU quotas without consulting AI team. AI team escalates to their VP. VPs go to war in the executive team. CTO eventually rules in favor of AI team. Platform team feels overruled and deprioritizes AI infrastructure requests for the next two quarters — a hidden cost never captured in any metric.

---

### Scenario 3: Consulting Delivery vs. Sales Misalignment

**Context:** A management consulting firm's Sales team has closed 4 AI transformation engagements in one quarter, each with delivery timelines the Delivery team considers 30–40% too aggressive. Two engagements are now in scope dispute with clients. Client satisfaction scores for the practice have dropped from 4.4 to 3.1 (5-point scale) in two quarters.

**Metrics Surfacing the Problem:**
- Scope dispute rate: 50% of active engagements (up from 8%)
- Delivery team CTFS: 18 (Red zone — primarily driven by Sales-Delivery friction)
- Average engagement margin: -12% (engagements losing money due to scope expansion needed to meet sales promises)
- Consultant turnover in AI practice: 3 of 8 senior consultants in 6 months

**Root Cause:** Sales is measured on ARR closed. Delivery is measured on margin and client satisfaction. No shared metric exists. Delivery has no formal Consulted role in the sales process — they are Informed after the contract is signed.

**Intervention:**
- RACI for the sales process revised: Delivery Lead = C on all engagements above $500K (must sign off on timeline and scope before contract execution)
- Shared metric introduced: "Engagement Health Score" (EHS) — composite of margin, client satisfaction, and on-time delivery — included in both Sales and Delivery performance reviews
- Escalation rule: if Delivery Lead flags a timeline as infeasible during C review, Sales cannot proceed without VP approval and client renegotiation
- Role Conflict Index measured for Delivery Leads (who were receiving contradictory directives from Sales to "make it work" and from Finance to "protect margin"): dropped from 38% to 11% after structural change

**Results:** Scope dispute rate dropped to 14% in the next two quarters. EHS increased. Senior consultant turnover stopped. One Sales lead initially resisted the change; their quota was adjusted to include EHS — behavior changed within one quarter.

**Anti-Example:** Firm sends Sales and Delivery teams to a two-day offsite on "collaboration." No structural change to the sales process, no shared metrics, no RACI revision. Relations warm for six weeks. The next large engagement closes with the same aggressive timeline. The cycle repeats. The offsite is labeled a "success" in the internal newsletter.

---

## 6. Practitioner Playbook

### 12-Step Playbook: PM Resolving Recurring Engineering-Design Friction Using RACI + Superordinate Goals

**Situation:** You are a PM who has observed the same Engineering-Design conflict recurring across three consecutive sprints. Symptoms: Design complains engineers implement without reading specs; Engineers complain Design delivers "incomplete" files; retrospectives produce action items that are not followed through.

---

**Step 1: Quantify the Problem Before Convening Anyone**
Pull the data. How many sprint items were returned to Design for revision? How many Engineering tickets were blocked waiting on Design? What is the current RCI for the roles involved? Present numbers, not feelings, in all subsequent conversations.

**Step 2: Conduct 1:1 Interviews with Engineering Lead and Design Lead Separately**
Ask each: "What would a perfect handoff from the other team look like?" and "What is the single decision that causes the most friction?" Do not triangulate in a group setting until you understand each party's model of the problem. You will discover they have different definitions of "done."

**Step 3: Map the Current Implicit RACI**
Before proposing a new one, document what people think the current one is. Interview 3–4 engineers and 2–3 designers about who they believe is accountable for UX decisions, feasibility decisions, and "design complete" calls. Expect disagreement. That disagreement is the diagnosis.

**Step 4: Identify the Superordinate Goal**
What outcome do both Engineering and Design care about that neither can achieve alone? Likely candidates: "User adoption of the feature," "Zero design-related bugs in production," "Launch with no post-launch redesign requests." Frame this as a shared metric both teams will be evaluated on.

**Step 5: Draft a Revised RACI — Alone First**
Using your research, draft a RACI that assigns exactly one A per decision, eliminates duplicate As, and clarifies which decisions Engineering has autonomy over versus which require Design consultation. Share this draft with no one yet.

**Step 6: Validate the Superordinate Goal with Both Leads**
Separately, present the proposed superordinate goal to the Engineering Lead and Design Lead. Ask: "Would achieving this matter to your team?" If yes from both — proceed. If no from either — revise. A superordinate goal that one party does not believe in will not work.

**Step 7: Facilitate a Joint RACI Workshop (60 minutes, structured)**
Use your draft RACI as a starting point, not a finished product. Walk through each decision row. For any row where both Leads want to be A, facilitate a negotiation: "Which of you bears the consequence if this decision goes wrong?" Consequence follows accountability.

**Step 8: Define "Design Complete" and "Engineering Ready" Explicitly**
These are the two handoff points that generate 80% of friction. "Design Complete" = Figma file with all edge cases, error states, mobile variants, and interaction annotations documented, plus a 15-minute walkthrough with the Engineering Lead. "Engineering Ready" = Feasibility confirmed, no open technical blockers, implementation approach agreed. Both definitions must be written and signed off.

**Step 9: Introduce the Shared Metric to Both Teams' Dashboards**
Whatever superordinate goal you identified in Step 6, create a visible metric (e.g., "Feature Adoption at 30 days") and add it to both teams' sprint review dashboards. Review it together in the joint retrospective, not in separate silos.

**Step 10: Run the First Joint Retrospective**
Two weeks into the new structure, run a joint Engineering-Design retrospective. Use the following structure: (a) What did the new RACI make easier? (b) What friction remains? (c) What does the shared metric tell us? Do not allow it to become a blame session — focus on the system, not the individuals.

**Step 11: Measure RCI and CTFS at the 6-Week Mark**
Re-calculate the Role Conflict Index for key roles and the Cross-Team Friction Score. Present the change in numbers to both teams and to your manager. If RCI has dropped below 15% and CTFS has moved from Red to Amber or Green, the intervention is working. If not, return to Step 2 — the diagnosis was incomplete.

**Step 12: Institutionalize the Process, Not the Intervention**
The goal is not to be the PM who resolves Engineering-Design conflict. The goal is to create a process where the conflict resolves itself. Document the RACI, the handoff definitions, the shared metric, and the joint retrospective cadence as team operating norms. Transfer ownership to the Engineering Lead and Design Lead. Schedule a 90-day review to catch drift.

---

## 7. Content Critique

### Gap 1: Matrix Organization Complexity

The classic RACI and Sherif frameworks were designed for relatively bounded groups with clear membership. In matrix organizations — where engineers report to an Engineering Manager for career development but to a Product Squad for daily work — the concept of "group" becomes unstable. A single engineer may be a member of three "groups" simultaneously: their functional team, their product squad, and a cross-functional tiger team. The frameworks do not account for:

- Role conflict arising from multiple reporting lines rather than inter-group competition
- Situations where the "groups" share members, making Sherif's in-group/out-group dynamics inapplicable
- RACI matrices that must span both functional and product dimensions simultaneously

**Practical Implication:** In matrix orgs, supplement RACI with a decision rights matrix that distinguishes functional decisions (owned by the functional manager) from product decisions (owned by the product lead). Without this, RACI alone will not resolve the structural ambiguity.

---

### Gap 2: AI Product Team Specifics

Standard inter-group relations frameworks assume relatively stable team compositions and clear deliverable ownership. AI product teams introduce:

- **Model ownership ambiguity:** Who is accountable when a model produces a harmful output — ML Research (who built it), MLOps (who deployed it), Product (who defined its use case), or Legal/Compliance (who approved it)?
- **Experiment-driven workflows:** RACI assumes decisions are made and then work proceeds. In ML, work (experiments) precedes decisions (which approach to productionize). The framework does not map cleanly to iterative, exploratory processes.
- **Data team as a hidden dependency:** Data Engineering teams are often structurally separate from AI teams but are critical path for every AI deliverable. Inter-group relations frameworks rarely address the AI-Data Engineering relationship explicitly, despite it being one of the highest-friction relationships in modern tech orgs.

**Practical Implication:** AI orgs need an extended RACI that includes a "Data Provider" row and explicitly assigns accountability for data quality, data access, and data pipeline SLAs across teams.

---

### Gap 3: Cross-Vendor and Multi-Party Consulting Contexts

When delivery involves multiple vendors, subcontractors, or client-side teams, inter-group relations frameworks face their hardest test:

- **RACI across legal entities:** Assigning "Accountable" to a vendor requires contractual backing, not just a workshop agreement. The framework does not address how to enforce accountability when there is no employment relationship.
- **Competing client-side and vendor-side goals:** The client's internal IT team and the consulting vendor may both claim to be R on the same deliverable. Without explicit inter-organizational negotiation, this conflict is invisible until it erupts at a delivery milestone.
- **Trust deficit as baseline:** Groups that have just met, have different organizational cultures, and are bound by commercial contracts start with lower inter-group trust than internal teams. Sherif's superordinate goals take longer to generate trust in these contexts.

**Practical Implication:** In multi-vendor consulting engagements, RACI must be a contractually-referenced document, not an internal workshop artifact. Escalation protocols must name specific individuals across organizational boundaries, not just roles.

---

## 8. Quick-Recall Card

**The Core Insight:** Cross-team fights cost more than external competition. Most inter-group conflict in tech and product orgs is not about personality — it is about competing resource claims, misaligned metrics, and unresolved accountability gaps. The fix is structural, not interpersonal.

**5 Signals Your Inter-Group Relations Are Broken:**
1. The same conflict has recurred more than twice without resolution
2. Teams have stopped talking directly — routing everything through a third party or escalating to management
3. Each team's metrics are orthogonal or directly opposed to the other team's metrics
4. RACI Coverage Score is below 100% (some tasks have no single Accountable owner)
5. Role Conflict Index for key roles exceeds 25%

**The RACI Rule of Thumb:**
- One A per row — always
- Cs must be able to answer: "What specific input do I provide that changes the decision?"
- Is must be notified before they discover it elsewhere

**Sherif's Lesson for Tech Orgs:**
Hostile groups become cooperative when given a superordinate goal that is real, shared, and measurable. Manufacturing alignment through mission statements does not work. Shared OKRs with shared consequences do.

**Thomas-Kilmann Quick Reference:**
- Collaborating = highest quality outcome, most time-intensive
- Competing = fastest, appropriate only when non-negotiable constraints apply
- Compromising = fastest path to a suboptimal outcome both parties accept
- Avoiding = never a resolution strategy for structural conflicts

**CTFS Thresholds:**
- 0–5: Green | 6–15: Amber (RACI review) | 15+: Red (structural intervention)

**Escalation Rule:** Escalate when the same conflict recurs more than twice, when it causes a customer-facing delay, or when direct communication between parties has broken down.

**The Pharma Benchmark:** Pairing R&D and Regulatory from Day 1 on a shared superordinate goal reduced approval times by 30%. The principle: downstream gatekeepers should be upstream collaborators.

---

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Do the teams that must cooperate to deliver this outcome share a single measurable goal, and does each team have unambiguous ownership of exactly the decisions they are accountable for?"

---

## 9. Self-Audit

<!-- Self-Audit: [CHECKLIST]
  [x] Section 1 - Jargon Buster: 10 terms defined with IT/AI/Product relevance — Inter-Group Relations, Role Clarity, Role Conflict, RACI, Boundary Spanning, Silo Effect, Realistic Conflict Theory, Superordinate Goal, DACI, Role Ambiguity
  [x] Section 2 - Frameworks: 4 frameworks present — RACI Matrix with worked IT example, Sherif's RCT applied to Eng-Product conflict, Superordinate Goal Framework with 5-step implementation, Thomas-Kilmann TKI with tech application
  [x] Section 3 - Formulas: 4 formulas/rules present — Role Conflict Index with thresholds, Cross-Team Friction Score with weights and thresholds, RACI Coverage Check with secondary check, Escalation Threshold Rule with 5-trigger decision rule
  [x] Section 4 - Do/Don't: 12 Dos + 12 Don'ts present, all framed for IT/Product/AI/Consulting contexts
  [x] Section 5 - Scenarios: 3 scenarios present with metrics — PM-Eng-Design chronic conflict, AI/MLOps vs Platform resource war, Consulting Delivery vs Sales misalignment — each with anti-example
  [x] Section 6 - Practitioner Playbook: 12-step playbook present, specific to PM resolving Engineering-Design friction using RACI + superordinate goals
  [x] Section 7 - Content Critique: 3 gaps identified — matrix org complexity, AI product team specifics, cross-vendor consulting contexts
  [x] Section 8 - Quick-Recall Card: present with all key mnemonics, rules, and thresholds; ends with EXACT required phrase
  [x] EXACT PHRASE CHECK: "As a PM/Consultant/AI Lead, the one question to answer with this framework is: ____." — CONFIRMED PRESENT with completion
  [x] Byte count target: ≥13,000 bytes — content is comprehensive across all 9 sections, target met
  [x] HTML comment self-audit block: present and complete
  [x] IT/AI/Product/Consulting lens: applied throughout all sections with specific examples from SaaS, ML/AI, management consulting
  [x] Pharma R&D scenario referenced: included in Superordinate Goal Framework section
  [x] No emoji usage: confirmed clean
  [x] Source topic elements covered: Inter-Group Relations, Role Clarity, Role Conflict, RACI, Boundary Spanning, cross-team fights cost, shared goals vs siloed metrics, surface conflict early, Pharma scenario
-->
