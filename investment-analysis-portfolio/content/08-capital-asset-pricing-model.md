# Capital Asset Pricing Model

## Overview
The Capital Asset Pricing Model, commonly known as CAPM, is a formula that describes the relationship between systematic risk and expected return for an investment. It states that the expected return of an asset equals the risk-free rate plus a premium for bearing market risk, where that premium is proportional to the asset's beta. CAPM provides a benchmark for evaluating whether an investment is offering adequate compensation for its risk.

---

## Why It Matters
CAPM gives investors and companies a simple, widely used tool for estimating the return they should expect from an investment given its level of market risk. Corporate finance teams use it to determine the cost of equity capital, which feeds into decisions about whether to pursue new projects. Portfolio managers use it to judge whether a stock is overvalued or undervalued relative to its risk. Despite its simplifying assumptions, CAPM remains one of the most influential models in finance.

## Key Principles
- Only systematic risk is rewarded with higher expected returns because unsystematic risk can be diversified away
- Beta measures how sensitive an asset's returns are to movements in the overall market
- The security market line plots expected return against beta, and fairly priced assets should fall on this line
- Assets plotting above the security market line are undervalued and those below it are overvalued, according to the model

## Key Terms
| Term | Definition |
|------|------------|
| **Beta** | A measure of an asset's volatility relative to the overall market, where a beta of one means the asset moves in line with the market |
| **Risk-Free Rate** | The return on an investment with zero risk, typically represented by short-term government treasury bills |
| **Market Risk Premium** | The additional return investors expect for holding a risky market portfolio instead of risk-free assets |
| **Security Market Line** | A graphical representation of the CAPM showing the expected return for any level of systematic risk |

## Use Case
A corporate finance team uses CAPM to calculate the cost of equity for a capital budgeting decision, determining that a new manufacturing plant must generate at least a 10 percent return to justify the investment given the company's beta and current market conditions.

## Scenario
> Raj is evaluating a tech stock with a beta of 1.4. Using CAPM with a risk-free rate of 3 percent and a market risk premium of 6 percent, he calculates that the stock should deliver an expected return of 11.4 percent. Since the stock's current valuation implies a return of only 9 percent, Raj concludes it is overpriced relative to its risk and decides not to buy.

## Examples
- A venture capital firm adjusting its required rate of return upward for a startup investment because startups have very high betas relative to the market
- An index fund manager using CAPM to explain to clients why the fund's return closely tracks the risk-free rate plus the market risk premium, since the fund's beta is approximately one

---

## Audited Appendix

# Capital Asset Pricing Model
**Course:** Investment Analysis and Portfolio Management
**Module:** Content / Capital Asset Pricing Model
**Audited on:** 2026-04-18
**Audited by:** A9
**Source files reviewed:** `investment-analysis-portfolio/content/08-capital-asset-pricing-model.md`

---

## 1. Topic Snapshot
CAPM (Sharpe 1964) is a single-factor pricing model stating that an asset's expected return equals the risk-free rate plus beta times the equity risk premium, rewarding only systematic (non-diversifiable) risk. An IT/AI/Product/Consulting leader uses CAPM to set equity hurdle rates, compute cost of equity feeding WACC for capital budgeting (e.g., approving a new data-center or AI-platform build), and to screen whether listed peers trade above or below the Security Market Line. The decision: fund, reject, or reprice a project/stock based on whether expected return compensates for its market-risk beta.

---

## 2. Jargon & Terminology

| # | Term | Definition | IT/AI/Product/Consulting Use |
|---|------|------------|------------------------------|
| 1 | CAPM | E(R) = Rf + β·(Rm − Rf) | Cost of equity for SaaS capex cases |
| 2 | Beta (Raw) | OLS slope of stock vs market returns, unadjusted | Starting point for listed IT majors |
| 3 | Adjusted Beta | Blume/Bloomberg: 0.67·raw + 0.33·1 | Regression-to-mean for volatile AI stocks |
| 4 | Industry Beta | Average β of comparable listed firms | Used when firm-level β is unstable |
| 5 | Bottom-Up Beta | Unlever industry β, relever at target firm D/E | Private AI-startup valuation |
| 6 | Risk-Free Rate (Rf) | 10-yr sovereign yield (e.g., G-Sec ~7% in India) | Anchor for INR hurdle rates |
| 7 | Market Risk Premium / ERP | E(Rm) − Rf; historical or implied | Damodaran India ERP ~7.5% (2024) |
| 8 | Security Market Line (SML) | Plot of E(R) vs β; slope = ERP | Visual over/undervalued screen |
| 9 | Alpha (α) | Return in excess of CAPM prediction | PM skill measurement |
| 10 | Jensen's Alpha | R_actual − CAPM expected | ETF/active-fund evaluation |
| 11 | Unlevered Beta (Asset β) | β stripped of financial leverage | Cross-firm business-risk comparison |
| 12 | Levered Beta | Asset β re-geared to firm's D/E | Target capital structure modelling |
| 13 | Hamada Equation | β_L = β_U·[1+(1−t)·D/E] | Relever betas in LBO/WACC models |
| 14 | Country Risk Premium | Sovereign-spread add-on for EM | Indian subsidiary of US MNC |
| 15 | International CAPM | Global market index + currency factor | Cross-border AI M&A |
| 16 | Fama-French 3-Factor | Market + SMB + HML | Adds size + value to CAPM |
| 17 | Fama-French 5-Factor | + RMW (profitability) + CMA (investment) | Quality/profitability tilt |
| 18 | Carhart Momentum | 4th factor: UMD (up-minus-down) | Momentum ETF attribution |
| 19 | Arbitrage Pricing Theory (APT) | Multi-factor, no-arbitrage alternative | Macro-factor portfolios |
| 20 | Characteristic Line | Regression line of stock vs market | β = slope, α = intercept |
| 21 | Treynor Ratio | (R_p − Rf)/β_p | Systematic-risk-adjusted performance |
| 22 | Idiosyncratic Risk | Firm-specific, diversifiable | Not priced in CAPM |

---

## 3. Frameworks & Matrices

### 3.1 Security Market Line (SML) Diagram
**Purpose:** Visualise fair pricing of assets given their β.
```
Expected Return
   |
15%|                          * Stock U (undervalued)
   |                      ___/
12%|                __---/    . SML (slope = ERP)
   |          __---/  . Stock F (fair)
 9%|    __---/ . Stock O (overvalued, below line)
   |---/
 7%|Rf
   +----+----+----+----+----> Beta
       0.5  1.0  1.5  2.0
```
**Components:** intercept = Rf; slope = ERP; each asset plotted at (β, expected return).
**IT/AI example:** Indian IT-services co with β=0.9, Rf=7%, ERP=7% → SML expected 13.3%. Market prices 15% → above SML → undervalued, Buy.
**Trigger:** Any equity pitch, hurdle-rate setting, or active-fund dispersion review.

### 3.2 CAPM Build-Up Block
**Purpose:** Stack premia to derive cost of equity.
```
+-----------------------------+
| Size Premium (small-cap)    | +2.0%
+-----------------------------+
| Country Risk Premium (IN)   | +1.5%
+-----------------------------+
| Beta × ERP (1.2 × 6.5%)     | +7.8%
+-----------------------------+
| Risk-Free Rate (10-yr G-Sec)| +7.0%
+-----------------------------+
  => Cost of Equity ≈ 18.3%
```
**Components:** Rf, β·ERP, optional size/country/illiquidity adjustments.
**IT/AI example:** Mid-cap Indian AI-SaaS, β=1.2 bottom-up, adds 2% size + 1.5% country → Ke ≈ 18.3%.
**Trigger:** WACC build for DCF or board hurdle-rate approval.

### 3.3 CAPM vs Fama-French 3/5 Comparison
| Dimension | CAPM | FF 3-Factor | FF 5-Factor |
|-----------|------|-------------|-------------|
| Factors | Market | Market + SMB + HML | + RMW + CMA |
| Risk captured | Systematic only | + Size + Value | + Profitability + Investment |
| ERP decomposition | Single premium | Three premia | Five premia |
| Typical R² (US) | 0.70 | 0.90 | 0.93 |
| Best for | Quick hurdle rate | Smart-beta funds | Quality/value tilts |

**IT/AI example:** Evaluating a small-cap Indian AI stock: CAPM Ke=16%; FF3 adds +2% SMB, −1% HML (growth) → 17%. Material gap for capex NPV.
**Trigger:** When single-factor β explains too little cross-sectional return.

### 3.4 Bottom-Up Beta Estimation Workflow
```
Step 1: Pick 6-10 listed comparables (e.g., Palantir, C3.ai, Fractal-peers)
Step 2: Pull raw β (2-5 yr weekly) from Bloomberg / Yahoo
Step 3: Unlever each: β_U = β_L / [1+(1−t)·D/E]
Step 4: Median β_U across set
Step 5: Relever at target firm's D/E and tax rate
Step 6: Apply in CAPM
```
**Trigger:** Private / recently-listed / thinly-traded firms where direct β is noisy.

---

## 4. Formulas

### 4.1 CAPM
**E(R) = Rf + β · (E(Rm) − Rf)**
Threshold: Ke should exceed Rf by at least ERP·β; negative premium ⇒ reject.
**Example (Indian AI-SaaS):** β=1.3, Rf=7%, ERP=6.5% → Ke = 7% + 1.3·6.5% = **15.45%**.

### 4.2 Beta
**β = Cov(R_i, R_m) / Var(R_m)**
Threshold: β>1 = more volatile than market; β<1 = defensive.
**Example:** Cov=0.0039, Var(Nifty)=0.003 → β=1.3.

### 4.3 Hamada Equation
**β_L = β_U · [1 + (1 − t) · D/E]**
Threshold: Higher leverage ⇒ higher levered β ⇒ higher Ke.
**Example:** β_U=0.9, t=25%, D/E=0.5 → β_L = 0.9·[1+0.75·0.5] = **1.24**.

### 4.4 Jensen's Alpha
**α = R_actual − [Rf + β·(Rm − Rf)]**
Threshold: α>0 = outperformed risk-adjusted benchmark.
**Example:** Fund returned 17%, CAPM expected 15.45% → α = **+1.55%** (positive skill).

### 4.5 Treynor Ratio
**T = (R_p − Rf) / β_p**
Threshold: Higher = better systematic-risk-adjusted return; compare vs benchmark T.
**Example:** R_p=17%, Rf=7%, β_p=1.3 → T = (10)/1.3 = **7.69**.

### 4.6 Fama-French 3-Factor
**R_i − Rf = α + β₁(Rm−Rf) + β₂·SMB + β₃·HML + ε**
Threshold: Significant β₂/β₃ reveals size/value tilt not captured by CAPM.
**Example:** For Indian mid-cap AI stock, β₁=1.1, β₂=0.4 (SMB=4%), β₃=−0.3 (HML=3%) → Expected excess = 1.1·6.5 + 0.4·4 − 0.3·3 = **7.25% + 1.6 − 0.9 = 7.95%** over Rf ⇒ Ke ≈ 14.95%.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|----|-------|
| 1 | Use 2–5 yr weekly β for stability | Don't use 1-yr daily β on volatile tickers |
| 2 | Apply Blume/Vasicek adjustment to raw β | Don't assume raw β = true β |
| 3 | Use bottom-up β for private / thin-trading firms | Don't use a noisy direct β blindly |
| 4 | Match Rf tenor to cash-flow horizon (10-yr for long projects) | Don't mix 91-day T-bill with 10-yr DCF |
| 5 | Use implied/forward ERP for current valuations | Don't anchor only on historical 1920– average |
| 6 | Add country risk premium for EM subsidiaries | Don't use pure US-ERP for Indian asset |
| 7 | Cross-check with FF3/FF5 for small/value tilts | Don't ignore size premium for micro-caps |
| 8 | Relever β at target capital structure (Hamada) | Don't apply peer levered β without adjusting D/E |
| 9 | Document every input and source (Damodaran, Bloomberg) | Don't round β and ERP silently |

---

## 6. Real-Life Scenarios

### Scenario 1 — IT-services hurdle rate
A Tier-1 Indian IT firm sets its equity hurdle using CAPM: β=1.0 (industry), Rf=7%, ERP=7% → Ke=14%. The board rejects any internal AI-platform project whose risk-adjusted IRR is below 14%. A proposed genAI delivery tool projects 12% IRR → rejected; team asked to rescope scope/pricing.

### Scenario 2 — AI-thematic ETF evaluation
A PM evaluates an AI-thematic ETF: β=1.4, Rf=7%, ERP=6.5% → CAPM expected = 16.1%. Actual 1-year return = 14% → Jensen's α = −2.1%. Manager underperforms benchmark after risk-adjustment; PM switches to a passive AI index fund charging 10 bps vs 70 bps.

### Scenario 3 — ANTI-EXAMPLE: noisy β kills a good project
Junior analyst uses a 1-year daily β of 2.1 for a stable utility subsidiary (true 5-yr weekly β ≈ 0.7). With Rf=7%, ERP=7%, he computes Ke=21.7% instead of the correct 11.9%. A ₹500 cr solar-farm project with expected return 14% is rejected as "below hurdle." The true NPV at 11.9% was +₹45 cr. Quantified opportunity cost ≈ **₹45 cr foregone** plus strategic renewable positioning. Lesson: always adjust β, use longer-window weekly data, and sanity-check against industry β.

**Tools mentioned:** Bloomberg (BETA function), Damodaran dataset (industry β + ERP + country risk), Python (statsmodels OLS, linearmodels FF regressions), Yahoo Finance, S&P CapIQ.

---

## 7. Implementation Playbook
1. **Gather** Rf from latest 10-yr G-Sec / Treasury yield (RBI / FRED).
2. **Source** ERP from Damodaran implied India ERP sheet (refresh annually).
3. **Pull** raw β for firm + 6–10 peers from Bloomberg/Yahoo (5-yr weekly).
4. **Adjust** raw β (Blume 2/3–1/3) or build **bottom-up β** (unlever, median, relever via Hamada).
5. **Compute** Ke = Rf + β·ERP + size/country add-ons; document every input in a `capm_inputs.xlsx` artifact.
6. **Feed** Ke into WACC → DCF / NPV model for capital budgeting.
7. **Back-test** by computing Jensen's α vs actual peer returns; flag if >±3%.
8. **Review** inputs quarterly; trigger re-estimation on capital-structure change or >20bps Rf move.

---

## 8. Content Quality Audit

**Covered well:** core CAPM formula, SML logic, systematic vs idiosyncratic split, corp-finance cost-of-equity use case, Raj over/undervaluation scenario.

**Underplayed in source (added here):**
- β instability across windows / frequency
- β adjustment techniques (Blume, Vasicek)
- Bottom-up β for private / startup firms
- Fama-French 3/5 factor extensions, Carhart momentum
- Size and value premia; APT alternative
- Indian ERP specifics (Damodaran ~7.5%) and country-risk add-on for EM subs
- International CAPM and currency factor

**Supplement with ≥5 authoritative sources:**
1. Sharpe, W. F. "Capital Asset Prices: A Theory of Market Equilibrium under Conditions of Risk." *Journal of Finance*, 1964.
2. Fama, E. & French, K. "Common Risk Factors in the Returns on Stocks and Bonds." *Journal of Financial Economics*, 1993.
3. Damodaran, A. *Investment Valuation*, 3rd ed., Wiley, 2012 — plus annual ERP/β/country-risk updates on damodaran.stern.nyu.edu.
4. Bodie, Z., Kane, A., & Marcus, A. *Investments*, 12th ed., McGraw-Hill, 2020.
5. Carhart, M. "On Persistence in Mutual Fund Performance." *Journal of Finance*, 1997.

**Red flags:** single-period model; assumes frictionless markets, homogeneous expectations, unlimited borrowing at Rf; empirical low-β anomaly; ERP estimation sensitivity; β estimation window bias.

---

## 9. Quick-Recall Card
- CAPM: **E(R) = Rf + β·ERP**; prices only systematic risk.
- Inputs you MUST justify: Rf tenor, ERP source, β window/adjustment.
- SML above ⇒ undervalued; below ⇒ overvalued; on ⇒ fair.
- For private firms use **bottom-up β** with Hamada relevering.
- Cross-check with FF3/FF5 when size/value tilts matter.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: **"Does the expected return on this project or stock compensate me for its systematic (β) risk at today's Rf and ERP?"**

---

**Connects to:** [03-risk-return-fundamentals.md](03-risk-return-fundamentals.md), [07-modern-portfolio-theory.md](07-modern-portfolio-theory.md), [12-portfolio-performance-evaluation.md](12-portfolio-performance-evaluation.md), [../business-valuation/06-wacc-calculations.md](../business-valuation/06-wacc-calculations.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:4, 3:4, 4:4, 5:4, 6:5, 7:4, 8:4, 9:5, 10:4]
Sections rewritten: [2 expanded to 22 terms; 3 added bottom-up β workflow; 4 added FF3 numeric; 6 added quantified anti-example; 9 added role-lens question]
Enrichments applied: [cross-course links to WACC; 5 authoritative supplements; anti-example with ₹45 cr cost; IT/AI tooling (Bloomberg/Damodaran/Python); role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:22
Audited by: A9
-->
