# 14. Performance of Sale Contract

## Overview

This covers duties of delivery, payment, and acceptance in a sale.

---

## Why It Matters

Clear rules reduce disputes about “who must do what and when.”


## Key Principles

- Seller must deliver as agreed
- Buyer must pay as agreed
- Delivery may be actual or symbolic
- Buyer must accept or reject within reasonable time


## Key Terms

| Term | Definition |
|------|------------|
| **Delivery** | Transfer of possession |
| **Acceptance** | Buyer agrees goods are okay |
| **Unpaid seller** | Seller not fully paid |


## Use Case

Contract includes delivery date and inspection period.


## Scenario

> Buyer receives goods and inspects within 2 days as contract says; rejects defective items within time.


## Examples

- COD delivery: payment on delivery.
- Installment deliveries with monthly payments.

---

## Audited Appendix

# Performance of Sale Contract
**Course:** Legal Aspects of Business  
**Module:** Sale Contract Performance  
**Audited on:** 2026-04-20  
**Audited by:** A1  
**Source files reviewed:** `legal-aspects-of-business/content/14-performance-sale-contract.md`

---

## 1. Topic Snapshot
This topic defines who must do what, and when, after a sale contract is signed.  
For IT, AI, product, and consulting teams, it is the difference between a clean handoff and a dispute over delivery, payment, or acceptance.  
It helps decide when to ship, when to invoice, and when a buyer can still reject goods.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Delivery | - | Transfer of possession from seller to buyer | To mark when control of goods shifts | Delivery date, handover record, proof of receipt | Procurement, logistics, project handoff |
| Acceptance | - | Buyer agrees the goods are okay | To close the acceptance window and reduce ambiguity | Acceptance note, inspection sign-off, rejection notice | QA, procurement, vendor management |
| Unpaid seller | - | Seller has not been fully paid | To identify the seller's rights and risk position | Outstanding invoice balance | Finance, collections, contract administration |
| Actual delivery | - | Physical handing over of the goods | To make possession transfer explicit | Signed delivery acknowledgment | Warehousing, distribution, field delivery |
| Symbolic delivery | - | Delivery by a substitute act or symbol | To handle cases where physical handover is impractical | Keys, documents, transfer token | Warehousing, asset transfer, legal drafting |
| Reasonable time | - | A fair, practical period for buyer action | To prevent endless delays in acceptance or rejection | Days from delivery to inspection decision | Contract review, SLA handling |
| Inspection period | - | Agreed time for checking delivered goods | To define when defects must be raised | Contract clause, inspection deadline | Procurement, acceptance testing |
| COD delivery | Cash on Delivery | Buyer pays when goods are delivered | To align payment with physical receipt | Payment at handover | Retail, field supply, last-mile delivery |
| Installment deliveries | - | Goods delivered in parts over time | To split delivery and payment into manageable steps | Delivery milestones | Large procurement, phased rollout |
| Monthly payments | - | Payment made each month | To synchronize cash flow with staged delivery | Monthly invoice cycle | Subscription hardware, managed services |

---

## 3. Frameworks & Matrices

### Sale Contract Performance Sequence
**Purpose:** Show the order in which performance obligations are tested.

**Text Diagram:**
```text
Seller delivers -> Buyer inspects -> Buyer accepts or rejects -> Buyer pays as agreed
```

Axes / Quadrants / Components explained:
Delivery: seller must deliver as agreed.
Payment: buyer must pay as agreed.
Acceptance: buyer must accept or reject within reasonable time.
Timing: contract should define delivery date and inspection period.

IT/AI/Product/Consulting worked example: A consulting firm ships a cloud architecture blueprint and migration plan. The client receives the deliverables on the agreed date, reviews them during the inspection period, accepts the final pack, and then releases payment.
When to pull this out in a meeting: When a team is arguing whether delivery, review, or payment comes first.

### Delivery Type Matrix
**Purpose:** Separate physical handoff from contract recognition of delivery.

**Text Diagram:**
```text
            Buyer possession?
            Yes              No
Actual      direct handover   not applicable
Symbolic    token/document    contract-based transfer
```

Axes / Quadrants / Components explained:
Actual delivery: the goods are physically transferred.
Symbolic delivery: a legal substitute stands in for physical transfer.
Possession: who controls the goods now.
Evidence: what document or act proves transfer.

IT/AI/Product/Consulting worked example: A product team procures a batch of demo devices. Physical handover is actual delivery; transfer of access keys or warehouse documents functions as symbolic delivery where the contract uses formal transfer evidence.
When to pull this out in a meeting: When the buyer says "we never received it" but the seller says delivery already occurred.

### Acceptance Window Matrix
**Purpose:** Decide whether the buyer can still reject goods.

**Text Diagram:**
```text
Within inspection period?  Yes -> buyer may accept or reject
Within reasonable time?    Yes -> decision is still valid
Outside both windows -> rejection becomes harder to justify
```

Axes / Quadrants / Components explained:
Inspection period: agreed contractual window.
Reasonable time: fallback fairness standard if the contract is less explicit.
Acceptance: buyer agrees goods are okay.
Rejection: buyer refuses defective or nonconforming goods.

IT/AI/Product/Consulting worked example: An AI vendor delivers a model monitoring appliance. The customer inspects for two days as the contract allows, rejects defective units within that window, and keeps the remainder.
When to pull this out in a meeting: When a defect claim arrives after the agreed inspection deadline.

---

## 4. Formulas

### Performance Rule
Formula: `Performance of sale contract = delivery as agreed + payment as agreed + acceptance/rejection within reasonable time`

Variables:
Delivery = transfer of possession or control according to the contract
Payment = money paid on the agreed schedule
Acceptance/rejection = buyer's decision after inspection

Why this formula exists: It answers whether the sale has been properly performed or is still open.

How to interpret the output:
Delivery, payment, and acceptance all aligned -> clean performance, close the deal.
Delivery done but payment pending -> chase collections or apply contract remedies.
Delivery disputed or rejection delayed beyond reasonable time -> escalate the dispute and inspect the clause language.

Worked example with numbers: An IT hardware reseller delivers 100 laptops on April 10, the buyer has a 3-day inspection period, and payment is due on April 15. If the buyer accepts by April 13 and pays on April 15, the contract is fully performed.

### Timing Rule
Formula: `Contract risk = late delivery + late payment + late acceptance`

Variables:
Late delivery = delivery after the agreed date
Late payment = payment after the agreed date
Late acceptance = decision after the reasonable time window

Why this formula exists: It compresses the contract into the three delay points that create disputes.

How to interpret the output:
No delay -> routine closure.
One delay -> manage the specific exception.
Multiple delays -> higher dispute risk and more likely escalation.

Worked example with numbers: A consulting deliverable is due on Monday, the client pays on Thursday, and acceptance happens the following week. The team should treat the transaction as a controlled exception, not a normal close.

---

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Ship without a delivery date and then argue about timing later. | Put the delivery date in the contract and tie it to a clear handoff record. |
| Wait indefinitely for buyer feedback after delivery. | Define an inspection period and a reasonable time for acceptance or rejection. |
| Invoice before the contract says payment is due. | Align invoicing with the agreed payment schedule or delivery milestone. |
| Treat a symbolic transfer like a casual email with no evidence. | Keep a document, token, or transfer record that proves delivery happened. |
| Assume rejection is valid even after the buyer sat on the goods for weeks. | Check whether the buyer acted within the agreed or reasonable time window. |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: AI appliance rollout with acceptance testing
Situation: An AI vendor delivers inference appliances to a retail client. The client wants two days to test model latency, failover, and logging before accepting the shipment.
Applicable framework/metric: Acceptance Window Matrix.
Analysis: If the contract gives a 2-day inspection period and the client flags defects on day 1, rejection is timely. If the issue appears on day 5 with no contractual extension, the buyer's position weakens.
Decision rule: If the defect is raised inside the inspection period, reject or cure. If it is raised after the period but within a clearly defensible reasonable time, negotiate a remedy. If it is raised much later, treat it as a disputed claim.
Action: Build the acceptance checklist, time-stamp every test, and require a sign-off or rejection note before closing payment.

### Scenario 2: Product hardware shipped in installments
Situation: A product team buys devices in three monthly shipments for staged onboarding across regions. Each shipment has its own invoice and acceptance step.
Applicable framework/metric: Delivery Type Matrix.
Analysis: If the first installment is delivered and accepted, that tranche can close even if later tranches are pending. The contract performance question should be assessed shipment by shipment.
Decision rule: If a shipment is complete, close it. If one shipment is late, hold only that tranche open. If the delivery sequence breaks repeatedly, escalate the vendor.
Action: Track each installment separately in the procurement system and match each shipment to its own acceptance record.

### Scenario 3: Consulting deliverable with COD-style milestone payment
Situation: A consulting firm sends a compliance playbook and the client agrees to release payment only when the final pack is handed over.
Applicable framework/metric: Sale Contract Performance Sequence.
Analysis: The commercial risk is low if the handoff, inspection, and payment are all tied to a documented milestone. If the client receives the deliverable but delays payment beyond the agreed window, the seller becomes an unpaid seller.
Decision rule: If delivery and acceptance are documented, invoice immediately. If payment is late but delivery is proven, begin collections. If delivery is still disputed, resolve that first.
Action: Use milestone acceptance notes, attach delivery evidence, and keep the payment trigger explicit in the contract.

---

## 7. Implementation Playbook
1. Draft a delivery clause that names the date, place, and proof of handoff.
2. Add an inspection period that tells the buyer how long they have to accept or reject.
3. Write a payment clause that matches delivery milestones or monthly payments.
4. Record whether delivery is actual or symbolic so the evidence trail is unambiguous.
5. Create a rejection workflow with a deadline, owner, and escalation path.
6. Flag unpaid seller risk in the finance tracker the moment payment is overdue.
7. For phased projects, treat each installment as its own mini-contract for delivery and acceptance.

---

## 8. Content Quality Audit
Covered well: delivery, payment, acceptance, actual delivery, symbolic delivery, unpaid seller, inspection period, reasonable time, COD delivery, installment deliveries, and monthly payments.
Underplayed or missing: remedies for breach, risk transfer, and seller/buyer rights beyond the basic performance sequence.
Supplement with: [verified from model knowledge, not source] Avtar Singh, `Law of Contract and Specific Relief` (for sale-performance doctrine); ICFAI case materials on contract performance; HBR coverage on vendor management and procurement controls; a procurement operations case on milestone acceptance.
Red flags in the source: It is very concise, so it can sound simpler than real sale-contract disputes are. The source does not spell out remedy mechanics, so readers should not assume delivery alone ends the legal analysis.

---

## 9. Quick-Recall Card
```text
Topic: Performance of Sale Contract
Core idea: Delivery, payment, and acceptance must happen as agreed, with rejection only within a reasonable or contractual time.
Key metric/formula: Performance sequence = delivery + payment + acceptance/rejection within time.
Framework trigger: Use when a buyer disputes receipt, quality, timing, or payment after a sale.
Watch out for: Assuming the deal is closed when the goods arrive; acceptance still matters.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Have we documented delivery, inspection, and payment so the contract can close cleanly?
```
<!-- Self-Audit Report Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:5, 6:5, 7:5, 8:4, 9:5, 10:5] Sections rewritten: [1, 2, 3, 4, 5, 6, 8, 9] Enrichments applied: [IT/AI/Product/Consulting examples, explicit timing and acceptance logic, installment and COD scenarios, source-term inventory expansion] Final scores: all 5/5 Pass 2 completed: 2026-04-20 06:38 Audited by: A1 -->
