# Define Phase

## Overview
The Define phase is the first step of the DMAIC framework where the team clearly states the problem, identifies the customer, and sets the boundaries of the project. A well-executed Define phase prevents scope creep and ensures everyone agrees on what success looks like. Key outputs include a project charter, a high-level process map, and a clear voice of the customer statement.

---

## Why It Matters
Projects fail most often because the problem was never clearly defined. If team members have different interpretations of the issue, they will pull in different directions and waste resources. The Define phase creates alignment by documenting the problem statement, business case, timeline, and team roles so that every stakeholder shares the same understanding before any data collection begins.

## Key Principles
- Start with the customer and work backward to the process
- Write a clear, measurable problem statement that avoids jumping to solutions
- Define project scope to keep the effort focused and achievable
- Secure executive sponsorship and assign team roles early

## Key Terms
| Term | Definition |
|------|------------|
| **Project Charter** | A formal document that outlines the problem, goals, scope, timeline, and team for a Six Sigma project |
| **Voice of the Customer (VOC)** | The process of capturing customer needs, expectations, and preferences |
| **SIPOC** | A high-level map showing Suppliers, Inputs, Process, Outputs, and Customers |
| **Critical to Quality (CTQ)** | The measurable characteristics of a product or process that must meet customer standards |

## Use Case
A retail chain launches a Six Sigma project to reduce checkout wait times and uses the Define phase to document customer expectations, map the current checkout process, and set a target of under three minutes per transaction.

## Scenario
> An online retailer notices a spike in return rates. During the Define phase, the team surveys customers and discovers that items frequently arrive in the wrong size. They write a problem statement, create a SIPOC diagram of the order fulfillment process, and set a goal of reducing size-related returns by 50% within six months.

## Examples
- A hospital defines a project to reduce surgical site infections by first mapping the entire pre-operative preparation process with a SIPOC diagram
- A software company creates a project charter to reduce deployment failures, clearly stating that the scope covers only the release pipeline and not feature development

---

## Audited Appendix

# Define Phase
**Course:** Six Sigma  
**Module:** Content / Define Phase  
**Audited on:** 2026-04-18  
**Audited by:** A4  
**Source files reviewed:** `six-sigma/content/03-define-phase.md`

---

## 1. Topic Snapshot
The Define phase turns a vague quality problem into a project with a customer, a scope, a target, and an owner.
For IT, AI, Product, and Consulting leaders, it is the point where you decide whether the team is solving the right problem before anyone starts collecting data.
The decision it helps make is how to set the charter, map the process, and keep the work from drifting into scope creep.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Define phase | - | The first DMAIC stage where the problem is framed. | Prevents the team from solving the wrong problem. | Charter completion, scope clarity, stakeholder alignment. | Six Sigma launches, operations reviews. |
| DMAIC | Define, Measure, Analyze, Improve, Control | The full Six Sigma improvement sequence. | Gives the project a disciplined path from problem to control. | Stage completion, milestone tracking. | Quality programs, process improvement, consulting. |
| Project charter | - | The formal document that states the problem, goal, scope, and team. | Aligns everyone before work starts. | Approved charter, date of sign-off, sponsor name. | PMO, Lean Six Sigma, operations. |
| Voice of the Customer | VOC | Customer needs, expectations, and preferences expressed in their language. | Keeps improvement anchored in what the buyer cares about. | Interview themes, survey counts, complaint patterns. | Product discovery, service design, CX. |
| SIPOC | Suppliers, Inputs, Process, Outputs, Customers | A high-level map of the process boundary. | Shows the project context before deep analysis begins. | SIPOC completion, handoff clarity. | Workshops, process mapping, consulting. |
| CTQ | Critical to Quality | The measurable thing that must meet customer standards. | Converts customer needs into a metric. | Pass/fail, target attainment, defect rate. | Quality reviews, product requirements, service ops. |
| Problem statement | - | A clear description of what is wrong today. | Stops teams from jumping to solutions. | Baseline metric, gap to target, time period. | Project kickoffs, executive updates. |
| Business case | - | Why the project matters financially or strategically. | Justifies the time and money spent. | Savings, risk reduction, revenue impact. | Leadership decks, prioritization forums. |
| Scope | - | What the project will and will not cover. | Keeps the team focused and achievable. | In-scope / out-of-scope list. | Charters, steering committee meetings. |
| Scope creep | - | The slow expansion of project boundaries. | Prevents endless projects and diluted results. | Scope changes, added deliverables. | PMO, consulting, program governance. |
| Executive sponsorship | - | Senior backing that clears obstacles and resources. | Gives the project authority and support. | Sponsor presence, escalation speed. | Transformation programs, quality councils. |
| Stakeholder | - | Anyone affected by or involved in the project. | Makes sure the right voices are included. | Stakeholder map, approval list. | Change management, project governance. |
| High-level process map | - | A simple view of the main process steps. | Lets the team see the flow before detailed analysis. | Step count, handoff count, map approval. | Workshops, process improvement, operations. |
| Team roles | - | The responsibilities of the people on the project. | Prevents confusion about ownership. | RACI, task ownership, meeting attendance. | PMO, cross-functional projects. |

## 3. Frameworks & Matrices

### Charter Canvas
**Purpose:** Lock the project so the team knows what problem it is solving, why it matters, and who owns it.

**Text Diagram:**
```text
customer -> problem -> target -> scope -> sponsor -> team -> timeline
```

Axes / Quadrants / Components explained:
Component 1: Customer - the person or group experiencing the pain.
Component 2: Problem - the gap between current and desired performance.
Component 3: Target - the measurable outcome the team wants to hit.
Component 4: Scope, sponsor, team, timeline - the guardrails that make the project executable.
IT/AI/Product/Consulting worked example: A SaaS company writes a charter for deployment failures, names the release pipeline as the scope, assigns the DevOps lead as owner, and sets a 90-day target to cut failures in half. That keeps the team from drifting into feature development or backlog grooming.
When to pull this out in a meeting: When everyone agrees there is pain but nobody can state the project in one sentence.

### VOC to CTQ Alignment Map
**Purpose:** Convert customer language into a measurable quality target and tie it to the process flow.

**Text Diagram:**
```text
VOC -> CTQ -> process step -> metric -> control
```

Axes / Quadrants / Components explained:
Component 1: VOC - what the customer says they need.
Component 2: CTQ - the measurable quality attribute that must be met.
Component 3: Process step - where the issue happens in the workflow.
Component 4: Metric and control - how the team will prove improvement and keep it there.
IT/AI/Product/Consulting worked example: A hospital hears that patients want "faster service." The team converts that into CTQs like under-three-minute registration and under-ten-minute triage, then ties those measures to the front desk and triage steps that drive the experience.
When to pull this out in a meeting: When customer complaints are qualitative but the team needs a quantitative project target.

### SIPOC Boundary View
**Purpose:** Show the system boundary before the team dives into root cause analysis.

**Text Diagram:**
```text
Suppliers -> Inputs -> Process -> Outputs -> Customers
```

Axes / Quadrants / Components explained:
Component 1: Suppliers - who provides the inputs.
Component 2: Inputs - the materials, data, or requests entering the process.
Component 3: Process - the main steps that transform inputs to outputs.
Component 4: Outputs and customers - what is delivered and who receives it.
IT/AI/Product/Consulting worked example: An online retailer uses SIPOC to map order entry, warehouse picking, packing, and shipment so it can locate where size-related returns begin. The map shows whether the failure is in order capture, inventory accuracy, or fulfillment.
When to pull this out in a meeting: When the team needs a common picture of the process before arguing about causes.

## 4. Formulas

Formula: Problem Gap = current metric - target metric
Variables:
Current metric = the baseline measure today.
Target metric = the desired level the charter promises.
Why this formula exists: It answers how large the improvement challenge is.
How to interpret the output:
Value close to 0 -> small gap -> narrow fix may be enough
Value moderate -> meaningful gap -> use a structured project
Value large -> severe gap -> clarify scope and sponsor support before work starts
Worked example with numbers: If checkout wait time is 4.8 minutes and the target is 3.0 minutes, the gap is 1.8 minutes. That is enough to justify a defined Six Sigma project.

Formula: Scope Ratio = in-scope steps / total process steps
Variables:
In-scope steps = steps the charter explicitly covers.
Total process steps = all steps in the end-to-end process.
Why this formula exists: It answers how focused the project really is.
How to interpret the output:
Value < 0.25 -> too narrow -> may miss the root cause
Value 0.25-0.60 -> focused and practical -> good project size
Value > 0.60 -> too broad -> risk of scope creep and slow progress
Worked example with numbers: If a release process has 12 steps and the project covers 4 of them, the scope ratio is 4/12 = 0.33. That is focused enough to execute without becoming a whole-program redesign.

Formula: VOC Traceability = CTQs mapped from VOC / total CTQs
Variables:
CTQs mapped from VOC = quality requirements directly traced to customer language.
Total CTQs = all measurable quality requirements in the charter.
Why this formula exists: It answers whether the project is truly customer-led.
How to interpret the output:
Value < 0.50 -> weak customer linkage -> revisit VOC collection
Value 0.50-0.80 -> usable linkage -> good enough to start
Value > 0.80 -> strong linkage -> the charter is well anchored in customer needs
Worked example with numbers: If 6 out of 8 CTQs trace directly to customer statements, VOC traceability is 0.75. That is a solid sign that the project is solving what the customer actually cares about.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Jump straight to a solution before defining the problem. | Write a measurable problem statement first. |
| Let the project cover everything and nothing at once. | Freeze scope and document what is out of scope. |
| Write a charter without customer language. | Start from VOC and convert it into CTQs. |
| Skip the sponsor and expect the project to clear itself. | Secure executive sponsorship and named team roles early. |
| Use a process map only after the team gets stuck. | Build a high-level process map in the Define phase. |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: Retail checkout delays
Situation: A retail chain is getting complaints that checkout takes too long. The operations team needs to decide whether the issue is a staffing problem, a layout problem, or a project scope problem.
Applicable framework/metric: Charter Canvas and Problem Gap.
Analysis: If the current checkout time is 4.8 minutes and the target is under 3.0 minutes, the gap is 1.8 minutes. That is enough to justify a formal project with a clear owner and timeline.
Decision rule: If the gap is small, use a local fix. If moderate, run a chartered project. If large, involve sponsorship and broader process redesign.
Action: Draft the charter, assign a store ops owner, and baseline checkout time by shift and location.

Scenario 2: Size-related returns in e-commerce
Situation: An online retailer sees a spike in returns because items are arriving in the wrong size. Product and consulting teams need to define the problem without jumping directly to a warehouse fix.
Applicable framework/metric: VOC to CTQ Alignment Map and VOC Traceability.
Analysis: If customer interviews reveal "wrong size" and "order accuracy" as the main pain points, those become CTQs. If 6 out of 8 CTQs are traced to customer language, VOC traceability is 0.75 and the charter is well grounded.
Decision rule: If VOC traceability is below 50%, go back to the customer. If 50%-80%, proceed. If above 80%, lock the charter and move on to measurement.
Action: Map order capture to fulfillment, define the size accuracy CTQ, and set a 50% reduction target for size-related returns.

Scenario 3: Software deployment failures
Situation: A software company wants fewer deployment failures, but the product team keeps pulling the project toward feature work. The delivery team needs a boundary that keeps the work focused on release reliability.
Applicable framework/metric: SIPOC Boundary View and Scope Ratio.
Analysis: If the release process has 12 steps and the charter covers only 4 critical release-pipeline steps, the scope ratio is 0.33. That is focused enough to execute and broad enough to catch the most important failure points.
Decision rule: If scope ratio is below 0.25, broaden the map. If between 0.25 and 0.60, proceed. If above 0.60, cut the scope before the project drifts.
Action: Freeze the scope to the release pipeline, document the SIPOC, and publish the team roles and escalation path.

## 7. Implementation Playbook
1. Capture VOC through interviews, complaint logs, or support tickets and convert the language into a first-pass problem statement.
2. Draft a project charter that names the customer, target, scope, timeline, business case, sponsor, and team roles.
3. Build a high-level process map or SIPOC so the team can see the boundaries before analysis begins.
4. Translate customer language into CTQs so the project has measurable outcomes instead of vague goals.
5. Baseline the current metric before any changes are made so the gap is visible.
6. Review scope and sponsorship with stakeholders before the project starts to prevent scope creep later.
7. Hand the charter cleanly to Measure phase with one owner, one metric, and one timeline.

## 8. Content Quality Audit
Covered well: The source correctly explains that Define is the first DMAIC step and that project charters, VOC, SIPOC, and CTQs are the core outputs.
Underplayed or missing: The source does not show how to turn VOC into CTQs, how to freeze scope, how to translate a business case into project governance, or how Define connects to later DMAIC stages.
Supplement with: Pande, Neuman, and Cavanagh, *The Six Sigma Way*; George, Rowlands, Price, and Maxey, *The Lean Six Sigma Pocket Toolbook*; Hal Plotkin, "Six Sigma: What It Is and How to Use It" (Harvard Business Review, 1999); Matthias Holweg, Thomas H. Davenport, and Ken Snyder, "How AI Fits into Lean Six Sigma" (Harvard Business Review, 2023); HBS case *The Cleveland Clinic: Improving the Patient Experience (Abridged)* (Raman, Tucker, and Gordon, 2010); and peer-reviewed reviews such as "Systematic Review of the Application of Lean and Six Sigma Quality Improvement Methodologies in Radiology" (2016) and "Lean and Six Sigma as continuous quality improvement frameworks in the clinical diagnostic laboratory" (2022).
Red flags in the source: It is clean and accurate but still introductory, so readers may understand the vocabulary without knowing how to operationalize the Define phase in a real project.

## 9. Quick-Recall Card
```text
Topic: Define Phase
Core idea: The Define phase sets the problem, customer, scope, and target before data collection starts.
Key metric/formula: Problem Gap = current metric - target metric.
Framework trigger: Use it when the problem is still fuzzy or the team is arguing about scope.
Watch out for: Jumping to solutions, vague problem statements, and scope creep.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What exact customer problem, scope, and measurable target are we committing to?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:5, 4:5, 5:4, 6:4, 7:4, 8:4, 9:5, 10:4] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [charter canvas, VOC-CTQ map, SIPOC boundary view, IT/AI/Product/Consulting examples, scope ratio, external references] Final scores: all 5/5 Pass 2 completed: 2026-04-18 20:03 Audited by: A4 -->
