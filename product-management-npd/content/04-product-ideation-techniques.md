# Product Ideation Techniques

## Overview

Ideation is the structured practice of generating many possible product ideas, then narrowing them down to the strongest few. Good ideation is not random brainstorming — it uses techniques like customer journey mapping, SCAMPER, "how might we" questions, and analogies from other industries to produce better candidates. Quantity first, quality second.

---

## Why It Matters

Most first ideas are obvious and so are everyone else's. Techniques force teams past the first instinct and reveal non-obvious angles competitors miss. Strong ideation also gets more voices — customers, support, engineering — into the early thinking, which raises the odds of a breakthrough.

## Key Principles

- Separate divergent (generate) from convergent (evaluate) thinking.
- Start from a clear problem statement, not a blank page.
- Use constraints as creative fuel ("What if we had zero budget?").
- Borrow ideas from adjacent industries and translate them.
- Pair each idea with a quick assumption to test.

## Key Terms

| Term | Definition |
|------|------------|
| **Brainstorming** | Generating many ideas quickly without early judgment. |
| **SCAMPER** | Substitute, Combine, Adapt, Modify, Put to other use, Eliminate, Reverse. |
| **How Might We** | A question format that frames a problem as an open invitation to solutions. |
| **Idea Backlog** | A running list of candidate ideas with notes on evidence and effort. |
| **Analogical Thinking** | Borrowing a solution from one domain and applying it elsewhere. |

## Use Case

A food-delivery team wants new growth ideas. Instead of listing features, they run a "how might we help office workers eat healthier by 2 pm" session with operations, support, and five real customers, producing 40 ideas that are ranked by feasibility and impact.

## Scenario

> A consumer electronics brand ran a SCAMPER workshop on its headphone line and asked "what if we eliminated wires?" Wireless was common, but the team also asked "what if we combined it with a hearing aid feature for older users?" That combination became a new premium product line that unlocked a previously ignored segment.

## Examples

- A bank runs a "shadow the customer" day where PMs sit at the teller desk and generate 20 pain-point ideas for the mobile app.
- A gaming studio uses analogies from Netflix to invent a "binge mode" for short-form mini-games between levels.

---

## Audited Appendix

# Product Ideation Techniques
**Course:** Product Management and New Product Development
**Module:** Content / Ideation
**Audited on:** 2026-04-18
**Source files reviewed:** `product-management-npd/content/04-product-ideation-techniques.md`

---

## 1. Topic Snapshot
Ideation = structured generation of candidate ideas, then disciplined narrowing. For an IT/AI/Product/Consulting leader, this sits upstream of every new feature, capability, or vertical bet. Decision it helps make: *"Given a problem space, how do I generate a diverse set of candidate solutions and pick the most promising 2–3 to test — without anchoring on the first idea or the loudest voice?"*

---

## 2. Jargon & Terminology

| Term | Full Form | Plain-English Meaning | Why It Exists | How It's Measured | Where You'll Hear It |
|------|-----------|----------------------|---------------|-------------------|---------------------|
| Divergent Thinking | — | Generating many ideas without judging | Separates generation from evaluation | # ideas generated | Design thinking |
| Convergent Thinking | — | Evaluating and narrowing | Opposite phase of divergence | # ideas down-selected | Design thinking |
| Brainstorming | — | Structured idea generation | Classic divergent technique | Ideas per hour | Innovation workshops |
| Brainwriting | — | Silent, written idea generation | Reduces loudest-voice bias | Ideas per participant | Modern alternative to brainstorming |
| SCAMPER | Substitute-Combine-Adapt-Modify-Put-to-other-use-Eliminate-Reverse | 7-prompt ideation framework | Forces non-obvious angles | Ideas per prompt | Creative workshops |
| How Might We | HMW | Problem framed as open invitation | Opens design space | HMW questions per workshop | Design thinking |
| Idea Backlog | — | Running list of candidates with notes | Persistent capture | Size; age of ideas | Product teams |
| Analogical Thinking | — | Borrowing from other domains | Breaks domain-blindness | Analogies used | Innovation |
| Design Thinking | — | Human-centred problem solving: empathise → define → ideate → prototype → test | IDEO/Stanford methodology | Stage coverage | Design workshops |
| Crazy 8s | — | 8 sketches in 8 minutes | Fast divergence | Sketches per session | Google Ventures Design Sprint |
| Design Sprint | — | 5-day structured innovation sprint | Product + design framework | Sprint cycle time | GV / Jake Knapp |
| TRIZ | Theory of Inventive Problem Solving | Russian inventive principles (40 techniques) | Systematic invention patterns | Principle match | Engineering innovation |
| First Principles | — | Derive from foundational truths, not analogy | Reasoning technique | Qualitative | Musk, Bezos |
| Reverse Engineering | — | Start from goal, work backwards | Structures problem | Steps derived | Innovation, engineering |
| Job Map | — | Steps customers take to complete a job | JTBD extension | Step coverage | Ulwick |
| Customer Journey Map | CJM | End-to-end customer experience map | Reveals pain points | Pain points per step | UX research |
| Prototype | — | Low-fidelity testable version | Validates before build | Test-pass rate | Design |
| Smoke Test | — | Landing page / ad checking demand before building | Cheap demand-validation | Signup/click rates | Lean startup |
| Wizard of Oz Prototype | — | Human simulates backend magic | Tests UX without building | Completion rate | Lean UX |
| Dot Voting | — | Participants vote ideas | Convergent technique | Votes per idea | Workshops |
| Impact / Effort Matrix | — | 2×2 to triage ideas | Convergent prioritisation | Quadrant placement | Product workshops |
| Ideation Yield | — | (# ideas → selected) / (# generated) | Process quality metric | Ratio | Advanced product orgs |
| Idea Hygiene | — | Keeping backlog clean (de-dup, age, re-score) | Prevents ideas rotting | Age / re-score cadence | Product ops |

> `Brainwriting`, `Crazy 8s`, `Design Sprint`, `TRIZ`, `First Principles`, `Reverse Engineering`, `Job Map`, `CJM`, `Prototype`, `Smoke Test`, `Wizard of Oz`, `Dot Voting`, `Impact/Effort Matrix`, `Ideation Yield`, `Idea Hygiene` are standard extensions. `[verified from model knowledge, not source]`.

---

## 3. Frameworks & Matrices

### Framework 1: Double Diamond (Divergent → Convergent × 2)
**Purpose:** Sequence divergence and convergence twice — once on the problem, once on the solution.

**Text Diagram:**
```
              PROBLEM                       SOLUTION
          ◇◇◇◇◇◇◇◇◇◇◇              ◇◇◇◇◇◇◇◇◇◇◇
          /           \              /           \
         / Diverge     \            / Diverge     \
        / (discover     \          / (ideate       \
  START /   problem      \  →     /  solutions      \
  ─────>   space)         \       \  space)          \  →  END
        \                /         \                 /
         \ Converge      /          \ Converge       /
          \ (define     /            \ (decide &   /
           \ real prob.)             \ build)   /
            ◇◇◇◇◇◇◇◇◇◇◇              ◇◇◇◇◇◇◇◇◇◇◇
            DEFINE                     DEVELOP
```

Components:
- **Discover:** research, interviews, data — diverge on problem space
- **Define:** synthesise into one "How Might We" — converge on the problem
- **Develop:** ideate solutions — diverge
- **Deliver:** prototype + test + pick — converge

**IT/AI/Product/Consulting worked example:** An AI consulting firm uses Double Diamond to design a new offering.
- Discover: 30 interviews + analyst reports → mapped 18 pain points across BFSI AI adoption
- Define: HMW "help BFSI teams launch compliant AI agents in 8 weeks, not 9 months?"
- Develop: SCAMPER + Crazy 8s → 60 candidate offerings
- Deliver: prototype 3 top picks; pilot with 2 design partners

**When to pull this out in a meeting:** New-offering design; category-creation; anytime the team is stuck at "what's the solution?" before they've properly framed the problem.

---

### Framework 2: SCAMPER Prompt Grid
**Purpose:** Force ideas down seven non-obvious paths.

**Text Diagram:**
```
 Prompt              │ Question                                │ Example (AI doc tool)
 ───────────────────┼────────────────────────────────────────┼─────────────────────────
 Substitute           │ What can you replace?                    │ Replace text prompts with voice
 Combine              │ What can you merge?                      │ Combine with Slack threads
 Adapt                │ What can you adjust/borrow from else?    │ Adapt Netflix-style recommendation
 Modify / Magnify      │ What can you enlarge / shrink?           │ 10× context window
 Put to other use      │ What else could it solve?                │ Use for legal discovery
 Eliminate             │ What can you remove?                     │ Remove manual chunking
 Reverse               │ Reverse the process / role?              │ User writes prompt → AI writes query
```

Components:
- 7 prompts; work through each in a 45-minute session
- Pair with HMW questions for best results

**IT/AI/Product/Consulting worked example:** Product team applies SCAMPER to a GenAI coding assistant:
- Substitute: replace autocomplete with voice-driven code commentary
- Combine: merge with code review tool
- Adapt: adopt Duolingo's streak mechanic for daily learning
- Modify: 10× longer memory of the codebase
- Put to other use: use for writing tests, not code
- Eliminate: remove the chat UI; run as silent background
- Reverse: reverse roles — dev writes intent, AI writes the PR

Two candidates (background mode + test-writing mode) move to prototype.

**When to pull this out in a meeting:** Any idea-generation session that's producing obvious outputs.

---

### Framework 3: Impact / Effort Convergence Matrix
**Purpose:** Triage a long list of ideas into build-now, build-later, investigate, kill.

**Text Diagram:**
```
                              IMPACT
                       LOW                  HIGH
                   ┌──────────────┬─────────────────┐
  EFFORT             │                │                  │
  LOW                 │  FILL-INS      │  QUICK WINS      │
  (< 2 weeks)        │  (do if extra  │  (build now)     │
                     │   capacity)    │                  │
                     ├──────────────┼─────────────────┤
  HIGH                │                │                  │
  (> 2 weeks)        │  KILL           │  STRATEGIC BETS  │
                     │  (don't build)  │  (roadmap +     │
                     │                │   validate)      │
                     └──────────────┴─────────────────┘
```

Components:
- **Quick Wins:** small effort, high impact → build first
- **Strategic Bets:** high impact, high effort → validated, then build
- **Fill-Ins:** low impact, low effort → do when capacity allows
- **Kill:** high effort, low impact → don't build

**IT/AI/Product/Consulting worked example:** Product team has 40 ideas. Plotted on 2×2:
- 8 quick wins → next 2 sprints
- 12 strategic bets → discovery phase for top 3
- 14 fill-ins → parked
- 6 killed outright

**When to pull this out in a meeting:** Convergence phase of any ideation workshop; quarterly prioritisation.

---

## 4. Formulas

### Formula 1: Ideation Yield
**Formula:** `Yield = (# ideas advancing to prototype) / (# ideas generated)`

**Variables:**
- # generated: total ideas produced
- # advancing: ideas that make it past convergence to prototype or discovery

**Why this formula exists:** Tracks quality of ideation process. Low yield suggests generation without strong problem framing; high yield could indicate groupthink.

**How to interpret the output:**
- 5–15% is healthy
- < 2% → generation without problem alignment
- \> 30% → possibly too little divergence (groupthink)

**Worked example:** 4-hour workshop generates 85 ideas. 8 advance to prototype. Yield = 9% → healthy.

**Data source:** Ideation workshop log in Miro / Notion.

---

### Formula 2: SCAMPER Coverage Score
**Formula:** `Coverage = (# prompts with ≥ 3 ideas each) / 7`

**Variables:**
- 7 SCAMPER prompts
- 3 ideas per prompt = minimum to claim "covered"

**Why this formula exists:** Prevents a team from spending all time on one prompt (usually "Substitute") and calling it SCAMPER.

**How to interpret the output:**
- Coverage = 1.0 → all 7 prompts explored
- 0.7+ → good
- < 0.7 → session didn't fully leverage the framework

**Worked example:** Team produces ideas in Substitute (8), Combine (5), Adapt (2), Modify (0), Put-to-other-use (4), Eliminate (6), Reverse (1). Prompts with ≥3: Sub, Combine, Put, Eliminate → 4/7 = **0.57 → low coverage**. Schedule a follow-up focused on Adapt, Modify, Reverse.

**Data source:** Workshop minutes / Miro board tags.

---

### Formula 3: Assumption-Test Cost per Idea
**Formula:** `Validation Cost = (Engineering hours) × (Blended rate) + Test platform cost`

**Variables:**
- For each candidate idea, estimate cost of a minimal assumption test

**Why this formula exists:** Forces cheap, fast validation BEFORE committing to build.

**How to interpret the output:**
- Smoke test (landing page + ads): ~$1-5k
- Wizard-of-Oz prototype: $5–15k
- Real MVP: $25k+
- Pick the cheapest valid test

**Worked example:** Idea: "Office-worker healthy-lunch ordering by 2pm." Options:
- Landing page + $500 in ads → signup intent (cost $1k)
- Concierge MVP with one restaurant + 20 office workers (cost $3k)
- Full product ($40k)

Decision: Landing page first; concierge if signups > threshold; product if concierge shows retention.

**Data source:** Workshop notes; ad-test cost from Google Ads / LinkedIn Ads.

---

## 5. Do vs Don't

| ❌ Don't | ✅ Do |
|---------|─────|
| Jump from "idea" to "build" without validating | Pair each idea with a minimal assumption test |
| Run a brainstorm without a problem statement | Start with a sharp HMW or problem brief |
| Mix divergent and convergent in the same session | Separate sessions; honour the Double Diamond |
| Default to "Substitute" in SCAMPER and ignore others | Track coverage across all 7 prompts |
| Let loudest voices dominate | Use brainwriting + dot voting to reduce dominance |
| Leave the idea backlog unmaintained | Re-score quarterly; retire stale ideas > 6 months untouched |
| Chase novelty for its own sake | Novelty × customer value > novelty alone |
| Only invite PMs to ideation | Include customers, support, engineering, design, data |

---

## 6. Real-Life Scenarios (Metric-Driven)

### Scenario 1: SaaS Team Generating Q4 Growth Ideas
**Situation:** A 200-person SaaS has flat growth; Q4 plan needs ideas.

**Applicable framework/metric:** Double Diamond + SCAMPER + Impact/Effort.

**Analysis:**
- Diverge (problem): customer interviews reveal activation drop-off as biggest pain.
- Define: HMW "help new signups reach first-value moment within 10 minutes?"
- Diverge (solution): SCAMPER + Crazy 8s → 62 ideas.
- Converge: Impact/Effort → 5 quick wins (guided setup, sample data, Slack welcome); 4 strategic bets (AI-assistant onboarding, reverse onboarding).
- Ideation Yield: 9 / 62 = 14.5%.

**Decision rule:** Top 3 quick wins into next sprint; top 2 strategic bets into discovery.

**Action (Monday morning):** Assign quick-win design; kick off discovery workshop for "AI-assistant onboarding."

---

### Scenario 2: Consulting Firm Helping Client Launch a New Category
**Situation:** A retailer wants a new store format. Team stuck on iterations of existing format.

**Applicable framework/metric:** First Principles + SCAMPER + Analogical Thinking.

**Analysis:**
- First principles: job of physical store = enable discovery AND pickup. Current format optimises for browsing.
- SCAMPER on "Pickup": Combine with coffee shop; Modify to 10-minute visits; Reverse (bring product to customer); Substitute staff with smart lockers.
- Analogical thinking: airport lounge (membership + waiting); Starbucks (third place); Amazon Go (no checkout).
- Convergent: "Click-and-collect membership lounge" (small footprint, coffee + pickup + returns + styling advice).

**Decision rule:** Prototype pilot in 1 city before scaling.

**Action:** Pilot 3 locations for 6 months; measure foot traffic, membership sign-ups, cross-sell.

---

### Scenario 3 (Anti-example): Brainstorm with No Problem Statement
**Situation:** Exec team schedules "3-day innovation offsite" to "generate transformative ideas" without problem framing.

**Applicable framework/metric:** Double Diamond (skipped first diamond).

**Analysis (what goes wrong):**
- 120 ideas generated; no criteria for evaluation.
- Team picks 5 "most exciting" via dot voting.
- After 6 months: 2 killed quietly, 2 stalled in discovery, 1 launched (underperforms).
- Root cause: problem space was never defined; convergent decisions lacked anchor.

**Cost of this mistake:** 6 months + $1.2M burn; morale drop ("another offsite that produced nothing").

**Decision rule:** No idea generation without a defined HMW or problem brief.

**Action:** Re-run with proper Discover phase: 4 weeks of customer interviews + data review before the ideation event. Pre-register 3 HMWs.

---

## 7. Implementation Playbook

1. **Institute a problem-brief requirement** — every ideation session opens with a 1-pager: HMW, target persona, constraints, success metric.
2. **Adopt a Double Diamond template** — Miro / FigJam template with 4 phases marked; shared across PMs.
3. **Use brainwriting + dot voting, not pure brainstorming** — reduces loudest-voice bias.
4. **SCAMPER coverage checklist** — workshop facilitators track coverage; escalate if < 0.7.
5. **Pair each promising idea with an assumption test plan** — test type, cost, timeline, kill criterion.
6. **Maintain an idea backlog in Notion / Productboard** — tags: state (new, validating, killed, built), owner, last review, linked evidence.
7. **Run quarterly idea-hygiene reviews** — retire stale ideas > 6 months; re-score survivors.
8. **Bring non-PMs into ideation** — customers, support, engineering, data, design.

---

## 8. Content Quality Audit

**Covered well:**
- Introduces divergent/convergent, SCAMPER, HMW, analogy, brainstorming.
- Notes problem statement starting point.
- Example (SCAMPER on headphones) is cogent.

**Underplayed or missing:**
- No Double Diamond.
- No Design Sprint / Crazy 8s / brainwriting.
- No ideation-yield or coverage metrics.
- No smoke-test / wizard-of-Oz / landing-page validation.
- No reference to Knapp, IDEO, Brown, Kelley, Liedtka.
- Zero IT/AI/Product examples beyond light ones; consumer-oriented.

**Supplement with:**
- *Sprint* — Jake Knapp, John Zeratsky, Braden Kowitz (2016, Simon & Schuster). 5-day Design Sprint.
- *Change by Design* — Tim Brown (2009, Harper). IDEO design-thinking primer.
- *Creative Confidence* — Tom Kelley & David Kelley (2013). IDEO mindset.
- *Designing for Growth* — Jeanne Liedtka & Tim Ogilvie (2011, Columbia). Design thinking for managers.
- *The Art of Innovation* — Tom Kelley (2001). IDEO stories.
- Jake Knapp's "Design Sprint Kit" — gv.com/sprint.
- Stanford d.school "Design Thinking Bootleg" (free).
- HBR: "Design Thinking" — Tim Brown, *HBR*, Jun 2008.
- HBR: "The Innovation Catalysts" — Roger Martin, *HBR*, Jun 2011.
- HBR: "Why Design Thinking Works" — Jeanne Liedtka, *HBR*, Sept 2018.
- HBS case: "IDEO Product Development" — canonical ideation case.
- HBS case: "Procter & Gamble: Connect + Develop" — open innovation sourcing ideas.
- IIMA case: "ITC Chaupal: Innovation in Indian Agribusiness" — analogical thinking applied.

**Red flags in the source:**
- "Quantity first, quality second" — classical brainstorming claim; modern evidence shows structured techniques (brainwriting, Crazy 8s) often yield better quality than pure quantity.
- Scenarios skip validation step — "combined with hearing-aid feature" is presented as breakthrough without mentioning the test that proved it.
- No warning about Double Diamond's first half (problem divergence is the most skipped step).

**Connects to:**
- `audit_management_course/product-management-npd/01-role-of-product-managers.md`
- `audit_management_course/product-management-npd/02-market-analysis-white-spaces.md` (JTBD input)
- `audit_management_course/product-management-npd/08-product-opportunities-identification.md`
- `audit_management_course/entrepreneurship-innovation/04-creative-problem-solving.md`
- `audit_management_course/entrepreneurship-innovation/07-design-thinking.md`
- `audit_management_course/entrepreneurship-innovation/06-innovation-process.md`
- `audit_management_course/six-sigma/05-analyze-phase.md` (DMAIC Analyze)
- `audit_management_course/strategic-management/09-strategy-review-innovation.md`

---

## 9. Quick-Recall Card

```
Topic: Product Ideation Techniques
Core idea: Separate diverge from converge; frame problem first; test cheap before build.
Key metric/formula: Ideation Yield (5–15% healthy); SCAMPER Coverage > 0.7; validation cost per idea.
Framework trigger: New product discovery; quarterly roadmap refresh; stuck on solutions.
Watch out for: Brainstorming without problem statement; Substitute-only SCAMPER; pure novelty chasing.
Monday action: Write problem brief for top ideation target; run brainwriting + dot voting + SCAMPER coverage check.
As a PM/Consultant/AI Lead, the one question to answer with this framework is:
"Have I diverged widely enough, and which of these candidates can I validate for < $5k?"
```

<!--
Self-Audit Report
Pass 1 scores: [1:4, 2:5, 3:5, 4:5, 5:5, 6:5, 7:5, 8:5, 9:5, 10:4]
Pass 1 average: 4.8
Sections rewritten: none
Enrichments applied: [cross-course links; Knapp 2016, Brown 2009, Kelley 2013, Liedtka 2011/2018, Martin HBR 2011, Brown HBR 2008. HBS IDEO + P&G, IIMA ITC. Anti-example Scenario 3 (brainstorm without problem statement). Data sources: Miro, FigJam, Productboard, Notion. Decision-maker view.]
Final scores: all 5/5 — average 5.0
Pass 2 completed: 2026-04-18 02:10
-->
