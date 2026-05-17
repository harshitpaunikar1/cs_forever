# Time Value of Money

## Overview

Time value of money says a rupee today is worth more than a rupee tomorrow. Money in hand can be invested, so future money must be discounted to compare fairly. This single idea sits behind every valuation model.

---

## Why It Matters

Ignoring the time value of money leads to bad choices — treating a payment 10 years out as equal to one today, or overpaying for delayed cash flows. Managers use this to compare projects, price bonds, and evaluate acquisitions. Every serious valuation depends on getting discounting right.

## Key Principles

- Future cash flows must be discounted to a present value before comparing.
- The higher the discount rate, the lower the present value of distant cash flows.
- Compounding works in both directions: forward (future value) and backward (present value).
- Risk and time both raise the discount rate — riskier or later money is worth less.
- Small changes in the discount rate create large changes in valuation for long-dated cash flows.

## Key Terms

| Term | Definition |
|------|------------|
| **Present Value (PV)** | Today's value of a future sum, discounted at a chosen rate. |
| **Future Value (FV)** | What a sum today will be worth later, after compounding. |
| **Discount Rate** | The rate used to convert future cash to present value. |
| **Annuity** | A series of equal cash flows over a fixed period. |

## Use Case

A CFO comparing two capex projects with different payout schedules discounts each project's cash flows to present value and picks the one with the higher net present value.

## Scenario

> A telecom operator chose between a tower deal paying 100 crore upfront and one paying 180 crore over 10 years. At a 12% discount rate, the 10-year stream was worth just 102 crore today — barely different. Once risk was added, the upfront deal was clearly better and locked in.

## Examples

- A lottery offers 1 crore now or 2 crore in 20 years — discount it to see which wins.
- A supplier offers a 2% discount for early payment — compare against your cost of capital.

---

## Audited Appendix

# Time Value of Money
**Course:** Business Valuation
**Module:** Content / Time Value of Money
**Audited on:** 2026-04-18
**Audited by:** A1
**Source files reviewed:** `business-valuation/content/04-time-value-of-money.md`

---

## 1. Topic Snapshot
Time Value of Money (TVM) states a rupee today is worth more than a rupee tomorrow because today's rupee can be invested, compounded, or redeployed — so any future cash must be discounted to a present value before fair comparison. It sits behind every valuation, capital budgeting call, and contract-structure decision (upfront license vs multi-year subscription, SaaS annual-prepay vs monthly, deferred vendor payments, AI GPU capex vs cloud commits, investment IRR hurdles). For an IT/AI/Product/Consulting leader, the decision TVM powers is: which of two cash-flow schedules creates more economic value today, given our cost of capital and risk profile — pay now, pay later, or spread over years.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| PV | Present Value | Today's worth of a future rupee | Lets us compare cash across time | FV / (1+r)^n | DCF models, NPV decisions |
| FV | Future Value | What today's rupee becomes later | Shows compounding power | PV × (1+r)^n | Retirement, deposit pitches |
| Discount Rate | Discount Rate (r) | Rate used to shrink future cash to PV | Prices time + risk | WACC or hurdle rate, % | Board capex memos |
| Compound Rate | Compounding Rate | Rate at which money grows forward | Mirrors investment return | Same r, forward direction | Interest accrual, SIP math |
| Annuity | Ordinary Annuity | Equal cash flows at period-end | Models rent, EMI, SaaS | C × [1−(1+r)^−n]/r | Lease, loan amortisation |
| Annuity Due | Annuity Due | Equal cash flows at period-start | Models prepaid rent/SaaS | Annuity × (1+r) | Prepaid lease, annual upfront |
| Perpetuity | Perpetuity | Equal cash flows forever | Terminal-value proxy | C / r | Preferred stock, TV in DCF |
| Growing Perpetuity | Gordon Growth | Cash flows growing at g forever | Terminal value with growth | C₁ / (r − g) | DCF terminal, dividend discount |
| NPV | Net Present Value | Sum of PV of all CF minus investment | Accept/reject decision rule | Σ CFₜ/(1+r)^t − I₀ | Capex committees |
| IRR | Internal Rate of Return | r that makes NPV = 0 | Breakeven return benchmark | Solve NPV=0 iteratively | VC returns, project ranking |
| EAR | Effective Annual Rate | Annual rate after intra-year compounding | Makes rates comparable | (1+r_nom/m)^m − 1 | Credit cards, bond quotes |
| Nominal Rate | Nominal / Stated Rate | Headline rate before compounding | Contract convention | Given in % APR | Loan docs, RBI notifications |
| Continuous Compounding | Continuous Compounding | Limit of m→∞ compounding | Clean math for options, FX | e^r − 1 | Derivatives, quant models |
| Discount Factor | Discount Factor (DF) | Multiplier 1/(1+r)^n | Table lookup shortcut | 1/(1+r)^n | DCF spreadsheets |
| Opportunity Cost of Capital | Opportunity Cost | Return foregone on next-best use | Sets the bar for r | Market comparable return | Investment committee |
| Risk-Free Rate | Rf | Return on default-free asset | Anchor for discount rate | 10Y G-Sec yield | Valuation memos |
| Real Rate | Real Rate | Nominal minus inflation | Strips inflation distortion | (1+nom)/(1+inf) − 1 | Infra, long-dated assets |
| Nominal Rate (vs Real) | Nominal Rate | Rate including inflation | Matches nominal CF | Stated market rate | SaaS pricing, bonds |
| Mid-Year Convention | Mid-Year Convention | Assume CF arrives mid-period | Smooths year-end lumpiness | Discount at t − 0.5 | LBO/DCF models |

---

## 3. Frameworks & Matrices

### 3.1 PV/FV Ladder
**Purpose:** Visualise how a cash flow stream collapses to a single PV at t=0.

```
Time:    t=0     t=1      t=2      t=3      ...    t=n
CF:      -I₀    +C₁      +C₂      +C₃             +Cₙ
                 |        |        |               |
                 v /(1+r) v /(1+r)² v /(1+r)³      v /(1+r)ⁿ
PV: <------------+--------+--------+---------------+
                       Σ = NPV (today's value)
```

**Components:** time-line, signed cash flows, discount arrows, r, summation.
**IT/AI/Product example:** AI platform pilot: -₹5 cr at t=0, +₹2 cr/yr for 4 yrs at r=14% → NPV ≈ +₹0.83 cr → GO.
**Trigger:** Any capex, contract, or licensing memo with cash flows spread over >1 year.

### 3.2 Discount Rate Decomposition
**Purpose:** Make the "r" defensible by breaking it into parts.

```
 Discount Rate (r)
 ┌─────────────────────────────────────────────┐
 │  Risk-Free Rate (Rf)       ~7.0%  (10Y G-Sec)│
 │ +Expected Inflation Premium ~0.5%            │
 │ +Equity Risk Premium        ~6.0%            │
 │ +Project/Company Beta Adj.  ~1.0%            │
 │ +Size / Execution Premium   ~1.5%            │
 │ = Discount Rate             ~14–16%          │
 └─────────────────────────────────────────────┘
```

**Components:** Rf, inflation, ERP, beta, size/execution premium.
**Consulting example:** AI-startup GTM advisory engagement discounts 3-yr management-fee stream at 18% (higher size+execution premium) vs 12% WACC for enterprise SaaS.
**Trigger:** Pick r for NPV/DCF; defending a hurdle rate to CFO.

### 3.3 Annuity vs Perpetuity vs Growing Perpetuity Matrix

```
                        Finite Horizon   | Infinite Horizon
                        ─────────────────┼────────────────────
 Flat cash flow (C)     Annuity           | Perpetuity
                        C × [1−(1+r)^−n]/r | C / r
                        ─────────────────┼────────────────────
 Growing cash flow (g)  Growing Annuity   | Growing Perpetuity
                        C₁/(r−g)×[1−((1+g)/(1+r))^n] | C₁ / (r − g)
```

**Components:** horizon (finite/infinite) × growth (flat/growing).
**Product example:** SaaS ARR of ₹10 cr growing 8%, r=14% → Terminal value = 10/(0.14−0.08) = ₹167 cr.
**Trigger:** Terminal value in DCF, lease PV, subscription LTV, bond PV.

---

## 4. Formulas

### 4.1 PV = FV / (1 + r)^n
**Threshold:** Use when comparing a single future lump sum to today's money.
**Example:** ₹2 cr lottery in 20 yrs at r=8% → PV = 2/(1.08)^20 = ₹0.429 cr. Take ₹1 cr now — it beats ₹0.429 cr PV.

### 4.2 FV = PV × (1 + r)^n
**Threshold:** Use for forward compounding — deposits, retained earnings, SIPs.
**Example:** ₹50 L parked at 10% for 7 yrs → FV = 50×(1.10)^7 = ₹97.4 L.

### 4.3 PV of Ordinary Annuity: PV = C × [1 − (1 + r)^−n] / r
**Threshold:** Equal periodic CF, end-of-period, finite horizon (leases, EMIs, SaaS annuals).
**Example:** 3-yr SaaS monthly ₹2 L (₹24 L/yr) at r=12% → PV = 24×[1−(1.12)^−3]/0.12 ≈ ₹57.6 L. Compare to upfront ₹60 L → prepay only if discount ≥ 4% or strategic.

### 4.4 Perpetuity: PV = C / r; Growing Perpetuity (Gordon): PV = C₁ / (r − g)
**Threshold:** Use for terminal value and truly infinite streams; Gordon requires r > g.
**Example:** AI compute recurring savings ₹5 cr/yr forever at r=15% → PV = 5/0.15 = ₹33.3 cr. With g=5%: PV = 5/(0.15−0.05) = ₹50 cr.

### 4.5 EAR = (1 + r_nominal/m)^m − 1; Continuous: EAR = e^r − 1
**Threshold:** Normalise rates with different compounding frequencies before comparing.
**Example:** 12% nominal compounded monthly → EAR = (1+0.12/12)^12 − 1 = 12.68%; continuous → e^0.12 − 1 = 12.75%.

### 4.6 NPV = Σ CFₜ / (1 + r)^t − I₀
**Threshold:** Accept if NPV > 0 at chosen r; rank projects by NPV when mutually exclusive.
**Example:** AI GPU capex: -₹12 cr at t=0, +₹4 cr/yr for 4 yrs at r=14% → NPV = -12 + 4×[1−(1.14)^−4]/0.14 = -12 + 11.66 = -₹0.34 cr → borderline REJECT; rerun at r=12% → NPV = +₹0.15 cr.

### 4.7 Discount Factor: DF_t = 1 / (1 + r)^t
**Threshold:** Pre-compute a table when you have many CFs at the same r.
**Example:** r=12%, t=5 → DF=0.5674; a ₹10 cr CF at year 5 → PV ₹5.67 cr.

---

## 5. Do vs Don't

| Do | Don't |
|---|---|
| Match real CF with real rate, nominal CF with nominal rate | Don't mix real cash flows with nominal discount rate (double-counts inflation) |
| Use post-tax WACC on post-tax (after-tax) free cash flow | Don't apply WACC (post-tax) to pre-tax cash flows |
| Discount raw future cash flows to PV | Don't discount already-discounted numbers ("double discounting") |
| Check r > g before using growing perpetuity | Don't assume r > g holds — if g ≥ r, formula explodes and is invalid |
| Normalise rates to EAR before comparing monthly vs annual vs continuous | Don't compare a monthly APR against an annual EAR directly |
| Run sensitivity on r (±100–200 bps) for long-dated CFs | Don't treat r as a single point estimate on 10-year streams |
| Use XNPV/XIRR in Excel for irregular dates | Don't use NPV() on irregular-date flows — it assumes equal periods |
| Apply mid-year convention when cash arrives through the year | Don't assume all annual CF lands on Dec 31 when it's actually monthly |
| Tie discount rate to risk of the cash flow, not the firm | Don't use company WACC on a riskier/safer ring-fenced project |

---

## 6. Real-Life Scenarios

### Scenario 1: SaaS Annual Upfront vs Monthly Billing
**Setup:** Vendor offers CRM at ₹60 L upfront for 3 yrs OR ₹2 L/month (₹24 L/yr) billed monthly.
**Analysis:** Company WACC = 12%. Monthly PV (ordinary annuity, 36 months, r=1%/mo) = 2 × [1−(1.01)^−36]/0.01 ≈ ₹60.3 L. Upfront PV = ₹60 L.
**Decision:** Near indifference; take monthly for cash-flow flexibility and optionality to churn. Upfront only if vendor offers ≥5% discount.
**Tools:** Excel XNPV with actual billing dates, Looker finance dashboard tracking committed spend.

### Scenario 2: AI GPU Capex vs Multi-Year Cloud Commit
**Setup:** Option A: Buy H100 cluster ₹20 cr now, ₹2 cr/yr opex, 4-yr life, ₹3 cr salvage. Option B: 3-yr AWS committed-use ₹8.5 cr/yr (monthly billed).
**Analysis:** At WACC=14%, Option A PV outflows = -20 − 2×3.17 (annuity factor) + 3/(1.14)^4 = -20 − 6.34 + 1.78 = -₹24.6 cr; Option B = -8.5 × [1−(1.14)^−3]/0.14 = -₹19.74 cr. Normalise monthly billing via EAR = (1+0.14/12)^12 − 1 = 14.93%, recompute → -₹19.57 cr.
**Decision:** Cloud commit wins by ~₹5 cr PV; revisit if GPU life extends to 6 yrs or utilisation >85%.
**Tools:** Anaplan scenario model, CapIQ for cloud-comparable pricing, Excel XNPV.

### Scenario 3: ANTI-EXAMPLE — Product Team Signs 5-Yr Deferred Revenue-Share at Face Value
**Setup:** Partner offers ₹50 cr revenue-share payable ₹10 cr/yr over 5 yrs instead of ₹35 cr upfront. Product team sees "₹50 cr > ₹35 cr" and signs.
**Flaw:** No TVM. At WACC=14%, PV of deferred = 10 × [1−(1.14)^−5]/0.14 = 10 × 3.433 = ₹34.3 cr.
**Quantified Loss:** Deferred PV ₹34.3 cr < upfront ₹35 cr → the "bigger" deal destroys ~₹0.7 cr of value; worse, at WACC=16% (execution risk) PV falls to ₹32.7 cr — a ₹2.3 cr loss. Over a portfolio of 10 such deals, that's ₹20–25 cr of avoidable value leakage.
**Fix:** Always discount at risk-adjusted WACC; run sensitivity at ±200 bps.
**Tools:** Excel XNPV, CapIQ for comparable deal benchmarks, Anaplan for portfolio roll-up.

---

## 7. Implementation Playbook

1. **Inventory** all cash flows (sign, date, currency, nominal vs real) in an Excel/Sheets schedule.
2. **Select** discount rate: start with firm WACC, then adjust for project-specific risk, log rationale in a memo.
3. **Normalise** compounding frequency: convert everything to EAR so monthly, quarterly, annual streams are comparable.
4. **Build** PV/NPV model using XNPV for irregular dates; apply mid-year convention where CFs arrive continuously.
5. **Stress-test** with sensitivity table: r ±200 bps, g ±100 bps, horizon ±2 yrs — surface break-even r (IRR) and break-even g.
6. **Validate** with two independent checks: annuity formula vs spreadsheet, or Gordon vs exit-multiple.
7. **Document** assumptions in a one-page appendix: Rf source, ERP, beta, inflation basis, tax treatment.
8. **Present** decision as NPV + IRR + payback + qualitative risk flags to investment committee; archive in CapIQ/Anaplan for audit trail.

---

## 8. Content Quality Audit

**Covered well (source):** core intuition (rupee today > tomorrow), basic discounting, PV/FV/Discount Rate/Annuity definitions, illustrative telecom upfront-vs-deferred example, lottery/supplier use cases.

**Underplayed / missing in source:**
- Continuous compounding and EAR normalisation (critical for derivatives, FX, cloud billing).
- Mid-year convention (standard in LBO/DCF, not mentioned).
- Real-vs-nominal rate consistency (a top-5 valuation error).
- Sensitivity of PV to small r changes on long-dated cash flows (terminal-value fragility).
- XNPV vs NPV distinction in Excel (irregular vs equal-period dates).
- Inflation adjustments for multi-country/multi-currency valuations.
- Gordon constraint r > g and terminal-value dominance in DCF (often 60–80% of value).
- IRR pitfalls (multiple IRRs, scale-insensitivity vs NPV).

**Supplementary sources (≥5):**
1. Damodaran, A. — *Investment Valuation*, 3rd ed., Wiley (2012) — Ch. 3 on discount rates.
2. Brealey, R., Myers, S., Allen, F. — *Principles of Corporate Finance*, 13th ed., McGraw-Hill (2019) — Ch. 2–5 on TVM and DCF.
3. Ross, S., Westerfield, R., Jaffe, J. — *Corporate Finance*, 12th ed., McGraw-Hill (2019) — Ch. 4 on discounted cash flow.
4. Koller, T., Goedhart, M., Wessels, D. — *Valuation: Measuring and Managing the Value of Companies*, 7th ed., McKinsey/Wiley (2020) — Part 2 on core valuation.
5. Gallo, A. — "A Refresher on Net Present Value," *Harvard Business Review* (Nov 19, 2014).
6. CFA Institute — *Quantitative Methods* curriculum reading on TVM (latest level-I).

**Red flags in source:**
- Source asserts "10-year stream at 12% = ₹102 cr today" for ₹180 cr paid over 10 years — arithmetic ambiguous (likely ₹18 cr/yr annuity: 18 × [1−(1.12)^−10]/0.12 = ₹101.7 cr — OK, but the structure of payments should be stated explicitly).
- No mention of post-tax vs pre-tax treatment of cash flows.
- No guidance on choosing discount rate beyond "risk+time raise discount rate" — under-specified for practical use.
- Missing growing perpetuity / terminal-value concept, which is where most valuation error sits.

---

## 9. Quick-Recall Card

- TVM: discount every future rupee before comparing — at risk-adjusted r.
- PV formulas: lump sum FV/(1+r)^n; annuity C×[1−(1+r)^−n]/r; perpetuity C/r; Gordon C₁/(r−g) with r>g.
- Normalise: convert nominal rates to EAR; match real-with-real, nominal-with-nominal.
- Decision rule: NPV > 0 accept; rank by NPV, cross-check with IRR and payback.
- Sensitivity: long-dated CFs swing hard on ±100–200 bps in r — always stress-test.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: **Which cash-flow schedule creates the most value today at our risk-adjusted cost of capital, and how fragile is that answer to a 200 bps change in the discount rate?**

---

**Connects to:** [03-cash-flow-valuation.md](03-cash-flow-valuation.md), [05-discounted-cash-flow-dcf-models.md](05-discounted-cash-flow-dcf-models.md), [06-wacc-calculations.md](06-wacc-calculations.md), [../financial-management/](../financial-management/).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:5, 5:5, 6:4, 7:4, 8:5, 9:5, 10:4]
Sections rewritten: [1 snapshot sharpened to IT/AI lens; 3 matrices expanded with ASCII; 6 anti-example quantified at WACC=14% and 16%; 8 red-flags added]
Enrichments applied: [cross-course links to DCF/WACC/financial-management; 6 supplements incl. Damodaran, BMA, RWJ, Koller, HBR, CFA; anti-example with ₹0.7–2.3 cr quantified loss and portfolio roll-up; IT tooling (Excel XNPV/XIRR, CapIQ, Anaplan, Looker); role-lens question prefixed exactly "As a PM/Consultant/AI Lead"]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A1
-->
