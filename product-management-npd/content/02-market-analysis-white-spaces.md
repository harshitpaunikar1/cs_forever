# Market Analysis and Finding White Spaces

## Overview

Market analysis is the work of studying customers, competitors, and trends to figure out where real opportunities live. A "white space" is a gap in the market — an unmet need, an underserved segment, or a jobs-to-be-done that no current product handles well. Finding it is half the battle in new product success.

---

## Why It Matters

Building in a crowded market means fighting for scraps of attention and margin. Finding a white space lets a product command higher prices, attract loyal customers, and grow without being copied overnight. Teams that skip market analysis often ship a feature that already exists from three competitors.

## Key Principles

- Map the competitive landscape before writing a single spec.
- Talk to non-customers — they reveal gaps your customers cannot.
- Look for pain points where users hack together workarounds in spreadsheets.
- Size the opportunity: a white space only matters if it has enough buyers.
- Validate with small experiments before committing budget.

## Key Terms

| Term | Definition |
|------|------------|
| **White Space** | An unmet or underserved market need with no dominant product. |
| **TAM** | Total Addressable Market — the full revenue possible if you had 100% share. |
| **Segmentation** | Grouping customers by shared needs, behaviors, or demographics. |
| **Jobs To Be Done** | The real goal a customer "hires" a product to accomplish. |
| **Competitive Landscape** | A map of who else serves the same customers and how. |

## Use Case

A consumer appliance brand reviews its category and notices every blender targets either budget or premium shoppers, with nothing built for small apartments. The PM team sizes the segment, interviews 40 urban renters, and launches a compact blender line that hits 12% market share in 18 months.

## Scenario

> An Indian edtech startup analyzed 2,000 user reviews of test-prep apps and found a recurring complaint: "no content in regional languages." Competitors all focused on English and Hindi. The team shipped a Tamil-first exam-prep product in 90 days and captured a loyal user base that larger rivals ignored for two more years.

## Examples

- A fintech scans UPI complaints on Twitter and finds small merchants struggle with refunds — launches a merchant-first refund tool.
- A skincare brand studies Sephora reviews and finds "sensitive skin" combo products are rare, building a new sub-brand around it.

---

## Audited Appendix

# Market Analysis and White Spaces
**Course:** Product Management and New Product Development
**Module:** Content / Market Analysis
**Audited on:** 2026-04-18
**Source files reviewed:** `product-management-npd/content/02-market-analysis-white-spaces.md`

---

## 1. Topic Snapshot
Market analysis maps the competitive and customer landscape to find *white spaces* — unmet needs or underserved segments. For an IT/AI/Product/Consulting leader, this determines whether a bet competes in a red ocean or creates new demand. Decision it helps make: *"Is there a gap big enough and defensible enough to be worth building for, and what validates it before we spend engineering dollars?"*

Cross-reference: Blue Ocean / ERRC / value innovation covered in `strategic-management/05-business-strategy.md`. Five Forces / strategic group map in `strategic-management/03-industry-analysis.md` and `04-internal-analysis.md`.

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| White Space | — | Unmet / underserved market need with no dominant product | Finds uncontested opportunity | Segment × need × dominance grid | Product, strategy |
| Market Analysis | — | Study of customers, competitors, trends | Upstream of product decisions | Coverage score | Strategy, PM |
| TAM | Total Addressable Market | Revenue if 100% share | Top-line ceiling | $ / year | Investor decks |
| SAM | Serviceable Addressable Market | Subset you can serve given business model | More realistic ceiling | $ / year | Investor decks |
| SOM | Serviceable Obtainable Market | Share realistically capturable | Year-3 target | $ / year | Investor decks |
| Bottom-up Sizing | — | Sizing from unit economics × customers | More defensible | Customers × ARPU | Product, strategy |
| Top-down Sizing | — | % of big market | Easier, weaker | Market × share | VC decks |
| Segmentation | — | Grouping customers by shared attributes | Enables targeting | # segments; within-segment variance | Marketing, product |
| ICP | Ideal Customer Profile | Best-fit customer definition | Focuses acquisition | Fit score | B2B |
| JTBD | Jobs To Be Done | "What job is the customer hiring this product for?" | Anti-demographic framing | Job statement + outcomes | Christensen et al |
| Forces of Progress (JTBD) | Push-Pull-Anxiety-Habit | 4 forces driving switch | Deeper JTBD analysis | Force-strength audit | Modern JTBD (Moesta) |
| Competitive Landscape | — | Map of competitors and alternatives | Orients positioning | 2x2 / strategic group | Strategy |
| Strategic Group Map | — | 2-axis clustering of competitors | Identifies white space | Occupied vs empty cells | See strategic-management/04 |
| Non-consumer | — | People NOT buying in the category | Source of Blue Ocean | Addressable count | Kim & Mauborgne |
| Underserved vs Overshot | — | Disruption-theory customer states | Predicts where disruption can win | Requirements vs performance | Christensen |
| Switching Cost | — | Pain of moving from competitor | Low = easier capture | Hours, $, integration complexity | Product, ICP |
| NPS Gap Analysis | — | Compare NPS of your product vs incumbent | Surfaces differentiator fit | Δ NPS | Product research |
| Voice of Customer | VoC | Qualitative input from customers | Ground truth | Interviews, reviews scraped | Product research |
| Review Mining | — | Scraping app-store / G2 / Reddit reviews | Cheap JTBD data | # reviews analysed | Modern product research |
| Market Map | — | Category taxonomy of competitors | Orientation tool | Coverage of players | Research analysts |
| Category Design | — | Define a new category to avoid head-on comparison | Play Bigger concept | Category defined? | Modern startup positioning |
| Market Segment Size | — | # buyers × ARPU × adjustment | Quantifies opportunity | $ | Sizing |
| Hype Cycle | — | Gartner framework: trigger → peak → trough → recovery | Timing entry | Position on curve | Analyst reports |
| Adoption Curve | — | Rogers' 5-segment diffusion: innovators → laggards | Targets entry market | Current % adopted | Diffusion theory |
| Crossing the Chasm | — | Moore's concept of moving from early adopters to majority | Product-market-expansion | Segment-ladder progression | Tech-startup strategy |

> `SAM/SOM`, `Bottom-up/Top-down sizing`, `ICP`, `JTBD + Forces`, `Strategic Group Map`, `Non-consumer`, `Underserved/Overshot`, `Review Mining`, `Category Design`, `Hype Cycle`, `Adoption Curve`, `Crossing the Chasm` are standard extensions. `[verified from model knowledge, not source]`.

---

## 3. Frameworks & Matrices

### Framework 1: White-Space Identification Grid
**Purpose:** Systematically find gaps by crossing customer needs (rows) with competitor coverage (columns).

**Text Diagram:**
```
                 COMPETITOR COVERAGE
           Player A   Player B   Player C   None / Weak
        ┌──────────┬──────────┬──────────┬────────────────┐
 Need 1 │ Strong   │  Strong  │  Weak    │                │
 Need 2 │  Weak    │  Weak    │  Strong  │                │
 Need 3 │          │          │          │   WHITE SPACE!  │
 Need 4 │  Strong  │          │          │                │
 Need 5 │          │          │   Weak   │   SPACE (small) │
        └──────────┴──────────┴──────────┴────────────────┘

 White space = needs no one serves well AND segment is large enough.
 "Space (small)" = real gap but likely not big enough to fund a business.
```

Components:
- **Rows:** distinct customer jobs / needs (derived from JTBD interviews)
- **Columns:** current competitors
- **Cells:** strength of competitor's solution for that need

**IT/AI/Product/Consulting worked example:** An AI-assistant startup maps needs (code completion, spec writing, test generation, doc search, code review) × competitors (GitHub Copilot, Cursor, Cody, Continue). Finding: "test generation with domain-specific fixtures for enterprise monoliths" → no dominant player. Validates with 20 interviews and 3 pilots. Builds specialised offering.

**When to pull this out in a meeting:** Market-entry debates; new product pitches; category-selection workshops.

---

### Framework 2: JTBD + Forces of Progress
**Purpose:** Move beyond "what features do customers want" to "what job are they trying to complete?"

**Text Diagram:**
```
   "When I ___ [situation],
    I want to ___ [motivation],
    so I can ___ [outcome]."

  Four Forces driving switch to a new solution:

  [PUSH] ─► current situation dissatisfaction ──────►  NEW
                                                       SOLUTION
  [PULL] ─► new solution's attraction    ──────►
  
  ◄── [ANXIETY] about new solution 
  ◄── [HABIT] of current solution

  Customer switches only when PUSH + PULL > ANXIETY + HABIT.
```

Components:
- **Job statement:** situation + motivation + outcome
- **Push:** why current solution frustrates
- **Pull:** what makes new option attractive
- **Anxiety:** fear of new
- **Habit:** comfort of existing

**IT/AI/Product/Consulting worked example:** A data-engineering startup interviewing CDOs: Job = "When we push a data-quality change, we want to validate it won't break downstream consumers." Current: spreadsheets + Slack. Push: 4-hour incidents/month. Pull: automated lineage + tests. Anxiety: yet-another-tool fatigue. Habit: current workflow is "good enough." Switch unlocked when Pull >> (Anxiety+Habit) via a 7-day ROI promise.

**When to pull this out in a meeting:** Customer-research synthesis; messaging design; sales-play creation.

---

### Framework 3: TAM-SAM-SOM Sizing with Dual Method
**Purpose:** Size a white space using both top-down AND bottom-up; reconcile.

**Text Diagram:**
```
   ┌────────────────────────────────┐
   │         TAM                     │  Top-down: $120B global
   │       (Total Addressable)       │  Bottom-up: 5M users × $200 = $1B
   │                                  │  (Discrepancy flag → investigate)
   └───┬──────────────────────────┬─┘
       │                          │
       ▼                          ▼
   ┌─────────────┐          ┌─────────────┐
   │    SAM      │          │   SAM       │
   │ (Serviceable│          │  Serviceable│
   │  Addressable)│          │  (bottom-up)│
   │  $20B       │          │   $400M     │
   └─────────────┘          └─────────────┘
       │                          │
       ▼                          ▼
   ┌─────────────┐          ┌─────────────┐
   │    SOM      │          │   SOM       │
   │ (3-yr grab) │          │             │
   │   $300M     │          │   $80M      │
   └─────────────┘          └─────────────┘
```

Components:
- **TAM:** market ceiling (top-down: IDC/Gartner; bottom-up: unit × ARPU)
- **SAM:** subset you can actually reach (geo, channel, product-fit filter)
- **SOM:** realistic 3-year obtainable share

**IT/AI/Product/Consulting worked example:** A vertical AI startup targeting law firms.
- Top-down: Legal-tech market $30B (IDC).
- Bottom-up: 500k US+UK firms × 100 lawyers × $40/mo × 50% addressable = $12B.
- SAM (mid-market firms, 50-500 lawyers): $2.5B.
- SOM (year-3 at 3% share of SAM): $75M ARR target.

Decision: plausible bet for a $150M raise at typical multiples.

**When to pull this out in a meeting:** Any market-sizing claim in an investor deck or internal business case.

---

## 4. Formulas

### Formula 1: Bottom-Up Market Sizing
**Formula:** `TAM_bottom-up = Σ (segment_size × ARPU × conversion_rate)`

**Variables:**
- segment_size = # of target customers in segment
- ARPU = average revenue per customer per period
- conversion_rate = % likely to actually buy (given price/value fit)

**Why this formula exists:** Top-down numbers (from analysts) are often inflated by 3-10×. Bottom-up is sanity-check reality.

**How to interpret the output:**
- Bottom-up ≈ top-down → sizing defensible
- Bottom-up << top-down → investigate; either segment is smaller OR addressable portion tighter
- Bottom-up >> top-down → likely overstating ARPU or count

**Worked example:** SaaS vertical AI for US healthcare.
- Segment: 6,000 mid-sized hospitals
- ARPU: $150k/yr (tier pricing)
- Conversion: 20% (likely buyers of AI-governance tooling in 5 years)
- TAM = 6,000 × 150k × 0.20 = **$180M/yr**

**Data source:** Segment data from industry registries (AHA directory for hospitals, Crunchbase, ZoomInfo). ARPU from pricing research and comparable deals. Conversion from interviews + pipeline conversion rates.

---

### Formula 2: Opportunity Scoring (JTBD Outcome-Driven Innovation)
**Formula:** `Opportunity Score = Importance + max(Importance − Satisfaction, 0)`

**Variables:**
- Importance = customer rating (1–10) of how important the outcome is
- Satisfaction = customer rating (1–10) of current-solution satisfaction

**Why this formula exists:** Ulwick's ODI method — prioritises underserved outcomes (high importance, low satisfaction).

**How to interpret the output:**
- Score > 15 → strong underserved opportunity
- 10–15 → moderate
- < 10 → adequately served; low priority

**Worked example:** Survey 100 data engineers on "push data-quality changes without breaking consumers":
- Importance = 9
- Satisfaction = 3 (spreadsheets + Slack current solution)
- Opportunity Score = 9 + (9-3) = **15** → strong.

Other outcomes in the survey:
- "Set up new pipeline" — Importance 7, Satisfaction 8 → Score 7 (overserved; don't build here).
- "Understand cost of pipelines" — Importance 8, Satisfaction 5 → Score 11 (moderate).

Decision: prioritise the top-scoring opportunity as the MVP focus.

**Data source:** Customer surveys via Typeform / Qualtrics; synthesised in Python + published in product doc.

---

### Formula 3: White-Space Attractiveness Score
**Formula:** `Attractiveness = (Unmet Need Strength × Segment Size × Defensibility) / Time to First Product`

**Variables:**
- Unmet Need (1–10): how strongly validated through research
- Segment Size ($ TAM or count)
- Defensibility (1–10): can we build moats (data, network, switching cost, IP)?
- Time to First Product (months)

**Why this formula exists:** Balances pain level, market size, moat potential, and speed.

**How to interpret the output:**
- High score → build now
- Low score → either need not validated, market too small, not defensible, or too slow
- Compare across candidates; pick top 1-2

**Worked example:** Three opportunities:
| Opp | Unmet (1-10) | TAM ($M) | Defens (1-10) | Time (mo) | Score |
|-----|--------------|----------|---------------|-----------|-------|
| AI test gen for monoliths | 8 | 800 | 7 | 6 | 7,467 |
| Generic code summary | 4 | 2,000 | 2 | 3 | 5,333 |
| Law-firm AI | 9 | 180 | 8 | 9 | 1,440 |

Winner: AI test gen — despite smaller TAM vs generic, high unmet + defensibility + fast time → highest score.

**Data source:** Scores populated jointly by product + research + engineering in a prioritisation workshop.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|-------|
| Use top-down sizing alone | Pair top-down with bottom-up; investigate gaps |
| Segment by demographics only | Add JTBD / behavioural / pain segments |
| Interview only current customers | Include non-customers and churned users |
| Declare "white space" from a hunch | Build a competitor × need grid with evidence in each cell |
| Skip opportunity-score testing | Run ODI-style surveys; prioritise high-score unmet needs |
| Build based on feature asks | Build based on validated JTBD and outcomes |
| Ignore hype-cycle timing | Map where your category sits (trigger → peak → trough → slope) |
| Copy competitors feature-for-feature | If a white space exists, go different; if not, rethink entry |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: Vertical AI Startup Finding Its White Space
**Situation:** A 15-person team considers entering GenAI. Hot space — 200+ competitors.

**Applicable framework/metric:** White-Space Grid + JTBD Opportunity Score + Bottom-up Sizing.

**Analysis:**
- Grid: 8 JTBD rows × 12 competitor columns. Found two weakly served cells: (a) regulated legal-compliance workflows, (b) SRE incident-response runbook AI.
- Opportunity scores: legal-compliance 16 (strong); SRE 12 (moderate).
- Bottom-up TAM: Legal-compliance $180M (US mid-market law firms); SRE $320M.
- Defensibility: Legal-compliance = proprietary law-firm partnerships; SRE = incident-data feedback loops.
- Time: Legal 9 months, SRE 5 months.

**Decision rule:** Pick highest Attractiveness score; accept lower TAM if unmet score and defensibility higher.

**Action (Monday morning):** Focus on legal-compliance AI. Run design-partner programme with 8 mid-market firms in next 90 days. Target MVP Q3.

---

### Scenario 2: Consulting Firm Advising Client on Regional Language White Space
**Situation:** An Indian edtech client competes in English + Hindi. Revenue flat. CEO asks: "Where do we expand?"

**Applicable framework/metric:** White-Space Grid + Non-consumer Analysis.

**Analysis:**
- Scraped 2,000 reviews of 10 competitors: "no regional language support" appears 340 times.
- 4 regional languages have >50M speakers each with no dominant player.
- Opportunity score for "Tamil-language test prep": Importance 9, Satisfaction 1 → Score 17.
- Bottom-up: Tamil Nadu 8M students × 20% addressable × $20/yr × 30% conversion = $9.6M ARR.
- Defensibility: content library in Tamil is moat; 18-month lead time over competitors.

**Decision rule:** Launch if Opportunity Score > 14 AND bottom-up ARR > 5× engineering cost.

**Action:** Launch Tamil-first test prep product. Budget $1.5M. Target 100k users in year 1; 500k by year 3.

---

### Scenario 3 (Anti-example): Sizing a White Space with TAM-Theater
**Situation:** A startup pitches investors with "trillion-dollar TAM" claim based on "global software spend."

**Applicable framework/metric:** Top-down vs Bottom-up sanity check.

**Analysis (what goes wrong):**
- Top-down: $1T global software = marketing number, not addressable
- Bottom-up: realistic segment = 10,000 mid-market firms × $50k ARPU × 30% conversion = $150M → 3 orders of magnitude off
- VCs spot the gap; term sheet withdrawn

**Cost of this mistake:** Lost fundraising round; founders look unprepared; 9-month delay.

**Decision rule:** Every TAM claim in deck has bottom-up corroboration OR is removed.

**Action:** Redraft deck with honest bottom-up sizing + path to TAM growth. Present as "today's SAM $150M, expanding to $1B over 5 years as product footprint grows" — credible and defensible.

---

## 7. Implementation Playbook

1. **Build a competitor × need grid** — Miro template; populate from customer interviews + review mining; used in every GTM kickoff.
2. **Run weekly JTBD interviews** — 2+ per week by PM; notes shared with Trio.
3. **Instrument review-mining pipeline** — scrape G2, Capterra, Reddit, App Store; cluster themes with topic modelling.
4. **Size every opportunity with dual-method TAM-SAM-SOM** — bottom-up required; spreadsheet template.
5. **Use Opportunity Score for feature prioritisation** — ODI survey at least quarterly; top-3 unmet outcomes feed backlog.
6. **Build a strategic group map quarterly** — update competitor positions; look for movement into white spaces.
7. **Validate with design partners** — 6-8 paying design partners before full GTM; 60-day proof points.
8. **Map category to hype cycle** — adjust entry timing (avoid Peak of Inflated Expectations).

---

## 8. Content Quality Audit

**Covered well:**
- Defines white space, TAM, segmentation, JTBD, competitive landscape.
- Notes need for non-customer interviews.
- Mentions sizing + validation.

**Underplayed or missing:**
- No SAM/SOM distinction.
- No bottom-up vs top-down sizing discipline.
- No JTBD Forces of Progress (Moesta, "When Coffee & Kale Compete").
- No Opportunity Score formula (Ulwick's ODI).
- No Hype Cycle / Adoption Curve / Crossing the Chasm.
- No category design (Play Bigger).
- No explicit review-mining / voice-of-customer pipeline.
- Zero reference to Christensen, Moesta, Ulwick, Moore, Kim & Mauborgne (cross-referenced in strategic-management but not here).

**Supplement with:**
- *Competing Against Luck* — Clayton Christensen, Taddy Hall, Karen Dillon, David Duncan (2016, Harper). JTBD canonical.
- *When Coffee and Kale Compete* — Alan Klement (2018). JTBD Forces of Progress.
- *The Jobs to Be Done Playbook* — Jim Kalbach (2020, Rosenfeld).
- *Outcome-Driven Innovation* — Tony Ulwick, *Strategy & Leadership* (2002); *What Customers Want* book (2005).
- *Crossing the Chasm* — Geoffrey Moore (3rd ed 2014, HarperBusiness).
- *Play Bigger* — Al Ramadan, Dave Peterson, Christopher Lochhead, Kevin Maney (2016). Category design.
- *Blue Ocean Strategy* — Kim & Mauborgne (2005). Value innovation.
- HBR: "Know Your Customers' Jobs to Be Done" — Christensen, Hall, Dillon, Duncan, *HBR*, Sept 2016.
- HBR: "The Big Idea: What Makes Products Succeed" — Ulwick, *HBR*, Jan 2002.
- Gartner Hype Cycle methodology (www.gartner.com).
- HBS case: "Slack: The Most Viral Business Application of All Time?" — white-space exploitation.
- HBS case: "Zoom: Growing Up Amidst COVID" — market-timing white space.
- IIMA case: "Zerodha: Disrupting Indian Broking" — Indian white-space in trading.

**Red flags in the source:**
- "A white space only matters if it has enough buyers" — correct; no sizing method taught.
- JTBD named but not operationalised; reader learns the term but not the forces / survey method.
- No warning about TAM theatre.
- Scenario is good (Tamil-first edtech) but lacks the scoring rigour — lucky rather than framework-driven.

**Connects to:**
- `audit_management_course/product-management-npd/01-role-of-product-managers.md` (PM role)
- `audit_management_course/product-management-npd/04-product-ideation-techniques.md` (ideation)
- `audit_management_course/product-management-npd/08-product-opportunities-identification.md` (opportunity ID)
- `audit_management_course/strategic-management/03-industry-analysis.md` (Five Forces)
- `audit_management_course/strategic-management/05-business-strategy.md` (Blue Ocean)
- `audit_management_course/marketing-research/*` (research methods)
- `audit_management_course/consumer-behaviour/06-segmentation-targeting-and-positioning.md` (STP)
- `audit_management_course/startup-strategy/02-opportunity-identification.md` (startup opportunity ID)

---

## 9. Quick-Recall Card

```
Topic: Market Analysis and White Spaces
Core idea: Find unmet jobs in underserved segments; validate with dual-method sizing.
Key metric/formula: TAM-SAM-SOM bottom-up; Opportunity Score = Importance + (Importance − Satisfaction); Attractiveness = UnmetNeed × Size × Defensibility / Time.
Framework trigger: New product / market-entry decisions; GTM kickoff; category-design debates.
Watch out for: TAM theatre; demographic-only segmentation; "vague JTBD" without forces analysis.
Monday action: Build competitor × JTBD grid; run 5 non-customer interviews; compute dual-method TAM.
As a PM/Consultant/AI Lead, the one question to answer with this framework is:
"Which customer job is underserved, sizeable, and defensible — and do I have evidence on all three?"
```

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Pass 1 average: 4.8
Sections rewritten: none (no criterion <4/5)
Enrichments applied: [cross-course links to product-management-npd/01, 04, 08; strategic-management/03, 05; marketing-research; consumer-behaviour/06; startup-strategy/02. Christensen/Hall/Dillon/Duncan 2016, Klement 2018, Kalbach 2020, Ulwick 2002/2005, Moore 2014, Ramadan et al 2016, Kim/Mauborgne 2005. HBS Slack + Zoom, IIMA Zerodha. Anti-example Scenario 3 (TAM theatre). Data sources: Crunchbase, ZoomInfo, AHA directory, G2/Capterra review mining, Typeform/Qualtrics ODI surveys. Decision-maker view in Quick-Recall.]
Final scores: [1:5, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:5] — average 5.0
Pass 2 completed: 2026-04-18 02:00
-->
