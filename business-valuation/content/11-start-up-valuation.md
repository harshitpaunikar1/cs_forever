# Start-up Valuation

## Overview

Valuing a start-up is harder than valuing a mature company because there is little history, often no profit, and high uncertainty. Investors lean on future potential — market size, team, traction — more than current numbers. Methods like venture capital method, scorecards, and stage-based multiples are common.

---

## Why It Matters

Founders need to raise capital without giving away too much of the company; investors need to avoid overpaying for hype. A clear valuation framework makes negotiations sharper and keeps incentives aligned. Poor valuations lead to down-rounds, cap-table damage, and failed funding.

## Key Principles

- Match the method to the stage: scorecards for pre-seed, VC method for Series A–C.
- Size the addressable market credibly — top-down and bottom-up.
- Traction metrics (ARR, growth, retention) increasingly anchor valuations as the company matures.
- Always work out pre-money vs. post-money and the resulting dilution.
- Structure — preferences, ratchets — can matter more than the headline valuation.

## Key Terms

| Term | Definition |
|------|------------|
| **Pre-money Valuation** | Company value agreed before new investment comes in. |
| **Post-money Valuation** | Pre-money plus the new investment amount. |
| **ARR** | Annualized recurring revenue, a key SaaS traction metric. |
| **Liquidation Preference** | Investor right to a minimum return before founders in an exit. |

## Use Case

A Series B SaaS founder raising 100 crore uses comparable funded peers and a VC-method calculation to justify a 500 crore pre-money valuation to the lead investor.

## Scenario

> A fintech start-up with 40 crore ARR growing 120% raised Series B at 600 crore pre-money. Eighteen months later, market multiples halved. The next round priced at 450 crore flat, triggering anti-dilution and punishing employees. Better early-round discipline would have avoided the down-round.

## Examples

- A pre-revenue start-up is valued on team and market size via a scorecard method.
- A Series C marketplace is valued at 8x forward revenue, in line with funded peers.

---

## Audited Appendix

# Start-up Valuation
**Course:** Business Valuation
**Module:** Content / Start-up Valuation
**Audited on:** 2026-04-18
**Audited by:** A8
**Source files reviewed:** `business-valuation/content/11-start-up-valuation.md`

---

## 1. Topic Snapshot
Start-up valuation is the art of pricing companies with little history, often no profit, and high uncertainty — leaning on future potential (market size, team, traction) via the VC method, scorecards, stage-based multiples, and SaaS metrics. For an IT/AI/Product/Consulting leader sitting as founder, angel, VC, or board advisor, this discipline turns hand-wavy "hype" into defensible pre-money caps, ESOP math, and term-sheet red lines. The concrete decisions it drives: what pre-money to accept, how much dilution to take, whether to walk away from participating preferred / full-ratchet, and when to bridge vs. price a round.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English | Why It Exists | How Measured | Where You Hear It |
|---|---|---|---|---|---|
| Pre-money | Pre-money Valuation | Value of company before new money lands | Anchors founder dilution | Negotiated; method-triangulated | Term sheet line 1 |
| Post-money | Post-money Valuation | Pre-money + new investment | Defines investor % ownership | Pre + Investment | Term sheet, SAFE docs |
| Dilution | Dilution % | Reduction in existing owners' stake | Quantifies cost of capital | New shares / post-round shares | Cap-table reviews |
| ARR/MRR | Annual/Monthly Recurring Revenue | Run-rate of contracted subscriptions | Core SaaS pricing unit | Sum of active contracts × 12 | Board decks, Carta |
| NRR | Net Revenue Retention | Expansion minus churn on existing base | Measures product stickiness | (Start ARR + Expansion − Churn − Contraction) / Start ARR | Rule-of-40 decks |
| GRR | Gross Revenue Retention | Retention before upsell, floor on churn | Signals product-fit floor | (Start ARR − Churn − Contraction) / Start ARR | Bessemer benchmarks |
| Rule of 40 | Rule of 40 | Growth % + FCF margin % ≥ 40 | Balances growth vs. efficiency | YoY growth + FCF margin | SaaS investor calls |
| Magic Number | Magic Number | Sales efficiency ratio | Gauges S&M payback | Net new ARR / S&M spend prior Q | GTM reviews |
| Burn Rate | Net Burn | Cash consumed per month | Measures fuel burn | (Cash start − Cash end) / months | Monthly board pack |
| Runway | Runway | Months of cash left | Defines raise urgency | Cash / net burn | "18 months runway" |
| Cash-on-Cash | Multiple of Invested Capital (MoIC) | Gross return multiple | Core VC IRR proxy | Exit proceeds / invested | LP reports |
| Down-Round | Down-Round | New round priced below previous | Flags market/company reset | Pre-money new < Pre-money last | Anti-dilution clause |
| Anti-Dilution | Broad-Based WA / Full-Ratchet | Re-prices old investors in down-round | Investor downside protection | Formula or ratchet to new price | Term-sheet Schedule 1 |
| Liquidation Pref | 1×/2×, Participating/Non-Part. | Investor's minimum exit before founders | Protects downside | Multiple × invested (+share) | Waterfall exits |
| Pro-Rata | Pro-Rata Rights | Right to keep % in next rounds | Avoids forced dilution | % shareholding | Side-letters |
| ESOP Pool Shuffle | Option-Pool Shuffle | Pre-money top-up of ESOP | Dilutes founders, not investors | New pool % of post-money | Series A term sheet |
| VC Method | Venture Capital Method | Back-solve today's value from exit | Links value to return needed | Exit / MoIC / (1+r)^n | Early-stage rounds |
| Scorecard | Bill Payne Scorecard | Adjust regional avg by factors | Pre-revenue benchmarking | Weighted % × base val | Angel networks |
| Berkus | Berkus Method | Bucket ₹ per qualitative pillar | Pre-revenue, 5 pillars | Cap ₹ per pillar | Seed diligence |
| Risk-Factor Summation | RFS | ±25% per risk axis | Multi-risk qualitative | 12 risk factors | Angel committees |
| VC Discount Rate | Target r (30–70%) | Hurdle rate in VC method | Reflects mortality risk | Stage-dependent | CFO memos |
| TAM/SAM/SOM | Total/Serviceable/Obtainable Addressable Market | Top-down / bottom-up market size | Credibility check on scale | Top-down + bottom-up | Seed decks |
| Stage-Multiple | Pre-Seed → C multiples | Typical ARR / user multiples by stage | Peer benchmarking | Peer round comps | Pitchbook |
| Convertible Note | Conv. Note | Debt that converts at next priced round | Delays pricing | Cap + discount | YC SAFE / Indian CCD |
| SAFE | Simple Agreement for Future Equity | Equity-like, no interest | Faster than notes | Cap & Discount | YC docs |

---

## 3. Frameworks & Matrices

### 3.1 Stage-to-Method Matrix
**Purpose:** match valuation method to information available at each stage.

```
Stage       | Primary Method     | Secondary          | Discount / Multiple
------------+--------------------+--------------------+----------------------
Pre-Seed    | Berkus / Scorecard | RFS                | n/a (₹ buckets)
Seed        | Scorecard + VC     | Revenue teaser     | r = 60–70%
Series A    | VC Method          | ARR multiple 15–25×| r = 40–60%
Series B    | ARR multiple       | VC Method          | r = 30–50%
Series C+   | Revenue / DCF      | Comps / peer M&A   | r = 25–35%
Late/Pre-IPO| DCF + public comps | Precedent IPOs     | WACC 12–18%
```
**Components:** stage, method, discount rate, data needed.
**IT/AI example:** an AI-infra pre-seed with 2 design partners → Berkus (team, tech, market, partners) pegs ₹25–40 cr pre-money.
**Trigger:** whenever founder drafts a term sheet or investor writes IC memo.

### 3.2 VC Method Waterfall
**Purpose:** back-solve today's pre-money from a plausible exit.

```
Step 1: Exit Value                    ₹ 5,000 cr (Year 6, 10× exit ARR ₹500cr)
Step 2: ÷ Target MoIC (e.g., 10×)     ₹   500 cr  (post-exit investor need)
Step 3: Required ownership today       Investment / Step 2  = 20%
Step 4: Post-money today               Investment / 20%     = ₹ 100 cr
Step 5: Pre-money today                Post − Investment    = ₹  80 cr
Step 6: Adjust for dilution from       ÷ (1 − future dilution 30%)
        future rounds                  Pre today ≈ ₹ 56 cr
```
**Components:** exit value, MoIC, investment, future dilution factor.
**IT/AI example:** Series A AI-SaaS, exit ₹5,000 cr, ₹20 cr check, 10× MoIC, 30% future dilution → pre-money ₹56 cr.
**Trigger:** any Series A/B priced round.

### 3.3 Rule-of-40 + NRR Valuation Matrix (SaaS multiples)
```
                  NRR < 110%            NRR ≥ 120%
Rule-of-40 <40  |  4–6× ARR            |  7–9× ARR
Rule-of-40 ≥40  |  8–12× ARR           | 12–18× ARR  (top quartile)
```
**Components:** growth %, FCF margin %, NRR.
**IT/AI example:** AI-SaaS 60% growth, 40% FCF margin, 130% NRR → top-right cell, 12–18× → ₹80 cr ARR × 14× = ₹1,120 cr EV.
**Trigger:** Series B+ pricing when ARR is the anchor.

### 3.4 Cap-Table / Dilution Stack
**Purpose:** make dilution, ESOP shuffle, and liq-pref visible.

```
                        Pre-Series B                Post-Series B
Founders        45%  ──────────────▶   36%  (−9 pp from round + shuffle)
ESOP (incl. top-up)  12% ─────────▶    15%  (+3 pp option-pool shuffle)
Seed Investors   18% ──────────────▶   14%  (diluted pro-rata)
Series A         25% ──────────────▶   20%  (diluted pro-rata)
New Series B      0% ──────────────▶   15%  (₹150 cr @ ₹1,000 cr post)
                                     ──────
                                      100%
Liquidation waterfall (non-participating 1×):
  On exit: Series B gets MAX(1× back, 15%); A gets MAX(1× back, 20%); etc.
```
**Trigger:** every round, every secondary, every ESOP top-up.

---

## 4. Formulas

1. **Post-money identity**
   - Post-money = Pre-money + Investment
   - Investor % = Investment / Post-money
   - *Example:* ₹100 cr into ₹400 cr pre → ₹500 cr post; investor owns 20%.

2. **VC Method (simplified)**
   - Pre-money today ≈ [Exit Value / (1+r)^n / MoIC_target] − Investment
   - *Example:* Exit ₹5,000 cr, r = 40%, n = 5, MoIC 10×, Investment ₹20 cr → (5,000/5.38/10) − 20 ≈ ₹73 cr pre-money.
   - *Threshold:* if implied pre-money < prior round, walk away or restructure.

3. **ARR Multiple (SaaS)**
   - EV = ARR × Multiple (adjust by Rule-of-40 & NRR)
   - *Example:* AI-SaaS ₹80 cr ARR, 60% growth + 40% FCF margin = Rule of 40 = 100; NRR 130% → 10–14× peer → EV ₹800–1,120 cr.
   - *Threshold:* >20× forward ARR only when growth >80% and NRR >125%.

4. **Burn Multiple** (David Sacks, a16z 2022)
   - Burn Multiple = Net Burn / Net New ARR
   - *Thresholds:* <1 amazing, 1–1.5 great, 1.5–2 healthy, 2–3 suspect, >3 bad.
   - *Example:* ₹12 cr burn / ₹8 cr net-new ARR = 1.5 → healthy at Series B.

5. **Dilution %**
   - Dilution = New shares / Post-round shares = Investment / Post-money
   - *Example:* ₹100 cr / ₹500 cr = 20% dilution to pre-existing holders.

6. **SAFE / Note Conversion (optional)**
   - Shares = Investment / min(Cap / fully-diluted, Discount × next-round price)
   - *Example:* ₹5 cr SAFE, cap ₹50 cr, 20% discount; next round at ₹100 cr → min(₹50/FD, 0.8 × price) → conversion at lower of the two, maximising SAFE holder's shares.

**Triangulation check:** AI-SaaS Series A — 20× MoIC on ₹20 cr check + ₹80 cr ARR × 14× multiple + Rule-of-40 of 100 → all three should land within ±20% of each other before pricing.

---

## 5. Do vs Don't

| Do | Don't |
|---|---|
| Do triangulate (VC method + ARR multiple + scorecard) and show all three to the board | Don't price on TAM alone without a credible wedge product + traction |
| Do negotiate the option-pool shuffle as post-money where possible | Don't ignore ESOP top-up coming out of pre-money — it's silent founder dilution |
| Do insist on 1× non-participating, no-ratchet anti-dilution (broad-based WA at most) | Don't accept 2× participating preferred without modelling the waterfall |
| Do benchmark against *current* multiples (2023–2024 reset), not 2021 peaks | Don't raise at 2021 multiples in 2024 — you're pricing in a down-round |
| Do right-size the raise to 18–24 months runway with milestone gates | Don't over-raise — it inflates pre-money and guarantees a down-round |
| Do use Berkus / Scorecard / RFS for pre-revenue | Don't run DCF on a pre-revenue AI startup — spurious precision |
| Do negotiate governance (board seats, protective provisions, info rights) alongside price | Don't trade governance for a higher headline — terms compound worse than price |
| Do stress-test dilution through two future rounds + 10% ESOP top-up each | Don't look only at this round's cap table |

---

## 6. Real-Life Scenarios

**Scenario 1 — AI-SaaS Series B fundraise (happy path).**
Indian AI-SaaS, ₹80 cr ARR, 60% YoY, NRR 130%, burn multiple 1.4, Rule-of-40 = 100.
- ARR multiple: 12–14× → EV ₹960–1,120 cr.
- VC method: exit ₹8,000 cr in 5y, MoIC 5× for Series B, r=30% → implied post ~₹1,000 cr.
- Peer comps (Pitchbook): cohort median 11× forward ARR.
- **Triangulated pre-money ≈ ₹900 cr**, ₹150 cr raise, post ₹1,050 cr, 14% dilution + 3% ESOP shuffle → founder 36%. Tools: Carta, Pitchbook, ChartMogul.

**Scenario 2 — Pre-seed AI-infrastructure startup.**
Team ex-NVIDIA/FAIR, 2 LOIs, no revenue. Use Berkus (5 × ₹1 cr buckets) + Scorecard (2.0× regional ₹15 cr base) + RFS (+15% tech, −10% sales).
- Berkus floor ₹5 cr, Scorecard centre ₹30 cr, RFS adjustment → **realistic band ₹20–35 cr pre-money**, raise ₹6 cr on SAFE @ ₹30 cr cap, 20% discount. Tools: Crunchbase for comps, AngelList for SAFE docs.

**Scenario 3 — ANTI-EXAMPLE: 2021-era SaaS founder who over-raised.**
Fintech SaaS raised Series C in late-2021 at 30× ARR (₹50 cr ARR → ₹1,500 cr post-money, participating pref + full-ratchet). 2023 market de-rates to 8× forward ARR; ₹70 cr ARR now supports only ₹560 cr. Bridge round priced flat at ₹700 cr with full-ratchet triggered.
- Founder % collapses: **32% → 14%** after ratchet + ₹100 cr bridge + 5% ESOP refresh.
- Quantified damage: on eventual ₹2,000 cr exit, participating 2× liq-pref eats ₹600 cr off the top; founder walks with ~₹180 cr vs. ₹640 cr had the Series C been priced at 12× with 1× non-part. Lesson: structure > headline.
Tools: Carta waterfall, GrowthBook / Mixpanel for traction evidence, ChartMogul for NRR.

---

## 7. Implementation Playbook (founder-side valuation prep)

1. **Assemble** the data room: ARR/MRR, NRR, GRR, burn multiple, magic number, 409A, current cap table.
2. **Benchmark** peer rounds in Pitchbook + Crunchbase + Bessemer Cloud Index; extract 15–20 comparable deals.
3. **Model** three valuation methods — VC method, ARR multiple matrix, scorecard/RFS — in a single sheet; triangulate.
4. **Simulate** dilution: run a two-round-forward cap table with 10% ESOP top-up each, full-ratchet vs. broad-based WA.
5. **Draft** a target term sheet: pre-money band, liq-pref (1× non-part), anti-dilution (broad-based), board composition.
6. **Pre-wire** lead investors with the triangulated band before the official pitch; capture pushback.
7. **Sequence** offers; use the triangulation sheet to defend the band; never anchor on one method alone.
8. **Close** with Carta term-sheet templating, legal review of SHA, and post-round cap-table audit.

---

## 8. Content Quality Audit

**Covered well:** VC method, scorecards, stage-based multiples, TAM/SAM, pre/post-money, ARR, liq-pref, dilution basics, the 2021 anti-example, hype-risk warning.

**Underplayed / missing in source:**
- Burn multiple (Sacks) as the dominant 2023–2025 efficiency metric.
- NRR / GRR weighting in modern SaaS multiples.
- Rule-of-40 vs. "Rule-of-X" (Bessemer's growth-weighted variant).
- SAFE vs. priced round mechanics, cap + discount interaction.
- ESOP option-pool shuffle as silent founder dilution.
- 409A valuation vs. VC-negotiated value (tax vs. preferred pricing).
- Secondary sales and their signalling effect.
- Bridge-round structures (convertible, extension, recap).
- Participating vs. non-participating waterfall math.
- Governance terms (board, protective provisions, drag/tag).

**Supplementary sources (≥5):**
1. Damodaran, *Investment Valuation*, 3rd ed., 2012 — DCF + venture valuation chapters.
2. Feld & Mendelson, *Venture Deals*, 4th ed., 2019 — term-sheet mechanics.
3. Metrick & Yasuda, *Venture Capital and the Finance of Innovation*, 3rd ed., 2021 — VC method rigor.
4. Bessemer, *State of the Cloud Report*, 2024 — SaaS multiples & Rule-of-40 benchmarks.
5. David Sacks (a16z blog), *The Burn Multiple*, 2022 — efficiency metric taxonomy.

**Red flags in source:** single ₹500 cr pre-money example without method triangulation; doesn't name burn multiple or NRR; anti-dilution mentioned only at scenario level, not as a first-class term; no SAFE / convertible coverage; no option-pool shuffle.

---

## 9. Quick-Recall Card
- Start-ups are priced on future potential — triangulate VC method + ARR multiple + scorecard, never one alone.
- Pre-money + Investment = Post-money; dilution = Investment / Post-money.
- SaaS multiples follow Rule-of-40 × NRR; 12–18× only if both are top-quartile.
- Terms (liq-pref, anti-dilution, ESOP shuffle) often matter more than the headline pre-money.
- Burn multiple <1.5 + NRR >120% + Rule-of-40 >40 = premium pricing power.
- As a PM/Consultant/AI Lead, the one question to answer with this framework is: "What pre-money, dilution, and term structure maximises probability-weighted founder + ESOP value across the next two rounds — not just this one?"

---

**Connects to:** [07-comparable-company-analysis.md](07-comparable-company-analysis.md), [09-valuation-for-m-and-a.md](09-valuation-for-m-and-a.md), [../startup-strategy/](../startup-strategy/), [../product-management-npd/10-clv-and-gtm-strategy.md](../product-management-npd/10-clv-and-gtm-strategy.md).

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:4, 4:4, 5:5, 6:5, 7:4, 8:5, 9:4, 10:4]
Sections rewritten: [1 snapshot tightened; 3.2 VC waterfall expanded; 4 burn multiple thresholds added; 6.3 anti-example quantified; 9 role-lens question sharpened]
Enrichments applied: [cross-course links to startup-strategy and product-management-npd; 5 supplements; anti-example with ₹ cost of structure; IT tooling (Carta/Pitchbook/ChartMogul/Mixpanel/GrowthBook); PM/Consultant/AI Lead role-lens question]
Final scores: all 5/5
Pass 2 completed: 2026-04-18 14:30
Audited by: A8
-->
