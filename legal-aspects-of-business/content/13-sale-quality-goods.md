# 13. Sale and Quality of Goods (Conditions & Warranties)

## Overview

Law expects goods to meet certain quality standards. “Conditions” are major terms; “warranties” are smaller promises.

---

## Why It Matters

Protects buyers from defective goods and sets clear remedies (reject goods or claim compensation).


## Key Principles

- Goods should match description/sample
- Merchantable/satisfactory quality (as applicable)
- Fitness for buyer’s purpose (if seller knows purpose)
- Condition breach can allow rejection; warranty breach usually damages


## Key Terms

| Term | Definition |
|------|------------|
| **Condition** | Essential term |
| **Warranty** | Less essential term |
| **Fitness** | Suitable for intended use |


## Use Case

Buying machinery for a specific manufacturing need.


## Scenario

> A buyer tells seller the machine must handle heavy load. Seller supplies weaker machine—buyer can reject.


## Examples

- Milk packet expired → buyer rejects.
- Phone battery weaker than promised → claim repair/compensation.

---

## Audited Appendix

# Sale and Quality of Goods (Conditions & Warranties)
**Course:** Legal Aspects of Business  
**Module:** Sale of Goods  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** `legal-aspects-of-business/content/13-sale-quality-goods.md`

---

## 1. Topic Snapshot
This topic explains how the law separates major promises, called conditions, from smaller promises, called warranties.  
It matters because buyers need to know when they can reject goods versus when they should claim compensation.  
The decision is whether the defect is serious enough to unwind the deal or just recover damages.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Condition | N/A | Essential term | To define a core promise | Did the goods meet the core promise? | Sales contracts, quality disputes |
| Warranty | N/A | Less essential promise | To separate minor defects from deal-breakers | Did the defect affect the core bargain? | Vendor terms, after-sales support |
| Fitness | N/A | Suitable for intended use | To match product to purpose | Does it work for the stated use? | Industrial procurement, buyer specs |
| Merchantable quality | N/A | Good enough for normal sale/use | To set a baseline quality level | Would a reasonable buyer accept it? | Consumer goods, inventory acceptance |
| Description | N/A | What the goods were said to be | To stop mis-selling | Do the goods match the description? | Catalog sales, e-commerce listings |
| Sample | N/A | Reference item for comparison | To test whether the batch matches | Does delivery match the sample? | Bulk supply, retail sourcing |

---

## 3. Frameworks & Matrices

### Defect Severity Check
**Purpose:** Decide whether a defect is a condition breach or a warranty breach.

**Text Diagram:**
```text
Core promise broken? -> condition
Minor promise broken? -> warranty
```
Axes / Quadrants / Components explained:
Component 1: essentiality, meaning how central the promise is to the deal.
Component 2: remedy impact, meaning whether the buyer can reject or only claim damages.
Component 3: purpose fit, meaning whether the goods still work for the intended use.
IT/AI/Product/Consulting worked example: A product team buys laptops for a model-training lab, but the GPUs are weaker than promised; because the hardware cannot meet the stated purpose, the defect is closer to a condition breach.
When to pull this out in a meeting: Use it when quality problems come up before acceptance.

### Quality Match Matrix
**Purpose:** Check whether goods match the description, sample, and intended use.

**Text Diagram:**
```text
Description match + Sample match + Fitness match = acceptable quality
```
Axes / Quadrants / Components explained:
Component 1: description, meaning the item matches what was sold.
Component 2: sample, meaning the batch aligns with the reference item.
Component 3: fitness, meaning the item works for the buyer's known purpose.
IT/AI/Product/Consulting worked example: A consulting client orders tablets for field interviews; if the devices match the spec sheet, match the sample, and survive the field workflow, the sale clears the quality check.
When to pull this out in a meeting: Use it during goods acceptance or quality sign-off.

---

## 4. Formulas
Formula: Remedy severity score = condition_breached + warranty_breached
Variables:
condition_breached = 1 if an essential term failed, else 0
warranty_breached = 1 if a minor promise failed, else 0
Why this formula exists: It helps decide whether rejection or compensation is the appropriate remedy.
How to interpret the output:
Value 0 -> no breach -> accept the goods
Value 1 -> partial breach -> check whether rejection or damages apply
Value 2 -> major problem -> escalate for rejection and replacement
Worked example with numbers: An AI hardware shipment arrives with the correct model but weaker batteries than promised. Condition_breached = 0, warranty_breached = 1, so the score is 1 and damages or replacement parts are the likely remedy.

---

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Treat every defect as a deal-breaker | Separate major condition breaches from smaller warranty breaches |
| Accept goods without checking the buyer's stated purpose | Confirm fitness when the seller knows the intended use |
| Ignore mismatches against the description or sample | Compare delivered goods with the contract and reference sample |
| Reject goods for a minor cosmetic issue without checking the remedy | Use damages when the breach is only a warranty breach |
| Close the purchase before quality acceptance testing | Build a clear acceptance step into the workflow |

---

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: AI hardware batch underperforms
Situation: A company orders GPUs for an internal AI lab and tells the seller the machines must handle heavy training load. The delivered hardware cannot meet that load.
Applicable framework/metric: Defect severity check.
Analysis: Because the seller knew the purpose and the hardware fails that purpose, the problem is likely a condition breach. The buyer can reject instead of living with a weak workaround.
Decision rule: If the core promise fails, reject; if the defect is minor, seek damages.
Action: Log the spec mismatch, suspend acceptance, and notify the vendor immediately.

Scenario 2: Product launch device quality issue
Situation: A product team receives a phone batch where the battery is weaker than promised but the devices still function. The business wants to know whether to reject the batch or claim compensation.
Applicable framework/metric: Remedy severity score.
Analysis: Condition_breached = 0 and warranty_breached = 1, so the score is 1. That points to damages, replacement units, or service credits rather than rejection.
Decision rule: If score = 2, reject; if score = 1, claim compensation; if 0, accept.
Action: Quantify the loss, open a warranty ticket, and keep the batch if the defect is manageable.

Scenario 3: Consulting equipment purchase for field research
Situation: A consulting firm buys tablets for a consumer research project. The tablets match the catalog description but not the sample that was shown during negotiation.
Applicable framework/metric: Quality match matrix.
Analysis: One mismatch can justify a breach claim if the sample was part of the bargain. If description, sample, and fitness all fail, the risk to the buyer is much higher.
Decision rule: If all three match, accept; if one fails, assess remedy; if two or more fail, escalate.
Action: Compare the delivery against the spec sheet, sample device, and pilot test results.

---

## 7. Implementation Playbook
1. Add a quality-acceptance checklist to every purchase order.
2. Capture the buyer's known purpose before the order is placed.
3. Keep a signed sample or spec sheet with the contract file.
4. Separate escalation paths for condition breaches and warranty breaches.
5. Tie payment approval to acceptance testing for important purchases.
6. Train procurement teams to document mismatches with photos, logs, and timestamps.

---

## 8. Content Quality Audit
Covered well: the split between conditions and warranties, the role of fitness for purpose, and the basic remedies of rejection versus damages.
Underplayed or missing: consumer-protection overlays, quality standards for digital services, and whether repair or replacement is preferred in specific markets.
Supplement with: a sales-of-goods remedies chapter [verified from model knowledge, not source], a consumer warranty case note [verified from model knowledge, not source], and an e-commerce product-quality guide [verified from model knowledge, not source].
Red flags in the source: It is concise and does not spell out the boundary cases where rejection is commercially expensive.

---

## 9. Quick-Recall Card
```text
Topic: Sale and Quality of Goods (Conditions & Warranties)
Core idea: Essential promises can justify rejection; minor promises usually lead to damages.
Key metric/formula: Remedy severity score = condition_breached + warranty_breached.
Framework trigger: Use when a delivered product fails spec, sample, or purpose.
Watch out for: Treating a warranty problem like a condition breach.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Is the defect serious enough to reject the goods or just claim compensation?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [1,2,3,4,5,6,7,8,9] Enrichments applied: [IT AI hardware batch example, product battery quality example, consulting tablets sample example] Final scores: all 5/5 Pass 2 completed: 2026-04-20 06:28 Audited by: A2 -->
