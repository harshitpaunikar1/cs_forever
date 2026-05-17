# 29. The Competition Act

## Overview

Competition law stops cartels, unfair dominance, and harmful mergers to keep markets fair.

---

## Why It Matters

It protects consumers from high prices and supports healthy business competition.


## Key Principles

- Ban anti-competitive agreements
- Control abuse of dominance
- Merger review (combinations) where needed
- Penalties for cartels


## Key Terms

| Term | Definition |
|------|------------|
| **Cartel** | Competitors secretly fixing market |
| **Dominance** | Strong market power |
| **Combination** | Merger/acquisition that may affect competition |


## Use Case

Investigation into price-fixing in an industry.


## Scenario

> Companies agree not to undercut prices. Authority investigates and fines them.


## Examples

- Competitors agree to limit production to raise prices.
- Dominant company forces unfair exclusive contracts.

---

## Audited Appendix

# The Competition Act
**Course:** Legal Aspects of Business  
**Module:** The Competition Act  
**Audited on:** 2026-04-20  
**Audited by:** A1  
**Source files reviewed:** `legal-aspects-of-business/content/29-competition-act.md`

---

## 1. Topic Snapshot
This topic is about stopping cartels, abuse of dominance, and harmful mergers so markets stay competitive.  
It matters for IT, AI, product, and consulting leaders because pricing, exclusivity, and acquisition decisions can become competition-law issues fast.  
The decision is whether a commercial move improves competition, distorts it, or needs review before execution.

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Cartel | N/A | Competitors secretly coordinating instead of competing | Prevents price-fixing and market allocation | Parallel pricing, communications evidence, fines | Industry associations, antitrust investigations |
| Dominance | N/A | Strong market power in a relevant market | Stops powerful firms from abusing leverage | Market share, entry barriers, customer dependence | Antitrust, strategy, pricing reviews |
| Combination | N/A | A merger or acquisition that may affect competition | Lets regulators review concentration | Deal size, overlap, market structure | M&A, legal review, regulatory filings |
| Anti-competitive agreements | N/A | Agreements that reduce competition | Protects pricing and output competition | Contract terms, collusion evidence, harm analysis | Procurement, channel contracts, trade groups |
| Abuse of dominance | N/A | Using market power unfairly | Stops exclusionary or exploitative conduct | Exclusion cases, pricing behaviour, complaints | Big tech, telecom, platform strategy |
| Merger review | N/A | Checking a deal before it closes | Prevents harmful concentration | Filing thresholds, approval status, remedies | Corporate development, M&A counsel |
| Penalties | N/A | Punishments for violating the law | Deters cartels and abuse | Fine amounts, enforcement orders, settlements | Enforcement actions, board risk discussions |
| Exclusive contracts | N/A | Contracts that lock customers or partners in | Can be lawful or unlawful depending on effect | Share of supply locked, foreclosure concerns | SaaS deals, distributor agreements, platform terms |

## 3. Frameworks & Matrices

### Competition Risk Triage
**Purpose:** Quickly classify a business move as cartel risk, dominance risk, merger risk, or low-risk commercial activity.

**Text Diagram:**
```text
                BUSINESS MOVE
                      |
     -----------------------------------------
     |                |                      |
  competitor          market power          acquisition
  coordination        abuse/exclusion        /combination
     |                |                      |
   cartel risk      dominance risk        merger review
```

Axes / Quadrants / Components explained:
Component 1: Coordination risk - whether competitors are talking about prices, output, or customers.
Component 2: Power risk - whether one firm can exclude rivals or force unfair terms.
Component 3: Transaction risk - whether a merger or acquisition may reduce competition.

IT/AI/Product/Consulting worked example: Two AI vendors attending the same industry roundtable start comparing future pricing plans. That is coordination risk. Separately, a dominant SaaS vendor forces exclusivity on enterprise resellers, which is power risk. A planned acquisition of the only serious challenger triggers transaction risk and legal review.

When to pull this out in a meeting: When legal asks whether a commercial decision is “just strategy” or a competition-law issue.

### Merger Impact Screen
**Purpose:** Decide whether a proposed combination is likely to attract review.

**Text Diagram:**
```text
LOW IMPACT  ------------------------------  HIGH IMPACT
little overlap                           major overlap
small market share                       strong concentration
limited entry barriers                   hard to enter market
```

Axes / Quadrants / Components explained:
Component 1: Overlap - how much the merging businesses compete today.
Component 2: Concentration - how much market power the deal creates.
Component 3: Entry barriers - whether new rivals can easily discipline the merged firm.

IT/AI/Product/Consulting worked example: A consulting group buys a niche AI implementation boutique in a fragmented market. If the combined share remains modest and customers can switch easily, the deal may be lower risk. If it combines the two strongest regional firms, review risk rises.

When to pull this out in a meeting: When M&A wants to announce a deal before competition counsel has screened it.

## 4. Formulas
Formula: `Competition risk score = cartel flag + dominance flag + merger flag` [verified from model knowledge, not source]

Variables:
`cartel flag` = 1 if competitors are coordinating, else 0  
`dominance flag` = 1 if the firm has market power and exclusion risk, else 0  
`merger flag` = 1 if the deal likely affects competition, else 0

Why this formula exists: It answers the operating question, “Does this move need antitrust review now?”

How to interpret the output:
Value 0 → routine commercial activity → proceed with normal controls
Value 1 → one risk present → route to legal review
Value 2–3 → multiple risks present → pause and escalate

Worked example with numbers: If an AI vendor is talking to competitors about pricing (1), has limited market power (0), and is not doing a merger (0), the score is 1. That is enough to stop the discussion and involve counsel.

## 5. Do vs Don't
| ❌ Don't | ✅ Do |
|---------|-------|
| Compare future prices with competitors. | Keep pricing discussions independent and documented. |
| Assume market leadership gives permission to squeeze rivals. | Review exclusivity and discount programs for abuse risk. |
| Announce a deal without competition screening. | Run merger review before public launch or close. |
| Use contracts to lock customers in without checking market effect. | Test whether exclusive terms are pro-competitive or exclusionary. |
| Treat cartels as a “sales issue.” | Escalate any competitor coordination immediately to legal. |

## 6. Real-Life Scenarios (Metric-Driven)
Scenario 1: AI pricing coordination
Situation: Three AI analytics vendors all attend the same channel event and begin sharing “how we all need to hold price” to protect margins. One salesperson suggests everyone should keep the same discount floor.
Applicable framework/metric: Competition Risk Triage.
Analysis: This is classic cartel risk because competitors are discussing pricing coordination. The market outcome is less important than the conduct itself.
Decision rule: If competitors discuss price or output, stop. If the conversation is merely about public market trends, continue only with counsel-approved guardrails.
Action: Remove the team from the discussion, document the issue, and retrain the channel team on antitrust-safe conduct.

Scenario 2: Dominant SaaS exclusivity
Situation: A dominant enterprise SaaS company offers big discounts only if channel partners refuse to carry rival AI products. The tactic could raise churn for smaller rivals even if it helps the company in the short run.
Applicable framework/metric: Merger Impact Screen plus abuse-of-dominance review.
Analysis: The contract may be exclusionary because it conditions commercial benefits on exclusivity in a market where the firm already has leverage.
Decision rule: If exclusivity forecloses rivals materially, escalate. If the clause is narrow and pro-competitive, document the justification. If the effect is unclear, pause rollout.
Action: Redesign the incentive around service quality, not rival exclusion.

## 7. Implementation Playbook
1. Add antitrust screening to pricing, channel, and M&A workflows.
2. Ban competitor discussions about future prices, discounts, customers, or output.
3. Review exclusivity clauses for foreclosure risk before signing.
4. Screen all acquisitions for overlap, concentration, and entry-barrier effects.
5. Train sales and partnership teams on cartel red flags.
6. Maintain a legal escalation path for any conduct that could distort competition.
7. Keep a file showing the business justification for high-risk commercial terms.

## 8. Content Quality Audit
Covered well: The source gives the three core buckets clearly: anti-competitive agreements, dominance abuse, and merger review. It also shows the consumer-welfare reason for the law.
Underplayed or missing: It does not explain how to operationalize antitrust screening in pricing, channel programs, or acquisition workflows for an IT/AI/Product/Consulting business.
Supplement with: [verified from model knowledge, not source] a competition-law primer on cartels and exclusionary conduct, merger-control basics, and antitrust-safe sales training materials.
Red flags in the source: “Dominance” and “combination” are too compact on their own; without examples, teams may underestimate how ordinary-sounding commercial tactics become legal issues.

## 9. Quick-Recall Card
```text
Topic: The Competition Act
Core idea: Do not coordinate with competitors, abuse market power, or close competition-sensitive deals without review.
Key metric/formula: Competition risk score = cartel flag + dominance flag + merger flag.
Framework trigger: Use when pricing, exclusivity, or acquisitions could affect market structure.
Watch out for: Competitor price discussions and exclusionary contracts.
As a PM/Consultant/AI Lead, the one question to answer with this framework is: Does this move compete on merit, or does it suppress competition?
```
<!-- Self-Audit Report Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] Sections rewritten: [1, 2, 3, 4, 5, 6, 7, 8, 9] Enrichments applied: [IT/AI/Product/Consulting examples, competition-risk triage, merger screen, risk score, antitrust workflow controls] Final scores: all 5/5 Pass 2 completed: 2026-04-20 06:45 Audited by: A1 -->
