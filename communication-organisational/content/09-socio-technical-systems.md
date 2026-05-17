# Socio-Technical Systems

## Overview

A socio-technical system is the combination of people and technology that together get work done. The idea is simple: you cannot redesign one without thinking about the other. A great tool with no buy-in fails, and great people with a broken tool burn out.

---

## Why It Matters

Most failed technology projects are not technical failures. They fail because nobody thought about how work habits, skills, and team structure would change. Thinking socio-technically from day one saves rework and rescues adoption rates.

## Key Principles

- Treat people and technology as two halves of one system.
- Design work in small, self-contained units that a team can fully own.
- Give workers control over the pace and method whenever possible.
- Match the skill level of the team to the demands of the tool, or train to close the gap.
- Measure the joint output, not just machine uptime or headcount.

## Key Terms

| Term | Definition |
|------|------------|
| **Socio-Technical System** | The joint arrangement of people, tasks, and technology that produces work. |
| **Joint Optimization** | Designing both the human and technical sides together for best overall result. |
| **Self-Managed Team** | A group that controls its own work methods, scheduling, and improvements. |
| **Work Design** | The structured choice of tasks, tools, and interactions that make up a job. |
| **Autonomy** | The degree of freedom a worker has to choose how to do the job. |

## Use Case

A car plant replaces a long assembly line with small cell-based teams. Each team builds a full module, maintains its own machines, and signs off on quality. Output rises and defects fall because workers see the whole picture.

## Scenario

> A hospital bought a new electronic records system but doctors pushed back hard. The vendor blamed users. A deeper look showed the system ignored how nurses actually handed over patients. The hospital redesigned the handover step with nursing input, and adoption rose from forty to ninety percent.

## Examples

- A bakery chain gives each shop team the freedom to adjust its own bake schedule around the weather and raises sell-through rates.
- A software team rotates the on-call role and pairs it with authority to fix root causes, reducing incidents steadily over six months.

---

## Audited Appendix

# Socio-Technical Systems — Audit File

---

## 1. Jargon Buster

| # | Term | Plain-English Definition | Why It Matters in IT/AI/Product Work |
|---|------|--------------------------|---------------------------------------|
| 1 | **Socio-Technical System (STS)** | A joint arrangement of people, tasks, and technology that together produce work outcomes. Neither the human side nor the technical side can be understood or redesigned in isolation. | Every software product, AI deployment, or platform rollout is an STS. Ignoring the social half causes failed adoptions and wasted engineering effort. |
| 2 | **Joint Optimization** | The design principle that the human subsystem and the technical subsystem must be designed together, simultaneously, to achieve the best overall result rather than optimising each separately. | A perfectly engineered AI model can destroy team performance if it overrides human judgment or removes meaningful work. Joint optimization prevents one-sided wins that produce system-level losses. |
| 3 | **Self-Managed Team** | A group that controls its own work methods, scheduling, quality checks, and continuous improvements without needing constant supervisory instruction. | Agile squads, DevOps teams, and platform engineering pods are self-managed teams. STS theory explains why giving them autonomy over tool choices accelerates adoption and quality. |
| 4 | **Work Design** | The structured choice of tasks, tools, roles, and interactions that define what a job is and how it feels to perform it. | Introducing an AI copilot without redesigning surrounding tasks leaves workers doing meaningless residual work — the cognitive scraps the machine left behind. |
| 5 | **Autonomy** | The degree of freedom a worker has to choose how, when, and in what sequence to perform the job. One of the five core job characteristics in the Hackman-Oldham model. | Low autonomy causes learned helplessness in AI-assisted roles. High autonomy enables workers to adapt tools to context, increasing both performance and satisfaction. |
| 6 | **Tavistock School** | The research tradition originating at the Tavistock Institute (London, 1940s-50s) that produced STS theory through studies of coal miners and textile workers. Founders: Eric Trist, Ken Bamforth, Fred Emery. | Foundational lineage for understanding why technology implementation is always a social intervention, not merely a technical one. |
| 7 | **Job Characteristics Model (Hackman-Oldham)** | A framework identifying five core job dimensions — Skill Variety, Task Identity, Task Significance, Autonomy, and Feedback — that predict motivation, performance, and satisfaction via three psychological states. Expressed as the MPS formula. | Directly applicable to AI role redesign: use MPS to diagnose which dimensions an AI tool destroys or enhances before launch. |
| 8 | **Adoption Friction** | The cumulative resistance force that slows or prevents workers from integrating a new technology into their actual workflow. Sources include skill gaps, fear of deskilling, distrust of outputs, poor UX, and loss of meaningful work. | Adoption friction explains why 70%+ of enterprise software rollouts underperform. Mapping friction points before launch is a core PM responsibility. |
| 9 | **Conway's Law** | "Organizations which design systems are constrained to produce designs which are copies of the communication structures of those organizations." (Melvin Conway, 1968) | An AI team's internal boundaries will be reflected in its model architecture, API surface, and data pipelines. Reorganize the team to change the system structure — not the other way around. |
| 10 | **Sociotechnical Debt** | Accumulated misalignments between the social system (roles, skills, norms, trust) and the technical system (tools, models, platforms, automations) that make future change increasingly costly. | Unlike code debt, sociotechnical debt is invisible until a rollout fails catastrophically. Auditing it requires interviewing workers, not reading repos. |

---

## 2. Frameworks & Mental Models

### 2.1 Tavistock STS Design Principles

Developed through Eric Trist and Ken Bamforth's coal mine studies, these principles guide how to design a socio-technical system rather than bolt technology onto an existing social structure.

| Principle | Description | IT/AI Application |
|-----------|-------------|-------------------|
| 1. Compatibility | The process of design must be compatible with its objectives — participative design produces participative outcomes. | Include engineers, analysts, and frontline users in AI tool selection, not just leadership. |
| 2. Minimal Critical Specification | Specify only what is absolutely necessary. Leave workers maximum discretion on how to achieve outcomes. | Define AI output requirements (accuracy, latency) but do not over-specify how workers must interact with model outputs. |
| 3. Variance Control at Source | Errors and deviations should be corrected as close to where they originate as possible. | AI anomaly detection should surface issues to the team that generated the data, not escalate to a central ops team by default. |
| 4. Boundary Location | Boundaries between teams should be drawn to support whole-task completion, not functional siloes. | Platform teams should own the full delivery cycle for a capability, not hand off between infra, security, and app dev at every step. |
| 5. Information Flow | Information should flow first to those who need it to act. | AI dashboards should deliver decision-relevant signals to the person taking action, before aggregating to management reports. |
| 6. Power and Authority | Authority should be located where decisions must be made, with the people who have the knowledge. | Frontline workers using AI models should have override authority; central AI governance should handle policy, not operational calls. |
| 7. Support Congruence | Support systems (HR, IT helpdesk, training) should reinforce the values embedded in the work design. | If work is designed for autonomy but the support system requires 48-hour ticket resolution for tool changes, the design fails. |
| 8. Design and Human Values | The design must produce a quality of working life that is satisfying and meaningful. | AI tools that reduce all cognitive work to button-clicking violate this principle and produce burnout, attrition, and covert workarounds. |

---

### 2.2 Hackman-Oldham Job Characteristics Model (5 Core Dimensions + MPS Formula)

**Five Core Job Dimensions:**

1. **Skill Variety** — The range of different skills and talents the job requires. High variety = worker experiences work as meaningful.
2. **Task Identity** — The degree to which the job involves completing a whole and identifiable piece of work. High identity = sense of completion and ownership.
3. **Task Significance** — The degree to which the job has a substantial impact on others inside or outside the organisation. High significance = work feels important.
4. **Autonomy** — The degree of freedom and independence in scheduling work and determining procedures. High autonomy = worker feels personal responsibility for outcomes.
5. **Feedback** — The degree to which carrying out work activities provides direct, clear information about performance. High feedback = worker knows results of efforts.

**Three Critical Psychological States (mediators):**
- Skill Variety + Task Identity + Task Significance → **Experienced Meaningfulness of Work**
- Autonomy → **Experienced Responsibility for Outcomes**
- Feedback → **Knowledge of Results**

**MPS Formula (see Section 3 for full detail)**

**Application to AI Role Design:** An AI copilot that handles all skill variety (writes the code), destroys task identity (delivers complete outputs requiring no worker completion), and removes feedback (worker never sees if the AI output succeeded) will score near zero on MPS. The worker is left holding a clipboard next to a machine. This predicts attrition and covert non-use.

---

### 2.3 Conway's Law and Its Implications for AI Teams

**Original Statement:** "Any organisation that designs a system (defined broadly) will produce a design whose structure is a copy of the organisation's communication structure."

**Inverse Conway Maneuver:** Intentionally restructure the team to produce the desired system architecture. If you want loosely coupled microservices, build loosely coupled teams. If you want an integrated AI platform, build a cross-functional AI platform team with unified communication.

**Implications for AI Teams:**

| Org Structure | System It Produces | Problem |
|--------------|-------------------|---------|
| Separate Data Science, ML Engineering, and MLOps teams | Models that can't deploy; pipelines that can't be retrained | Three-team handoff introduces coordination debt and version mismatches |
| Centralised AI CoE with no embedded product team | AI features misaligned with user needs | CoE solves for model quality, not workflow integration |
| Cross-functional AI squad (DS + Eng + PM + Domain Expert) | Deployable, adopted, improving AI features | Requires deliberate boundary design and governance |

**Sociotechnical implication:** Conway's Law is a special case of STS theory applied to system architecture. The communication structure is the social system; the system architecture is the technical system. They mirror each other whether you plan it or not.

---

### 2.4 Joint Optimization Model

**Core Premise:** Neither maximising the technical subsystem independently nor maximising the social subsystem independently produces the best overall result. The optimum is achieved by designing both together.

```
                    JOINT OPTIMIZATION TARGET
                           /\
                          /  \
          Technical      /    \    Social
          Optimum       /  ★   \   Optimum
         (efficiency,  /        \  (satisfaction,
          speed,      /          \ meaning, autonomy)
          accuracy)  /____________\
                    
         ★ = Joint Optimum (lower on both axes but
             higher on overall system performance)
```

**Four Quadrants of Deployment Decisions:**

| | High Social Fit | Low Social Fit |
|--|----------------|----------------|
| **High Technical Fit** | Deploy and scale | Redesign work before scaling |
| **Low Technical Fit** | Pilot with heavy human oversight | Do not deploy |

---

## 3. Formulas / Thresholds / Decision Rules

### 3.1 Motivating Potential Score (MPS)

```
MPS = [(Skill Variety + Task Identity + Task Significance) / 3] × Autonomy × Feedback
```

**Scoring:** Each dimension rated 1–7 by job incumbents.

**Interpretation:**

| MPS Score | Interpretation | Action |
|-----------|---------------|--------|
| < 50 | Critically low motivation potential | Redesign the role before adding more automation |
| 50–100 | Moderate — acceptable but improvable | Identify which of the 5 dimensions is lowest; target interventions |
| 100–150 | High motivation potential | Maintain; watch for automation eroding specific dimensions |
| > 150 | Exceptional | Benchmark this role design; document what's working |

**AI Deployment Diagnostic — MPS Delta Analysis:**
Calculate MPS for the role before and after AI tool introduction. A negative delta on Skill Variety, Task Identity, or Autonomy signals sociotechnical debt accumulation.

```
MPS_delta = MPS_post_AI - MPS_pre_AI

If MPS_delta < -20: Halt rollout; redesign human-AI task allocation
If MPS_delta -20 to 0: Proceed with mitigation plan
If MPS_delta > 0: Proceed; document design for replication
```

---

### 3.2 Adoption Rate Threshold

**Definition:** Percentage of target users who have integrated the tool into their standard workflow within 90 days of deployment.

**Threshold Decision Rules:**

| Adoption Rate | Classification | Action |
|--------------|---------------|--------|
| > 70% | Success | Proceed to full rollout; document success factors |
| 50–70% | At Risk | Identify blocking friction points; targeted enablement |
| 30–50% | Failure in Progress | Pause rollout; conduct sociotechnical audit; redesign onboarding |
| < 30% | Deployment Failure | Halt; root-cause analysis mandatory before resumption |

**Hospital EHR Benchmark:** Pre-intervention adoption = 40% (At Risk/Failure). Post nursing-input handover redesign = 90% (exceeds Success threshold). Delta = +50pp. Driver: joint optimization of workflow step + technology interface.

---

### 3.3 Skill-Tool Fit Assessment

**Formula:**
```
Skill-Tool Fit Score = (Σ Worker Competency Ratings × Tool Demand Ratings) / n

Where:
- Worker Competency Rating: self-assessed 1–5 on each skill the tool requires
- Tool Demand Rating: PM-assessed 1–5 weight of each skill in tool use
- n = number of assessed skill dimensions
```

**Decision Rule:**
- Score > 3.5: Deploy with standard onboarding
- Score 2.5–3.5: Deploy with enhanced training program
- Score < 2.5: Delay deployment; structured upskilling program required first

---

### 3.4 STS Health Index

**Composite metric for ongoing monitoring:**

```
STS Health Index = 0.25(Adoption Rate) + 0.25(MPS Score/7) + 
                   0.25(Variance-at-Source %) + 0.25(Team Autonomy Score)

Normalised to 0–100.
```

**Variance-at-Source %:** Percentage of system errors/exceptions resolved by the team that generated them (vs. escalated to central support).

**Team Autonomy Score:** Average worker rating (1–7) of freedom to adjust tools and processes.

**Threshold:** STS Health Index < 60 = system under structural stress; intervention required.

---

## 4. Do / Don't

### For IT System Rollout, AI Deployment, and Platform Engineering

#### DO

1. **Do conduct a pre-deployment sociotechnical audit** — map existing workflows, skill levels, informal workarounds, and trust structures before writing a single line of integration code.

2. **Do calculate MPS delta** — measure the Motivating Potential Score of affected roles before and after the proposed AI/tool change to quantify impact on meaningful work.

3. **Do apply minimum critical specification** — define what the system must achieve (outcomes), not how workers must interact with it (process). Leave discretion at the worker level.

4. **Do include frontline workers in design sessions** — not as feedback recipients but as co-designers with decision-making power over workflow steps that affect them.

5. **Do co-locate variance control** — configure systems so that errors, exceptions, and edge cases surface to the team closest to the work, not to a central ops function.

6. **Do run pilot groups using the Inverse Conway Maneuver** — restructure the pilot team's communication boundaries to match the desired system architecture before scaling.

7. **Do set an explicit 90-day adoption rate target (>70%)** — and build a structured off-ramp plan for what happens if adoption falls below 50%.

8. **Do redesign surrounding tasks when automating** — if an AI model takes over task A, explicitly redesign the human's role to preserve skill variety, task identity, and feedback loops.

9. **Do measure sociotechnical debt quarterly** — survey workers on the gap between their current tools and their work practices; track trend lines.

10. **Do build override authority into AI systems** — frontline workers must have a documented, low-friction path to override or escalate AI outputs without managerial approval.

11. **Do train on why, not just how** — workers who understand the model's logic, limitations, and failure modes adopt it more fully and use it more safely than those who receive only button-click training.

12. **Do treat adoption failure as a design signal, not a people problem** — when adoption is low, audit the system design before initiating performance management.

---

#### DON'T

1. **Don't design the technical system first and inform the social system afterward** — retrofitting human workflows to a finished technical system is the leading cause of enterprise software failure.

2. **Don't optimise the AI model in isolation** — a model with 94% accuracy deployed into a workflow that requires 99% human trust to function is not a 94%-accurate deployment; it is a failed deployment.

3. **Don't remove feedback from the worker** — if the AI consumes the feedback signal that told workers how they were performing, you have destroyed one of the five MPS dimensions and created a monitoring void.

4. **Don't equate training completion with adoption** — a worker who has completed the LMS modules and still uses their old spreadsheet is not adopted. Measure actual tool use, not training certificates.

5. **Don't draw team boundaries that cut across whole tasks** — a platform team that owns infra but not deployment, or a data team that owns pipelines but not model quality, is structurally guaranteed to produce handoff friction.

6. **Don't launch without a Skills-Tool Fit assessment** — deploying a tool that requires skills workers don't have and providing no structured path to acquire them produces learned helplessness, not productivity.

7. **Don't ignore Conway's Law** — if the AI architecture needs to be integrated but the teams building it are siloed, no amount of API documentation will produce integration. Reorganise first.

8. **Don't let support systems contradict work design values** — if you design for autonomy but IT change management requires three approvals to adjust a tool setting, the support system will silently undo the work design.

9. **Don't use adoption rate as the only metric** — a tool can be adopted and still destroy MPS, increase cognitive load, and erode skill. Measure quality of use, not just frequency of use.

10. **Don't skip the informal system audit** — most organisations have informal workarounds that actually make the formal system function. Automating the formal system without mapping the informal one breaks the actual system.

11. **Don't make AI override a stigmatised action** — if workers feel professionally penalised for flagging AI errors or choosing not to use AI outputs, you will get silent non-use and undetected errors, not adoption.

12. **Don't declare rollout complete at go-live** — STS alignment degrades over time as the social system evolves. Schedule sociotechnical health checks at 30, 90, and 180 days post-launch.

---

## 5. Metric-Driven Scenarios with Anti-Examples

### Scenario 1: AI Copilot Rollout in an Engineering Team

**Context:** A 60-person software engineering organisation deploys an AI code generation copilot. PM sets a 90-day adoption target of >70%.

**Metrics Tracked:**
- MPS pre-deployment: 138 (high — developers have strong skill variety, task identity, autonomy)
- MPS post-deployment (month 1): 89 (significant drop — skill variety crushed; copilot generates full functions)
- Adoption rate at 90 days: 61% (at risk)
- Variance-at-Source %: 44% (bugs flagged to central AI ops team, not dev squads)

**Correct STS Intervention:**
1. PM runs joint optimization workshop with dev leads: redefine copilot as a "first draft" tool, not a completion tool. Developers own review, refactoring, and integration decisions — preserving skill variety and task identity.
2. Error/suggestion feedback loop routed back to the squad's own copilot fine-tuning queue — restoring variance-at-source and feedback dimension.
3. MPS post-redesign: 121. Adoption rate at day 120: 78%. STS Health Index: 74.

**Anti-Example:**
PM treats 61% adoption as a training problem. Mandates a second round of LMS completion. Developers who completed training continue using the copilot minimally ("comply and coast"). At day 180, active use is 58%. PM attributes failure to "developer resistance to change" and escalates to HR. Root cause — MPS destruction by poor work design — is never diagnosed.

---

### Scenario 2: DevOps Platform Adoption Failure

**Context:** A platform engineering team at a 200-person consultancy builds an internal developer platform (IDP) intended to standardise CI/CD, secrets management, and environment provisioning. After 6-month build, they launch to 8 product squads.

**Metrics Tracked:**
- Adoption rate at 90 days: 28% (deployment failure classification)
- Skill-Tool Fit Score: 2.1 (below deployment threshold — platform required Kubernetes, Terraform, and Vault expertise that squads lacked)
- Team Autonomy Score: 2.4/7 (platform enforced fixed pipeline templates; squads could not customise)
- Variance-at-Source %: 19% (all platform issues required platform team tickets)

**Correct STS Intervention:**
1. Skill-Tool Fit gap identified through structured squad audits — platform team embeds engineers into squads for 6-week capability transfer.
2. Minimum critical specification applied — platform defines security and compliance guardrails; squads choose implementation approach within those guardrails.
3. Variance control redesigned — squads given self-service runbooks and autonomy to resolve tier-1 platform issues without tickets.
4. Adoption rate at day 180 post-redesign: 74%. Team Autonomy Score: 4.8.

**Anti-Example:**
Platform team presents adoption failure data to leadership as evidence that "squads are too immature for modern DevOps." Leadership mandates all squads adopt by quarter-end or face architectural review board scrutiny. Squads comply by running dual workflows — official platform for visibility, old shell scripts for actual delivery. Platform adoption metrics show 90%. Actual platform-driven delivery: 31%. Sociotechnical debt reaches critical level when a compliance audit discovers the divergence.

---

### Scenario 3: ERP Migration in a Consulting Firm

**Context:** A 500-person management consulting firm migrates from a legacy time-tracking and project management system to a new integrated ERP. Rollout managed by central IT; consultants informed via email announcement.

**Metrics Tracked:**
- Adoption rate at 90 days: 35% (failure in progress)
- MPS pre-migration: 104 (consultants had high autonomy in how they logged and managed project data)
- MPS post-migration: 61 (ERP enforces rigid entry workflows; autonomy dimension collapsed from 6.1 to 2.8)
- Workaround detection rate: 67% of consultants maintaining parallel spreadsheets

**Correct STS Intervention:**
1. PM conducts variance analysis — identifies 4 workflow steps where ERP enforcement eliminated consultant discretion without improving data quality.
2. ERP vendor configures optional fields as optional (not mandatory); consultant-preferred reporting views built into dashboard.
3. Frontline consultants co-design onboarding materials, identifying which legacy workflows the ERP genuinely improves vs. which it merely replaces.
4. Adoption rate at day 180: 81%. Parallel spreadsheet use: 12%. MPS: 88.

**Anti-Example:**
IT team responds to 35% adoption by removing access to the legacy system 30 days early. Consultants forced into ERP without workarounds. Data quality collapses — mandatory fields filled with placeholder values ("TBD," "000," "N/A"). Project financials become unreliable. Finance team manually corrects 200+ timesheets per week. ERP adoption rate: 100%. ERP data quality: unusable. A system with perfect adoption and zero value produced by ignoring the social system entirely.

---

## 6. Practitioner Playbook

### 12-Step Playbook for PM Rolling Out a New AI/Internal Tool with Socio-Technical Fit

**Phase 1: Diagnosis (Before Any Build Decisions)**

**Step 1 — Map the Existing Socio-Technical System**
Document the current workflow: who does what, with which tools, in what sequence, and what informal adaptations make it actually work. Include shadow IT, workarounds, and undocumented expert knowledge. Deliverable: STS current-state map.

**Step 2 — Conduct a Skill-Tool Fit Assessment**
Survey target users on current competency across skills the proposed tool requires. Calculate Skill-Tool Fit Score. If score < 2.5, halt technical development and initiate upskilling design first.

**Step 3 — Calculate MPS for Affected Roles (Baseline)**
Administer a 15-item job characteristics survey to all roles that will be affected by the tool. Record MPS baseline. Identify which of the 5 dimensions are strongest — these are the dimensions most at risk of being eroded by automation.

**Step 4 — Run a Joint Optimization Workshop**
Bring together: technical leads (what the tool can do), frontline workers (what the work actually requires), and domain experts (what quality looks like). Do not separate these groups. Output: agreed human-AI task allocation that preserves MPS score.

---

**Phase 2: Design (Co-Design, Not Consultation)**

**Step 5 — Apply Minimum Critical Specification**
Define non-negotiable requirements (security, compliance, data quality thresholds). Leave all other design decisions to the team. Document explicitly: what is fixed vs. what is discretionary.

**Step 6 — Apply Conway's Law Check**
Draw the communication map of the team that will build and maintain this tool. Does it match the architecture you need? If not, restructure the team before freezing the architecture. Deliverable: aligned team-architecture map.

**Step 7 — Design Variance Control at Source**
For every category of error, exception, or edge case the tool will surface — explicitly decide who handles it and where. Default rule: the team closest to the work handles tier-1 issues without escalation.

**Step 8 — Build Override Authority into the System**
Specify the exact mechanism by which a frontline worker can override, flag, or bypass AI outputs. This must be low-friction and destigmatised. Document override events as learning data, not compliance violations.

---

**Phase 3: Pilot (Measure Before Scaling)**

**Step 9 — Run Controlled Pilot with STS Metrics**
Deploy to one team for 30 days. Measure: adoption rate, MPS post-deployment, Skill-Tool Fit Score actualised, Variance-at-Source %. Compare to baselines. Calculate MPS delta.

**Step 10 — Set Go/No-Go Thresholds Before Pilot Begins**
Define explicit decision rules before pilot data arrives:
- Adoption rate > 50% at day 30: proceed to phase rollout
- MPS delta > -20: proceed with monitoring
- Adoption rate < 30% OR MPS delta < -30: halt and redesign

---

**Phase 4: Scale and Sustain**

**Step 11 — Redesign Support Systems for Congruence**
Audit every support system that touches the new tool: IT helpdesk SLA, training paths, change request process, manager incentives. Identify and eliminate any support structure that contradicts the autonomy or feedback dimensions built into the work design.

**Step 12 — Schedule Sociotechnical Health Checks**
At 30, 90, and 180 days post-full-launch, re-administer the MPS survey, measure adoption rate, and calculate the STS Health Index. Treat any STS Health Index drop of > 10 points between checkpoints as an early warning signal requiring investigation before it becomes a deployment failure.

---

## 7. Content Critique

### Gaps in Standard STS Theory for AI/Automation, Platform Engineering, and Remote-First Work Design

**Gap 1: STS Theory Was Designed for Co-Located, Stable Teams**
The Tavistock studies involved coal miners and textile workers in fixed physical locations. The self-managed team concept assumes physical proximity enables informal coordination. In remote-first organisations, the informal social system that STS theory relies on — hallway conversations, visual cues, spontaneous knowledge transfer — is absent or severely degraded. Standard STS frameworks provide no guidance on designing sociotechnical systems for asynchronous, geographically distributed teams. *Practitioners need: async-first STS design principles, digital social infrastructure requirements, and norms-as-code approaches.*

**Gap 2: AI Systems Are Not Passive Tools — They Are Active Agents**
STS theory models technology as a passive instrument that workers use. AI systems are different: they generate outputs, make recommendations, take actions, and adapt over time. This introduces a third actor — the model — into the human-technology dyad. The sociotechnical implications of AI agency (model drift, hallucination, emergent behaviour) are not addressed by any classical STS framework. *Practitioners need: human-AI-organisation triadic models that account for model behaviour as a sociotechnical variable.*

**Gap 3: No Framework for Continuous Change in the Technical Subsystem**
Tavistock STS design principles assume a relatively stable technical system that is designed once and then lived with. Modern platform engineering and AI deployment involve continuous updates — model retraining, dependency upgrades, API changes, feature flags. Each update can shift the sociotechnical balance without triggering a formal redesign process. *Practitioners need: rolling sociotechnical impact assessment integrated into CI/CD pipelines and sprint planning.*

**Gap 4: Conway's Law Is Not Part of STS Curriculum**
Conway's Law is one of the most practically powerful sociotechnical principles in software engineering, but it is not derived from the STS tradition and is not typically taught alongside it. The result is that STS practitioners design good work systems but do not consider how team communication structures determine system architecture — and vice versa. *Practitioners need: unified curriculum combining STS principles with Conway's Law and team topology frameworks.*

**Gap 5: MPS Formula Does Not Account for Human-AI Collaboration Modes**
The Hackman-Oldham model scores dimensions based on the human's experience of their job. When an AI model is doing 60% of a task, it is unclear whether Skill Variety should be scored for the 40% residual human work or for the original job. There is no validated adaptation of the MPS formula for hybrid human-AI roles. *Practitioners need: an updated HJC-AI model that scores the human component of hybrid work independently and compares it to a meaningful-work floor.*

**Gap 6: No Sociotechnical Framework for Platform-as-Product**
Platform engineering has introduced a model where the "product" is an internal capability (a CI/CD platform, an MLOps platform, an internal API gateway) and the "customers" are internal developer teams. Classical STS theory addresses production work systems, not platform product relationships. The social dynamics of internal platform adoption — power asymmetries between platform teams and product squads, internal market failures, invisible platform costs — have no standard STS treatment. *Practitioners need: an STS extension specifically addressing internal platform economics and adoption dynamics.*

---

## 8. Quick-Recall Card

**The Core Idea in One Sentence:**
People and technology form a single system — redesign one without the other and you will optimise a part while degrading the whole.

**The 5-Dimension MPS Skeleton:**
Skill Variety | Task Identity | Task Significance | Autonomy | Feedback

**The Formula:**
MPS = [(SV + TI + TS) / 3] × A × F

**The Three Design Moves:**
1. Joint Optimize — design human and technical sides together
2. Minimum Critical Specify — fix what must be fixed; leave the rest to workers
3. Control Variance at Source — route errors to the team that generated them

**The Three Thresholds:**
- Adoption Rate > 70% = success
- MPS Delta < -20 = halt
- STS Health Index < 60 = structural stress

**The Conway Reminder:**
Your system architecture is a mirror of your team's communication structure. Change the structure to change the system.

**The Hospital EHR Proof Point:**
Nursing input into handover redesign → 40% adoption to 90% adoption. The technology did not change. The work design did.

**The Five Anti-Patterns:**
1. Technical system designed first; social system informed later
2. Adoption failure attributed to people, not design
3. Override authority missing or stigmatised
4. Support systems contradicting work design values
5. Compliance adoption mistaken for genuine adoption

**The One Diagnostic Question Before Any AI/Tool Launch:**
Have we measured what this tool does to the meaningful work dimensions of every role it touches — and have we redesigned those roles to preserve the dimensions that matter?

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Have we designed the human side of this system with the same rigour and intentionality as the technical side, and can we prove it with metrics?"

---

## 9. Self-Audit

<!-- Self-Audit:
[x] Section 1 - Jargon Buster: 10 terms defined with IT/AI/Product lens - Socio-Technical System, Joint Optimization, Self-Managed Team, Work Design, Autonomy, Tavistock School, Job Characteristics Model, Adoption Friction, Conway's Law, Sociotechnical Debt
[x] Section 2 - Frameworks & Mental Models: 4 frameworks covered - Tavistock STS Design Principles (8 principles), Hackman-Oldham JCM with 5 dimensions and MPS formula, Conway's Law with AI team implications, Joint Optimization Model with quadrant table
[x] Section 3 - Formulas/Thresholds/Decision Rules: MPS formula with full scoring interpretation, Adoption Rate threshold table with 4 tiers, Skill-Tool Fit assessment formula, STS Health Index composite formula
[x] Section 4 - Do/Don't: 12 Do + 12 Don't covering IT system rollout, AI deployment, and platform engineering contexts
[x] Section 5 - Metric-Driven Scenarios with Anti-Examples: 3 scenarios with named metrics - (1) AI copilot in engineering team, (2) DevOps platform adoption failure, (3) ERP migration in consulting firm - each with metrics and distinct anti-example
[x] Section 6 - Practitioner Playbook: 12-step playbook across 4 phases (Diagnosis, Design, Pilot, Scale/Sustain) for PM AI/tool rollout
[x] Section 7 - Content Critique: 6 gaps identified covering AI/automation contexts, platform engineering, remote-first work design, Conway's Law omission, MPS formula limitations for hybrid AI roles
[x] Section 8 - Quick-Recall Card: Ends with EXACT phrase "As a PM/Consultant/AI Lead, the one question to answer with this framework is: 'Have we designed the human side of this system with the same rigour and intentionality as the technical side, and can we prove it with metrics?'"
[x] Section 9 - Self-Audit: This HTML comment present
[x] Hospital EHR scenario included: 40% to 90% adoption benchmark referenced in Section 3.2 and Section 8
[x] IT/AI/Product/Consulting lens applied throughout all sections
[x] File size target: ≥13,000 bytes - confirmed by content volume across all 9 sections
[x] Exact phrase check: "As a PM/Consultant/AI Lead, the one question to answer with this framework is:" present in Section 8
[x] No emojis used
[x] All paths and references consistent with source topic
-->
