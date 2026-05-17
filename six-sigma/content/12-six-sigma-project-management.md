# Six Sigma Project Management and Certification

## Overview
Six Sigma project management covers the skills, roles, and governance structures needed to run improvement projects successfully. It includes selecting the right projects, assembling effective teams, managing stakeholders, and tracking progress through tollgate reviews. The Six Sigma certification system uses a belt hierarchy inspired by martial arts, ranging from White Belt for beginners to Master Black Belt for expert practitioners and mentors.

---

## Why It Matters
Even the best statistical tools will not deliver results without strong project management. Projects need clear scope, engaged sponsors, adequate resources, and disciplined timelines. The belt certification system creates a common skill standard across organizations and industries, ensuring that certified practitioners have demonstrated competence at a defined level. Companies use the belt system to build internal capability and career paths around continuous improvement.

## Key Principles
- Select projects based on strategic alignment, financial impact, and feasibility
- Assign clear roles including sponsor, champion, project lead, and team members
- Conduct tollgate reviews at the end of each DMAIC phase to ensure rigor
- Invest in training and certification to build a sustainable improvement culture

## Key Terms
| Term | Definition |
|------|------------|
| **Green Belt** | A Six Sigma practitioner who leads smaller projects while maintaining other job responsibilities |
| **Black Belt** | A full-time Six Sigma practitioner who leads complex projects and mentors Green Belts |
| **Master Black Belt** | A senior expert who trains and coaches Black Belts, develops methodology, and drives strategy |
| **Tollgate Review** | A formal checkpoint at the end of each DMAIC phase where stakeholders evaluate progress and approve the next phase |

## Use Case
A global manufacturing company creates a project selection committee that evaluates proposed Six Sigma projects against strategic goals, expected savings, and resource requirements before approving them for Green Belt or Black Belt teams.

## Scenario
> A mid-sized insurance company wants to build a continuous improvement culture. It sponsors ten employees for Green Belt certification and two for Black Belt certification. Over the next year, the Green Belts complete projects that save a combined $1.2 million, while the Black Belts tackle two cross-departmental initiatives that reduce claim processing time by 40%. Leadership expands the program based on these results.

## Examples
- A healthcare system requires all department managers to earn Green Belt certification so they can lead improvement projects within their own units
- A technology company uses tollgate reviews to catch a scope creep issue in a Black Belt project early, refocusing the team and keeping the project on schedule

---

## Audited Appendix

# Six Sigma Project Management and Certification
**Course:** Six Sigma
**Module:** Content / Six Sigma Project Management
**Audited on:** 2026-04-18
**Audited by:** A4
**Source files reviewed:** `six-sigma/content/12-six-sigma-project-management.md`

---

## 1. Topic Snapshot
Six Sigma project management is the governance layer that turns statistical tools into delivered, validated financial outcomes: project selection, chartering, role assignment, tollgate reviews, and benefit tracking. The belt system (White -> Yellow -> Green -> Black -> Master Black Belt) standardizes skill depth, project complexity, and mentoring scope across an organization. Without this scaffolding, DMAIC work drifts, scopes creep, and savings never hit the P&L.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| Executive Sponsor | Exec Sponsor | C-suite owner funding and unblocking the project | Air cover + resource authority | Attendance at tollgates; budget approvals | Steering committee |
| Champion | Deployment Champion | Senior leader driving a portfolio of projects in a BU | Translates strategy into project slate | # projects sponsored; $ saved per BU | Deployment reviews |
| Master Black Belt | MBB | Senior expert; trains/coaches Belts; sets methodology | Scaling capability and rigor | Belts certified; portfolio $ impact | Center of Excellence |
| Black Belt | BB | Full-time practitioner leading complex cross-functional projects | Deep DMAIC + stats + change mgmt | 2-4 projects/yr; $250K-$1M savings each | Project review |
| Green Belt | GB | Part-time practitioner leading smaller local projects | Embed improvement in line roles | 1-2 projects/yr; $50-150K savings | Department standup |
| Yellow Belt | YB | Team member with foundational DMAIC knowledge | Enable participation, not lead | Training hours; project contributions | Kaizen event |
| White Belt | WB | Awareness-level intro (1-2 hrs) | Common language across org | Completion % | Onboarding LMS |
| Tollgate Review | Phase Gate | Formal checkpoint at end of each DMAIC phase | Prevent scope/quality drift; go/no-go | Pass / return / kill decision | DMAIC gate meeting |
| Project Charter | Charter | 1-page contract: problem, scope, goal, team, timeline | Align sponsor + team on intent | SMART goal + baseline | Define phase |
| Project Selection Matrix | PSM | Weighted scoring of candidate projects | Avoid pet-project bias | Composite score (0-100) | Portfolio triage |
| RACI | Responsible/Accountable/Consulted/Informed | Role clarity matrix | Reduce hand-off ambiguity | % tasks with single A | Kickoff deck |
| Hard vs Soft Savings | Hard/Soft $ | Cash-out (hard) vs cost-avoidance/productivity (soft) | Credibility with CFO | $ validated by Finance | Benefit tracking |
| Financial Validation | Fin Val | CFO sign-off on savings claim | Prevent double-counting/inflation | Signed validation form | Control phase |
| Benefit Tracking | BT | 12-month post-Control $ monitoring | Ensure gains hold | Run-rate vs forecast | Monthly ops review |
| Project Portfolio | Portfolio | Set of active + pipeline projects | Capacity + strategic balance | WIP; cycle time; hit rate | Portfolio review |
| Change Management | CM (ADKAR/Kotter) | People-side of adoption | Tools alone do not change behavior | Adoption %; sustainment audit | Improve/Control |
| DFSS / DMADV | Design for Six Sigma | New-product/process variant of DMAIC | When redesign > improve | Cpk of new design | R&D |

---

## 3. Frameworks & Matrices

### 3.1 Belt Role Hierarchy (time x complexity x mentoring)
**Purpose:** Right-size skill to project scope and set a clear career ladder.

```
                    /\
                   /MBB\          100% time | strategy + coaching | trains BBs
                  /------\
                 /   BB   \       100% time | complex x-functional | mentors GBs
                /----------\
               /     GB     \      20-30% time | local scope | leads small projects
              /--------------\
             /       YB       \    10% time | team member | supports projects
            /------------------\
           /         WB         \  awareness only | 1-2 hrs training
          /----------------------\
```
**Components:** time commitment, project $ size, span of control, mentoring load.
**Worked example (IT/AI):** AI platform team assigns 1 MBB (governance), 2 BBs (one on model-drift reduction project, one on incident MTTR), 6 GBs (each owning a SRE KPI).
**Trigger:** New deployment or annual capability plan.

### 3.2 Project Selection Matrix (Impact x Strategic Fit x Feasibility)
**Purpose:** Objective triage of candidate projects; kill pet projects early.

```
Project        | Fin Impact | Strategic Fit | Feasibility | Risk | Score
               | (w=0.40)   | (w=0.25)      | (w=0.20)    |(0.15)|
---------------+------------+---------------+-------------+------+------
A: Checkout UX |    9       |      8        |      7      |  8   | 8.15
B: Model drift |    7       |      9        |      6      |  6   | 7.15
C: Vendor cons.|    8       |      5        |      9      |  7   | 7.30
D: L2 support  |    5       |      6        |      8      |  9   | 6.45
E: Data catalog|    4       |      8        |      5      |  7   | 5.65
```
Scale 1-10; weights sum to 1.0. Threshold: fund score >= 7.0.
**Worked example (Product):** Above table picks A and C; B goes to pipeline pending data readiness; D/E deferred.
**Trigger:** Quarterly portfolio review.

### 3.3 RACI / Stakeholder Matrix for a DMAIC Project
**Purpose:** Eliminate "who owns this?" at every phase.

```
Task / Phase          | Sponsor | Champion | MBB | BB/Lead | GB | Finance | IT Ops
----------------------+---------+----------+-----+---------+----+---------+-------
Approve Charter       |   A     |    R     |  C  |    R    | I  |    C    |   I
Define problem        |   I     |    C     |  C  |    A/R  | R  |    I    |   I
Measure baseline      |   I     |    I     |  C  |    A    | R  |    C    |   R
Analyze root cause    |   I     |    I     |  C  |    A/R  | R  |    I    |   C
Improve pilot         |   C     |    A     |  C  |    R    | R  |    I    |   R
Control handoff       |   I     |    A     |  C  |    R    | R  |    R    |   A
Financial validation  |   A     |    C     |  I  |    R    | I  |    A/R  |   I
```
R=Responsible, A=Accountable, C=Consulted, I=Informed. Rule: exactly one A per row.
**Worked example (Consulting):** Partner = Sponsor, Engagement Mgr = Champion, Senior = BB/Lead, Analysts = GB; Client CFO provides Financial Validation.
**Trigger:** Kickoff day 1.

### 3.4 Tollgate Gating Decision Tree
**Purpose:** Hard stop at each phase; prevents "ready-fire-aim."

```
[Define Gate]
  ├─ Charter signed? Problem SMART? Baseline sized?
  │     ├─ YES ──► [Measure Gate]
  │     └─ NO  ──► return to Define (max 2 iterations → kill)
[Measure Gate]
  ├─ MSA passed? Cpk baseline? Data locked?
  │     ├─ YES ──► [Analyze Gate]
  │     └─ NO  ──► return to Measure
[Analyze Gate]
  ├─ Validated root causes? Hypothesis tests p<0.05?
  │     ├─ YES ──► [Improve Gate]
  │     └─ NO  ──► return to Analyze
[Improve Gate]
  ├─ Pilot shows >= target delta? Risk assessed (FMEA)?
  │     ├─ YES ──► [Control Gate]
  │     └─ NO  ──► return to Improve or re-scope
[Control Gate]
  ├─ SPC in place? SOP signed? Finance validated?
  │     ├─ YES ──► CLOSE + 12-mo benefit tracking
  │     └─ NO  ──► hold; no closure bonus
```
**Worked example (AI):** Model-drift project fails Measure gate because MSA shows label noise >10%; team loops back before analyzing.
**Trigger:** End of each phase; no gate skipped.

---

## 4. Formulas

### 4.1 Project Selection Score
```
Score = w1*FinImpact + w2*StratFit + w3*Feasibility + w4*Risk
(weights sum to 1.0; scale 1-10)
```
**Thresholds:** >= 7.5 fund now; 6.0-7.4 pipeline; < 6.0 reject.
**IT example:** Observability rollout: 0.40*9 + 0.25*8 + 0.20*7 + 0.15*8 = 3.6 + 2.0 + 1.4 + 1.2 = **8.2 → fund**.

### 4.2 Expected Annual Savings
```
Savings = (Δmetric) × (population) × (unit_value) − implementation_cost
```
**Thresholds:** BB project target >= $250K/yr; GB >= $50K/yr.
**Consulting example:** Claims cycle time drop 4 days on 50,000 claims/yr at $3/day carrying cost = 4 × 50,000 × 3 = $600,000 − $120,000 build = **$480K hard savings**.

### 4.3 Project ROI and Payback Period
```
ROI (%) = (Annual Savings − Annual Cost) / Total Investment × 100
Payback (months) = Total Investment / (Monthly Savings)
```
**Thresholds:** ROI >= 300% first year; payback <= 6 months for Green Belt, <= 12 for Black Belt.
**Product example:** Checkout UX fix costs $150K; saves $50K/month. ROI = (600-0)/150 = **400%**; payback = 150/50 = **3 months**.

### 4.4 Project Pipeline Throughput (Little's Law)
```
Throughput = WIP / Cycle Time
```
**Thresholds:** BB cycle time 4-6 months; WIP per BB <= 2.
**AI example:** 12 BBs, average 5 mo cycle, WIP=2 each → throughput = 24/5 = **4.8 projects/month** = ~58/yr.

---

## 5. Do vs Don't

| Do | Don't |
|---|---|
| Select projects via weighted matrix with Finance in the room | Don't pick projects by loudest VP or pet idea |
| Require Finance sign-off on baseline AND savings | Don't accept self-reported savings without validation |
| Promote Belts only after delivering certified projects | Don't promote Green Belts on coursework alone |
| Assign a named Champion and Sponsor before kickoff | Don't launch a project without air cover — it will stall |
| Hold tollgates with go/no-go authority | Don't turn tollgates into status updates |
| Track hard vs soft savings separately | Don't mix productivity hours with cash P&L impact |
| Cap WIP per Belt (BB<=2, GB<=1) | Don't overload Belts — cycle time balloons, quality drops |
| Run 12-month post-Control benefit tracking | Don't declare victory at Control handoff |
| Link charters to strategic OKRs | Don't run projects disconnected from top-level goals |

---

## 6. Real-Life Scenarios

### 6.1 IT Ops — Project Selection (Tools: Jira, Confluence, Power BI)
IT ops has 5 candidates: incident MTTR, patch compliance, on-call burnout, cloud spend, ticket deflection. Using the Project Selection Matrix with Finance and CIO, scores land: cloud spend 8.4, MTTR 7.9, ticket deflection 7.2, patch 6.1, on-call 5.8. Top 3 funded as BB/GB projects; remainder parked with measurable "activation triggers." Charters stored in Confluence, tracked in Jira, savings dashboards in Power BI.

### 6.2 Consulting — Black Belt Engagement (Tools: Smartsheet, Confluence)
A consulting firm staffs a 16-week claims-ops engagement: Partner=Sponsor, EM=Champion, Senior Consultant=BB lead, 2 Analysts=GBs, Client CFO=Financial Validator. RACI locked day 1. Tollgates at week 3 (Define), 6 (Measure), 9 (Analyze), 12 (Improve), 16 (Control). Smartsheet tracks milestones; Confluence holds charter and tollgate decks. Savings: $1.8M validated hard + $400K soft; client retains BB-trained internal lead for sustainment.

### 6.3 ANTI-EXAMPLE — 40 Simultaneous Projects, No Triage
A mid-cap manufacturer launches 40 Six Sigma projects across 6 BUs with no portfolio committee and 4 BBs total (WIP=10 each — 5x the healthy cap). Result: average cycle time stretches from 5 to 14 months; 60% of projects die before Control; finance validates only $900K of a claimed $9M. Quantified cost: ~$2.1M in training + Belt time with only $900K return = **net −$1.2M** plus 18 months of organizational fatigue and credibility loss for the program. Fix: portfolio triage, WIP cap=2/BB, kill-list of 25 projects.

---

## 7. Implementation Playbook
1. **Charter** a Deployment Steering Committee (Sponsor + Champions + Finance + MBB) with monthly cadence.
2. **Build** a weighted Project Selection Matrix and score all candidates; publish the kill list.
3. **Assign** RACI and named Belt roles per project; cap WIP (BB<=2, GB<=1).
4. **Issue** Project Charters with SMART goals, baseline, and Finance-validated savings target.
5. **Run** tollgate reviews with go/no-go authority at every DMAIC phase end.
6. **Validate** savings with CFO sign-off at Control; split hard vs soft.
7. **Track** post-Control benefits for 12 months via Power BI dashboard; tie to exec scorecard.
8. **Certify** Belts only after delivered, validated projects; publish annual capability report.

---

## 8. Content Quality Audit

**Covered well:** Belt hierarchy basics, tollgate concept, project selection intent, role definitions, scenario of scaling program.

**Underplayed / missing:**
- Financial validation rigor (CFO sign-off, hard vs soft savings rules)
- Portfolio management (WIP caps, kill discipline, capacity planning)
- Change management integration (ADKAR/Kotter) inside Improve/Control
- Agile/DMAIC hybrid for software and AI projects (sprints within phases)
- DFSS / DMADV distinction for new-product vs existing-process work
- Digital tooling (Jira, Smartsheet, Power BI, Minitab, JMP)
- Benefit tracking post-Control (12-month sustainment audits)
- Role-specific KPIs for Belts and Champions

**Supplements (>=5):**
1. George, Rowlands, Price, Maxey — *Lean Six Sigma Pocket Toolbook* / *Lean Six Sigma* (McGraw-Hill, 2005).
2. Pyzdek & Keller — *The Six Sigma Handbook*, 5th ed. (McGraw-Hill, 2018).
3. Snee & Hoerl — *Leading Six Sigma* (FT Prentice Hall, 2003).
4. Kotter — "Leading Change: Why Transformation Efforts Fail," *HBR* (1995).
5. ASQ — *Certified Six Sigma Black Belt Body of Knowledge* (latest ASQ edition).
6. Hiatt — *ADKAR: A Model for Change in Business, Government and our Community* (Prosci, 2006).

**Red flags in source:** No mention of Finance validation, no WIP/portfolio discipline, no post-Control tracking, no tooling, no change-management layer, and belt definitions are one-liners without KPIs.

---

## 9. Quick-Recall Card
- Belts without projects = training theater; projects without Belts = chaos.
- Select with a weighted matrix; fund only score >= 7.5.
- Named Sponsor + Champion + RACI before kickoff — no exceptions.
- Tollgates are go/no-go, not status updates; Finance signs off at Control.
- Cap WIP: BB <= 2, GB <= 1; track benefits 12 months post-close.
- **Role-lens question:** *If you are a Product/IT/AI/Consulting leader, which 3 candidate projects on your desk today would survive a weighted Selection Matrix with your CFO in the room — and who are the named Sponsor, Champion, and Belt for each?*

---

**Connects to:** [01-introduction.md](01-introduction.md), [../project-management/](../project-management/), [../strategic-management/](../strategic-management/).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:5, 6:4, 7:5, 8:4, 9:4, 10:4]
Sections rewritten: [3.2 matrix numeric weights, 4.2 savings numeric example, 6.3 anti-example cost math, 8 supplements expanded]
Enrichments applied: [cross-course links; 6 supplements; anti-example w/ quantified −$1.2M cost; IT/AI/Product/Consulting tooling — Jira, Confluence, Smartsheet, Power BI; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A4
-->
