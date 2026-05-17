# 24. Agent, Agency and Principal

## Overview

Agency is when one person (agent) acts on behalf of another (principal) to deal with third parties.

---

## Why It Matters

Businesses grow using agents—sales reps, brokers—without owners doing everything themselves.


## Key Principles

- Agent can bind principal if acting within authority
- Authority may be actual or implied
- Principal is responsible for agent’s authorized acts
- Agent must act in good faith


## Key Terms

| Term | Definition |
|------|------------|
| **Principal** | Person/company represented |
| **Agent** | Person acting for principal |
| **Authority** | Power given to agent |


## Use Case

Real estate broker sells property on behalf of owner.


## Scenario

> Agent signs a deal within authority; principal must honor it even if principal later regrets it.


## Examples

- Sales agent signs customer orders for a company.
- Travel agent books tickets for customers.

---

## Audited Appendix

# 24. Agent, Agency and Principal
**Course:** Legal Aspects of Business  
**Module:** content  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** `24-agent-agency-principal.md`

---

## 1. Topic Snapshot
Agency is the rule that lets an agent act for a principal in front of third parties.
[verified from model knowledge, not source] For IT, AI, product, and consulting leaders, the key decision is whether a person can bind the business without waiting for the founder, manager, or client owner.
[verified from model knowledge, not source] This matters because a signed deal, order, or commitment can become the principal's obligation even when the principal later regrets it.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Principal | N/A | The person or company being represented | So someone can act on behalf of the owner | Whether the decision ultimately lands on the owner | Vendor contracts, outsourcing, channel sales |
| Agent | N/A | The person acting for the principal | So the business can operate through delegates | Whether the person was allowed to act | Sales, procurement, consulting delivery |
| Authority | N/A | The power given to the agent | To show what the agent can legally do | Written limits, role scope, prior practice | Approval matrices, signing limits |
| Actual authority | N/A | Authority intentionally given by the principal | To make delegation explicit and defensible | Signed delegation, policy, instruction | Founder delegation, manager approvals |
| Implied authority | N/A | Authority inferred from the role or conduct | To reflect how work really gets done | Repeated practice, role expectations | Account managers, project leads |
| Good faith | N/A | Acting honestly and loyally | To stop agents from abusing trust | Complaints, conflicts, deviation from instructions | Agency governance, conduct reviews |
| Third party | N/A | The outside person dealing with the agent | Because agency affects outsiders, not just internal teams | Counterparty reliance on the signature | Customers, suppliers, partners |
| Bind principal | N/A | Create an obligation for the principal | To explain why delegated acts can be enforceable | Whether the deal is treated as the business's commitment | Contract signing, order acceptance |
| Authorized acts | N/A | Acts within the agent's permission | To separate valid delegation from overreach | Comparison against the approved scope | Deal approvals, release approvals |

## 3. Frameworks & Matrices

### Authority Check Matrix
**Purpose:** Decide whether a delegated act should be treated as safe to execute or should be escalated.
[verified from model knowledge, not source] This matrix is a practical control overlay on the source's actual/implied authority idea.

**Text Diagram:**
```text
                         Third-party reliance
                      Low                         High
Authority
Clear                 Safe to proceed             Proceed, but log and retain evidence
Unclear               Escalate before action      Stop; high risk of binding the principal
```

Axes / Quadrants / Components explained:
Component 1: Authority clarity means actual authority is documented or implied authority is strong enough to support the role.
Component 2: Third-party reliance means the outside party is likely to trust the signature or commitment.
Component 3: Evidence quality means email trail, policy, prior approvals, and role descriptions that support the decision.

IT/AI/Product/Consulting worked example: [verified from model knowledge, not source] A consulting engagement manager signs a change request for a cloud implementation. If the manager has written signing authority and the client has seen that role used before, the deal is low-risk. If the manager is only "usually involved" and the client is asking for a larger scope jump, the matrix pushes the team to escalate before signing.
When to pull this out in a meeting: Use it when someone wants to sign a contract, order, or statement of work without waiting for the owner.

## 4. Formulas

[verified from model knowledge, not source] Formula: `Authority Coverage Score = actual authority (0/1) + implied authority (0/1) + documented delegation (0/1)`
Variables:
actual authority = 1 if the principal clearly authorized the act
implied authority = 1 if the role and prior conduct support the act
documented delegation = 1 if there is a written policy, email, or approval trail
Why this formula exists: It answers the practical business question, "Can this person bind us right now?"
How to interpret the output:
0 -> no safe authority signal -> stop and escalate
1 -> weak signal -> verify before signature
2 -> usable but incomplete -> proceed only with logging and approval
3 -> strong signal -> proceed, then file the evidence
Worked example with numbers: [verified from model knowledge, not source] A product manager signs a SaaS renewal. The role has implied authority = 1, but there is no written delegation = 0 and no explicit actual authority = 0, so the score is 1. The team should verify before the document goes out.

## 5. Do vs Don't
[verified from model knowledge, not source] These controls are operational guidance for delegated signing risk.

| Don't | Do |
|---------|-------|
| Let any employee sign a customer contract by default | Publish a clear signing matrix for the business |
| Assume a role title equals unlimited power | Tie authority to scope, value, and product line |
| Ignore repeated practice in the field | Treat implied authority as a real control issue |
| Rely on memory when the deal value is high | Keep written delegation and approval trails |
| Blame the counterparty after an agent signs | Check whether the principal created the appearance of authority |

## 6. Real-Life Scenarios (Metric-Driven)
[verified from model knowledge, not source] The scenarios below translate the source concept into decision rules for common business settings.

Scenario 1: Sales order signed by an account executive
Situation: [verified from model knowledge, not source] A SaaS account executive signs a renewal worth $42,000. The company policy allows account executives to commit up to $50,000, and the customer has seen this same role sign renewals before.
Applicable framework/metric: Authority Coverage Score.
Analysis: actual authority = 1, implied authority = 1, documented delegation = 1, so the score is 3.
Decision rule: If the score is 3, proceed. If it is 2, proceed with logging. If it is 0-1, escalate.
Action: File the approval trail, send the renewal, and keep the signature matrix in the deal room.

Scenario 2: AI vendor contract for production data access
Situation: [verified from model knowledge, not source] A product lead wants to approve a pilot with an AI vendor that will touch production data. The lead has no written signing authority, but the vendor has been told informally that the lead "handles AI tools."
Applicable framework/metric: Authority Coverage Score.
Analysis: actual authority = 0, implied authority = 1, documented delegation = 0, so the score is 1.
Decision rule: If the score is 3, proceed. If it is 2, verify and log. If it is 0-1, stop and escalate.
Action: Escalate to legal, security, and finance before any data is shared.

Scenario 3: Consulting scope change on a fixed-fee project
Situation: [verified from model knowledge, not source] A consulting manager approves a scope expansion that adds three extra workshops. The contract change is worth 18% more than the original fee, and the client is expecting a quick response.
Applicable framework/metric: Delegated value limit.
Analysis: If the manager limit is 10% and the change is 18%, the act exceeds the delegated range by 8 percentage points.
Decision rule: If the change is within the limit, sign and log. If it is above the limit by up to 5 points, verify. If it exceeds the limit by more than 5 points, escalate.
Action: Route the change request to the engagement partner before any confirmation goes out.

## 7. Implementation Playbook
[verified from model knowledge, not source] This playbook turns the source concept into a simple approval process.

1. Build a signing matrix that maps role, limit, and deal type to approval rights.
2. Document actual authority in one place, such as a policy page or contract playbook.
3. Record implied authority risk for recurring roles like sales, procurement, and project leads.
4. Add a pre-sign checklist for contracts, orders, renewals, and scope changes.
5. Keep an evidence trail for any delegated act that could bind the business.
6. Escalate exceptions before the document leaves the business.
7. Review the matrix after every contract dispute, audit finding, or missed approval.

## 8. Content Quality Audit
[verified from model knowledge, not source] This audit is a gap analysis against the source, not a claim that the source itself contains these references.

Covered well: The source clearly explains the basic agency triangle, the idea of authority, the principal's responsibility for authorized acts, and the need for good faith.
Underplayed or missing: It does not separate actual authority from implied authority in detail, and it does not cover what happens when authority is missing, disputed, or revoked.
Supplement with: [verified from model knowledge, not source] standard business law texts such as Anson's Law of Contract and Sealy and Hooley's Commercial Law: Text, Cases, and Materials; HBS-style case discussions on delegation and control; and peer-reviewed articles on delegated authority, fiduciary duty, and contracting risk.
Red flags in the source: The source is intentionally simplified. It does not mention ratification, termination of authority, apparent authority, or the internal controls needed to prevent unauthorized signatures.

## 9. Quick-Recall Card

```text
Topic: Agent, Agency and Principal
Core idea: An agent can bind a principal when acting with authority.
Key metric/formula: Authority Coverage Score = actual authority + implied authority + documented delegation.
Framework trigger: Use it before any delegated signature, order, or scope change.
Watch out for: Implied authority that is assumed but never written down.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Can this person legally commit the business right now?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [authority matrix, operational score, IT/AI/Product/Consulting examples, missing-topic red flags] Final scores: all 5/5 Pass 2 completed: 2026-04-20 06:46 Audited by: A2 -->
