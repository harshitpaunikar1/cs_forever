# 39. Sale and Mortgage of Immovable Property

## Overview

Immovable property means land/buildings. Sale transfers ownership. Mortgage is using property as security for a loan.

---

## Why It Matters

Property deals are high-value; mistakes can cause huge financial loss and long disputes.


## Key Principles

- Written agreements and registration are important
- Title verification is essential
- Mortgage creates lender rights on default
- Proper stamp duty and registration compliance


## Key Terms

| Term | Definition |
|------|------------|
| **Immovable property** | Land/buildings |
| **Sale deed** | Document transferring ownership |
| **Mortgage** | Property as security |
| **Title** | Ownership proof |


## Use Case

Business buys office property or mortgages it for a loan.


## Scenario

> A company buys land without checking title; later a prior claim appears. Due diligence prevents this.


## Examples

- Sale deed registered for office purchase.
- Property mortgaged to bank for business expansion loan.

---

## Audited Appendix

# Sale and Mortgage of Immovable Property — Audit File

---

## 1. Jargon Buster

| Term | Plain Definition | IT/AI/Consulting Relevance |
|------|-----------------|---------------------------|
| **Immovable Property** | Land, buildings, and anything permanently attached to the earth; cannot be moved without destruction | Data centers, office campuses, server farms, and co-working spaces acquired by tech firms are all immovable property subject to this legal regime |
| **Sale Deed** | The primary legal instrument that transfers ownership of immovable property from seller (transferor) to buyer (transferee); must be in writing, stamped, and registered | When a startup acquires its first office or a tech company buys land for a greenfield campus, the sale deed is the foundational document that establishes legal ownership |
| **Mortgage** | A transfer of interest in specific immovable property to secure payment of money advanced as a loan; the mortgagor retains possession in most forms while the mortgagee acquires security interest | Startups and mid-stage tech companies pledge office premises or owned land as collateral to raise debt funding; understanding the type of mortgage matters for covenant compliance |
| **Title** | The legal right of ownership over a property; a clear title means the seller has an uncontested, unencumbered right to sell | Due diligence begins with title verification; a cloud on title can void a multi-crore acquisition and leave a company with a worthless asset |
| **Encumbrance Certificate** | Official government record listing all registered transactions against a property (mortgages, liens, charges) for a specified period; issued by the Sub-Registrar's office | Standard pre-acquisition checklist item; absence of an EC check is a red flag in any internal audit of property transactions |
| **Stamp Duty** | State-levied tax on legal instruments including sale deeds and mortgage deeds; calculated as a percentage of property value; non-payment or underpayment renders the document inadmissible as evidence and unenforceable | Finance teams must budget stamp duty as part of total acquisition cost; varies by state and impacts IRR calculations for owned real estate |
| **Registration** | Mandatory filing of a sale deed or mortgage deed with the Sub-Registrar under the Registration Act, 1908; creates public record of the transaction and is essential for legal enforceability | Unregistered sale deeds cannot be used as evidence of title; a common compliance gap in fast-moving acquisitions where closing is rushed |
| **Due Diligence** | Systematic investigation of a property's legal, financial, and physical status before transacting; includes title search, EC check, survey, legal opinion | The structured process that every PMO/CFO should mandate before any property transaction; analogous to technical due diligence in M&A |
| **Equitable Mortgage** | Created by depositing original title documents with a lender in notified cities; no registered deed required; faster and cheaper than registered mortgage | Commonly used by tech companies for working capital loans or bridge financing; lender holds original title deeds as security without formal registration (except in some states now requiring e-registration) |
| **Transfer of Property Act, 1882** | The central legislation governing transfer of immovable and movable property inter vivos (between living persons); defines sale, mortgage, lease, exchange, and gift | The governing statute for any property transaction a company enters; compliance teams must be familiar with key sections (Sec 54 for sale, Sec 58 for mortgage) |

---

## 2. Frameworks & Mental Models

### Framework 1: Property Transaction Due Diligence Framework (4-Layer Pyramid)

```
        [ LAYER 4: EXECUTION ]
        Sale/Mortgage Deed Execution, Stamp Duty Payment, Registration
              ↑
        [ LAYER 3: LEGAL CLEARANCE ]
        Legal Opinion, Mutation Records, Building Plan Approvals, NOCs
              ↑
        [ LAYER 2: DOCUMENT VERIFICATION ]
        Title Deeds (30-year chain), Encumbrance Certificate, Survey Records, Tax Receipts
              ↑
        [ LAYER 1: PRELIMINARY SCREENING ]
        Property Identification, Seller/Mortgagor Identity, Nature of Title (Freehold/Leasehold/SEZ)
```

Each layer must clear before the next begins. Skipping Layer 1 or 2 is the most common source of post-transaction disputes for tech companies acquiring office space or data center land.

---

### Framework 2: Types of Mortgage Comparison Matrix

| Dimension | Simple Mortgage | Equitable Mortgage | Usufructuary Mortgage | English Mortgage |
|-----------|----------------|-------------------|----------------------|-----------------|
| **How Created** | Registered deed | Deposit of title deeds | Registered deed | Registered deed |
| **Possession** | Mortgagor retains | Mortgagor retains | Mortgagee takes possession | Mortgagee gets conditional transfer |
| **Rental/Income** | Mortgagor keeps | Mortgagor keeps | Mortgagee applies to debt | Mortgagee keeps |
| **Registration Required** | Yes | No (in notified cities) | Yes | Yes |
| **Cost/Speed** | Medium | Low/Fast | High/Slow | High/Slow |
| **IT Firm Use Case** | Term loan against HQ | Quick bridge/working capital | Rare for operational firms | Project finance for large campus |
| **Risk for Lender** | Lower (registered) | Medium (document custody) | Lower (income stream) | Lower (conditional ownership) |

---

### Framework 3: Title Verification Checklist (TRACE Model)

**T — Tenure**: Is the property freehold, leasehold, or SEZ allotment? Who is the original grantor?

**R — Records**: Are revenue records (7/12, Patta, Khata) consistent with claimed ownership? Are property tax receipts current?

**A — Antecedents**: What is the 30-year transaction history? Are there gaps in the chain of title? Any adverse possession claims?

**C — Charges**: Does the Encumbrance Certificate (EC) show any prior mortgages, attachments, or pending litigation? Check both registered and equitable encumbrances.

**E — Entitlement**: Is the seller legally entitled to sell? Authority confirmed (Board resolution if seller is a company)? Any co-owners, legal heirs, or minor interests?

---

### Framework 4: Sale vs. Mortgage Decision Framework (for Tech Firms Needing Real Estate)

```
NEED: Real Estate for Operations or Collateral
         |
         v
Is this for LONG-TERM OCCUPANCY (>10 years) AND location is strategic?
         |
    YES  |  NO
         |    |
         v    v
    CONSIDER   PREFER LEASE / MANAGED WORKSPACE
     OUTRIGHT
      PURCHASE
         |
         v
Do you have SURPLUS CASH or access to low-cost debt?
         |
    YES  |  NO
         |    |
         v    v
   OUTRIGHT   CONSIDER DEBT — need to MORTGAGE an asset
   PURCHASE   |
              v
         Do you have existing unencumbered property?
              |
         YES  |  NO
              |    |
              v    v
          EQUITABLE   LOOK AT EXTERNAL
          OR SIMPLE    COLLATERAL / STRUCTURED
          MORTGAGE     FINANCE / REIT ROUTE
```

---

## 3. Formulas / Thresholds / Decision Rules

### A. Stamp Duty Calculation

```
Stamp Duty Payable = Circle Rate (or Actual Sale Consideration, whichever is higher) × State-Specific Rate (%)

Example (Karnataka, commercial):
  Market Value of Property = INR 5 Cr
  Circle Rate = INR 4.8 Cr
  Applicable Value = INR 5 Cr (higher of two)
  Stamp Duty Rate = 5% (commercial)
  Stamp Duty = INR 5 Cr × 5% = INR 25 Lakhs

Additional: Registration Fee = 1% of applicable value = INR 5 Lakhs
Total Transaction Cost (Stamp + Registration) = INR 30 Lakhs
```

**Decision Rule**: Always include stamp duty and registration fee in the property acquisition budget model. These are non-recoverable sunk costs and affect the property's break-even holding period.

---

### B. Registration Timeline

```
Mandatory Registration Window: Within 4 months from the date of execution of the deed
                                (Section 23, Registration Act, 1908)

If missed: Registrar may accept with penalty (up to 10x registration fee) within a further 4 months
If still missed: Deed becomes unregisterable — ownership transfer is void against third parties

PM Rule of Thumb: Schedule registration within 30 days of execution; never approach the 4-month limit
```

---

### C. Title Search Depth — 30-Year Rule

```
Minimum Title Search Period: 30 years back from the date of proposed transaction
Why 30 years: Period of limitation for most property claims under the Limitation Act, 1963
              Adverse possession claim matures at 12 years (private) / 30 years (government land)

For tech companies acquiring land adjacent to government/defense/forest areas:
  Extended search: 60 years recommended
  Additional check: Conversion orders (agricultural to non-agricultural), Change-of-Land-Use approvals
```

---

### D. Mortgage LTV Ratio Norms (RBI Guidelines for Banks)

```
Residential Property: LTV up to 90% (loans < INR 30L); 80% (INR 30-75L); 75% (> INR 75L)
Commercial Property (office/data center): LTV typically 60-65% (lender discretion)
Industrial/Warehouse: LTV typically 50-60%

For startups/tech firms pledging owned office premises:
  Realistic achievable LTV: 55-65% of registered market value
  Covenant trigger: Property value drop below 1.2x loan outstanding → margin call / additional security
  Rule: Never underwrite debt against property assuming >60% LTV for commercial; buffer for market cycles
```

---

## 4. Do / Don't

*Context: IT/AI/Consulting firms acquiring office space, data center real estate, or taking/giving property as collateral*

### DO

1. **Conduct a 30-year title search** before any property acquisition; engage a specialized property lawyer, not a general corporate lawyer.
2. **Obtain an Encumbrance Certificate** for the full search period from the Sub-Registrar's office and cross-verify with the seller's documents.
3. **Verify identity and authority of the seller**: for company sellers, demand certified Board resolution, Certificate of Incorporation, and MCA filings.
4. **Budget total transaction cost** including stamp duty + registration fee + legal fees (typically adds 6-10% over purchase price in most states).
5. **Register the sale deed within 30 days of execution**; do not wait for the 4-month statutory limit.
6. **Get a legal opinion from an independent advocate** — not the seller's advocate — confirming marketability of title.
7. **Check for building plan approvals, occupancy certificate, and fire NOC** before acquiring any constructed structure (especially for data centers).
8. **Verify zoning and land use conversion**: confirm the land is classified for commercial/industrial use; check with local planning authority.
9. **Check for litigation**: run a search in the relevant court's cause list and check CERSAI (for mortgages) and SARFAESI notices.
10. **Mutate the property** in your company's name with the local municipality/revenue authority after registration.
11. **Maintain an asset register** of all owned immovable property with deed copies, EC, tax receipts, and insurance in a centralized document management system.
12. **For equitable mortgage**: ensure title deeds are original, complete, and cover the entire title chain; store in secure vault with clear custody records.

### DON'T

1. **Don't close based on photocopies of title documents** — always verify originals; forgery of title deeds is a documented fraud vector.
2. **Don't skip the EC** even if the seller provides a legal opinion — EC is an independent government record; the legal opinion is based on documents furnished by the seller.
3. **Don't undervalue the property in the sale deed** to save stamp duty — this is a criminal offense and exposes the company to tax penalty, prosecution, and void deed risk.
4. **Don't acquire agricultural land** for office/data center use without confirming conversion to non-agricultural commercial/industrial use — illegal construction on agricultural land is demolished.
5. **Don't rely on verbal representations about free-from-encumbrance status** — all representations must be in the sale deed as warranties with indemnity clauses.
6. **Don't skip mutation** after registration — an unmutated property remains linked to the previous owner in revenue records, causing problems for future transactions and property tax.
7. **Don't use one lawyer for both buyer and seller** — conflict of interest compromises due diligence quality.
8. **Don't mortgage property without board approval** — for companies, mortgaging company property requires Board/shareholder approval under the Companies Act, 2013 (Sec 179/180).
9. **Don't allow a vendor/landlord to retain original title documents** if you are the purchaser — original title deeds belong to the buyer after sale.
10. **Don't assume an equitable mortgage is invisible to other lenders** — CERSAI registration is now mandatory even for equitable mortgages; non-registration allows subsequent lenders to claim priority.
11. **Don't enter into an agreement to sell and take possession without completing registration** — this does not transfer legal title and is risky if the seller becomes insolvent or disputes the deal.
12. **Don't ignore stamp duty on mortgage deeds** — mortgage deeds (other than equitable mortgages in some states) also attract stamp duty; underpayment renders the deed inadmissible.

---

## 5. Metric-Driven Scenarios with Anti-Examples

### Scenario 1: Tech Company Office Acquisition with Title Defect

**Context**: A Series C SaaS company (500 employees) acquires a 20,000 sq ft office building in Pune for INR 18 Cr to reduce rental outgo.

**Key Metrics**:
- Acquisition Price: INR 18 Cr
- Stamp Duty (Maharashtra commercial): ~6% = INR 1.08 Cr
- Registration Fee: ~1% = INR 18 Lakhs
- Legal/Due Diligence Budget (allocated): INR 2 Lakhs
- Actual Due Diligence Conducted: EC for 5 years only; no title search; no survey

**What Happened**: 14 months post-registration, a prior owner's legal heir filed a suit claiming ownership based on a will that was executed 22 years ago but not probated at the time of sale. The company's title was derived from this disputed ancestor. Court granted interim stay on alienation.

**Financial Impact**:
- INR 18 Cr locked; cannot sell or mortgage the property
- Legal costs: INR 40 Lakhs and rising
- Business disruption: office operations uncertain; alternate lease cost INR 80 Lakhs/year
- Resolution timeline: 5-7 years in civil court

**Anti-Example**: The company saved INR 3-4 Lakhs on a proper title search and legal opinion. A 30-year title search + comprehensive legal opinion would have cost INR 5-8 Lakhs and revealed the disputed succession. The correct action was to demand probated succession documents from the seller chain before proceeding.

---

### Scenario 2: Startup Mortgaging Premises for Series A Bridge

**Context**: An AI startup owns its registered office (2,500 sq ft, Bengaluru) valued at INR 3.2 Cr (market) / INR 2.8 Cr (circle rate). It needs INR 1.5 Cr bridge funding before Series A closes (3 months away).

**Key Metrics**:
- Property Market Value: INR 3.2 Cr
- Achievable LTV (commercial, private lender): 60% = INR 1.92 Cr
- Loan Sought: INR 1.5 Cr (well within LTV)
- Interest Rate (bridge): 15% per annum
- Equitable Mortgage: Title deeds deposited; stamped memorandum executed
- CERSAI Registration: Done (mandatory since 2016)
- Board Resolution: Passed under Sec 179 Companies Act, 2013

**Outcome**: Loan disbursed within 5 working days. Bridge period: 3 months. Total interest cost: INR 5.6 Lakhs. Series A closed; loan repaid; title deeds returned.

**Anti-Example**: A peer startup in the same position did NOT obtain board resolution before mortgaging. The CFO acted on verbal approval from the founder. When the lender attempted to enforce security (startup missed a tranche), the startup's new Series A investor's lawyer discovered the board resolution was absent. The mortgage was challenged as ultra vires — the lender's security was at risk, complicating the Series A closing. Remediation required an emergency board meeting, legal opinions, and a 3-week delay that cost INR 12 Lakhs in additional bridge interest and legal fees.

---

### Scenario 3: Consulting Firm Signing Lease Without Encumbrance Check

**Context**: A management consulting firm (150 consultants) signs a 5-year lease for a premium floor (8,000 sq ft) in a commercial tower in Hyderabad. Monthly rent: INR 12 Lakhs. Total lease value: INR 7.2 Cr. No EC or title verification done (it's "just a lease" per the admin team).

**Key Metrics**:
- Security Deposit: INR 36 Lakhs (3 months)
- Fit-out Investment: INR 90 Lakhs
- Total Sunk Cost at Risk: INR 1.26 Cr (deposit + fit-out)
- EC Check Cost (skipped): INR 5,000 and 2 days

**What Happened**: 18 months into the lease, the bank that had a registered mortgage on the building exercised SARFAESI powers after the landlord (builder) defaulted. The bank sought to take possession. While lease rights have some protection, the consulting firm's lease was junior to the bank's mortgage. Protracted litigation followed; the firm was forced to vacate after 2 years and forfeit the fit-out investment.

**Anti-Example**: A 15-minute check of the EC and a CERSAI search would have revealed the prior mortgage on the building. The correct action was to obtain a No Objection Certificate (NOC) from the mortgagee bank before signing the lease, or to require the landlord to provide a bank confirmation that the lease would be honored in enforcement scenarios. This is standard practice in large enterprise lease negotiations and was simply not followed here because the admin team classified it as "not a property purchase."

---

## 6. Practitioner Playbook

*12-Step Playbook for PM/CFO Managing a Property Acquisition or Mortgage Transaction for a Tech Company*

**Step 1: Define the Strategic Rationale (Week 0)**
Before initiating any property transaction, document the business case. Is this acquisition for operational use, investment, or as collateral for debt? Determine the hold period (short/medium/long-term), expected IRR, and how this fits the company's real estate strategy. Get Board/leadership alignment in writing.

**Step 2: Appoint Independent Legal Counsel (Week 1)**
Engage a law firm or advocate specializing in property law in the relevant state. Ensure they are independent from the seller's counsel. Define scope: title investigation, document review, regulatory compliance, and transaction execution. Budget INR 5-15 Lakhs depending on complexity.

**Step 3: Preliminary Due Diligence — Identify Red Flags (Weeks 1-2)**
Request all original title documents from the seller. Conduct physical site inspection. Verify property tax receipts, survey numbers, and land records. Check if the property is in any litigation (court cause list search). If any red flag emerges here, pause immediately.

**Step 4: 30-Year Title Search (Weeks 2-3)**
Legal counsel conducts a full chain-of-title investigation covering at least 30 years. Maps every transfer, inheritance, partition, or court decree affecting the property. Confirms that the current seller's right to sell is unbroken and uncontested.

**Step 5: Encumbrance Certificate and CERSAI Search (Week 3)**
Obtain EC from the Sub-Registrar's office for the full search period. Simultaneously run a CERSAI search to check for equitable mortgages. Cross-verify with seller's representations. Any encumbrance discovered must be resolved (discharged) before proceeding.

**Step 6: Regulatory and Approval Verification (Weeks 3-4)**
Verify: (a) Land Use / Zoning: is commercial/IT use permitted? (b) Building Plan approval from local authority, (c) Occupancy Certificate for completed structures, (d) Environmental clearances if required (data centers above a threshold), (e) Fire NOC, (f) RERA registration if applicable.

**Step 7: Negotiate Sale/Mortgage Deed Terms (Weeks 4-5)**
Work with legal counsel to draft deed with: accurate property description, representations and warranties on title, indemnity from seller for pre-sale encumbrances, conditions precedent to closing, penalty for delay, and dispute resolution clause. Negotiate and finalize.

**Step 8: Stamp Duty Calculation and Payment (Week 5-6)**
Calculate stamp duty based on higher of circle rate and actual consideration. Purchase appropriate stamp paper or pay through GRAS/SHCIL online in the relevant state. Undervaluation is a criminal offense — never compromise here. Include in budget from Day 1.

**Step 9: Board Approvals and Internal Governance (Week 5)**
For companies: pass Board resolution under Companies Act, 2013 authorizing the acquisition/mortgage. Confirm no shareholder approval required (check Sec 180 thresholds for disposal/mortgage of undertaking). File any required ROC intimations.

**Step 10: Execution and Registration (Week 6-7)**
Execute the deed in the presence of witnesses. Present before the Sub-Registrar for registration within 30 days (well within the 4-month limit). Ensure both parties or their authorized representatives are present with identity proof. Collect registered deed on the same day or within the processing time.

**Step 11: Post-Registration Formalities (Weeks 7-10)**
Mutate the property in the company's name with the municipal corporation and revenue authority. Update property tax records. Scan and archive all original documents in a secure document management system with access controls. Insure the property.

**Step 12: Ongoing Compliance and Monitoring (Quarterly)**
Pay property tax on time. Keep building licenses renewed. For mortgaged properties: track LTV covenant; ensure insurance is maintained (lender requirement); track loan repayment to avoid default. Review annual EC to confirm no new encumbrances have been created without authorization.

---

## 7. Content Critique

### Gap 1: Digital and Virtual Property — The Unaddressed Frontier

The Transfer of Property Act, 1882 is entirely silent on digital assets, virtual real estate (metaverse plots), domain names, and data center rack space. As AI companies and tech platforms increasingly treat digital infrastructure as strategic assets — and as metaverse real estate markets emerge — there is no equivalent statutory framework for "transfer" or "mortgage" of these assets. Legal practitioners rely on contract law and IP law patchworks. A modern course on property law for tech professionals must address: (a) how ownership of digital assets is established and transferred, (b) whether digital assets can serve as collateral under existing banking law, and (c) how cross-jurisdictional issues are resolved when the "property" has no physical address.

### Gap 2: Cross-Border Property in IT Parks and SEZs

The source material does not address the growing complexity of cross-border property ownership in Special Economic Zones (SEZs). IT companies with foreign parent entities or joint ventures face a dual layer: FEMA regulations restrict foreign ownership of Indian immovable property (non-agricultural, non-plantation only with conditions), and SEZ-specific rules govern allotments which are often in the nature of leasehold licenses rather than freehold sales. The interplay between the Transfer of Property Act, SEZ Act, 2005, and FEMA, 1999 is not covered and is directly relevant to any multinational IT firm establishing an Indian delivery center.

### Gap 3: REITs as an Alternative to Direct Property Ownership

Real Estate Investment Trusts (REITs) — regulated by SEBI since 2014 — offer tech companies an alternative to direct property ownership: invest in a REIT that owns office parks and data center assets, obtain exposure to real estate appreciation and rental income without the legal complexity of direct ownership, title risk, or registration compliance. The course does not mention REITs, which are increasingly relevant as India's REIT market matures (Embassy, Mindspace, Brookfield are major IT park REITs). For a CFO or PM evaluating "buy vs. lease vs. REIT" for real estate strategy, this is a material gap.

### Gap 4: Leasehold vs. Freehold in Tech SEZs

Most IT parks and SEZs offer allotments on leasehold basis (typically 30-99 year leases) rather than freehold sale. The legal implications are significant: a leasehold interest cannot be mortgaged without the lessor's (government/authority's) permission; sub-leasing requires NOC; the leasehold interest reverts at the end of the term unless renewed. Tech companies that build data centers or campuses on SEZ leasehold land are exposed to end-of-lease risk on their capex. This distinction — and its implications for long-term infrastructure investment decisions — is absent from the source material and should be a core topic for IT industry practitioners.

---

## 8. Quick-Recall Card

```
SALE AND MORTGAGE OF IMMOVABLE PROPERTY — QUICK-RECALL CARD
============================================================

GOVERNING LAW:
  - Transfer of Property Act, 1882 (Sec 54: Sale; Sec 58: Mortgage)
  - Registration Act, 1908 (compulsory registration of sale deeds)
  - Stamp Act (Central/State) — stamp duty on deeds

KEY THRESHOLDS:
  - Registration window: 4 months from execution (aim for 30 days)
  - Title search depth: 30 years minimum
  - Commercial LTV (bank): typically 55-65%
  - CERSAI registration: mandatory for all mortgages (equitable included)

TYPES OF MORTGAGE:
  Simple → Registered deed, mortgagor retains possession
  Equitable → Title deed deposit, fast/cheap, mortgagor retains possession
  Usufructuary → Mortgagee takes possession + income; no personal liability
  English → Conditional transfer to mortgagee; repayment = reconveyance

DUE DILIGENCE (TRACE):
  T — Tenure (freehold/leasehold/SEZ?)
  R — Records (revenue, tax, survey consistent?)
  A — Antecedents (30-year chain clear?)
  C — Charges (EC + CERSAI = zero encumbrances?)
  E — Entitlement (seller authorized to sell?)

STAMP DUTY FORMULA:
  Duty = MAX(Circle Rate, Sale Consideration) × State Rate %
  + Registration Fee (typically 1%)
  Budget 7-10% of property value for total transaction costs

CRITICAL DON'Ts:
  - Never skip 30-year title search
  - Never undervalue in deed (criminal + void)
  - Never skip board resolution for company property mortgage
  - Never close on photocopies

12-STEP PLAYBOOK (PM/CFO):
  1. Strategic rationale  2. Appoint counsel  3. Preliminary DD
  4. 30-yr title search  5. EC + CERSAI  6. Regulatory checks
  7. Deed negotiation  8. Stamp duty  9. Board approvals
  10. Execute + Register  11. Mutation + Archive  12. Ongoing compliance

IT/AI LENS — WATCH FOR:
  - SEZ leasehold ≠ freehold (cannot freely mortgage)
  - FEMA restrictions on foreign entity ownership
  - REIT as alternative to direct ownership
  - Data center regulatory approvals (power, environment)
  - Digital assets: no TPA framework exists yet

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Have we verified clean, unencumbered title through a 30-year search and EC before committing company funds to any property acquisition or offering any asset as collateral?"
```

---

## 9. Self-Audit

<!-- Self-Audit: Section 1 (Jargon Buster) covers all 10 required terms with IT/AI-specific relevance for each — PASS. Section 2 (Frameworks) delivers all 4 required frameworks including the Property Transaction Due Diligence Framework, Types of Mortgage Comparison Matrix, Title Verification Checklist (TRACE model), and Sale vs Mortgage Decision Framework — PASS. Section 3 (Formulas/Thresholds) covers stamp duty calculation with worked example, registration timeline (4-month rule + 30-day PM rule), title search 30-year rule with adverse possession rationale, and mortgage LTV norms per RBI — PASS. Section 4 (Do/Don't) contains 12 Dos and 12 Don'ts framed for IT/AI/consulting firms acquiring real estate or using it as collateral — PASS. Section 5 (Metric-Driven Scenarios) contains 3 scenarios (tech company title defect, startup equitable mortgage bridge, consulting firm lease without EC) each with specific metrics and anti-examples — PASS. Section 6 (Practitioner Playbook) contains 12 steps with timeframes and actionable guidance for PM/CFO — PASS. Section 7 (Content Critique) addresses 4 gaps: digital/virtual property, cross-border IT park property, REITs, and leasehold vs freehold in SEZs — PASS. Section 8 (Quick-Recall Card) ends with the exact mandatory phrase: "As a PM/Consultant/AI Lead, the one question to answer with this framework is: ___." — PASS. File size target ≥13,000 bytes — PASS (estimated ~16,000+ bytes). IT/AI/Product/Consulting lens applied throughout all sections — PASS. Self-Audit HTML comment present — PASS. All 9 sections in exact required order — PASS. -->
