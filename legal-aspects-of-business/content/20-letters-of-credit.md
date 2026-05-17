# 20. Letters of Credit

## Overview

A letter of credit (LC) is a bank’s promise to pay the seller if required documents are provided (common in international trade).

---

## Why It Matters

It reduces risk when buyer and seller don’t fully trust each other.


## Key Principles

- Bank pays based on documents, not actual goods quality
- Strict compliance with document terms
- Involves issuing bank, beneficiary (seller), applicant (buyer)


## Key Terms

| Term | Definition |
|------|------------|
| **LC** | Bank payment guarantee against documents |
| **Beneficiary** | Seller receiving payment |
| **Applicant** | Buyer requesting LC |


## Use Case

Import/export payments.


## Scenario

> An Indian importer opens LC. Exporter ships goods and submits documents; bank pays exporter.


## Examples

- Import of machinery using LC.
- Export of textiles with confirmed LC.

---

## Audited Appendix

# Letters of Credit
**Course:** Legal Aspects of Business  
**Module:** Documentary Trade Finance  
**Audited on:** 2026-04-20  
**Audited by:** A2  
**Source files reviewed:** `legal-aspects-of-business/content/20-letters-of-credit.md`

---

## 1. Topic Snapshot
This topic explains how a letter of credit makes a bank pay a seller if the required documents are presented.
For IT, AI, Product, and Consulting leaders, it reduces trust risk in cross-border hardware, software, or services deals.
The practical question is whether the documents match the LC terms.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| LC | Letter of Credit | Bank promise to pay against documents | It reduces counterparty risk | By checking document compliance | Trade finance and procurement |
| Beneficiary | N/A | Seller who receives payment | It identifies the payee under the LC | By naming the receiving party in the LC | Export, vendor payment, and treasury teams |
| Applicant | N/A | Buyer asking the bank to issue the LC | It identifies who needs the guarantee | By matching the buyer to the bank application | Import and purchase-order workflows |
| Issuing bank | N/A | Bank that issues and pays under the LC | It is the payment backbone | By checking which bank controls the LC | Banking, treasury, and trade operations |
| Strict compliance | N/A | Documents must match the LC terms exactly | It keeps payment rule-based rather than subjective | By comparing each document to the required list | LC review, discrepancy resolution, and shipping docs |

## 3. Frameworks & Matrices

### Document-Compliance Funnel
**Purpose:** Decide whether the seller gets paid under the LC.

**Text Diagram:**
```text
Present documents
      |
      v
Match LC terms exactly?
   | yes -> issuing bank pays beneficiary
   | no
   v
Resolve discrepancy or amend LC before expiry
```

Axes / Quadrants / Components explained:
Component 1: Required documents, meaning the exact papers the bank asks for.
Component 2: Presented documents, meaning what the beneficiary actually submits.
Component 3: Compliance check, meaning whether each document matches the terms.
Component 4: Payment decision, meaning whether the bank pays or flags a discrepancy.
IT/AI/Product/Consulting worked example: A product company imports GPUs for an AI cluster. The LC requires invoice, bill of lading, packing list, and insurance certificate; if all four match, the bank pays even before the goods are inspected.
When to pull this out in a meeting: Use it when payment depends on shipping or completion documents rather than on trust.

## 4. Formulas

Formula: LC payout = documents comply with LC terms
Variables:
Documents = the invoice, shipping papers, certificates, and any other LC-mandated record.
Compliance = exact match to the wording, dates, and signatures required by the LC.
Why this formula exists: It answers when the bank must pay.
How to interpret the output:
Documents comply = yes -> bank pays beneficiary
Documents comply = no -> payment is delayed until the discrepancy is fixed or waived
Documents are incomplete -> no payout -> gather missing papers before expiry
Worked example with numbers: A consulting firm submits 4 required documents and all 4 match the LC. The compliance score is 4/4, so the issuing bank pays the beneficiary.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Assume the bank checks product quality | Verify only the required documents are in order |
| Submit papers with missing names or dates | Match every field to the LC wording |
| Wait until the last day to review documents | Pre-check the packet before shipment closes |
| Ignore the role of the applicant and beneficiary | Map who requests the LC and who receives payment |
| Treat a discrepancy as harmless | Fix it or amend the LC before expiry |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: AI hardware import
Situation: An AI startup imports servers from a vendor overseas. The LC requires 4 documents and the shipping agent submits 3 correctly, with one insurance certificate missing.
Applicable framework/metric: Document-Compliance Funnel.
Analysis: Compliance is 3/4, so the bank should not pay until the missing certificate is corrected or the LC is amended.
Decision rule: If all documents match, pay. If any required document is missing or inconsistent, hold payment. If the LC is near expiry, amend immediately.
Action: Build a pre-shipment checklist and a discrepancy owner for each required document.

Scenario 2: Product company milestone purchase
Situation: A product company buys offshore test equipment and ties payment to LC presentation. The invoice and bill of lading match, but the invoice date is one day outside the LC window.
Applicable framework/metric: Document-Compliance Funnel.
Analysis: The mismatch creates a discrepancy even though the goods may be fine.
Decision rule: If date, amount, or naming fields mismatch, the packet is non-compliant. If everything matches, bank payment should proceed. If the error is small, amend rather than argue after the fact.
Action: Freeze the template and check dates before the shipment leaves port.

Scenario 3: Consulting delivery against documentary proof
Situation: A consulting firm bills a foreign client through an LC after delivering a transformation report and sign-off certificate. The LC requires a signed completion certificate plus invoice.
Applicable framework/metric: Document-Compliance Funnel.
Analysis: If both documents are present and correctly signed, the bank pays without judging the quality of the consulting work.
Decision rule: If documents are complete, collect payment. If the certificate is missing, do not ship the packet. If the client wants different wording, amend the LC first.
Action: Align the project closure template with the LC wording before the final submission.

## 7. Implementation Playbook
1. List every required LC document and assign an owner for each one.
2. Compare the LC wording against the invoice, shipping, and certificate templates.
3. Run a pre-submission compliance check 48 hours before dispatch.
4. Build a discrepancy log with the exact mismatch and the fix.
5. Train finance, procurement, and operations teams on expiry dates and amendment timing.
6. Keep beneficiary and applicant details identical across all documents.

## 8. Content Quality Audit
Covered well: The source clearly states that the LC is document-based and depends on strict compliance among the applicant, beneficiary, and issuing bank.
Underplayed or missing: It does not discuss discrepancies, amendments, confirmed LCs, or how to operationalize the review process.
Supplement with: [verified from model knowledge, not source] ICC UCP 600, a trade-finance textbook on documentary credits, and a case note on strict compliance in letter-of-credit disputes.
Red flags in the source: The quality-of-goods issue is not addressed, so teams should not confuse documentary payment with product acceptance.

## 9. Quick-Recall Card
```text
Topic: Letters of Credit
Core idea: The bank pays on documents, not on trust.
Key metric/formula: LC payout = documents comply with LC terms.
Framework trigger: Use when cross-border payment depends on shipping or completion papers.
Watch out for: Treating a document mismatch as a minor issue.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Do our documents match the LC exactly?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [] Enrichments applied: [IT/AI/Product/Consulting trade examples, document-compliance funnel, discrepancy controls] Final scores: all 5/5 Pass 2 completed: 2026-04-20 06:42 Audited by: A2 -->
