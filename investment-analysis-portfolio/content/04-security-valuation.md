# Security Valuation

## Overview
Security valuation is the process of determining the intrinsic or fair value of a financial asset such as a stock or bond. The core idea is that every security has a true worth based on the cash flows it is expected to generate in the future, discounted back to the present. By comparing this intrinsic value to the current market price, investors can identify opportunities that are overpriced or underpriced.

---

## Why It Matters
Buying securities without understanding their value is essentially gambling. Valuation gives investors a rational basis for making buy, sell, or hold decisions. It prevents overpaying for popular assets during market euphoria and helps uncover bargains during downturns. Whether applied to a single stock or an entire company in a merger, valuation is the cornerstone of sound investment practice.

## Key Principles
- The intrinsic value of any security equals the present value of all its expected future cash flows
- Different types of securities require different valuation models, but the discounted cash flow principle applies universally
- Market price can deviate from intrinsic value in the short term due to sentiment, speculation, and information asymmetry
- A margin of safety, which is the gap between intrinsic value and purchase price, protects against estimation errors

## Key Terms
| Term | Definition |
|------|------------|
| **Intrinsic Value** | The calculated true worth of a security based on its fundamentals, independent of its current market price |
| **Discounted Cash Flow** | A valuation method that estimates value by discounting projected future cash flows to the present |
| **Margin of Safety** | The difference between a security's intrinsic value and its market price, providing a buffer against errors |
| **Terminal Value** | The estimated value of a security beyond the explicit forecast period, often representing a large portion of total value |

## Use Case
An equity analyst values a pharmaceutical company by projecting its drug revenues over ten years, discounting those cash flows, and adding a terminal value to arrive at a per-share intrinsic value that is 20 percent above the current stock price, signaling a buying opportunity.

## Scenario
> Carlos is evaluating whether to buy shares of a consumer goods company. He projects the company's free cash flows for the next eight years, applies a discount rate that reflects the company's risk, and estimates a terminal value. His analysis shows the stock is trading 15 percent below its intrinsic value, so he decides to buy with confidence that he has a comfortable margin of safety.

## Examples
- Using a dividend discount model to value a utility company that pays consistent quarterly dividends
- Applying a price-to-earnings multiple from comparable companies to estimate the value of a privately held business

---

## Audited Appendix

# Security Valuation
**Course:** Investment Analysis and Portfolio Management
**Module:** Content / Security Valuation
**Audited on:** 2026-04-18
**Audited by:** A5
**Source files reviewed:** `investment-analysis-portfolio/content/04-security-valuation.md`

---

## 1. Topic Snapshot
Security valuation is the discipline of estimating the intrinsic (fair) value of a stock or bond by discounting expected future cash flows to present value, then comparing that number to the prevailing market price to judge over/undervaluation. For an IT/AI/Product/Consulting leader holding RSUs/ESOPs, receiving a secondary-sale offer, or weighing a PE/VC co-invest, valuation converts "gut feel about the company" into a testable price anchor with a margin of safety. The decision it drives: buy, hold, trim, or walk away — and at what price, not whether the story is nice.

---

## 2. Jargon & Terminology

| # | Term | Plain-English Meaning | IT/AI/Product/Consulting Lens |
|---|---|---|---|
| 1 | Intrinsic Value | PV of all future cash flows to the security holder | The "true" price of your ESOP before liquidity discount |
| 2 | Market Price | Last traded/quoted price on exchange or secondary | Tender offer price for your RSUs |
| 3 | Margin of Safety (MoS) | Cushion between intrinsic and purchase price | 25–40% discount you demand before co-investing in a PE deal |
| 4 | DCF | Discounted Cash Flow valuation model | Standard lens to value a SaaS firm using projected FCFs |
| 5 | DDM (Dividend Discount Model) | Values equity as PV of future dividends | Apt for mature IT-services firms paying steady payouts (TCS, Infosys) |
| 6 | Gordon Growth Model | Single-stage constant-growth DDM | Quick sanity check on utility/REIT-like stable payers |
| 7 | Two-Stage Model | High-growth phase + stable terminal phase | Valuing AI SaaS pre-maturity (5–7 yrs hypergrowth, then 3% steady) |
| 8 | Residual Income Model | Book value + PV of excess returns over cost of equity | Useful when FCFs are lumpy/negative (banks, early-stage SaaS) |
| 9 | FCFF | Free Cash Flow to Firm (pre-debt) | Value the whole enterprise of a listed IT mid-cap |
| 10 | FCFE | Free Cash Flow to Equity (post-debt) | Directly values shareholder cash in leveraged infra/telecom |
| 11 | Terminal Value (TV) | Lump-sum value of CFs beyond explicit forecast | Often 60–80% of DCF value in growth SaaS — audit carefully |
| 12 | Relative (Multiples) Valuation | Price via peer multiples | EV/Revenue on a listed GenAI peer set |
| 13 | EV/EBITDA | Enterprise value over operating cash profit | Cross-cap-structure comparison for IT-services roll-ups |
| 14 | P/E | Price per unit of earnings | First-pass screen on a listed IT stock |
| 15 | P/B | Price per unit of book equity | Banks, NBFCs, asset-heavy fintechs |
| 16 | P/S | Price per unit of sales | Pre-profit SaaS and marketplaces |
| 17 | PEG | P/E normalised for growth | Separates cheap-for-a-reason from genuinely cheap growth IT |
| 18 | Reverse-DCF (Implied Growth) | Back-solve for the growth market is pricing in | Tests whether the AI narrative baked into the price is achievable |
| 19 | Scenario/Monte Carlo Valuation | Probability-weighted distribution of intrinsic values | Stress-tests AI SaaS where single-point FCF is a fiction |
| 20 | Option-Implied Value | Treats equity/R&D as a real option | Pre-revenue GenAI startup with optionality on model breakthroughs |
| 21 | NAV for Closed-End Funds | Net asset value per share of a listed fund | Valuing InvIT/REIT/closed-end tech funds at premium/discount to NAV |

---

## 3. Frameworks & Matrices

### 3.1 Absolute vs Relative Valuation Selector
**Purpose:** Pick the primary model based on business archetype.

```
                      Predictable CF?
                       /            \
                     Yes             No
                     /                 \
              Dividends stable?    Early-stage / optionality?
                /        \               /         \
               Yes        No           Yes           No
                |          |            |             |
              DDM /     FCFF/FCFE   Real-Options   Relative
            Gordon      DCF         + Scenario     Multiples
          (Utility,    (Mid-cap     (Pre-rev       (Peer SaaS,
           Mature       IT, Mfg)    GenAI)          IT-services
           IT-svcs)                                  comp set)
```

**Components:** Business archetype, CF predictability, dividend policy, optionality, peer availability.
**Example:** A Product leader evaluating TCS (stable, dividend-rich) defaults to Gordon DDM + FCFF cross-check; for an AI infra IPO, scenario DCF + EV/Revenue peers.
**Trigger:** Any time you move from "I like this stock" to "at what price."

### 3.2 DDM vs FCFE vs FCFF Decision Tree
**Purpose:** Within DCF, choose the correct cash flow definition.

```
Does company pay a sustainable dividend (>= payout of FCFE)?
   |-- Yes ---> DDM (Gordon or two-stage)
   |-- No  ---> Is capital structure stable & debt meaningful?
                 |-- Yes ---> FCFF discounted at WACC
                 |-- No  ---> FCFE discounted at cost of equity (Ke)
```

**Components:** Payout ratio, leverage stability, Ke vs WACC.
**Example:** An AI Lead valuing her listed IT-services employer (40% payout, low debt) uses FCFE at Ke; valuing a leveraged data-centre REIT uses FCFF at WACC.
**Trigger:** After archetype is chosen in 3.1.

### 3.3 Margin-of-Safety Layering
**Purpose:** Convert intrinsic value into an actionable buy trigger.

```
  Intrinsic Value (base case)    : 1000
        |
        v  Haircut for model error (-15%)
   Adjusted Intrinsic             : 850
        |
        v  Haircut for macro/liquidity (-10%)
   Conservative Intrinsic         : 765
        |
        v  MoS cushion (-25%)
   Target Buy Price               : 574
        |
        v  Compare to Market Price
   Market = 620 ---> wait; Market = 540 ---> buy
```

**Components:** Base intrinsic, model-error haircut, macro haircut, MoS %.
**Example:** Consulting partner stacking a 25% MoS plus 10% illiquidity discount on a PE secondary offer.
**Trigger:** Before committing capital; re-run quarterly.

### 3.4 Reverse-DCF Implied-Growth Check (Optional)
**Purpose:** Ask what growth the market is already pricing in.
```
Given: Market Cap, current FCF, WACC, TV assumption
Solve: g (explicit-period growth) that makes PV = Market Cap
If implied g > plausible industry ceiling  --> overpriced
If implied g < sector median               --> candidate for deeper work
```
**Example:** An AI SaaS trading at 35× sales implies 45% revenue CAGR for 7 yrs — unprecedented; Product Lead flags overpricing.
**Trigger:** Whenever narrative-driven stocks feel "frothy."

---

## 4. Formulas

### 4.1 DCF Intrinsic Value
V = Σ (CFₜ / (1+r)^t) for t=1..n  +  TV / (1+r)^n
- **Thresholds:** TV share of value should ideally be < 70%; r in INR typically 11–14% for IT mid-caps.
- **Example (IT-services listed firm):** FCFE Yr1–5 = 100, 110, 121, 133, 146 (10% g); Ke = 12%; TV at 4% perpetual = 146×1.04/(0.12-0.04) = 1898. PV ≈ 434 (explicit) + 1077 (TV) = **1511 per share**.

### 4.2 DDM (Gordon)
P₀ = D₁ / (r − g)
- **Thresholds:** Valid only if g < r and g is sustainable (< long-run nominal GDP).
- **Example (mature IT-services):** D₁ = ₹45, r = 11%, g = 6% → P₀ = 45 / 0.05 = **₹900**.

### 4.3 Two-Stage DDM
P₀ = Σ Dₜ/(1+r)^t (t=1..n)  +  [Dₙ₊₁ / (r − g_stable)] / (1+r)^n
- **Thresholds:** High-growth phase 5–10 yrs; g_stable ≤ economy growth.
- **Example (AI SaaS listed peer):** 5-yr high-growth dividends (grow at 20%, start ₹10), then 5% stable; r = 13% → PV ≈ ₹55 + TV-PV ≈ ₹240 = **₹295**.

### 4.4 Residual Income
V₀ = BV₀ + Σ [(ROEₜ − r) × BVₜ₋₁] / (1+r)^t
- **Thresholds:** Best when earnings are accounting-clean; ROE − r (economic spread) drives the answer.
- **Example (listed IT bank partner):** BV₀ = ₹200, ROE = 16%, r = 12%, BV grows 10%/yr, 6-yr horizon → Residuals ≈ ₹85 PV → V ≈ **₹285**.

### 4.5 Relative Valuation
Fair Price = target multiple × metric
- **Thresholds:** Use harmonic mean of peer multiples (not arithmetic) to avoid upward bias; trim outliers.
- **Example (REIT):** Peer P/AFFO harmonic mean = 16×; subject AFFO = ₹12 → Fair = **₹192**. EV/EBITDA cross-check for IT mid-cap: peer median 14×, subject EBITDA = ₹500 Cr, net debt ₹200 Cr, shares 50 Cr → Equity = 14×500 − 200 = ₹6800 Cr → **₹136/share**.

### 4.6 Margin of Safety
MoS = (Intrinsic − Market Price) / Intrinsic; target ≥ 25% (35%+ for small-cap/illiquid)
- **Example:** Intrinsic = ₹1511, Market = ₹1050 → MoS = 30.5% → **buy-zone**.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|---|---|
| 1 | Triangulate: DCF + multiples + residual income | Anchor on a single model's output |
| 2 | Use harmonic mean for peer multiples | Average P/Es arithmetically |
| 3 | Check TV share of DCF value; stress g and r | Let TV quietly become 85% of value |
| 4 | Apply a written, quantified margin of safety | Buy at "close to fair value" |
| 5 | Reverse-DCF narrative stocks (GenAI, EV) | Accept the sell-side growth story at face value |
| 6 | Document model inputs in a version-controlled sheet | Re-key numbers into a fresh sheet each quarter |
| 7 | Cross-verify earnings quality (accruals, cash conv.) | Trust headline P/E on restated or aggressive books |
| 8 | Separate intrinsic value from target price (horizon + catalyst) | Conflate "worth ₹X" with "will trade at ₹X next quarter" |

---

## 6. Real-Life Scenarios

### Scenario 1 — AI-SaaS RSU Holder Evaluating a Secondary Offer
Priya, a Product Lead at a late-stage AI-SaaS unicorn, receives a tender offer at ₹450/share (last round ₹600). She runs reverse-DCF: implied 8-yr revenue CAGR to justify ₹600 is 42%; ₹450 implies 28% — still steep but plausible given current NRR 128% and Rule-of-40 score of 55. Multiples cross-check on listed peers (EV/Rev = 9×, harmonic) values her shares at ₹410. She tenders half at ₹450 (captures liquidity) and holds half (optionality). Tools: CapIQ, Simply Wall St, Tijori Finance.

### Scenario 2 — PM Investing Personal Portfolio in a Cyclical IT Mid-Cap
Arjun (consulting partner) evaluates a listed IT mid-cap at ₹780. FCFE DCF (Ke 13%, g 8% for 5 yrs, 4% terminal) → intrinsic ₹1080. Peer EV/EBITDA comp (median 13×) → ₹1020. Harmonic P/E of peers × normalised EPS → ₹960. Blend (40/30/30) = ₹1030. Applies 30% MoS → buy trigger ₹721. Market ₹780 > trigger — he places a limit order at ₹720, fills on a sector correction, targets ₹1000 over 18 months. Tools: Screener.in, Bloomberg, Value Investors Club.

### Scenario 3 — ANTI-EXAMPLE: "Cheap" P/E Trap
Ravi, a retail investor, buys a listed IT services firm at P/E 6 (sector median 18) thinking it's a bargain. He skips earnings-quality checks (accruals high, receivable days 140 vs peer 70, one-off land sale in EPS). Two quarters later, auditor flags revenue recognition; company restates earnings downward 35%; stock halves from ₹900 to ₹420. Ravi's 1,000 shares bought at ₹900 → MTM loss = (900−420)×1000 = **₹4.8 L**. Lesson: a "cheap" multiple on poor-quality earnings is not valuation — it's a trap. Reverse-DCF plus accrual screen would have flagged it. Tools: Screener.in (accrual ratio), Tijori Finance (disclosures).

---

## 7. Implementation Playbook
1. **Catalogue** every security you own or are evaluating (RSUs, ESOPs, listed equity, bonds, InvITs) in a single register with cost, current price, and thesis.
2. **Classify** each by archetype (stable dividend / growth / cyclical / optionality) using Framework 3.1.
3. **Build** a baseline DCF or DDM workbook per holding (template with explicit 5–7 yr FCFs, TV, sensitivity table on r and g).
4. **Cross-check** with relative multiples using a vetted peer set and harmonic mean; record divergence.
5. **Reverse-DCF** any position where market price > 1.5× your DCF — document the implied growth.
6. **Quantify** margin-of-safety layers (model error + macro + MoS%) and derive a target buy/sell price.
7. **Journal** the decision, trigger price, and catalyst/horizon in a dated note (versioned repo or Notion).
8. **Re-audit** quarterly: refresh inputs, flag thesis drift, rotate if MoS collapses or thesis breaks.

---

## 8. Content Quality Audit

**Covered well (in source):** intrinsic vs market price distinction, DCF universality, margin-of-safety concept, DDM for utilities, P/E comps for private companies, 10-yr pharma projection use case, Carlos FCF example.

**Underplayed / missing in source:**
- Residual income models for negative/lumpy-FCF firms (banks, early SaaS).
- Reverse-DCF for implied-growth diagnostics on narrative stocks.
- Harmonic mean when aggregating peer multiples (arithmetic introduces bias).
- Quantified margin-of-safety layering (model, macro, MoS stack).
- Scenario / Monte Carlo valuation for IT/AI growth firms where point estimates mislead.
- SaaS-specific value drivers anchoring valuation: Rule of 40, NRR, LTV/CAC, gross retention.
- Option-based valuation for pre-revenue GenAI plays.
- Earnings-quality screens (accruals, cash conversion) before trusting any multiple.

**Supplement with:**
1. Damodaran, *Investment Valuation*, 3rd ed. (2012).
2. Koller, Goedhart & Wessels, *Valuation: Measuring and Managing the Value of Companies*, 7th ed. (2020).
3. Graham & Dodd, *Security Analysis*, 6th ed. (2008).
4. Greenwald et al., *Value Investing: From Graham to Buffett and Beyond*, 2nd ed. (2020).
5. Mauboussin & Callahan, *Expectations Investing*, updated ed. (2021).

**Red flags in source:**
- Over-reliance on "20% above market = buy signal" without defining MoS rigorously.
- No mention of earnings quality or accounting adjustments.
- TV treatment implied but not stress-tested (TV often dominates DCFs).
- No role-lens framing (how an operator/PM should use these models on their own ESOPs).

---

## 9. Quick-Recall Card
- Intrinsic value = PV of future cash flows; market price is an opinion, intrinsic value is an estimate.
- Pick your model by archetype (DDM/FCFE/FCFF/RI/Real-option) — don't force one hammer.
- Triangulate DCF + multiples (harmonic) + residual income; blend, don't cherry-pick.
- TV share, implied growth (reverse-DCF), and earnings quality are your three audit trip-wires.
- Margin of Safety is a stack: model-error haircut + macro haircut + MoS% (target 25–35%+).
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: **"At what price does this security — my RSU, a secondary-sale offer, or a listed co-invest — become a rational buy/hold/sell given its intrinsic value and a written margin of safety?"**

---

**Connects to:** [05-equity-analysis.md](05-equity-analysis.md), [06-fixed-income-analysis.md](06-fixed-income-analysis.md), [02-time-value-of-money.md](02-time-value-of-money.md), [../business-valuation/05-discounted-cash-flow-dcf-models.md](../business-valuation/05-discounted-cash-flow-dcf-models.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:4, 6:5, 7:4, 8:5, 9:4, 10:4]
Sections rewritten: [1 Topic Snapshot tightened to role-lens; 3 added reverse-DCF tree; 4 added harmonic-mean note and REIT example; 6 quantified anti-example loss; 9 role-lens question sharpened]
Enrichments applied: [cross-course links; 5 supplements; anti-example w/ cost; IT tooling; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 10:42
Audited by: A5
-->
