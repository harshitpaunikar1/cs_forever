# Fixed-Income Analysis

## Overview
Fixed-income analysis is the study of bonds and other debt securities to assess their value, risk, and suitability for an investment portfolio. Bonds pay periodic interest and return the principal at maturity, making them attractive to investors who want predictable income. Analysts evaluate credit quality, interest rate sensitivity, and yield to determine whether a bond is fairly priced.

---

## Why It Matters
Bonds form the backbone of most institutional portfolios and play a critical role in retirement planning, capital preservation, and income generation. Understanding how bonds are priced and how their values change with interest rates is essential for managing risk. Poor fixed-income analysis can lead to losses from credit defaults or unexpected rate movements that erode portfolio value.

## Key Principles
- Bond prices move inversely to interest rates: when rates rise, existing bond prices fall, and vice versa
- Credit risk reflects the likelihood that the bond issuer will fail to make promised payments
- Duration measures a bond's sensitivity to interest rate changes, with longer-duration bonds being more volatile
- Yield to maturity captures the total expected return if a bond is held until it matures, accounting for coupon payments and any price gain or loss

## Key Terms
| Term | Definition |
|------|------------|
| **Yield to Maturity** | The total annual return an investor earns if a bond is held until maturity, factoring in coupon payments and price difference |
| **Duration** | A measure of a bond's price sensitivity to changes in interest rates, expressed in years |
| **Credit Rating** | An assessment by agencies like Moody's or S&P of the likelihood that a bond issuer will meet its obligations |
| **Coupon Rate** | The annual interest rate paid by the bond issuer, expressed as a percentage of the bond's face value |

## Use Case
A treasury manager at a corporation invests surplus cash in a ladder of short-term investment-grade bonds, using duration analysis to ensure the portfolio's value remains stable while generating income above what a savings account would provide.

## Scenario
> David manages a small endowment fund and is concerned about rising interest rates. He reviews the duration of every bond in his portfolio and finds that several long-term government bonds have high duration, meaning they will lose significant value if rates increase. He shifts a portion of the allocation into shorter-duration corporate bonds to reduce the portfolio's overall interest rate sensitivity while maintaining a reasonable yield.

## Examples
- Comparing the yield to maturity of a corporate bond rated BBB with a government bond to assess whether the credit spread compensates for the additional default risk
- Using duration matching to align a pension fund's bond portfolio with its future liability payments so that interest rate movements affect both sides equally

---

## Audited Appendix

# Fixed-Income Analysis
**Course:** Investment Analysis and Portfolio Management
**Module:** Content / Fixed-Income Analysis
**Audited on:** 2026-04-18
**Audited by:** A7
**Source files reviewed:** `investment-analysis-portfolio/content/06-fixed-income-analysis.md`

---

## 1. Topic Snapshot
Fixed-income analysis is the disciplined valuation of bonds and debt securities by decomposing cash flows into yield, duration, convexity and credit-risk components so an investor knows what they own, what drives mark-to-market swings, and what the held-to-maturity return actually is.
For an IT/AI/Product/Consulting leader wearing the hat of a corporate treasurer, post-exit founder, or HNI saver, bonds are the backbone of capital preservation and income — a wrong call on duration or credit quality quietly erodes real wealth far more than a missed equity rally.
The decision: given my liability schedule and rate view, what mix of maturities, issuers and instruments (gilts, AAA PSU, AA corporate, inflation-linked, SGBs) hits the target duration and expected-loss budget?

---

## 2. Jargon & Terminology

| # | Term | One-line Definition | Why it matters to IT/AI/Product/Consulting leader |
|---|------|---------------------|---------------------------------------------------|
| 1 | Coupon Rate | Fixed % of par paid periodically as interest | Headline cash yield on ESOP-proceeds parked in bonds |
| 2 | Face / Par Value | Principal repaid at maturity (typ. ₹1,000 / ₹1L) | Anchor for coupon and redemption maths |
| 3 | Maturity | Date principal is returned | Aligns bond to liability horizon (e.g., kid's college in 7 yrs) |
| 4 | YTM (Yield to Maturity) | IRR if held to maturity, coupons reinvested at YTM | Single-number comparison across bonds |
| 5 | YTW (Yield to Worst) | Lowest yield across all call/put scenarios | Use this, not YTM, for callable bonds |
| 6 | YTC (Yield to Call) | Yield if bond is called at first call date | Relevant for callable AT1/perpetual bank bonds |
| 7 | Current Yield | Annual coupon / current price | Quick cash-on-cash check, ignores capital gain/loss |
| 8 | Running Yield | Synonym for current yield in UK/India usage | Used in CCIL screens |
| 9 | Credit Rating | Issuer default grade (AAA→D; Moody's / S&P / Fitch / CRISIL / CARE / ICRA) | Screens out names below mandate threshold |
| 10 | Credit Spread | Corporate YTM − risk-free YTM (same maturity) | Compensation for default + liquidity risk |
| 11 | Macaulay Duration | Weighted-average time to cash flows (years) | Intuitive "average life" concept |
| 12 | Modified Duration | Macaulay/(1+y); % price change per 1% yield move | Key lever for rate-risk sizing |
| 13 | Effective Duration | Numerical duration allowing for embedded options | Correct measure for callables/MBS |
| 14 | Convexity | Second-derivative correction to duration estimate | Captures curvature; matters for large Δy |
| 15 | DV01 | Dollar (₹) value of 1 bp yield change | Treasury desk's P&L-per-bp number |
| 16 | Interest-Rate Risk | MTM loss when yields rise | Dominant risk on long-duration gilts |
| 17 | Credit Risk | Probability of issuer default / downgrade | Dominant risk on HY / AA- and below |
| 18 | Reinvestment Risk | Coupons reinvested at lower future yields | Hurts bullet strategies in falling-rate regimes |
| 19 | Call Risk | Issuer calls bond when rates fall | Caps upside on callables; use YTW |
| 20 | Liquidity Risk | Wide bid-ask / inability to exit at fair value | Chronic in Indian corporate bond secondary market |
| 21 | Inflation-Linked (TIPS / SGB) | Principal/coupon indexed to CPI or gold | Protects real purchasing power |
| 22 | Zero-Coupon Bond | No coupons; issued at discount to par | Cleanest duration exposure; tax quirks in India |
| 23 | Callable / Puttable Bond | Embedded issuer call / investor put option | Must price with OAS, not plain YTM |
| 24 | OAS (Option-Adjusted Spread) | Spread after stripping embedded-option value | True credit compensation on callables |
| 25 | Credit Migration Risk | Rating downgrade (not default) causing MTM loss | Silent killer in AA → A transitions |
| 26 | Expected Loss | PD × LGD × EAD | Credit-budget framework for portfolio |

---

## 3. Frameworks & Matrices

### 3.1 Bond Risk Stack
**Purpose:** Enumerate every risk a bondholder absorbs so none is implicitly priced at zero.

```
+-----------------------------------------------------------+
|  INFLATION RISK        (real return erosion)              |
+-----------------------------------------------------------+
|  LIQUIDITY RISK        (exit slippage, wide spreads)      |
+-----------------------------------------------------------+
|  CALL / PREPAY RISK    (issuer optionality)               |
+-----------------------------------------------------------+
|  REINVESTMENT RISK     (coupon reinvested at lower y)     |
+-----------------------------------------------------------+
|  CREDIT / DEFAULT RISK (PD x LGD x EAD)                   |
+-----------------------------------------------------------+
|  INTEREST-RATE RISK    (duration x Delta-y)               |
+-----------------------------------------------------------+
         ^ base layer — present in every bond
```
**Components:** six stacked layers, each with its own hedge (duration match, credit limits, covenants, ladder, reserve liquidity, linkers).
**IT/AI/Product/Consulting worked example:** SaaS CFO parking ₹300 cr pre-IPO cash — checks all 6 layers before approving AA NBFC paper; vetoes due to liquidity + migration risk concentration.
**Trigger:** any new bond mandate, annual IPS review, rate-regime change.

### 3.2 Duration–Convexity Diagram
**Purpose:** Estimate MTM price change for a given yield shock using a 2nd-order Taylor expansion.

```
  Price
   |      *   actual price curve (convex)
   |    *  .
   |   *     .    <-- convexity gap
   |  *        .
   | *  .........   duration-only line (tangent)
   |*   .
   +----+------------> Yield
        y0
   DeltaP/P  ~=  - ModDur * Delta-y  +  0.5 * Convexity * (Delta-y)^2
```
**Components:** tangent slope = −ModDur; curvature correction = ½·C·(Δy)².
**IT/AI/Product/Consulting worked example:** Product leader with ₹5 cr in a 10-yr gilt (ModDur 7.3, Conv 68). +150 bps shock → duration term = −10.95%; convexity term = +0.77%; net ≈ −10.18% MTM. Enough to rethink duration.
**Trigger:** any yield shock > 50 bps, stress-test cycle.

### 3.3 Bond Ladder / Barbell / Bullet Strategy Selector

```
Ladder:   [1y][2y][3y][4y][5y]  — equal weights, staggered maturity
Barbell:  [1y][1y]........[10y][10y]  — short + long, no mid
Bullet:   .......[5y][5y][5y]........  — concentrated at target horizon
```

| Strategy | Best when | Rate view | Reinvestment risk | Convexity |
|----------|-----------|-----------|-------------------|-----------|
| Ladder | Income + liquidity, no rate view | Neutral | Low | Medium |
| Barbell | Expect flattening / volatility | Shift expected | Medium | High |
| Bullet | Funding a known liability date | Neutral | High | Low |

**IT/AI/Product/Consulting worked example:** Consulting-partner's ₹8 cr retirement corpus — bullet around 2035 college-fee liability; barbell for surplus to harvest convexity.
**Trigger:** IPS refresh, liability-driven investing review.

### 3.4 (Optional) Credit Spread Analysis — Rating × Sector

```
Spread (bps)   AAA    AA    A    BBB    BB
----------------------------------------------
Sovereign       0     —     —    —      —
PSU            25    45    80   —      —
Private Fin    40    70   120   220    450
NBFC           55   100   180   320    600
```
Use to spot rich/cheap pockets; e.g., AA NBFC at 100 bps looks tight vs historical 140 bps median.

---

## 4. Formulas

1. **Bond Price** P = Σ_{t=1..n} C/(1+y)^t + F/(1+y)^n
   *Threshold:* if market price > P at coupon rate → bond trades at premium (y < c).
   *Example:* 5-yr AA corporate, C = ₹78/yr on ₹1,000 par, y = 7.8% → P ≈ ₹1,000 (par).

2. **Modified Duration** ModDur ≈ −(1/P) · dP/dy  = Macaulay/(1+y)
   *Threshold:* treasury cap 3–4 yrs; pension LDI 10–15 yrs matched to liabilities.
   *Example:* Macaulay 4.5 yrs, y = 7.8% → ModDur = 4.5/1.078 ≈ 4.17.

3. **Convexity** C = (1/P) · d²P/dy²
   *Threshold:* higher-convexity bonds command lower yield — check you're not overpaying.
   *Example:* 5-yr bullet C ≈ 22; 10-yr zero C ≈ 95.

4. **Approximate Price Change %** ΔP/P ≈ −ModDur·Δy + ½·C·(Δy)²
   *Example (corporate treasury):* 5-yr AA, 7.8% YTM, ModDur 4.2, C 22; +100 bps shock → −4.2% + 0.5·22·(0.01)² = −4.2% + 0.11% ≈ **−4.09%** MTM.

5. **Credit Spread** CS = YTM_corp − YTM_govt (same maturity)
   *Threshold:* historical median ± 1σ defines "rich/cheap".
   *Example:* 5-yr AA corporate YTM 7.8% − 5-yr G-Sec 7.05% = **75 bps** spread.

6. **Expected Loss (credit)** EL = PD × LGD × EAD
   *Threshold:* set per-issuer EL cap (e.g., 5 bps of portfolio).
   *Example:* ₹10 cr AA exposure, PD 0.6%, LGD 55% → EL = 0.006·0.55·10 cr = **₹3.3 lakh**/yr.

7. **DV01** DV01 = ModDur · P · 0.0001
   *Example:* ₹100 cr at ModDur 4.2 → DV01 = ₹4.2 lakh per bp. A 25 bp move = ₹1.05 cr.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|-----|-------|
| 1 | Match portfolio duration to liability horizon | Don't chase yield by extending duration when liabilities are short |
| 2 | Use YTW, not YTM, on callable/perpetual bonds | Don't quote YTM on an AT1 as if it were a bullet bond |
| 3 | Compute EL (PD×LGD×EAD) and cap it at issuer level | Don't rely solely on rating labels — watch migration |
| 4 | Stress-test +200 / −200 bps on the whole book | Don't ignore convexity on shocks > 100 bps |
| 5 | Track credit spread vs historical distribution | Don't buy AA paper when spreads are 1σ tight |
| 6 | Build a ladder for income + liquidity needs | Don't park emergency cash in illiquid 10-yr corporates |
| 7 | Read the prospectus: call, put, covenants, seniority | Don't assume secondary-market liquidity will exist in India |
| 8 | Use inflation-linked (SGB / linkers) for real-return goals | Don't assume nominal 7% beats 6% inflation comfortably |
| 9 | Reconcile accrued interest & dirty vs clean prices | Don't compare clean prices while ignoring accrual timing |

---

## 6. Real-Life Scenarios

### Scenario 1 — Tech firm's ₹500 cr treasury ladder
A listed-SaaS CFO (post-QIP cash) builds a 1-3-5-year ladder of AAA PSU bonds (REC, PFC, NHAI), ₹100 cr in each of years 1, 2, 3, 4, 5. Weighted ModDur target = 2.5 yrs, which caps a 100 bp shock to ≈ −2.5% MTM (~₹12.5 cr). Annual maturity rolls create liquidity without forced sales. Credit-spread pickup vs G-Sec ≈ 35 bps → ₹1.75 cr extra annual yield at zero meaningful default risk.

### Scenario 2 — Post-exit founder, real-purchasing-power ladder
Founder exits a product startup, nets ₹45 cr, reduces equity from 80% to 45%. Builds fixed-income sleeve: 40% 3–7 yr AAA corporates + PSU (core income), 25% gilts 10-yr (rate hedge + convexity), 20% Sovereign Gold Bonds (inflation + rupee-depreciation hedge), 15% TIPS-equivalent via RBI inflation-indexed bonds. Portfolio ModDur ≈ 5.5; expected real return ≈ 2.5–3% over CPI. Rebalanced annually on 50 bp moves or rating migration.

### Scenario 3 — ANTI-EXAMPLE: duration-reach blow-up
A corporate treasurer, under pressure to beat FD rates, parks ₹100 cr surplus in 15-yr BB+ high-yield paper for an extra 150 bps (YTM 9.3% vs 7.8% on 3-yr AAA). ModDur ≈ 9.1, Convexity ≈ 105. Rate-hike cycle delivers +200 bps over 18 months. Price change ≈ −9.1·0.02 + 0.5·105·(0.02)² = −18.2% + 2.1% = **−16.1%**. MTM loss ≈ **₹16.1 cr** on a ₹100 cr book — wipes out 10+ years of the 150 bp "extra yield" (₹1.5 cr/yr). Board orders IPS rewrite capping duration at 3 yrs and rating at AA.

**Tools:** Bloomberg FIXI, CCIL NDS-OM (India), NSE / BSE debt-market terminals, ICRA / CRISIL / CARE credit-research portals, Zerodha Fixed-Income / GoldenPi / IndiaBonds for retail, bond-ladder calculators, RBI Retail Direct for gilts & SGBs.

---

## 7. Implementation Playbook

1. **Draft** a Fixed-Income Investment Policy Statement (IPS): allowed ratings, max ModDur, issuer caps, liquidity buckets.
2. **Map** liabilities (payroll 1y, tax 1y, capex 3y, dividends 1y) to required cash-flow dates → target duration & ladder shape.
3. **Screen** universe on CCIL/Bloomberg: rating ≥ AA, residual maturity ≤ cap, liquidity score, YTW (not YTM).
4. **Compute** per-bond and portfolio-level ModDur, convexity, DV01, EL (PD·LGD·EAD); store in a `portfolio.xlsx` / `pandas` notebook.
5. **Stress-test** book with ±100 / ±200 bp parallel shifts and a 2x-credit-spread-widening scenario; document MTM tolerance.
6. **Execute** via primary auction (gilts, SGBs) or secondary market; reconcile clean vs dirty price and accrued interest.
7. **Monitor** rating actions, spread moves > 25 bps, and covenant triggers in a weekly Slack/Notion digest.
8. **Rebalance** quarterly or on IPS breach; maturing rungs rolled to new 5-yr rung to preserve ladder shape.

---

## 8. Content Quality Audit

**Covered well:** bond pricing inverse to rates, YTM, duration intuition, credit rating, ladder concept, spread vs gilts.

**Underplayed / missing in source:**
- Convexity as a second-order correction beyond duration.
- OAS for embedded-option bonds (callables, AT1, MBS).
- Expected-loss (PD × LGD × EAD) as a credit-budget framework.
- Inflation-linked mechanics (TIPS / RBI IIBs) and real-yield construct.
- Sovereign Gold Bond treatment as a rupee-and-inflation hedge with tax quirks.
- Credit migration risk (downgrade-driven MTM loss, not just default).
- Liquidity discount embedded in Indian corporate-bond secondary-market pricing.
- YTW vs YTM distinction for callable/perpetual bank capital.

**Supplementary sources (≥5):**
1. Fabozzi, *The Handbook of Fixed Income Securities*, 9th ed., 2021.
2. Choudhry, *Bond and Money Markets: Strategy, Trading, Analysis*, 2nd ed., 2022.
3. Bodie, Kane, Marcus, *Investments*, 12th ed., 2020 — chapters on fixed income.
4. Ilmanen, *Expected Returns*, 2nd ed., 2022 — bond-risk-premium chapters.
5. CFA Institute, *Fixed Income* readings, 2024 curriculum (L1–L3).
6. RBI *Handbook of Statistics on the Indian Economy* & CCIL *Factbook* (2024) for India-specific data.

**Red flags:**
- Quoting YTM on callables without adjusting for call optionality.
- Ignoring convexity on shocks >100 bps → under-estimated losses.
- Assuming secondary-market exit for AA corporate bonds in India.
- Treating rating as static — no migration-risk reserve.
- Confusing nominal yield with real yield when inflation > 5%.

---

## 9. Quick-Recall Card
- Bond price = PV of coupons + PV of par; moves inversely to yield.
- ModDur sizes rate risk; convexity is the curvature correction.
- ΔP/P ≈ −ModDur·Δy + ½·C·(Δy)² — memorise this one line.
- Credit risk = PD × LGD × EAD; migration, not just default, bites.
- Use ladders for income, barbells for convexity, bullets for known liabilities.
- **As a PM/Consultant/AI Lead, the one question to answer with this framework is: "Given my liability schedule and rate view, does my bond book's duration and expected-loss budget match what I can actually tolerate in a +200 bps, 1-notch-downgrade stress?"**

---

**Connects to:** [02-time-value-of-money.md](02-time-value-of-money.md), [03-risk-return-fundamentals.md](03-risk-return-fundamentals.md), [09-portfolio-construction-diversification.md](09-portfolio-construction-diversification.md), [../financial-management/](../financial-management/).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:4, 6:5, 7:4, 8:5, 9:4, 10:4]
Sections rewritten: [1 Snapshot tightened; 3 added credit-spread matrix; 4 added DV01; 6 sharpened anti-example maths; 9 role-lens question]
Enrichments applied: [cross-course links; 6 supplements incl. RBI/CCIL; anti-example with ₹16.1 cr cost; IT tooling (Bloomberg/CCIL/Zerodha/RBI Retail Direct); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 11:20
Audited by: A7
-->
