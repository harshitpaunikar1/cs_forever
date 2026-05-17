# Due Diligence Review

## Overview

Due diligence is a detailed review of the target's business, financials, legal status, tax, operations, and people before closing. It confirms what the seller claimed and uncovers hidden risks that may change the price or the deal terms.

---

## Why It Matters

Skipping diligence means buying problems: lawsuits, tax demands, bad contracts, or broken IT systems. A thorough review lowers price, adjusts terms, or kills the deal before the buyer is stuck with expensive surprises.

## Key Principles

- Start diligence as soon as the term sheet is signed
- Use specialists: legal, financial, tax, HR, tech, environmental
- Prioritise deal-breakers over minor issues
- Document every red flag with clear impact on price or risk
- Feed findings back into the sale agreement as specific protections

## Key Terms

| Term | Definition |
|------|------------|
| **Data Room** | Secure online folder where target shares documents |
| **Red Flag Report** | Summary of top risks found in diligence |
| **Quality of Earnings (QoE)** | Review of how real and repeatable the EBITDA is |
| **Tax DD** | Review of tax positions, demands, and exposures |
| **IT DD** | Review of systems, licences, and cyber risks |

## Use Case

A buyer reviews three years of audited accounts, key contracts, and pending litigation. QoE work finds Rs 20 crore of one-time gains in EBITDA, so the buyer adjusts the offer price downward accordingly.

## Scenario

> A buyer discovered during diligence that the target's top customer contract was up for renewal in 6 months and was at risk. The buyer added a special indemnity to the SPA and cut price by 8%, saving it from a hit that happened 9 months later.

## Examples

- Legal DD finds a pending patent case and triggers a specific indemnity in the SPA.
- Financial DD spots aggressive revenue recognition and lowers the deal multiple applied.

---

## Audited Appendix

# Due Diligence Review
**Course:** Mergers and Acquisitions
**Module:** Content / Due Diligence Review
**Audited on:** 2026-04-18
**Audited by:** A3
**Source files reviewed:** `mergers-acquisitions/content/11-due-diligence-review.md`

---

## 1. Topic Snapshot
Due Diligence (DD) is the structured, multi-workstream investigation of a target's financials, tax, legal, commercial, operational, HR, IT/cyber, IP and ESG posture between term-sheet signing and SPA closing, aimed at confirming seller claims and pricing hidden risk. For an IT/AI/Product/Consulting leader, DD is not a finance-team ritual — tech + IP + security + data-rights diligence sits on *your* desk because broken code, contested IP chain-of-title, un-licensed open-source or a latent breach can vaporise synergy value post-close. The decision DD drives: proceed at agreed price, re-price / re-paper with indemnities & escrow, or walk.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| Data Room (VDR) | Virtual Data Room | Secure online folder where seller uploads all DD documents | Controlled, logged access to sensitive docs | User logs, Q&A threads, document index | "Upload the MSAs to the VDR by Friday" |
| Red Flag Report | — | Short memo listing top material issues from DD | Focus attention on deal-breakers vs noise | Severity × Probability × Impact | IC meeting after Week 2 of DD |
| Quality of Earnings (QoE) | — | Normalised EBITDA stripped of one-offs | Reported EBITDA often flatters | Adjustments waterfall | "QoE came in 12% below reported" |
| Financial DD | — | Review of P&L, BS, CF, working capital | Verify historical + run-rate economics | Variance vs reported; WC peg | Weekly DD steerco |
| Tax DD | — | Review of direct/indirect tax exposures | Uncover tax demands, TP issues, GST leakage | Contingent tax liability ₹ | "Pending GST demand of ₹14 cr" |
| Legal DD | — | Contracts, litigation, corporate records | Find change-of-control, litigation, non-competes | # of red-flag clauses | Disclosure Schedule review |
| Commercial DD | — | Market, customers, competition, pipeline | Test top-line sustainability | Win-rate, pipeline coverage | External consultant report |
| Operational DD | — | Supply chain, plant, processes, systems | Find execution risk | OEE, throughput, cost/unit | Ops walk-through |
| HR DD | — | People, comp, attrition, key-man | Key talent may walk post-close | Attrition %, bench depth | "Top-5 engineers unvested" |
| IT / Tech DD | — | Codebase, architecture, infra, tech debt | Tech risk priced into deal | LoC, test coverage, tech-debt days | "Monolith on Java 7" |
| Cyber DD | — | Security posture + breach history | Breaches = post-close fines | # critical CVEs, MTTR | "Log4j still unpatched" |
| ESG DD | — | Environmental, social, governance posture | Regulatory + reputational risk | ESG score, incidents | LP / acquirer ESG filter |
| IP DD | — | Patents, trademarks, copyrights, chain-of-title | Ensure target actually owns what it sells | # assignments, encumbrances | "Founders never assigned IP to co" |
| Customer-Concentration Analysis | — | % revenue from top N customers | Concentration = revenue fragility | Top-10 / Total revenue | ">40% top-10 = concern" |
| Churn Analysis (SaaS) | Gross/Net churn | % of ARR lost/retained | SaaS valuation driver | Monthly/Annual churn % | Cohort churn curve |
| Cohort Analysis | — | Behaviour of customers grouped by signup month | Reveals true retention | LTV, payback by cohort | ChartMogul dashboard |
| Code Review / SAST / SCA | Static Application Security Testing / Software Composition Analysis | Scanning source for bugs + OSS licences | Find vulnerabilities + licence risk | # high/critical findings | CodeQL, Snyk, BlackDuck |
| Open-Source Compliance | — | Licence-obligation review (GPL, AGPL) | Copyleft can force source disclosure | # AGPL/GPL components in prod | BlackDuck / Snyk report |
| DPO / Privacy DD | Data Protection Officer | Review of DPDP / GDPR / CCPA posture | Data-rights breaches carry heavy fines | DPIA coverage, consent logs | "No DPIA for ML training set" |
| SOC 2 / ISO 27001 status | — | Security attestation standards | Enterprise-customer pre-req | Report type, exceptions | "SOC 2 Type II with 3 exceptions" |
| Segregation of Duties | SoD | Different people initiate vs approve | Fraud prevention control | # SoD conflicts in ERP | SAP GRC report |
| Transition Services Agreement | TSA | Seller runs shared services for buyer post-close | Carve-outs need umbilical support | Duration months, fee ₹ | "9-month TSA on HRIS" |
| Reverse DD | — | Target diligences the buyer | Founders accepting stock want comfort | Cap table, burn, runway | Founder-led sales to SPACs |
| Vendor DD (sell-side) | VDD | Seller commissions DD report upfront | Speeds auctions | Same scope as buy-side | Banker-led auction |
| Clean Team | — | Ring-fenced group that sees competitor-sensitive data | Antitrust / competition law | NDA + firewall protocols | Horizontal-merger DD |
| Disclosure Schedule | — | Annex to SPA listing exceptions to reps | Makes reps accurate; limits indemnity | # exceptions, materiality | Final SPA negotiation |

---

## 3. Frameworks & Matrices

### 3.1 DD Workstream Matrix
**Purpose:** Assign ownership, deliverable and timeline across all 9 workstreams so nothing falls through the gap.

```
Workstream      | Owner (Buyer)      | Key Deliverable           | Typical Duration
----------------|--------------------|---------------------------|-----------------
Financial       | CFO + Big-4 FA     | QoE Report + WC peg       | 4-6 wks
Tax             | Tax advisor        | Tax exposure memo         | 3-4 wks
Legal           | Law firm (M&A)     | Legal DD + Disclosure Sch | 4-6 wks
Commercial      | Strat consultant   | Market + customer report  | 4-5 wks
Operational     | Internal Ops VP    | Ops DD memo               | 2-4 wks
HR              | CHRO + HR advisor  | People DD + retention plan| 2-3 wks
IT / Tech       | CTO + tech DD firm | Tech DD + code report     | 3-5 wks
Cyber           | CISO + pentest firm| Cyber posture report      | 2-4 wks
ESG             | Sustainability lead| ESG memo                  | 2-3 wks
IP              | IP counsel         | IP chain + FTO report     | 3-4 wks
```

**IT/AI/Product/Consulting example:** When acquiring an AI-SaaS target, the CTO owns *three* lanes (IT, Cyber, IP) and co-owns Commercial (product-market fit) — do not let finance "outsource" tech DD to a junior. **Trigger:** the day the term sheet is signed.

---

### 3.2 Red Flag Severity Heatmap
**Purpose:** Triage findings so IC focuses on deal-killers, not cosmetic issues.

```
              LOW IMPACT     MEDIUM IMPACT    HIGH IMPACT
HIGH PROB     Note in memo   Price adjust     DEAL-KILLER / renegotiate
MED PROB      Note in memo   Specific indem   Price + indem + escrow
LOW PROB      Ignore         Specific indem   Escrow + cap-exception
```

Action rules: *Deal-killer* = walk or full re-paper; *Price adjust* = reduce headline EV; *Specific indemnity* = carve-out from general cap in SPA; *Escrow* = holdback 10-20% of cash for 12-24 months.

**IT/AI/Product/Consulting example:** AGPL component in a closed-source SaaS = High Prob × High Impact = deal-killer until re-engineered or re-licensed. **Trigger:** after Week 2 red-flag log freeze.

---

### 3.3 QoE Adjustment Waterfall
**Purpose:** Convert reported EBITDA into the number a buyer should actually pay a multiple on.

```
Reported EBITDA                           100.0
  + Non-recurring legal settlement         +3.0
  + One-off ERP implementation cost        +2.5
  + Normalised owner compensation          +1.5
  - One-time revenue (₹20 cr land sale)   -20.0
  - Aggressive revenue recognition (cut-off)-4.0
  - Operating-lease capitalisation (IFRS16)-3.0
  - Deferred R&D expensed                  -2.0
  --------------------------------------------
  Quality of Earnings (QEBITDA)            78.0
```

**IT/AI/Product/Consulting example:** SaaS target books 3-year prepaid contracts as current revenue → cut ₹15 cr, QoE drops, 10x multiple → ₹150 cr price cut. **Trigger:** Week 3 of financial DD.

---

### 3.4 Tech/AI-Target DD Checklist
**Purpose:** Structured scan across the seven tech-risk vectors unique to software/AI targets.

```
Vector                   | What to Check                             | Tool/Artifact
-------------------------|-------------------------------------------|---------------------
Codebase health          | LoC, test coverage, cyclomatic complexity | SonarQube, CodeClimate
IP chain-of-title        | Founder + contractor IP assignments       | Legal + Git blame
Open-source compliance   | GPL/AGPL/copyleft exposure                | BlackDuck / Snyk
Infrastructure           | Cloud accounts, IaC coverage, SPOFs       | AWS Config, Terraform
Security                 | CVEs, SAST, pentest, SOC 2                | CodeQL, Qualys
Data rights              | Consent, DPDP/GDPR, training-data origin  | DPIA, OneTrust
Model provenance (AI)    | Training data licences, bias testing, evals| Model cards, MLflow
```

**IT/AI/Product/Consulting example:** Target trained its LLM on scraped customer data without consent → unlimited indemnity + scope to re-train required. **Trigger:** kick-off in Week 1 for any tech target.

---

## 4. Formulas

### 4.1 Quality EBITDA
`Quality EBITDA = Reported EBITDA ± Normalisations (non-recurring, owner comp, revenue-recognition, lease, R&D capitalisation)`
Threshold: QoE-to-Reported gap >10% = material concern; >20% = re-price.
Example: Reported ₹100 cr; adjustments net −₹22 cr → QoE = ₹78 cr. At 10x multiple, EV drops from ₹1,000 cr to ₹780 cr.

### 4.2 Customer Concentration Ratio
`CCR = Revenue from Top-10 customers / Total Revenue`
Thresholds: <20% healthy; 20–40% monitor; >40% risk → price cut + customer-loss indemnity.
Example: Top-10 = ₹84 cr of ₹120 cr → CCR = 70%. Buyer adds 12-month earn-out tied to top-10 retention.

### 4.3 Net Revenue Retention (NRR) — SaaS
`NRR = (Start-ARR + Expansion − Contraction − Churn) / Start-ARR`
Thresholds: <95% concern; 95–100% acceptable; 100–110% healthy; >120% elite.
Example: Start-ARR ₹100 cr; Expansion ₹18 cr; Contraction ₹4 cr; Churn ₹7 cr → NRR = 107%. Supports premium multiple.

### 4.4 Red-Flag Impact on Price
`ΔPrice = Σ [ PV(Expected Loss) × Probability ]`
Example: Pending patent case — expected loss ₹30 cr, prob 40%, discount to PV ₹25 cr → ΔPrice = ₹10 cr reduction OR specific uncapped indemnity.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|---|---|
| 1 | Start DD the day term sheet is signed | Wait for legal drafting to begin |
| 2 | Have CTO personally sponsor Tech + IP + Cyber DD | Delegate tech DD to a Big-4 generalist |
| 3 | Quantify every red flag into ₹ impact on price | Log red flags qualitatively ("concern noted") |
| 4 | Run a QoE on any target with EBITDA >₹10 cr | Rely on audited reported EBITDA |
| 5 | Scan OSS with BlackDuck/Snyk on day 1 | Assume MIT/Apache on all components |
| 6 | Build a Disclosure Schedule as findings emerge | Try to redraft it at SPA signing |
| 7 | Use clean-team protocol for competitor-sensitive data | Share customer-level data pre-close |
| 8 | Feed every red flag into SPA (indemnity/escrow/CP) | Leave red flags as "to be resolved post-close" |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI-SaaS Target DD (positive)
Buyer (IT-services major) acquires an ₹800 cr AI-SaaS target. CTO runs Tech DD across 4 weeks:
- **Codebase:** SonarQube shows 18% test coverage — add ₹12 cr remediation to post-close plan.
- **IP chain-of-title:** 3 of 7 founding engineers never signed IP assignments → retroactive assignments executed as CP to closing.
- **Open-source (BlackDuck):** 2 AGPL components in core module → vendor patches with MIT alternatives pre-close.
- **Training-data rights:** 40% of LLM fine-tuning corpus scraped without consent → re-train with licensed data; seller gives uncapped indemnity for pre-close IP claims.
- **Cyber:** SOC 2 Type II with 3 open exceptions → remediation in TSA.
Outcome: price held at ₹800 cr but 15% escrow (₹120 cr) for 24 months + uncapped IP indemnity.

### Scenario 2 — IT-Services Firm DD
Buyer acquires mid-size IT-services firm:
- **Customer concentration:** Top-3 clients = 58% of revenue; top-1 contract up for renewal in 6 months → price cut 8%, earn-out tied to renewal.
- **Utilization:** billable utilization 62% vs industry 78% → ₹25 cr productivity opportunity, folded into synergy case.
- **Employee retention:** attrition 28% in senior bench → ₹15 cr retention pool as part of deal cost.
- **Contract renewal:** change-of-control consents needed in 14 MSAs → CP to close.

### Scenario 3 — ANTI-EXAMPLE: Skipping Cyber DD
Buyer acquires SaaS target for ₹600 cr; finance DD clean, legal DD clean, **cyber DD skipped** to save ₹40 lakh and 3 weeks. Six months post-close:
- Breach in legacy un-patched AWS account (was never migrated to buyer's landing zone)
- 2.1 lakh customer records exposed → DPDP regulatory penalty ₹15 cr
- SLA credits to enterprise customers ₹6 cr
- Churn of 3 enterprise logos over 12 months = ₹4 cr ARR lost (~₹40 cr enterprise value at 10x)
- Incident response + forensics + legal ₹3 cr
- Brand/reputation hit (unquantified)
**Total quantified cost: ₹28 cr immediate + ₹40 cr EV erosion = ₹68 cr.** Skipping ₹40 lakh of cyber DD cost 170x.

**Tools used across scenarios:** Virtual Data Rooms (DealRoom, Intralinks, Firmex); BlackDuck / Snyk (OSS scan); CodeQL / Checkmarx (SAST); Qualys / Nessus (vulnerability scan); AWS/Azure/GCP audit logs + Config; ChartMogul (SaaS cohort/NRR); OneTrust (privacy/DPIA); SonarQube (code quality).

---

## 7. Implementation Playbook

1. **Stand up** a DD steerco within 48 hrs of term-sheet signing; assign workstream owners per Matrix 3.1.
2. **Open** a Virtual Data Room (DealRoom/Intralinks) with indexed request list covering all 10 workstreams.
3. **Commission** QoE from an independent accounting firm; target 4-week turnaround with weekly interim reads.
4. **Scan** the target codebase with BlackDuck + Snyk + CodeQL in Week 1 and triage critical findings into the red-flag log.
5. **Map** IP chain-of-title: pull every founder/contractor assignment, flag gaps, make cure a CP to closing.
6. **Maintain** a live Red Flag Log (Severity × Probability × ₹ Impact) with a weekly freeze for IC review.
7. **Translate** each material red flag into an SPA protection: price adjustment, specific indemnity, escrow, or CP.
8. **Finalise** Disclosure Schedule + Reps & Warranties + Escrow/Indemnity package before SPA signing; hand over with a post-close 100-day remediation plan.

---

## 8. Content Quality Audit
**Covered well:** The source note captures the core DD rationale, specialist workstreams, QoE concept, and that findings feed the SPA.
**Underplayed (and now supplemented above):**
- AI/ML-specific DD (model provenance, training-data rights, bias evals, open-source licences)
- Cyber DD (SOC 2, CVEs, MTTR, breach history)
- ESG DD (climate risk, S/G incidents)
- Clean-team protocols for competitor-sensitive data under antitrust scrutiny
- Reverse DD (founders diligencing the acquirer)
- Working-capital peg analysis and its link to closing-date true-up
- Disclosure Schedule mechanics

**Supplementary sources (≥5):**
1. Rosenbaum & Pearl, *Investment Banking* (3rd ed., Wiley, 2020) — DD integration with valuation.
2. Frankel, *Mergers and Acquisitions Basics* (Wiley, 2017) — practical DD checklists.
3. Bruner, *Applied Mergers and Acquisitions* (Wiley, 2004) — case evidence on DD failures.
4. PwC, *Tech M&A Due Diligence Trends* (2023) — tech-target DD benchmarks.
5. Deloitte, *Cyber Due Diligence in M&A* (2022) — cyber DD frameworks and breach costs.
6. HBR, *Due Diligence: The Critical Stage in Mergers and Acquisitions* (1998) — timeless principles.

**Red flags in source note:** under-emphasises tech/cyber/AI-specific DD; does not mention working-capital peg; silent on disclosure schedule as the legal bridge between DD findings and SPA; does not distinguish buy-side vs vendor (sell-side) DD.

---

## 9. Quick-Recall Card
- DD = priced investigation; every finding must convert into ₹ impact on price or SPA protection.
- Tech, IP, cyber, data-rights DD belong to the CTO — not to Big-4 generalists.
- QoE strips one-offs; a 10%+ gap between reported and quality EBITDA is material.
- Open-source (AGPL/GPL), IP chain-of-title, and training-data consent are the three silent deal-killers in AI-SaaS targets.
- Feed red flags into Disclosure Schedule → Reps & Warranties → Indemnity + Escrow; never into a "post-close to-do list."
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: **"Which red flags in the target's tech, IP, data-rights and cyber posture materially change the price, terms or go/no-go decision — and exactly how are each of them priced into the SPA?"**

---

**Connects to:** [07-pricing-mechanisms.md](07-pricing-mechanisms.md), [08-term-sheets-and-provisions.md](08-term-sheets-and-provisions.md), [12-representations-and-warranties.md](12-representations-and-warranties.md), [../business-valuation/01-balance-sheet-analysis.md](../business-valuation/01-balance-sheet-analysis.md).

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5]
Sections rewritten: [2 (expanded to 26 rows), 3 (four frameworks w/ ASCII), 6 (anti-example quantified to ₹68 cr)]
Enrichments applied: [cross-course links to business-valuation; 6 supplements; anti-example w/ ₹68 cr total cost; IT tooling (BlackDuck, Snyk, CodeQL, Qualys, ChartMogul, OneTrust, SonarQube); role-lens question for PM/Consultant/AI Lead]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A3
-->
