# Enterprise Value vs. Equity Value

## Overview

Enterprise value (EV) is the total value of the business to all capital providers — debt and equity. Equity value is the slice that belongs only to shareholders. The bridge between them is net debt: EV = Equity Value + Debt − Cash.

---

## Why It Matters

Mixing up EV and equity value is the most common valuation mistake in practice. Multiples, cash flows, and comps pair with one or the other — not both. Managers, bankers, and investors who confuse them end up with numbers that look reasonable but are off by the size of the debt balance.

## Key Principles

- EV pairs with metrics before interest (EBITDA, EBIT, FCFF).
- Equity value pairs with metrics after interest (net income, FCFE, EPS).
- Add debt and deduct cash when moving from equity value to EV.
- Include minority interest, preferred stock, and pension deficits in EV.
- For private deals, decide upfront if the price quoted is "cash-free, debt-free" (EV basis).

## Key Terms

| Term | Definition |
|------|------------|
| **Enterprise Value (EV)** | Total value of a firm's operations to all capital providers. |
| **Equity Value** | Value belonging to shareholders, equal to share price × shares outstanding. |
| **Net Debt** | Total debt minus cash and cash equivalents. |
| **Minority Interest** | Portion of a subsidiary owned by outsiders, added to EV. |

## Use Case

An M&A lawyer drafts a share purchase agreement that fixes a 1,500 crore enterprise value, then adjusts for actual net debt at closing to compute the final equity price paid.

## Scenario

> A buyer offered 2,000 crore for a manufacturing target — assuming that was the cheque size. The target insisted it was an EV, not equity, figure. After adjusting for 700 crore of net debt, the actual cash paid to shareholders was 1,300 crore. Clear documentation upfront would have avoided a bitter renegotiation.

## Examples

- A listed company with a 3,000 crore market cap and 1,000 crore net debt has an EV of 4,000 crore.
- A cash-rich tech firm with 200 crore market cap and 50 crore net cash has an EV of 150 crore.

---

## Audited Appendix

# Enterprise Value vs. Equity Value
**Course:** Business Valuation
**Module:** Content / Enterprise Value vs Equity Value
**Audited on:** 2026-04-18
**Audited by:** A9
**Source files reviewed:** `business-valuation/content/12-enterprise-value-vs-equity-value.md`

---

## 1. Topic Snapshot
Enterprise Value (EV) is the total value of a company's operating assets to ALL capital providers (debt + equity + minority + preferred), while Equity Value is the slice that belongs to shareholders only — connected by the bridge EV = Equity Value + Debt − Cash (plus minority, preferred, pension). This distinction matters because an IT/AI/Product/Consulting leader negotiating an SPA, comparing SaaS multiples across peers with different leverage, or translating a "₹2,000 cr deal" headline will silently mis-price the transaction by 20–40% if they confuse the two. The decision: which value do I quote/compare/wire, and with which earnings metric do I pair it?

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|------|-----------|---------------|---------------|--------------|-------------------|
| EV | Enterprise Value | Price for the whole business engine | Captures value to all capital providers, leverage-neutral | Equity + Debt + Minority + Pref + Pension − Cash | "EV/EBITDA of 14x" |
| Equity Value | Market Cap / Shareholders' Value | Slice going to shareholders | What founders/shareholders actually pocket | Share price × diluted shares | "Market cap ₹3,000 cr" |
| Net Debt | Net Debt | Debt after using available cash to repay it | Normalizes deals for balance-sheet cash buffer | Total Debt − Cash − ST Investments | "Net debt adjustment at closing" |
| Gross Debt | Total Debt | Sum of all interest-bearing borrowings | Cash not always usable (trapped, regulatory) | Short-term + long-term borrowings + lease liab. | "Gross debt of ₹850 cr" |
| Total Debt | Total Debt | All borrowings incl. leases & converts | SPA "debt-like items" schedule | Gross debt + lease liabilities + debt-like items | "Debt-like items schedule" |
| Cash & Equivalents | Cash & Cash Equivalents | Liquid cash + <3-month instruments | Reduces EV vs equity | Balance sheet line | "Cash pile of ₹200 cr" |
| Short-Term Investments | ST Investments / Marketable Securities | Liquid investments (MF, T-bills) | Treated as near-cash in net debt | Current investments line | "Treasury book" |
| Minority Interest | Non-Controlling Interest (NCI) | Outsiders' share of consolidated sub | Consolidated EBITDA includes 100%, so add NCI to EV | BS equity section | "NCI of ₹120 cr added to EV" |
| Preferred Stock | Preferred Equity | Debt-like equity with fixed dividend | Senior to common equity, added to EV | Face value or market | "Preference shares bridge" |
| Pension Deficit | Underfunded Pension Obligation | Promised pensions > plan assets | Debt-like obligation to employees | PBO − plan assets (IAS 19/ASC 715) | "Pension deficit of ₹300 cr" |
| Operating Lease Liab. | Lease Liabilities (IFRS 16 / ASC 842) | Capitalized lease commitments on BS | Post-2019, leases sit on BS as debt-like | PV of lease payments | "IFRS 16 lease add-back" |
| Finance Leases | Capital Leases | Ownership-transfer leases | Always debt-like, pre- and post-IFRS 16 | BS liability line | "Finance lease of ₹40 cr" |
| Convertible Debt | Converts | Bond that converts to equity | Hybrid: treat as debt until converted / if-converted | Face + accrued or if-converted | "Convertible at ₹100 strike" |
| Contingent Consideration | Earn-Out | Future payment tied to milestones | Debt-like to seller-exit modelling | Fair value (IFRS 3) | "Earn-out cap ₹150 cr" |
| CFDF Price | Cash-Free Debt-Free | Headline price assumes BS stripped of cash & debt | SPA convention; = EV basis | Headline price | "CFDF at ₹2,000 cr" |
| Locked-Box | Locked-Box Mechanism | Price fixed at a past "box date" | Certainty; no closing true-up | Reference BS at box date | "Box date 31-Dec" |
| Completion Accounts | Completion Accounts Mechanism | Post-close adjustment for debt/cash/WC | Matches payment to real closing BS | 60–90 day post-close audit | "Completion accounts dispute" |
| Excess Cash | Excess vs Minimum Operating Cash | Cash beyond what operations need | Only excess reduces EV; operating cash is locked | Cash − minimum WC peg | "Operating cash buffer ₹60 cr" |
| Treasury Shares | Treasury Stock | Shares repurchased and held | Excluded from diluted share count | BS equity (contra) | "Buyback cancelled 5 cr shares" |
| Dilutive Securities | Options, Warrants, RSUs | ITM equity-settled instruments | Increase diluted share count | TSM formula | "ESOP dilution 4%" |
| TSM | Treasury Stock Method | Way to count ITM options as net new shares | Proceeds assumed to repurchase shares | Basic + Options × (1 − K/P) | "TSM diluted share count" |

---

## 3. Frameworks & Matrices

### 3.1 EV ↔ Equity Bridge
**Purpose:** convert between the two values without double-counting; audit every SPA and every comp.

```
         EQUITY VALUE  (Price × Diluted Shares, TSM)
               +
           Total Debt  (ST + LT borrowings + finance leases + IFRS 16 lease liab.)
               +
   Minority Interest   (NCI book or market)
               +
      Preferred Stock  (face or market)
               +
     Pension Deficit   (underfunded portion)
               +
   Contingent Consid.  (earn-out fair value)
               −
 Cash & Equivalents    (excess cash only; keep min operating cash)
               −
      ST Investments   (liquid treasury book)
   ─────────────────────────────────────────
           = ENTERPRISE VALUE
```
**Components:** equity (shareholder slice), debt-like (senior claims), cash-like (offsets).
**IT/AI/Product/Consulting example:** SaaS target: equity ₹2,500 cr + debt ₹600 cr − cash ₹150 cr = EV ₹2,950 cr. Used to compute EV/ARR for comp set.
**Trigger:** any time a headline number is quoted without "EV" or "equity" labelling.

### 3.2 Metric-to-Value Pairing Matrix

```
         ┌─────────────────────┬──────────────────────┐
         │  PAIRS WITH EV      │  PAIRS WITH EQUITY   │
         │  (pre-interest)     │  (post-interest)     │
─────────┼─────────────────────┼──────────────────────┤
Profit   │  EBIT, EBITDA       │  Net Income, EPS     │
Cash Flow│  FCFF (unlevered)   │  FCFE (levered)      │
Revenue  │  Sales, ARR         │  —                   │
Multiples│  EV/EBITDA, EV/Sales│  P/E, P/B, P/FCFE    │
Discount │  WACC               │  Cost of Equity (Ke) │
─────────┴─────────────────────┴──────────────────────┘
```
**Purpose:** never cross-pair; crossing EV with net income (or P/E with EBITDA) is the single most common valuation error.
**IT example:** a SaaS peer with ₹0 debt has P/E = 40, EV/EBITDA = 25. A leveraged peer with same ops has P/E = 28, EV/EBITDA = 25. The EV multiple is the leverage-neutral signal.
**Trigger:** drafting any comp sheet or LBO exit assumption.

### 3.3 SPA Price Mechanism Decision Tree

```
Headline price quoted
        │
        ▼
Is it CFDF / EV basis?
   ├── Yes ──► Will close via:
   │           ├── Locked-Box: fix at box date, no true-up
   │           │              (risk: leakage clause tight)
   │           └── Completion Accounts: true-up net debt + WC
   │                                    at closing (risk: disputes)
   └── No (equity / cheque basis) ──► read SPA for:
                      ├── What counts as "debt-like"?
                      ├── Is min WC pegged?
                      └── Are leases/pensions excluded?
```
**Purpose:** decide upfront which mechanism and what sits in "debt-like items."
**IT example:** AI startup headline ₹2,000 cr CFDF, completion accounts; at close ₹700 cr net debt + earn-out → cash to founders ₹1,300 cr.
**Trigger:** SPA term-sheet drafting.

### 3.4 Treasury Stock Method Diluted Share Count

```
Basic Shares Outstanding            10.00 cr
+ Options ITM (strike ₹100, price ₹400)
       Options granted:  1.00 cr
       Proceeds = 1 × ₹100 = ₹100 cr
       Shares repurchased = ₹100 cr / ₹400 = 0.25 cr
       Net new shares = 1.00 − 0.25 = 0.75 cr
+ RSUs vested but unissued           0.20 cr
+ Convertibles (if-converted)        0.30 cr
─────────────────────────────────────────
= Diluted Shares (TSM)              11.25 cr
```
**Trigger:** any equity value calc where ESOP/convertibles are material (>2% dilution).

---

## 4. Formulas

### 4.1 EV Bridge (full)
```
EV = Equity Value + Total Debt + Minority Interest + Preferred Stock
     + Pension Deficit + Contingent Consideration
     − Cash & Equivalents − Short-Term Investments
```
**Threshold:** if net debt > 15% of equity value, EV ≠ equity (don't skip the bridge).
**Numeric:** AI-SaaS deal headline ₹2,500 cr. Debt ₹600 cr, cash ₹150 cr, pension ₹0, NCI ₹0, earn-out ₹100 cr. EV = 2,500 + 600 + 100 − 150 = ₹3,050 cr.

### 4.2 Net Debt
```
Net Debt = Total Debt − Cash & Equivalents − Short-Term Investments
```
**Threshold:** negative net debt = net-cash company (EV < equity). Common in tech.
**Numeric:** cash-rich tech: ₹200 cr market cap, ₹50 cr net cash → EV = 200 − 50 = ₹150 cr.

### 4.3 Equity Value (TSM-diluted)
```
Equity Value = Share Price × Diluted Shares Outstanding (TSM)
```
**Threshold:** if ESOP pool > 5% or convertibles material, never use basic shares.
**Numeric:** ₹400 × 11.25 cr TSM shares = ₹4,500 cr equity value vs ₹4,000 cr at basic shares — 12.5% under-count fixed.

### 4.4 Multiples
```
EV/EBITDA = EV / EBITDA         (pair with EV)
EV/Sales  = EV / Revenue        (pair with EV)
P/E       = Share Price / EPS   (pair with equity)
P/B       = Share Price / Book Value per Share (pair with equity)
```
**Threshold:** SaaS EV/ARR typically 6–12x; EV/EBITDA 15–25x for growth tech; P/E loses comparability when leverage differs.
**Numeric:** EV ₹3,050 cr, EBITDA ₹200 cr → EV/EBITDA = 15.25x.

### 4.5 Treasury Stock Method (optional)
```
TSM Net New Shares = Options Outstanding × (1 − Strike Price / Share Price)
                    (applied only to ITM options; OTM excluded)
Diluted Shares = Basic + Σ TSM Net New + RSUs + If-Converted Converts
```
**Numeric:** 1 cr options at strike ₹100, price ₹400 → 1 × (1 − 100/400) = 0.75 cr net new shares.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|----|-------|
| 1 | Pair EV with EBITDA/EBIT/FCFF/Sales | Don't pair EV with net income or EPS |
| 2 | Pair Equity Value with Net Income/FCFE/EPS | Don't pair equity/P/E with EBITDA |
| 3 | Ask "CFDF or cheque basis?" before signing any term sheet | Don't assume announced "deal value" = equity to shareholders |
| 4 | Include IFRS 16 / ASC 842 operating lease liabilities as debt-like | Don't forget lease liabilities — they add 5–25% of debt for retail/tech-office targets |
| 5 | Add pension deficit for old-economy / manufacturing targets | Don't ignore pension deficit (often ₹100–500 cr off an industrial) |
| 6 | Use TSM diluted shares when options/RSUs are material | Don't use basic shares when ESOP pool > 5% |
| 7 | Add minority interest to EV when sub is consolidated | Don't double-count minority (either consolidate EBITDA + add NCI, OR proportional consolidation — not both) |
| 8 | Use EV/EBITDA for cross-peer comp across different leverage | Don't use P/E for peers with structurally different debt |
| 9 | Subtract only EXCESS cash; leave minimum operating cash in the business | Don't strip 100% of cash — buyer needs operating float on day 1 |
| 10 | Read SPA "debt-like items" schedule line-by-line | Don't assume the schedule captures earn-outs, tax liabilities, customer deposits automatically |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI-SaaS acquisition at "₹2,000 cr"
An AI-SaaS target announces a ₹2,000 cr deal. Buyer (Indian IT services PE arm) pushes for Cash-Free Debt-Free basis with Completion Accounts mechanism. Target BS: debt ₹450 cr, cash ₹180 cr, earn-out ₹100 cr, ESOP pool 8%.
- EV negotiated: ₹2,000 cr
- Net debt at close: 450 − 180 = ₹270 cr
- Earn-out cap: ₹100 cr (payable on 3-year ARR milestone)
- Equity to founders (ex-ESOP): 2,000 − 270 − 100 = ₹1,630 cr, of which ESOP holders take ~₹130 cr
**Outcome:** founders walk with ~₹1,500 cr net — buyer and seller both happy because every line was labelled.

### Scenario 2 — Cross-peer benchmarking on SaaS multiples
Consulting engagement: benchmark 5 peers for a listco acquirer. Peer A is net-cash (₹300 cr cash, zero debt). Peer B is levered (₹800 cr debt, ₹100 cr cash).
- If the analyst uses P/E: Peer A trades at 45x, Peer B at 18x — looks like Peer B is half the price.
- Switch to EV/EBITDA: Peer A 22x, Peer B 21x — apples-to-apples; leverage noise removed.
**Tool:** CapIQ EV template, Bloomberg EV bridge, Factset peer tearsheet. Deliverable: a footnoted comp sheet that calls out every non-recurring item, lease, and NCI.

### Scenario 3 — ANTI-EXAMPLE: Locked-Box gone wrong (quantified hidden cost)
Buyer signs "EV ₹2,000 cr" via Locked-Box mechanism, box date 31-Dec. SPA defines "debt-like items" narrowly — excludes IFRS 16 lease liabilities and contingent consideration. Between box date and close (5 months):
- ₹120 cr of new office lease liabilities recognized (IFRS 16)
- ₹60 cr earn-out to an earlier sub-acquisition crystallizes
- Buyer has no true-up mechanism to recover these
**Hidden cost:** ₹180 cr post-close; buyer's effective EV is ₹2,180 cr (9% overpay) and the board has to explain to investors.
**Lesson:** Locked-Box works only if "debt-like" is drafted broadly AND a leakage clause is airtight; otherwise insist on Completion Accounts.

**Tools:** CapIQ, Bloomberg, Factset (EV bridges & peer sets); Excel diluted-share calc (TSM); data-room VDR (Intralinks, Ansarada, Datasite); SPA redline (Litera Compare).

---

## 7. Implementation Playbook — Extract a Clean EV Bridge and SPA-Safe Price

1. **Pull** the latest audited + most recent quarterly balance sheet from VDR; tag every line as equity / debt-like / cash-like / neither.
2. **List** debt-like items explicitly: bank loans, NCDs, finance leases, IFRS 16 op-lease liabilities, pension deficit, preferred stock, earn-outs, contingent consideration, tax demands under dispute, customer deposits, deferred consideration.
3. **Compute** net debt = total debt − (cash + ST investments − minimum operating cash peg); document the peg assumption (typically 30–60 days of operating expenses).
4. **Build** diluted share count via TSM: basic + ITM options + vested RSUs + if-converted converts; reconcile to cap table.
5. **Bridge** Equity Value ↔ EV on one Excel tab with every line traced to a BS source; circulate for legal + tax review.
6. **Draft** SPA price mechanism: choose Locked-Box (certainty, simpler) OR Completion Accounts (true-up, safer for buyer); define leakage / debt-like schedule exhaustively.
7. **Stress-test** the bridge at ±10% on debt, cash, earn-out crystallization, lease extensions; quantify range of equity cheque.
8. **Sign-off**: CFO + deal lawyer + tax partner initial the bridge before term sheet is signed.

---

## 8. Content Quality Audit

**Covered well in source:**
- Core EV ↔ Equity bridge arithmetic.
- "Most common valuation mistake" framing.
- Metric-pairing principles (pre- vs post-interest).
- One good SPA renegotiation scenario.

**Underplayed / missing:**
- Operating lease liabilities under IFRS 16 / ASC 842 — post-2019 these are on BS and must be added as debt-like; source is silent.
- Contingent consideration / earn-outs fair-value accounting (IFRS 3).
- Locked-Box vs Completion Accounts mechanism contrast.
- Treasury Stock Method and diluted-share methodology.
- Excess-cash definition and minimum operating cash peg.
- ESOP pool treatment in private deals.
- Stock-based compensation (SBC) adjustment to EBITDA and its knock-on to EV/EBITDA multiples.
- If-converted method for convertibles vs TSM for options.

**Supplementary sources (≥5):**
1. Damodaran, A., *Investment Valuation* (3rd ed., Wiley, 2012) — Ch. 15 (Firm Valuation) and Ch. 19 (Multiples).
2. Rosenbaum, J. & Pearl, J., *Investment Banking: Valuation, LBOs, M&A, and IPOs* (3rd ed., Wiley, 2020) — Ch. 1 (Comparable Companies), Ch. 5 (M&A).
3. Koller, T., Goedhart, M., Wessels, D. (McKinsey), *Valuation: Measuring and Managing the Value of Companies* (7th ed., Wiley, 2020) — Ch. 12 (EV multiples), Ch. 15 (non-operating items).
4. Deloitte / PwC, *M&A Price Adjustment Mechanisms: Locked-Box vs Completion Accounts* (2023 white paper).
5. IFRS 16 *Leases* and ASC 842 standards references (IASB / FASB technical summaries).
6. (Bonus) Mergermarket / Bloomberg League Tables deal databases for real CFDF vs cheque practice.

**Red flags in source:**
- No mention of IFRS 16 / ASC 842 — a 2019+ blind spot.
- Treats cash as uniform — no excess-vs-operating-cash distinction.
- Ignores diluted-share methodology; silently uses basic shares.
- No Locked-Box vs Completion Accounts contrast, despite the SPA use-case.

---

## 9. Quick-Recall Card
- EV = value to ALL capital providers; Equity Value = shareholders' slice only.
- Bridge: EV = Equity + Debt + Minority + Preferred + Pension + Earn-outs − Excess Cash.
- Pair EV with pre-interest metrics (EBITDA, EBIT, FCFF); pair Equity with post-interest (Net Income, EPS, FCFE).
- Never cross-pair (EV/EBITDA vs P/E is meaningful; EV/Net-Income is nonsense).
- In SPAs: is it CFDF? Locked-Box or Completion Accounts? What's in "debt-like"?
- **As a PM/Consultant/AI Lead, the one question to answer with this framework is: when a "₹X cr deal" headline lands, is X the Enterprise Value (total price for the business) or the Equity Value (cheque to shareholders), and which pre/post-interest metric should I pair with it for an apples-to-apples comp?**

---

**Connects to:** [01-balance-sheet-analysis.md](01-balance-sheet-analysis.md), [03-cash-flow-valuation.md](03-cash-flow-valuation.md), [05-discounted-cash-flow-dcf-models.md](05-discounted-cash-flow-dcf-models.md), [09-valuation-for-m-and-a.md](09-valuation-for-m-and-a.md), [../mergers-acquisitions/07-pricing-mechanisms.md](../mergers-acquisitions/07-pricing-mechanisms.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:5, 5:5, 6:4, 7:4, 8:5, 9:5, 10:4]
Sections rewritten: [1 tightened for role lens; 3 added TSM framework; 6 added quantified anti-example; 8 expanded red flags and supplements]
Enrichments applied: [cross-course links; 5+ supplements; anti-example with ₹180 cr hidden cost; IT tooling (CapIQ/Bloomberg/VDR/Litera); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A9
-->
