# Modern Portfolio Theory

## Overview
Modern Portfolio Theory, developed by Harry Markowitz, is a framework for constructing portfolios that maximize expected return for a given level of risk. The key insight is that an investment's risk and return should not be evaluated in isolation but in the context of how it affects the overall portfolio. By combining assets that do not move perfectly together, investors can reduce total portfolio risk without sacrificing return.

---

## Why It Matters
Before Modern Portfolio Theory, investors often evaluated each investment on its own merits. This theory changed finance by showing that what matters most is how assets interact within a portfolio. Two individually risky assets can actually lower overall risk when combined, as long as their returns are not perfectly correlated. This insight is the scientific basis for diversification and forms the foundation of professional portfolio management.

## Key Principles
- Portfolio risk depends not only on individual asset risks but also on the correlations between assets
- The efficient frontier represents the set of portfolios offering the highest return for each level of risk
- Rational investors should only hold portfolios that lie on the efficient frontier
- Combining assets with low or negative correlations reduces overall portfolio volatility more than simply picking low-risk assets

## Key Terms
| Term | Definition |
|------|------------|
| **Efficient Frontier** | The curve showing all optimal portfolios that offer the maximum expected return for each level of risk |
| **Correlation** | A statistical measure ranging from negative one to positive one that describes how two assets move relative to each other |
| **Optimal Portfolio** | The portfolio on the efficient frontier that best matches an investor's risk tolerance |
| **Mean-Variance Optimization** | The mathematical process of finding the asset weights that minimize risk for a target return or maximize return for a target risk |

## Use Case
A wealth management firm uses mean-variance optimization software to build client portfolios that sit on the efficient frontier, ensuring each client gets the best possible return for their stated risk tolerance.

## Scenario
> Anika manages a university endowment and wants to add international stocks to the existing domestic equity and bond portfolio. She runs a correlation analysis and finds that international stocks have a low correlation with domestic bonds. After optimizing the allocation, the new portfolio has a higher expected return and lower overall risk than before, moving it closer to the efficient frontier.

## Examples
- Combining gold and equities in a portfolio because gold often rises when stocks fall, lowering overall volatility
- A robo-advisor platform automatically allocating client funds across six asset classes using mean-variance optimization to build an efficient portfolio

---

## Audited Appendix

# Modern Portfolio Theory
**Course:** Investment Analysis and Portfolio Management
**Module:** Content / Modern Portfolio Theory
**Audited on:** 2026-04-18
**Audited by:** A8
**Source files reviewed:** `investment-analysis-portfolio/content/07-modern-portfolio-theory.md`

---

## 1. Topic Snapshot
Modern Portfolio Theory (Markowitz, 1952) is the mathematical framework that builds portfolios on the efficient frontier — maximising expected return per unit of risk by exploiting imperfect correlations across assets.
An IT/AI/Product/Consulting leader must think at portfolio level (not asset level) because diversification is the only "free lunch" in finance; individually risky assets can combine into a lower-risk whole when ρ < 1.
The decision: given expected returns, volatilities, and a correlation matrix, what weight vector **w** should I hold — and does my portfolio actually sit on the frontier or drift off it?

---

## 2. Jargon & Terminology

| # | Term | Definition | IT/AI/Product/Consulting Cue |
|---|------|------------|------------------------------|
| 1 | Expected Return E(R) | Probability-weighted mean of future returns | Input to MVO objective |
| 2 | Variance σ² | Dispersion of returns around mean | Risk proxy in mean-variance |
| 3 | Covariance Cov(i,j) | Joint variability of two assets | Off-diagonal of Σ matrix |
| 4 | Correlation ρ | Normalised covariance ∈ [−1, +1] | Diversification lever |
| 5 | Efficient Frontier | Set of portfolios with max return per σ | North star for allocation |
| 6 | Minimum Variance Portfolio (MVP) | Left-most point on frontier | Risk floor anchor |
| 7 | Optimal / Tangency Portfolio | Max Sharpe point touched by CML | Where rational investors sit |
| 8 | Capital Market Line (CML) | Line from r_f tangent to frontier | Risky+riskless mix line |
| 9 | Mean-Variance Optimisation (MVO) | Quadratic optimisation over w | Core MPT engine |
| 10 | Unconstrained vs Constrained MVO | Allow shorts/leverage vs box/long-only | Real-world mandate filter |
| 11 | Short-Sale Constraints | w_i ≥ 0 | Most retail/PF rules |
| 12 | Black-Litterman | Prior + investor views → posterior E(R) | Fixes MVO estimation error |
| 13 | Rebalancing Drift | Weights drift from target as prices move | Triggers trade list |
| 14 | Home Bias | Overweight domestic assets vs global cap | Behavioural anti-pattern |
| 15 | Diversification Decay (tails) | Correlations → 1 in stress | Crisis risk |
| 16 | Risk Parity | Equal risk contribution, not equal weight | MPT alternative |
| 17 | 60/40 Portfolio | 60% equity / 40% bonds baseline | Default benchmark |
| 18 | Correlation Instability in Stress | ρ jumps from 0.2 → 0.8 in crash | Model break |
| 19 | Fat Tails / Gaussian Assumption | Real returns are non-normal | MPT limitation |
| 20 | Estimation Error | Noisy μ, Σ dominate MVO output | Why BL/shrinkage used |

---

## 3. Frameworks & Matrices

### 3.1 Efficient Frontier Diagram (ASCII)
```
 E(R)
   ^
   |                          ____-------•  Aggressive (100% EQ)
   |                    __---•  ← Tangency (max Sharpe)
   |              __--- /
   |          __-- CML /
 r_f •----___---     /  ← Efficient Frontier (upper curve)
   |       \______ /
   |              • MVP (min variance)
   |              (inefficient arm below MVP)
   +------------------------------------------> σ (risk)
```
*IT/AI worked example:* Consulting firm's CIO plots 6 client model portfolios; 2 sit below the MVP line → immediate reallocation trigger.

### 3.2 Correlation Matrix Template (ASCII 4×4)
```
              | Equity | Bonds | Gold  | Alts  |
--------------+--------+-------+-------+-------+
Equity        |  1.00  | +0.10 | -0.25 | +0.40 |
Bonds         | +0.10  |  1.00 | +0.05 | +0.15 |
Gold          | -0.25  | +0.05 |  1.00 | -0.10 |
Alts (PE/Inf) | +0.40  | +0.15 | -0.10 |  1.00 |
```
*Product-lens trigger:* a PM building a robo-advisor surfaces this matrix in-app so clients see *why* gold is added (negative ρ with equities).

### 3.3 Portfolio Construction Workflow
```
[Inputs]                [Engine]                [Constraints]         [Output]
E(R) vector μ  ───┐                           ┌── long-only
σ (vols)       ───┼──►  Mean-Variance     ────┼── sector caps  ────►  Weights w*
Σ (cov matrix) ───┘     Optimiser (QP)        └── turnover/tax        on frontier
                                                                       + Sharpe, σ_p
```
*Consulting example:* wealth-mgmt firm feeds client risk score → constrained MVO → 5 model portfolios mapped to risk buckets.

### 3.4 (Optional) Black-Litterman Enhancement
```
Market-cap equilibrium prior  π   ──┐
                                    ├─►  Posterior E(R)  ──►  MVO  ──►  Stable w*
Investor views P, Q, Ω (conf)  ─────┘
```
*AI-lead example:* AI team has a factor-model view "Indian IT +3% next 12m, conf 0.6"; feeds as BL view instead of hacking μ directly — avoids corner-solution blowups.

---

## 4. Formulas

1. **Portfolio return:** E(R_p) = Σ wᵢ · E(Rᵢ)
2. **2-asset variance:** σ_p² = w₁²σ₁² + w₂²σ₂² + 2·w₁·w₂·ρ·σ₁·σ₂
3. **n-asset variance:** σ_p² = wᵀ Σ w
4. **2-asset MVP weight (asset 1):** w₁* = (σ₂² − ρ·σ₁·σ₂) / (σ₁² + σ₂² − 2·ρ·σ₁·σ₂)
5. **Tangency portfolio:** w_tan ∝ Σ⁻¹ (μ − r_f · **1**)
6. **Correlation:** ρ = Cov(i,j) / (σᵢ · σⱼ), ρ ∈ [−1, +1]
7. **Sharpe ratio:** S_p = (E(R_p) − r_f) / σ_p (maximised at tangency)

**Numeric example — MVP (2-asset).** Domestic equity σ₁ = 18%, international equity σ₂ = 22%, ρ = 0.4.
- Numerator: σ₂² − ρσ₁σ₂ = 0.0484 − 0.4·0.18·0.22 = 0.0484 − 0.01584 = 0.03256
- Denominator: σ₁² + σ₂² − 2ρσ₁σ₂ = 0.0324 + 0.0484 − 0.03168 = 0.04912
- **w₁* = 0.03256 / 0.04912 ≈ 0.663 (66.3% domestic), w₂* ≈ 33.7% international**
- σ_p² = 0.663²·0.0324 + 0.337²·0.0484 + 2·0.663·0.337·0.4·0.18·0.22
       = 0.01424 + 0.00550 + 0.00708 = 0.02682 → **σ_p ≈ 16.4%**
- Risk drops from 18% (single asset) to 16.4% even though asset 2 is riskier — diversification free lunch.

**Thresholds:** ρ > 0.8 → marginal diversification benefit; ρ < 0.3 → strong benefit; ρ ≤ 0 → hedge-like.

---

## 5. Do vs Don't

| # | Do | Don't |
|---|----|-------|
| 1 | Evaluate each asset's contribution to **portfolio** σ, not standalone σ | Rank assets by individual Sharpe in isolation |
| 2 | Re-estimate Σ with shrinkage (Ledoit-Wolf) or factor models | Plug in raw 5-yr sample covariance and trust it |
| 3 | Apply long-only / sector caps before running MVO | Run unconstrained MVO and accept 300% short weights |
| 4 | Stress-test with ρ → 0.9 crisis scenario | Assume correlations stable through a drawdown |
| 5 | Rebalance on bands (e.g., ±5%) or calendar + tax lens | Rebalance every day ignoring turnover/tax cost |
| 6 | Use Black-Litterman to blend views with equilibrium | Hand-tune μ until output "looks sensible" |
| 7 | Document role-lens objective (PM/Consultant/AI Lead) before optimising | Optimise without a risk-tolerance or horizon anchor |
| 8 | Cross-check MVO output vs risk-parity and 60/40 baselines | Ship a single black-box MVO portfolio to clients |

---

## 6. Real-Life Scenarios

**Scenario 1 — HNI founder post-exit (Anika-style endowment analogue).**
Founder exits SaaS firm with ₹80 Cr liquid. Consulting advisor runs constrained MVO across Indian equity (σ 20%), international equity (σ 18%, ρ 0.45 to India), gilts (σ 6%, ρ 0.1), gold (σ 15%, ρ −0.2), REITs (σ 14%, ρ 0.3). Output: 35/25/20/10/10. Expected portfolio σ ≈ 11% vs 20% for all-India-equity baseline — same E(R), nearly half the risk.

**Scenario 2 — IT pension fund adds Alts via Black-Litterman.**
Indian IT pension fund's trustee board wants to introduce private credit and infrastructure. Naive MVO produces 70% alts (corner solution from noisy μ). Team instead uses BL: market-cap equilibrium prior + three views ("PC spread +150bps over IG", "Infra ρ to equity = 0.3 not historical 0.5", confidence 0.4 each). Posterior MVO yields a sane 8% PC + 7% infra allocation that the IC approves.

**Scenario 3 — ANTI-EXAMPLE: assumed-stable correlations blow up.**
Robo-advisor's 60/40 model assumes equity-bond ρ = 0.2 (2015–2019 sample). March 2020: both equities and bonds drop together, ρ → 0.85. 60/40 drawdown hits −30% instead of modelled −18%. **Behavioural-exit cost:** 22% of clients redeem at the bottom, locking in losses; firm's lifetime AUM lost ≈ ₹600 Cr × 6% fee NPV ≈ ₹36 Cr. Fix post-mortem: stress-scenario ρ matrix + risk-parity overlay + BL views on regime shifts.

**Tools:** Python (**PyPortfolioOpt**, **riskfolio-lib**, cvxpy); Excel Solver for <10-asset toy MVO; **Portfolio Visualizer** for backtest + frontier plots; **BlackRock Aladdin** for institutional multi-mandate construction; **R PortfolioAnalytics** for factor-aware MVO.

---

## 7. Implementation Playbook

1. **Define** investment policy statement (role-lens objective, horizon, constraints) — artifact: IPS doc.
2. **Collect** return, vol, correlation estimates for each candidate asset class — artifact: μ vector, Σ matrix (CSV).
3. **Apply** shrinkage / factor model to Σ to tame estimation error — artifact: cleaned Σ̂.
4. **Run** constrained MVO in PyPortfolioOpt/cvxpy with long-only + sector caps — artifact: weight vector w*.
5. **Overlay** Black-Litterman views where team has conviction — artifact: posterior μ and revised w*.
6. **Stress-test** portfolio with crisis ρ matrix (ρ → 0.8) and fat-tail scenarios — artifact: scenario P&L table.
7. **Implement** trade list with tax/turnover filter + rebalance bands — artifact: rebalancing policy doc.
8. **Monitor** drift, realised σ, realised Sharpe vs target; review quarterly — artifact: governance dashboard.

---

## 8. Content Quality Audit

**Covered well:** efficient frontier intuition, 2-asset math, diversification-as-free-lunch framing, tangency/CML linkage.

**Underplayed (and added here):**
- **Correlation breakdown in stress** — ρ instability is where MPT most often fails in practice; added crisis scenario.
- **Gaussian / normal-return assumption** — real returns are fat-tailed; MPT understates tail risk.
- **Black-Litterman** as a practical fix for MVO's estimation-error sensitivity (corner solutions).
- **Risk parity** as a robust MPT-alternative when expected returns are unreliable.
- **Rebalancing frequency trade-offs** — daily ≠ better; tax and turnover dominate.
- **Estimation error in MVO** — small changes in μ cause huge weight swings; needs shrinkage.
- **Home bias** — systematic over-allocation to domestic markets, a behavioural drag on the frontier.

**Supplementary sources (≥5):**
1. Markowitz, H. (1952). *Portfolio Selection.* Journal of Finance, 7(1), 77–91.
2. Bodie, Z., Kane, A., & Marcus, A. (2020). *Investments* (12th ed.). McGraw-Hill.
3. Black, F., & Litterman, R. (1990). *Asset Allocation: Combining Investor Views with Market Equilibrium.* Goldman Sachs Fixed Income Research.
4. Ang, A. (2014). *Asset Management: A Systematic Approach to Factor Investing.* Oxford University Press.
5. Ilmanen, A. (2022). *Expected Returns* (2nd ed.). Wiley.

**Red flags:**
- Presenting MVO weights as precise truth without showing input sensitivity.
- Using a single historical sample window for Σ across regimes.
- Ignoring non-normality and tail dependence when advising retail clients.
- Silent short / leverage positions in unconstrained MVO output slipping into a long-only mandate.

---

## 9. Quick-Recall Card
- MPT (Markowitz, 1952): portfolio risk ≠ sum of asset risks — correlations rule.
- Efficient frontier = max E(R) per σ; tangency = max Sharpe when r_f exists.
- σ_p² = wᵀ Σ w; diversification benefit scales with (1 − ρ).
- MVO is estimation-error sensitive → use shrinkage, Black-Litterman, or risk parity.
- Correlations rise in stress; always stress-test with ρ → 0.8 crisis matrix.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: **Given my clients' constraints and my confidence in μ/Σ, does my current weight vector w sit on the efficient frontier under both normal and stressed correlation regimes — and if not, what is the minimum-turnover trade that puts it there?**

---

**Connects to:** [08-capital-asset-pricing-model.md](08-capital-asset-pricing-model.md), [09-portfolio-construction-diversification.md](09-portfolio-construction-diversification.md), [03-risk-return-fundamentals.md](03-risk-return-fundamentals.md), [12-portfolio-performance-evaluation.md](12-portfolio-performance-evaluation.md).

<!--
Self-Audit Report
Pass 1 scores: [1:5, 2:5, 3:4, 4:5, 5:5, 6:5, 7:4, 8:5, 9:4, 10:5]
Sections rewritten: [3 (added BL diagram), 7 (verb+artifact tightened), 9 (role-lens question)]
Enrichments applied: [cross-course links; 5 supplements; anti-example w/ cost; IT tooling; role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A8
-->
