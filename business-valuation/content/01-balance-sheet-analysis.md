# Balance Sheet Analysis

## Overview

A balance sheet is a snapshot of what a company owns and owes on a given day. Analyzing it means checking the mix of assets, liabilities, and equity to judge financial health. For valuation, it tells you how much value is already locked inside the business before you even look at future earnings.

---

## Why It Matters

The balance sheet shows whether a company can pay its bills, how much debt it carries, and what tangible value backs its share price. Weak liquidity or bloated debt can sink an otherwise good business. For a buyer or investor, misreading the balance sheet means overpaying — or missing a hidden bargain.

## Key Principles

- Assets must always equal liabilities plus equity.
- Separate current (under 1 year) from non-current items to judge liquidity.
- Watch for off-balance-sheet items like operating leases or guarantees.
- Compare ratios (current, debt-to-equity) against industry peers, not absolutes.
- Book value rarely equals market value — adjust for intangibles and fair value.

## Key Terms

| Term | Definition |
|------|------------|
| **Current Assets** | Cash and items convertible to cash within 12 months. |
| **Working Capital** | Current assets minus current liabilities. |
| **Book Value** | Total assets minus total liabilities, per the accounts. |
| **Goodwill** | Premium paid over fair value of net assets in an acquisition. |

## Use Case

A private equity firm studying a target company reads the balance sheet first to size up debt, working capital needs, and the quality of reported assets before building any cash flow model.

## Scenario

> A regional retailer looked profitable on paper, but its balance sheet showed inventory up 60% year-on-year while sales grew just 8%. The analyst flagged overstocking and a liquidity squeeze, and the buyer cut the offer price by 15% to cover the working capital cleanup.

## Examples

- A manufacturer with high fixed assets and low cash is asset-heavy but cash-poor.
- A SaaS firm with mostly intangible assets has low book value but high earning power.

---

## Audited Appendix

# Balance Sheet Analysis
**Course:** Business Valuation
**Module:** Content / Balance Sheet Analysis
**Audited on:** 2026-04-18
**Audited by:** A8
**Source files reviewed:** `business-valuation/content/01-balance-sheet-analysis.md`

---

## 1. Topic Snapshot
Balance sheet analysis is the structured read of a company's assets, liabilities, and equity on a single date to judge solvency, liquidity, and the quality of value already locked inside the business. For an IT/AI/Product/Consulting leader evaluating an acquisition target, a funding round, or a strategic supplier, it exposes hidden debt, deferred-revenue obligations, intangible bloat, and working-capital traps that income statements hide. It helps decide: pay the asking price, renegotiate, inject more cash, or walk away.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| Current Assets | Current Assets (CA) | Cash-ish within 12 months | Measures short-term resources | Sum of cash, AR, inventory, prepaid | CFO review, lender covenants |
| Non-current Assets | Long-term Assets | Used beyond a year | Tracks invested capital base | PP&E + intangibles + LT investments | Capex planning, M&A |
| Current Liabilities | Current Liabilities (CL) | Bills due within 12 months | Captures near-term cash outflow | AP + short-term debt + accrued | Treasury, audit |
| Non-current Liabilities | Long-term Liabilities | Debts owed beyond a year | Measures structural leverage | LT debt + pension + lease LT | Bond prospectus, 10-K |
| Equity | Shareholders' Equity | Owners' residual stake | Residual claim after debt | Assets − Liabilities | Cap table, valuation |
| Working Capital | WC | Operating cash cushion | Buffer to run day-to-day | CA − CL | Ops reviews, diligence |
| Quick Ratio | Acid-test Ratio | Pay bills without selling inventory | Liquidity stress test | (CA − Inventory) / CL | Credit analysts |
| Current Ratio | CR | Short-term pay-ability | Covenant threshold | CA / CL | Bank covenants |
| Debt-to-Equity | D/E | Leverage vs owners' skin | Solvency signal | Total Debt / Equity | Rating agencies |
| Book Value | BV | Accounting net worth | Floor value anchor | Assets − Liabilities | Value investing |
| Goodwill | GW | Premium over fair value acquired | Residual of M&A price | Purchase price − FV net assets | Post-merger PPA |
| Intangible Assets | Intangibles | Non-physical value (IP, software, brand) | Captures digital-era assets | Capitalized cost less amort | SaaS, AI balance sheets |
| Deferred Revenue | Contract Liabilities | Cash in, service not yet delivered | ASC 606/IFRS 15 matching | Unearned portion of billings | SaaS ARR diligence |
| Lease Liabilities | IFRS 16 / ASC 842 | On-BS rent obligation | Ends off-BS lease loophole | PV of lease payments | Real estate, DC leases |
| Net Debt | ND | Debt minus cash | True leverage | Total debt − cash & equivalents | EV bridge |
| Cash and Equivalents | Cash & CE | Cash + near-cash < 90 days | Immediate liquidity | Bank + money-market + T-bills | Runway calc |
| Accounts Receivable | AR (DSO) | Money customers owe | Gauges collection speed | AR / Revenue × 365 | Credit & collections |
| Inventory | DIO | Goods held for sale | Measures stock turns | Inventory / COGS × 365 | Ops, retail, hardware |
| Accounts Payable | AP (DPO) | Money owed to suppliers | Measures payment delay | AP / COGS × 365 | Procurement |
| Cash Conversion Cycle | CCC | Days cash is tied up | End-to-end WC efficiency | DSO + DIO − DPO | CFO dashboards |
| Off-Balance-Sheet Item | OBS | Obligation not on BS | Hides true leverage | Guarantees, SPVs, factoring | Audit committees |
| Book Value vs Market Value | BV vs MV | Accounting vs trading value | Frames valuation gap | P/B ratio | Equity research |

---

## 3. Frameworks & Matrices

### 3.1 Asset Quality Matrix
**Purpose:** Classify a target's asset base by tangibility and reliability before pricing.

```
                   HARD ASSETS            SOFT / INTANGIBLE         GOODWILL
                 (PP&E, cash, AR)     (capitalized R&D, software, (M&A residual)
                                         customer relationships)
   HIGH       +-------------------+-------------------------+-------------------+
              | Industrial / Infra|  SaaS / AI platform     |  Roll-up PE       |
              | safe collateral   |  high earning power,    |  impairment-prone |
              |                   |  fragile book           |  watch triggers   |
   MED        +-------------------+-------------------------+-------------------+
              | Consulting-firm   |  Product co. w/         |  Serial acquirer  |
              | WIP + receivables |  capitalized dev costs  |  mid-cycle        |
   LOW        +-------------------+-------------------------+-------------------+
              | Early startup     |  Pre-revenue deep-tech  |  Clean BS         |
```
**Components:** tangible PP&E, intangible/IP, acquired goodwill.
**IT/AI example:** An AI inference platform with 70% intangibles and 15% goodwill maps top-center/right — demand impairment-test history.
**Trigger:** use when target's book value looks "light" or "heavy" vs peers.

### 3.2 Liquidity Ladder
**Purpose:** Rank assets by speed to cash; align covenants and runway math.

```
  FASTEST  Cash & Equivalents        ---- Quick Ratio ----
           Marketable Securities          numerator
           Accounts Receivable       ---- Current Ratio ---
           Inventory (SaaS: none)         numerator
           Prepaid Expenses
           Fixed Assets (PP&E)
           Intangibles / Goodwill
  SLOWEST
```
**Components:** each rung with expected days-to-cash.
**Consulting example:** A boutique consultancy has 65% of CA in AR (DSO 72) — quick ratio looks fine but cash risk is concentrated in top-5 clients.
**Trigger:** covenant structuring, lender negotiations.

### 3.3 Financial Health 2x2
**Purpose:** One-glance archetype placement.

```
                    LEVERAGE LOW          LEVERAGE HIGH
                 +---------------------+----------------------+
   LIQUIDITY HIGH| SAFE                 | GROWTH               |
                 | well-funded SaaS     | PE-backed AI infra   |
                 | (e.g., Series B AI)  | (levered rollup)     |
                 +---------------------+----------------------+
   LIQUIDITY LOW | STRESS               | DISTRESSED           |
                 | bootstrapped         | legacy IT services   |
                 | consulting firm      | w/ goodwill overhang |
                 +---------------------+----------------------+
```
**IT/AI example:** Cash-rich Series B AI co. = SAFE; highly levered consulting rollup with negative WC = DISTRESSED.
**Trigger:** opening slide of any diligence memo.

### 3.4 Working Capital Cycle (Optional)
```
   Purchase Inventory --DIO--> Sell on credit --DSO--> Collect Cash
           ^                                                   |
           |----------------- DPO ----------------------------- v
                           Pay Suppliers
   CCC = DSO + DIO - DPO
```
**Use:** quantify how many days of revenue are trapped in operations — critical for hardware-heavy AI/IoT firms.

---

## 4. Formulas

### 4.1 Current Ratio = CA / CL
Thresholds: <1 stress, 1-2 healthy, >3 idle cash.
SaaS example: CA $120M / CL $80M = **1.5** — healthy but check deferred rev share of CL.

### 4.2 Quick Ratio = (CA - Inventory) / CL
Thresholds: <0.7 tight, 0.7-1 ok, >1 comfortable.
AI platform: ($120M - $2M inventory) / $80M = **1.48** — essentially same as current ratio (low inventory), typical for SaaS.

### 4.3 Debt-to-Equity = Total Debt / Equity
Thresholds: <0.5 conservative, 0.5-1.5 typical tech, >2 levered.
Consulting firm: $45M debt / $60M equity = **0.75** — moderate; confirm earn-out and lease liabilities.

### 4.4 Working Capital & Days WC
WC = CA - CL = $120M - $80M = **$40M**.
Days WC = WC / Revenue x 365 = $40M / $200M x 365 = **73 days** — high for SaaS (expect 30-60); investigate AR ageing.

### 4.5 Cash Conversion Cycle = DSO + DIO - DPO
SaaS target: DSO 55 + DIO 0 - DPO 40 = **15 days**.
Hardware AI: DSO 60 + DIO 90 - DPO 45 = **105 days** — negotiate working-capital adjustment at close.

### 4.6 Book Value per Share = Equity / Shares Outstanding
Thresholds: compare with market price; P/B > 5 common in SaaS, <1 may signal distress or deep value.
Example: Equity $60M / 10M shares = **$6.00** vs market price $48 -> P/B 8.0x — paying for future, not book.

---

## 5. Do vs Don't

| Do | Don't |
|---|---|
| Reconcile deferred revenue to ARR and billings schedule | Assume deferred revenue is "free money" without service obligation |
| Add operating lease liabilities (IFRS 16 / ASC 842) when calculating net debt | Ignore leases because old GAAP treated them off-BS |
| Separate capitalized R&D from acquired intangibles | Lump all intangibles as "goodwill" |
| Age AR by customer to spot concentration and stale balances | Accept gross AR at face value |
| Compute net debt (debt - cash) for EV bridges | Use gross debt in EV — you'll overpay |
| Test goodwill impairment history for the last 3 years | Treat goodwill as permanent value |
| Compare ratios to 3-5 peers and the target's own trailing 8 quarters | Benchmark against a single industry median |
| Read footnotes on contingent liabilities and SPVs | Stop reading at the four financial statements |

---

## 6. Real-Life Scenarios

### Scenario 1 — SaaS Acquisition Target
A mid-market PE firm eyes a $250M ARR vertical SaaS. Balance sheet shows $180M deferred revenue, $90M capitalized commissions (ASC 606), and $120M intangibles from two prior bolt-ons. Analyst (using **CapIQ** + **NetSuite** export) builds a deferred-revenue waterfall, confirms 92% renewal, and identifies $22M of operating leases (ASC 842) previously framed as opex. Final bid adjusts EV down $35M for lease debt; deferred rev treated as value-neutral liability with performance obligations covered by existing cost base.

### Scenario 2 — Series C AI Startup Cash Runway
A lead investor uses **Carta** cap table + **Xero** GL pull via **Looker** dashboard. Cash $42M + AR $8M, monthly burn $4.5M. Effective runway = ($42M + 0.85 x $8M) / $4.5M = **~10.8 months**. Round sized to extend to 24 months; balance sheet covenant added: min cash $15M, quick ratio >= 1.0 through maturity.

### Scenario 3 — ANTI-EXAMPLE: Book-Value Tunnel Vision
A strategic acquirer buys an IT services firm at 1.1x book ($110M for $100M BV). Overlooked: 48% of AR from a single telco client (DSO 95), $28M capitalized software (US GAAP ASC 350-40 internal-use software) that failed impairment test 6 months later, and an off-BS receivables-factoring facility of $15M. Outcome: $40M write-down in year 1 (goodwill + capitalized software) + $12M AR reserve when telco client churned. Effective overpayment ~$52M (47% of deal value). Using **PitchBook** comps and proper intangible scrub would have surfaced all three red flags pre-LOI.

**Tools:** CapIQ, PitchBook, Carta, NetSuite, Xero, Looker on finance data warehouse.

---

## 7. Implementation Playbook

1. **Pull** last 8 quarters of audited balance sheets from data room into NetSuite/Xero export + CapIQ peers.
2. **Reclassify** lease liabilities (IFRS 16 / ASC 842), capitalized R&D, and deferred revenue into a standardized template.
3. **Compute** ratio pack (current, quick, D/E, net debt, WC days, CCC, P/B) with 3-peer benchmark in Looker.
4. **Age** AR by customer top-10 in CapIQ or Excel pivot; flag concentration >15%.
5. **Test** goodwill & intangible impairment history; list triggering events in diligence memo.
6. **Map** off-BS items (guarantees, SPVs, factoring, purchase commitments) from footnotes.
7. **Model** net debt & working-capital adjustment for the SPA; peg to 12-month average WC.
8. **Present** 1-page Financial Health 2x2 + red-flag register to IC with recommended price adjustment.

---

## 8. Content Quality Audit

**Covered well:** accounting identity (A = L + E), current/non-current split, book-vs-market caveat, off-BS awareness, peer comparison, retailer inventory scenario.

**Underplayed / missing:**
- Deferred revenue mechanics in SaaS (ASC 606, revenue recognition vs billing).
- Lease capitalization under IFRS 16 / ASC 842 and its effect on net debt and EV.
- Capitalized R&D under US GAAP (generally expensed, except internal-use software ASC 350-40) vs IFRS (IAS 38 development-phase capitalization).
- Intangible asset impairment tests (annual for indefinite-life; triggering events for finite).
- Customer concentration risk visible through AR ageing and top-N disclosure.
- Off-balance-sheet SPVs, receivables factoring, and purchase commitments.

**Supplements (≥5):**
1. Damodaran, A. "Investment Valuation" 3rd ed. (2012) — intangibles and book-value adjustments.
2. Penman, S. "Financial Statement Analysis and Security Valuation" 5th ed. (2013) — reformulating the balance sheet.
3. Koller, Goedhart, Wessels (McKinsey) "Valuation: Measuring and Managing the Value of Companies" 7th ed. (2020) — invested-capital view.
4. Tracy, J. "How to Read a Financial Report" 8th ed. (2014) — practitioner primer.
5. IFRS 16 (leases) and FASB ASC 842 (leases), plus IAS 38 / ASC 350-40 for intangibles and internal-use software.

**Red flags in source:** only 4 key terms defined; zero ratios or thresholds; no SaaS-specific treatment of deferred revenue or capitalized commissions; no mention of leases post-IFRS 16; scenario is retail-only, not IT/AI/Product/Consulting.

---

## 9. Quick-Recall Card
- Balance sheet = snapshot of owned, owed, owned-by-shareholders on a given date.
- Always reclassify: add lease liabilities, split intangibles vs goodwill, reconcile deferred revenue.
- Core ratios: Current, Quick, D/E, Net Debt, CCC, P/B — each with thresholds.
- Red flags: rising inventory/AR vs revenue, goodwill-heavy book, off-BS guarantees, single-customer AR.
- Book value is a floor, not a price — for SaaS/AI, earning power dominates.
- **Role-lens question:** "If I were signing the SPA tomorrow, which three balance-sheet lines would change my bid by more than 5%?"

---

**Connects to:** [02-income-statement-interpretation.md](02-income-statement-interpretation.md), [03-cash-flow-valuation.md](03-cash-flow-valuation.md), [05-discounted-cash-flow-dcf-models.md](05-discounted-cash-flow-dcf-models.md), [../mergers-acquisitions/11-due-diligence-review.md](../mergers-acquisitions/11-due-diligence-review.md), [../financial-management/](../financial-management/).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:4, 7:4, 8:4, 9:4, 10:4]
Sections rewritten: [2 (expanded to 22 rows), 3 (added 2x2 + WC cycle), 4 (added thresholds + numeric), 6 (added anti-example with quantified cost), 8 (added 5 supplements + standards)]
Enrichments applied: [cross-course links; 5 supplements with author+year; anti-example w/ $52M quantified cost; IT tooling CapIQ/PitchBook/Carta/NetSuite/Xero/Looker; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A8
-->
