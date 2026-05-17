# 15. Sale, Service and Goods (Mixed Transactions)

## Overview

Some deals include both goods and services—like restaurant food (goods) plus serving (service).

---

## Why It Matters

Legal rights depend on whether it’s treated as a sale of goods or a service—or both.


## Key Principles

- Identify main purpose of contract
- Separate value of goods vs service if needed
- Consumer remedies may apply for services
- Tax/legal treatment can differ


## Key Terms

| Term | Definition |
|------|------------|
| **Composite contract** | Goods + services together |
| **Service contract** | Work performed for payment |


## Use Case

AMC (Annual maintenance contract) including spare parts + labor.


## Scenario

> A company signs printer maintenance: parts replacement + service visits. Defective parts and poor service both create remedies.


## Examples

- Smartphone repair: parts (goods) + labor (service).
- Restaurant: food (goods) + dining service.

---

## Audited Appendix

# Sale, Service and Goods (Mixed Transactions)
**Course:** Legal Aspects of Business  
**Module:** Mixed Transactions  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** `legal-aspects-of-business/content/15-sale-service-mixed.md`

---

## 1. Topic Snapshot
This topic explains how to classify a deal that bundles goods and services.
For IT, AI, Product, and Consulting leaders, the decision changes remedies, pricing splits, and legal treatment.
The practical question is: what is the main purpose of the contract, and what part should be treated as service work?

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Mixed transaction | N/A | One deal that includes both goods and services | It captures bundled commercial arrangements | By reading the contract scope and deliverables | Procurement, legal review, and SOW discussions |
| Composite contract | N/A | Goods and services packaged together | It helps classify a bundle instead of forcing one label too early | By separating item value from work value | Contract drafting and dispute analysis |
| Service contract | N/A | Payment is for work performed | It distinguishes labor, support, and maintenance from sale of goods | By checking output, effort, and service levels | MSP, consulting, and support agreements |
| AMC | Annual Maintenance Contract | Ongoing maintenance plus parts or visits | It is the source's core example of a mixed deal | By splitting parts, labor, and visit frequency | IT hardware support and facilities contracts |

## 3. Frameworks & Matrices

### Main-Purpose Split
**Purpose:** Classify the deal by the contract's dominant commercial purpose.

**Text Diagram:**
```text
Bundle of goods + services
        |
        v
Is the main purpose sale of goods?
   | yes -> treat goods as primary
   | no
   v
Is the main purpose service work?
   | yes -> treat services as primary
   | no
   v
Split value, scope, and remedies across both parts
```

Axes / Quadrants / Components explained:
Component 1: Main purpose, meaning what the buyer is really paying for.
Component 2: Goods value, meaning the hardware, parts, or licensed deliverables.
Component 3: Service value, meaning implementation, support, maintenance, or labor.
Component 4: Remedy bucket, meaning which rules and escalation path apply to each part.
IT/AI/Product/Consulting worked example: A consulting firm sells an AI monitoring appliance plus six months of support. If the appliance is the real commercial core, procurement should treat hardware defects separately from support SLA misses.
When to pull this out in a meeting: Use it when the contract has one price but multiple deliverables.

## 4. Formulas

Formula: Predominant characterization = main purpose of contract [verified from model knowledge, not source]
Variables:
Main purpose = what the client is actually buying.
Goods value = value of physical or saleable items.
Service value = value of labor, maintenance, or support.
Why this formula exists: It answers whether the legal analysis should start with goods rules, service rules, or a split treatment.
How to interpret the output:
Value goods > service -> goods-first analysis -> focus on delivery, defect, and replacement rights
Value service > goods -> service-first analysis -> focus on performance, SLA, and remediation
Values are close or intertwined -> mixed treatment -> document a split and write explicit remedies
Worked example with numbers: An AI deployment contract is priced at $120,000, with $80,000 for appliance delivery and $40,000 for onboarding and support. The goods element dominates, so the first question is whether the deliverable itself is defective before arguing about service credits.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Bundle hardware and support into one vague line item | Split the invoice into goods, services, and support artifacts |
| Assume a mixed deal is automatically a pure sale | Classify the main purpose before assigning remedies |
| Ignore service failures because goods were delivered | Track SLA misses, escalation steps, and cure periods |
| Treat every maintenance fee as the same risk | Separate parts replacement from labor and site visits |
| Wait for a dispute before defining who owns what | Write ownership, acceptance, and remedy rules into the contract |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: Managed AI appliance with support
Situation: A product team buys an AI inference box for a customer support bot plus a 12-month managed support package. The deal is priced at $200,000, with $140,000 for the appliance and $60,000 for support.
Applicable framework/metric: Main-Purpose Split.
Analysis: The goods share is 70%, so the contract reads as goods-first, but the support failure still needs a separate SLA review.
Decision rule: If the goods share is above 60%, treat product defects as primary. If it is between 40% and 60%, split remedies. If it is below 40%, treat service performance as primary.
Action: Separate defect management for the appliance from ticket response and uptime tracking for support.

Scenario 2: Enterprise software rollout with implementation
Situation: A consulting team sells a CRM platform plus 400 hours of configuration, migration, and training. The platform license is $90,000 and the services are $110,000.
Applicable framework/metric: Main-Purpose Split.
Analysis: The service share is 55%, so the commercial center of gravity is implementation quality rather than sale of a static product.
Decision rule: If services exceed 50%, lead with service performance controls. If the split is near even, write dual remedies. If product value is dominant, prioritize delivery and acceptance criteria.
Action: Add separate sign-off for license delivery and for migration milestones.

Scenario 3: IT maintenance bundle for branch devices
Situation: A consulting-led IT vendor sells printer maintenance for 50 branch offices, including replacement parts, field visits, and remote diagnostics. The annual fee is $75,000, and 45% of that value is estimated parts, while 55% is labor and service travel.
Applicable framework/metric: Main-Purpose Split.
Analysis: Because services are slightly dominant, missed visit windows and repair turnaround are the key management risks.
Decision rule: If services are above 50%, monitor response-time SLAs first. If goods are above 50%, monitor replacement quality first. If both are close, negotiate dual KPIs.
Action: Put parts lead times, technician response times, and escalation contacts into the SOW.

## 7. Implementation Playbook
1. Inventory every bundled line item in the contract and tag it as goods, services, or mixed.
2. Split the commercial value into separate pricing lines for hardware, labor, support, and travel.
3. Map the main purpose of the contract and write that classification into the procurement note.
4. Draft acceptance, rejection, repair, and service-credit clauses for each component.
5. Build an internal escalation checklist for defects, delays, and SLA misses.
6. Train procurement, legal, product, and consulting teams to avoid single-line bundle pricing.

## 8. Content Quality Audit
Covered well: The source clearly explains that mixed deals must be classified by main purpose and may need value separation.
Underplayed or missing: It does not spell out a formal legal test, remedy sequencing, or contract drafting language.
Supplement with: [verified from model knowledge, not source] Benjamin's Sale of Goods; Chitty on Contracts; an Indian consumer-law note on composite contracts; and a current journal article on mixed-contract characterization.
Red flags in the source: The examples are brief and do not show how to split remedies or price allocation in a real contract.

## 9. Quick-Recall Card
```text
Topic: Sale, Service and Goods (Mixed Transactions)
Core idea: Classify bundled deals by main purpose, then split value and remedies where needed.
Key metric/formula: Predominant characterization = main purpose of contract.
Framework trigger: Use when a contract bundles goods, labor, support, or maintenance in one deal.
Watch out for: Treating every bundle as a pure sale or pure service.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: What is the main commercial object of this contract?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [] Enrichments applied: [IT/AI/Product/Consulting framing, dominant-purpose analysis, contract-splitting examples] Final scores: all 5/5 Pass 2 completed: 2026-04-20 06:40 Audited by: A2 -->
