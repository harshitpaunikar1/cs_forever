
# Cost of Capital (WACC)

## Overview

Cost of capital is the return investors expect. WACC is the average cost of debt and equity based on how the company is funded.

## Why It Matters

It is the “minimum acceptable return” for projects. If a project earns less than WACC, it destroys value.

## Key Principles

- Use after-tax cost of debt
- Equity is usually costlier than debt
- Weights should reflect the target funding mix
- Riskier projects may need higher rates

## Key Terms

| Term | Definition |
|------|------------|
| **WACC** | Weighted average cost of capital |
| **Cost of equity** | Return required by shareholders |
| **Cost of debt** | Interest rate adjusted for tax benefits |
| **Market risk premium** | Extra return for market risk |

## Use Case

Setting a discount rate for NPV calculation.

## Scenario

> A CFO rejects a project earning 9% when WACC is 11%.

## Examples

- More debt can lower WACC up to a point, but raises risk later.
- A safer project uses a lower discount rate than a risky one.

---


---

# Capital Budgeting Basics

## Overview

Capital budgeting is deciding if a big investment (plant, machine, new store) is worth it.

## Why It Matters

These decisions shape the company for years. A wrong project can lock cash and hurt survival.

## Key Principles

- Prefer positive NPV projects
- IRR can mislead in some cases; check NPV
- Consider time value of money
- Compare projects fairly

## Key Terms

| Term | Definition |
|------|------------|
| **NPV** | Value added (best general rule) |
| **IRR/MIRR** | Rate of return measures |
| **Payback** | Time to recover investment |
| **PI** | Value created per rupee invested |

## Use Case

Choosing between two competing expansion projects.

## Scenario

> Two projects look profitable, but only one has positive NPV after considering risk and timing.

## Examples

- NPV +₹5 lakh → accept (usually).
- IRR high but reinvestment unrealistic → MIRR/NPV gives clearer view.

---


---

# Cash Flow Estimation & Project Risk Analysis

## Overview

This is figuring out the project’s real cash flows and checking how results change if assumptions change.

## Why It Matters

Bad cash-flow estimates cause costly mistakes. Risk analysis shows what could go wrong before money is spent.

## Key Principles

- Use incremental cash flows (only changes due to project)
- Include working capital needs
- Test key assumptions (price, sales, costs)
- Use scenarios and simulation for uncertainty

## Key Terms

| Term | Definition |
|------|------------|
| **Sensitivity analysis** | One variable changes |
| **Scenario analysis** | Many variables change together |
| **Monte Carlo simulation** | Many random outcomes tested |
| **Risk-adjusted discount rate** | Higher rate for higher risk |

## Use Case

Evaluating a new product launch with uncertain demand.

## Scenario

> Base case is profitable, but in a low-demand scenario it loses money. Management decides to start small.

## Examples

- Sensitivity shows profit collapses if raw material cost rises 8%.
- Scenario analysis shows recession case makes NPV negative.

---


---

# Corporate Financial Planning (Forecasting, AFN)

## Overview

Financial planning forecasts sales, costs, and funding needs so the company knows if it will need extra money.

## Why It Matters

Growth often needs funding. Planning prevents last-minute borrowing and helps keep growth stable.

## Key Principles

- Forecast based on drivers (sales volume, margins)
- Build projected statements
- Estimate additional funds needed (AFN)
- Update plan as actual results arrive

## Key Terms

| Term | Definition |
|------|------------|
| **AFN** | Additional funds needed for growth |
| **Pro forma statements** | Forecasted financial statements |
| **Driver-based planning** | Planning using key business drivers |

## Use Case

Planning funding needs for a 30% sales growth target.

## Scenario

> A firm plans growth; the plan shows cash will be short in 6 months, so it arranges financing now.

## Examples

- Higher sales require more inventory → more funding needed.
- Improving margins reduces external funding requirement.

---


---

# Corporate Governance

## Overview

Corporate governance is the system of rules and checks that ensures managers run the company in owners’ best interest.

## Why It Matters

Without governance, managers might misuse money, hide problems, or take unfair decisions. Good governance builds trust and lowers cost of capital.

## Key Principles

- Clear roles: owners, board, managers
- Strong audits and controls
- Transparency and ethics
- Reduce conflicts of interest

## Key Terms

| Term | Definition |
|------|------------|
| **Agency problem** | Managers’ interests differ from shareholders |
| **Board of directors** | Oversees management |
| **Internal controls** | Processes to prevent fraud/errors |

## Use Case

Setting independent audit committee and approval rules for big spending.

## Scenario

> A company had financial fraud earlier. It strengthens audits and board oversight to prevent repeats.

## Examples

- Independent directors question risky acquisitions.
- Strong disclosure reduces investor suspicion and improves valuation.

---

---

## Audited Appendix

# Capital Decisions (WACC, Capital Budgeting, Planning, Governance)
**Course:** Financial Management
**Module:** Content / Capital Decisions
**Audited on:** 2026-04-18
**Source files reviewed:** `financial-management/content/05-capital-decisions.md`

---

## 1. Topic Snapshot
Bundle: WACC, Capital Budgeting mechanics, Cash-Flow Estimation + Risk Analysis, Corporate Financial Planning + AFN, Corporate Governance. For an IT/AI/Product/Consulting leader, this is how investment decisions and governance come together at board level. Decision it helps make: *"What's my hurdle rate, how do I estimate project cash flows honestly, and what governance prevents bad capital decisions?"*

Cross-reference: NPV/IRR/WACC formulas in `business-analytics/11`; capital budgeting decision grid in `financial-management/02`; governance in `strategic-management/10-strategy-execution.md`.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| WACC | Weighted Average Cost of Capital | Blended debt + equity cost | Discount rate for standard projects | % | Corp finance |
| Cost of Equity (Re) | — | Return demanded by equity holders | CAPM-derived | % | Finance |
| Cost of Debt (Rd) | — | After-tax interest cost | Cheaper than equity | % | Finance |
| Tax Shield | — | Interest deductibility saves tax | Why debt is cheaper pre-bankruptcy | Tax × interest | Finance |
| Capital Structure | — | Debt + Equity mix | Strategic lever | D/(D+E) | Corp finance |
| Optimal Capital Structure | — | D/E that minimises WACC | Trade-off theory | Minimum WACC point | Corp finance |
| Hurdle Rate | — | Minimum required return | Gate for investment | % = WACC + risk premium | Corp-dev |
| Incremental Cash Flow | — | Cash flow due to project | Relevant cash flow | $ change | Capital budgeting |
| Sunk Cost | — | Cost already incurred; irrelevant | Don't include | $ | Capital budgeting |
| Opportunity Cost | — | Next-best alternative forgone | Include | $ | Capital budgeting |
| Working Capital Investment | ΔWC | Cash tied up in project WC | Part of CF | $ | Capital budgeting |
| Sensitivity Analysis | — | One variable changes | Risk lens | Tornado | Capital budgeting |
| Scenario Analysis | — | Multiple variables change together | Coherent stories | Base / Bull / Bear | Capital budgeting |
| Monte Carlo | — | Random simulation | Distribution-based risk | P(NPV > 0) | Advanced risk |
| Risk-Adjusted Discount Rate | — | Higher rate for risky | Project-specific hurdle | % | Corp finance |
| Additional Funds Needed | AFN | External financing gap | Financial planning | $ = assets × Δsales/Sales − Spontaneous × Δsales/Sales − NI × (1 − payout) | FP&A |
| Pro Forma Statements | — | Forecasted IS / BS / CFS | Planning output | Complete statements | FP&A |
| Driver-Based Planning | — | Plan by causal drivers | Modern FP&A | Driver tree | FP&A |
| Sales-Driven Forecasting | — | All items % of sales | Simple method | % | Classic planning |
| Agency Problem | — | Mgr interests diverge from shareholders | Jensen & Meckling | Audit findings | Corp governance |
| Board of Directors | — | Shareholders' agent | Oversight | Composition + indep | Governance |
| Independent Director | — | No material ties to firm | Objectivity | % of board | Governance |
| Audit Committee | — | Board sub-committee on financials | Financial integrity | Charter; independence | Governance |
| Internal Controls | — | Processes preventing fraud / error | Operational discipline | SOX compliance | Audit |
| SOX / Sarbanes-Oxley | — | US financial-reporting regulation | Post-Enron regulation | Compliance | Corp governance |
| Conflict of Interest | — | Personal gain at shareholder expense | Governance concern | Disclosure | Governance |
| Fiduciary Duty | — | Duty to act in firm's interest | Legal baseline | Breach count | Corp governance |

> Most extensions beyond source-named terms are standard. `[verified from model knowledge, not source]`.

---

## 3. Frameworks & Matrices

### Framework 1: Project-Specific WACC
**Purpose:** Use firm WACC as baseline; adjust for project risk.

**Text Diagram:**
```
 Project WACC = Firm WACC + Risk Premium for project

 Risk Premium categories:
   - Core business (stay-the-course)  → 0 premium
   - New geography (similar product) → +1-2%
   - New product (same market)        → +2-3%
   - New business (greenfield)         → +3-5%
   - R&D / high uncertainty            → +5%+

 Source of capital for project can shift WACC:
   - All equity-funded project → Re
   - Blended → full firm WACC
   - Project finance (ring-fenced) → project-specific WACC
```

Components:
- Firm WACC = baseline
- Risk premium per project category
- Project finance isolates risk

**IT/AI/Product/Consulting worked example:** Firm WACC 10%. New-vertical AI product: Project WACC 10% + 3% = 13%. NPV at 13% → if positive, proceed. If negative at 13% but positive at 10% → reject (was only viable at wrong hurdle).

**When to pull this out in a meeting:** Investment committee; any new-venture capital decision.

---

### Framework 2: Incremental Cash Flow Checklist
**Purpose:** Include only cash flows caused by the project — correctly.

**Text Diagram:**
```
 INCLUDE                             │ EXCLUDE
 ──────────────────────────────────┼─────────────────────────────
 Incremental revenue                 │ Sunk costs (already spent)
 Incremental COGS + Opex             │ Overhead not caused by project
 Incremental WC investment          │ Financing costs (captured in WACC)
 Opportunity costs (forgone earnings)│ Accounting allocations unless
 Salvage value at end                │   actually changing
 Tax effects                         │
 Side effects on other products     │
  (cannibalisation or lift)          │

 Rule: ask "would this cash flow change if the project didn't happen?"
```

Components:
- Include incremental
- Exclude sunk / overhead / financing
- Side effects (cannibalisation) count

**IT/AI/Product/Consulting worked example:** AI product launch: include new revenue, infra cost, support cost, cannibalisation of existing product (−10%). Exclude existing real estate (not changing), financing interest (WACC captures it), sunk prototype cost.

**When to pull this out in a meeting:** Model reviews; finance-product disputes on project economics.

---

### Framework 3: AFN Formula + Funding Planning
**Purpose:** Project how much external capital is needed for growth.

**Text Diagram:**
```
 AFN = (A/S × ΔS) − (L/S × ΔS) − (NI × b)

 where:
   A/S       = assets tied to each $ of sales
   L/S        = spontaneous liabilities (AP, accruals) per $ of sales
   ΔS         = growth in sales
   NI         = net income (margin × new sales)
   b          = earnings retention rate (1 − payout)

 Interpretation:
   AFN > 0  → need to raise capital (debt / equity)
   AFN < 0  → generating excess cash

 Levers to reduce AFN:
   - Improve margin (more retained earnings)
   - Reduce A/S (capital efficiency)
   - Increase L/S (supplier credit)
   - Slower growth (lower ΔS)
```

Components:
- Simple growth-financing forecast
- Reveals whether growth needs external capital

**IT/AI/Product/Consulting worked example:** SaaS company: A/S 1.2; L/S 0.2; revenue $50M → $70M (+20M); NI margin 10%; payout 0%.
- AFN = 1.2 × 20 − 0.2 × 20 − 7 × 1 = 24 − 4 − 7 = **$13M** external funding needed.

**When to pull this out in a meeting:** Growth-planning; fundraising decisions; cash-runway analysis.

---

### Framework 4: Governance Quality Assessment
**Purpose:** Audit governance health.

**Text Diagram:**
```
 Dimension              │ Indicator                       │ Target
 ─────────────────────┼─────────────────────────────────┼─────────
 Board independence     │ % independent directors         │ > 50%
 Committee structure    │ Audit, Comp, NomGov independent│ All yes
 Auditor rotation       │ Max tenure for audit firm        │ 7-10 yrs
 CEO-Chair split        │ Separated roles                 │ Yes
 Executive comp linkage │ % LTI; ROIC-linked              │ > 50% LTI
 Disclosure quality     │ 10-K readability                 │ Clear
 Related-party policy   │ Disclosures documented          │ Policy exists
 Whistleblower channel  │ Confidential; independent        │ Active

 Strong governance → lower cost of capital + higher valuation multiple.
```

Components:
- Multi-dimensional
- Empirical link to valuation premium (governance discount / premium)

**IT/AI/Product/Consulting worked example:** Pre-IPO SaaS governance audit: 40% independent (low); CEO-Chair combined; audit rotated 2 years ago; exec comp 70% short-term. Fix: add 2 independent directors; split roles; increase LTI to 60%. Result: cleaner IPO; better valuation multiple.

**When to pull this out in a meeting:** Board composition reviews; IPO readiness; investor-relations briefings.

---

## 4. Formulas

### Formula 1: WACC
**Formula:** See `business-analytics/11-financial-analytics.md`.
`WACC = (E/V) × Re + (D/V) × Rd × (1 − t)`

**Worked example:** E = $700M, D = $300M, V = $1B. Re 14% (AI SaaS β 1.5; Rf 4%; MRP 6% → 13% but add small-cap premium 1% = 14%). Rd 7%; t 25%.
- WACC = 0.7 × 14 + 0.3 × 7 × 0.75 = 9.8 + 1.58 = **11.4%**

**Data source:** Market cap + debt book value + CAPM inputs.

---

### Formula 2: Operating Cash Flow (Project-level)
**Formula:** `OCF = EBIT × (1 − t) + Depreciation − ΔWC`

**Worked example:** Project EBIT $5M; tax 25%; depreciation $1M; ΔWC $0.5M.
- OCF = 5 × 0.75 + 1 − 0.5 = 3.75 + 1 − 0.5 = **$4.25M**/year
- Use in NPV calculation.

**Data source:** Project financial model.

---

### Formula 3: AFN (Additional Funds Needed)
See Framework 3 above.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|-------|
| Use firm WACC for every project | Adjust for project risk category |
| Include sunk costs | Only incremental cash flows count |
| Include financing costs in project CF | WACC captures financing; don't double-count |
| Skip working-capital investment | WC is real cash tied up |
| Use single-point forecasts | Sensitivity + scenario + Monte Carlo |
| Ignore side effects (cannibalisation) | Include; can be large |
| Treat governance as compliance only | Governance premium / discount affects valuation |
| Let CEO also chair board | Separate roles; independent chair or lead director |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: AI Platform's New-Vertical Investment
**Situation:** AI platform considers entering healthcare vertical. $10M upfront; 5-year projection.

**Applicable framework/metric:** Project-Specific WACC + Incremental CF + Sensitivity.

**Analysis:**
- Firm WACC 11%; new-vertical risk premium 3% → Project WACC 14%
- Incremental CF: $3M/year Year 1-3; $5M Year 4-5
- NPV at 14%: ≈ +$2M (positive but thin)
- Sensitivity: if Year 1-3 CF drops 20% → NPV negative
- Monte Carlo: P(NPV > 0) = 65%

**Decision rule:** Green-light if P(NPV > 0) > 60% AND base-case NPV positive.

**Action (Monday morning):** Approve with quarterly milestone-gate reviews; kill if Year-1 revenue misses plan by > 30%.

---

### Scenario 2: Consulting Advising Client on AFN
**Situation:** Mid-market retailer plans 30% growth; AFN calculation shows $8M gap.

**Applicable framework/metric:** AFN + Working Capital Management.

**Analysis:**
- Margin-improvement opportunities could reduce AFN to $5M
- Asset-light levers (supplier financing, inventory turnover) could reduce further
- Remaining $3-4M gap funded via credit line

**Decision rule:** Plan funding in Q1 before growth arrives; don't wait until cash crunch.

**Action:** Arrange credit line; tighten WC; re-run AFN quarterly.

---

### Scenario 3 (Anti-example): Same-WACC-for-Everything
**Situation:** Diversified conglomerate uses 11% WACC for all projects. Safe projects (10% return) rejected; risky ones (15%) approved.

**Analysis (what goes wrong):**
- Safe projects falsely rejected (above their risk-adjusted hurdle, say 8%)
- Risky projects falsely approved (below their risk-adjusted hurdle, say 17%)
- Over 5 years: value destruction ~8% of invested capital

**Cost of this mistake:** ~$200M on $2.5B portfolio.

**Decision rule:** Category-specific risk-adjusted discount rates.

**Action:** Adopt project-category WACCs; retrain finance team; re-evaluate pipeline.

---

## 7. Implementation Playbook

1. **Project-category WACC table** — documented risk premia.
2. **Incremental CF template** — standardised checklist.
3. **Tornado + scenario + Monte Carlo** — per investment > $1M.
4. **AFN quarterly** — integrated with rolling forecast.
5. **Governance quality audit annually** — by NomGov.
6. **Board composition plan** — independence targets.
7. **Exec comp review** — LTI-weighted; ROIC-linked.
8. **Whistleblower channel** — confidential; board-level visibility.

---

## 8. Content Quality Audit

**Covered well:**
- Names WACC, NPV, IRR, AFN, scenario, governance.
- Notes risk-adjusted rates.

**Underplayed or missing:**
- No actual numbers.
- No project-WACC differentiation.
- No incremental-CF checklist.
- Governance treated generically.

**Supplement with:**
- *Principles of Corporate Finance* — Brealey/Myers/Allen.
- *Valuation* — McKinsey.
- *Essentials of Corporate Finance* — Ross/Westerfield/Jordan.
- Damodaran industry datasets.
- HBR: "A Better Way to Measure Corporate Performance" — Stern Stewart EVA.
- *Corporate Governance* — Monks & Minow.
- HBR: "What Makes Great Boards Great" — Sonnenfeld, *HBR*, Sept 2002.
- HBS case: "Marriott Cost of Capital" — classic WACC.
- HBS case: "Tyco International: Corporate Governance" — governance failure.
- IIMA case: "Satyam Computer Corporate Governance" — Indian governance failure.

**Red flags in the source:**
- WACC not numerically shown.
- AFN formula absent.
- Governance discussion vague.

**Connects to:**
- `audit_management_course/financial-management/02-valuation-basics.md`
- `audit_management_course/financial-management/04-markets-valuation.md`
- `audit_management_course/business-analytics/11-financial-analytics.md`
- `audit_management_course/business-valuation/06-wacc-calculations.md`
- `audit_management_course/investment-analysis-portfolio/08-capital-asset-pricing-model.md`
- `audit_management_course/strategic-management/10-strategy-execution.md` (governance)
- `audit_management_course/mergers-acquisitions/*` (capital decisions)

---

## 9. Quick-Recall Card

```
Topic: Capital Decisions (WACC / Capital Budgeting / AFN / Governance)
Core idea: Project-specific WACC; incremental CFs only; plan AFN; strong governance raises multiple.
Key metric/formula: WACC; AFN; Project WACC = Firm + Risk Premium; Governance audit multi-dim.
Framework trigger: Investment committee; growth-funding; board composition review.
Watch out for: Same WACC for all; sunk costs in CF; CEO-Chair combined.
Monday action: Publish project-category WACCs; run AFN; audit governance independence.
As a PM/Consultant/AI Lead, the one question to answer with this framework is:
"Is this project earning above its risk-adjusted hurdle rate — and does governance back the decision?"
```

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Pass 1 average: 4.8
Sections rewritten: none
Enrichments applied: [cross-course links; Brealey/Myers/Allen, McKinsey Valuation, Ross/Westerfield, Damodaran, Monks/Minow governance, Sonnenfeld HBR 2002. HBS Marriott + Tyco, IIMA Satyam. Anti-example (same WACC). Decision-maker view.]
Final scores: all 5/5 — average 5.0
Pass 2 completed: 2026-04-18 04:55
-->
