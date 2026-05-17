# Curriculum Overview

## Overview

This curriculum is built around a simple idea: if you want a strong nuclear-energy career, you need to understand both the plant and the digital layers around it. That means reactor and plant systems, but also controls, software, data, maintenance, and safety culture.

## Why This Topic Matters

Without a curriculum map, nuclear study becomes fragmented: one course on reactor physics, one on controls, one on Python, and no clear bridge to jobs or projects.

## Mental Model / Big Picture

```text
Plant understanding
    + controls and automation
    + software and data
    + safety and discipline
    = industry-ready nuclear profile
```

## Main Concepts / Core Concepts

- start from the plant, not from abstract theory alone
- connect every topic to operation, maintenance, or digitalization
- keep the learning path text-first and documentation-heavy
- treat projects as proof, not as optional extras

## Study Sequence

1. Foundation
1. Core Nuclear
1. Advanced
1. Projects
1. Resource deepening

## Practical / Design / Operational Sections

The intended outcome is one of these career combinations:

- nuclear systems + automation
- nuclear systems + embedded
- nuclear systems + simulation
- nuclear systems + industrial data
- nuclear systems + OT cyber

## Best Practices

- keep notes in your own words
- build one artifact per phase
- prioritize official sources
- review plant diagrams until the energy path feels obvious

## Common Pitfalls

- treating nuclear engineering as only reactor physics
- ignoring chemistry and electrical systems
- learning software without plant context
- learning theory without building anything

## Portfolio / Resume Application

Use this page as the baseline to explain why your profile is intentionally cross-disciplinary rather than narrowly academic.

## Next Step

Move to [Learning Roadmap](02_Learning_Roadmap.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

A curriculum overview earns its place only if it functions as a real map of the industry, not a cosmetic table of contents. In nuclear energy, the work that engineers actually do clusters into seven recognizable capability lanes: reactor analysis and core engineering, plant systems and thermal-hydraulics, instrumentation and control, chemistry and radiation protection, maintenance and reliability engineering, electrical systems, and digital modernization including data engineering, simulation, and OT cybersecurity. A curriculum overview should orient the learner toward those lanes from day one, so that every later topic is understood as preparation for a specific kind of engineering work, not as a self-contained academic subject.

For a learner coming from computer science or AI, the curriculum overview has a specific function: it shows where software becomes relevant without letting the learner mistake the software layer for the plant itself. Historian data is not the same as plant state. A dashboard is not the same as a safety function. An anomaly detection model is not the same as a trip. These boundaries exist in real nuclear work and the curriculum is designed to make them visible before they are crossed inadvertently.

The curriculum is also deliberately cross-disciplinary because real nuclear careers require it. An I&C engineer who does not understand the thermal-hydraulic consequence of the valve they are controlling will make worse design decisions. A plant data engineer who does not understand what drives radiation dose fields will build a maintenance dashboard that misses the most expensive constraints. The five intended career combinations — nuclear systems + automation, nuclear systems + embedded, nuclear systems + simulation, nuclear systems + industrial data, nuclear systems + OT cyber — all depend on breadth as well as depth.

### Industry Tool Stack

- `Plant P&IDs and system descriptions` — used to build topology understanding before any tool is applied to plant signals or systems
- `Python (numpy, matplotlib, pandas, scipy)` — used for calculations, data analysis, and notebook-based engineering studies across all curriculum lanes
- `Bash / Linux shell` — used for log processing, file management, and building text-first engineering habits
- `OpenMC` — used for reactor-physics calculations, benchmark replication, and Monte Carlo neutron transport studies
- `DCS / PLC / historian documentation` — used to understand how plant measurements flow from sensor to database to engineer
- `IAEA and NRC public documents` — used as primary references for regulatory framework, safety guidance, and technical standards across all curriculum lanes
- `Markdown + Git` — used for structured documentation that is version-controlled, reviewable, and demonstrates professional engineering communication discipline

### Step-by-Step Applied Workflow

1. Read the curriculum overview as a map of the industry, not as a reading list. For each section, ask: what kind of job does this lane lead to, and who hires for it?
2. Identify your current strongest lane (likely CS or data engineering) and your weakest one (likely reactor physics or plant systems). The curriculum is designed to build toward the weakest lanes while leveraging the strongest.
3. As you move through Foundation, track which topics belong to which capability lane. By the end of Foundation, you should be able to draw the plant as a system and name the lane that each part belongs to.
4. Enter Core Nuclear with one concrete specialization hypothesis: "I am targeting I&C and plant automation" or "I am targeting reactor analysis and simulation" or "I am targeting plant reliability and digital maintenance." This hypothesis will focus your project choices.
5. Build one portfolio artifact per lane before going deep in any single lane. Breadth artifacts prove you understand the context; depth artifacts prove you can deliver value in it.
6. By the end of Advanced, compare your portfolio against the hiring signals for your target role. Identify the gap between what you have and what a strong candidate for that role should show.
7. Use the Projects tier to close that gap with a final, portfolio-grade artifact that demonstrates your chosen specialization in a technically honest, plant-contextualized, and reviewable way.

### AI Integration

The curriculum overview is an appropriate place to be honest about where AI fits and where it does not. In nuclear operations, AI sits in one well-defined zone: advisory analytics, not protective or control functions. That means AI can support anomaly detection in equipment health monitoring, surrogate modeling for repeated engineering studies, document and operating-event summarization, and operator support tools that present analyzed information without acting on it. AI does not sit in protective I&C logic, safety function validation, or any role where a software error could cause or mask a plant safety event.

For a learner building a curriculum-aligned portfolio, the AI integration story should be specific to each capability lane: in reactor physics, AI appears as surrogate models trained on OpenMC output; in plant reliability, AI appears as anomaly detection on vibration or temperature trends; in I&C, AI appears only in post-event analysis tools, never in protective logic; in OT cybersecurity, AI appears in log analysis and threat-pattern detection. Each use case is defensible and bounded.

### Case Studies

- `IAEA Nuclear Knowledge Management programme`: The IAEA's Nuclear Knowledge Management (NKM) programme documents how operating member states approach nuclear workforce development, curriculum design, and competency frameworks. It provides the clearest public benchmark for what industry-aligned nuclear engineering education looks like at a national level, making it directly relevant to curriculum design choices.
- `NRC-sponsored university programmes (NERI, NEUP)`: The US Department of Energy's Nuclear Energy University Program (NEUP) publicly documents the research and education projects it funds, which gives a real-time map of which nuclear engineering competency areas are receiving institutional investment. Following NEUP project abstracts is a practical way to track where industry and government see the most valuable nuclear engineering capability gaps.
- `BARC and DAE public training frameworks`: The Bhabha Atomic Research Centre (BARC) and India's Department of Atomic Energy publish orientation materials for their training programs (including the BARC Training School) that describe what technical competencies are expected from entering graduate engineers in the Indian public nuclear sector — a directly relevant benchmark for India-facing learners.

### Failure Modes & Safety

The dominant curriculum failure mode is specialization too early. A learner who jumps directly into OpenMC simulation or ML-based anomaly detection before understanding what a reactor coolant pump does and why its head-flow curve matters will build technically functional tools that lack plant credibility. Reviewers from nuclear organizations can immediately distinguish a project built by someone who understands the physical system from one built by someone who only understands the algorithm.

The second failure mode is ignoring chemistry, electrical, and maintenance content because it seems less "technical" than reactor physics or software. In actual nuclear plant employment, chemistry engineers, reliability engineers, electrical protection engineers, and maintenance planners fill a very large fraction of total headcount — and the roles that combine these disciplines with digital skills are among the most in-demand. Excluding these lanes from self-study is a significant career constraint.

The third failure mode is the advisory/safety boundary confusion: building a tool that is framed or described as if it could make safety-relevant decisions, when it has not been validated to the standard required for such use. This is both a technical failure (the tool probably is not validated for that use) and a professional failure (it signals that the candidate does not understand nuclear engineering governance).

### Business & Commercial Layer

Nuclear engineering generates direct economic value through generation revenue, and its engineering support ecosystem creates commercial value through: outage cost reduction, asset-life extension, digital modernization projects, simulation and training products, regulatory compliance services, fuel services, and vendor product supply. The curriculum is designed to produce engineers who can participate in that value chain, not only in the physics and theory that surrounds it.

In India, the economic driver is somewhat different: DAE/NPCIL/BARC/IGCAR/AERB collectively represent the primary institutional demand for trained nuclear engineers in the country, and the career economics are those of the public-sector technical officer pathway. This curriculum is designed to support both tracks — the Indian public-sector pathway and the international private-sector pathway — because the technical competencies overlap substantially even though the commercial contexts differ.

Key commercial areas directly served by curriculum-trained engineers: plant I&C upgrades (Westinghouse Ovation, Framatome TELEPERM, Areva TELEPERM/SPPA-T2000 systems), digital historian and asset-health platforms deployed at nuclear utilities, PRA (probabilistic risk assessment) services at nuclear consultancies, OT cybersecurity assessments for nuclear plants under IEC 62645 and applicable regulatory frameworks, and simulation software for operator training and reactor-safety analysis.

### Hiring Signal

**Five job titles this curriculum overview maps to:**
- Nuclear Engineer / Graduate Engineer — at NPCIL, BARC, Westinghouse, EDF Energy, Framatome, Bruce Power
- Plant Systems Engineer — at nuclear EPCs (Aecom, Jacobs, Worley, Wood Group) and utilities
- I&C Engineer (Nuclear) / Automation Engineer (Nuclear) — at vendors, utilities, and I&C service firms
- Nuclear Data Engineer / Plant Historian Analyst — at nuclear digital platform vendors and utilities
- Probabilistic Risk Assessment (PRA) / Safety Analysis Engineer — at consultancies and utility safety functions

**Five curriculum-overview-level interview screens:**
1. "Describe the five major technical disciplines in a nuclear power plant and which type of engineer is responsible for each." Tests whether the candidate has a systems-level view of the organization of nuclear engineering work.
2. "Why does a software or data engineering background alone not qualify someone for nuclear plant digital work, and what additional competency is required?" Tests self-awareness about the gap the curriculum is designed to close.
3. "What is the difference between a safety-related and a non-safety-related system in a nuclear plant, and why does the distinction matter for digital work?" Tests the advisory/safety boundary understanding that the curriculum overview introduces.
4. "If you were designing a data pipeline that connects plant historian data to an anomaly detection model, what nuclear-specific constraints would you need to understand before starting?" Tests whether the candidate can map the curriculum's physical-system content onto a digital engineering problem.
5. "Which Indian institutions are involved in the nuclear engineering career pathway in India, and what roles does each play?" Tests India-specific nuclear ecosystem awareness that is directly relevant for BARC/NPCIL/IGCAR/AERB career tracks.

### Portfolio Projects

**Beginner:**
`nuclear-role-map`
Deliverables: one structured document mapping the seven capability lanes to tools, job titles, hiring organizations, and one portfolio signal for each lane.
Repo tree: `role_map.md`, `lane_overviews/`, `README.md`.
Acceptance criteria: (1) all seven capability lanes named with at least two real hiring organizations per lane, (2) the tools listed for each lane are real and specific (not generic "Python and data science"), (3) a one-sentence summary for each lane explaining what plant problem engineers in that lane actually solve.

**Intermediate:**
`cross-domain-nuclear-pack`
Deliverables: three small artifacts covering three different capability lanes — one reactor-physics or thermal-hydraulics notebook, one controls or I&C artifact, and one reliability or maintenance-analytics artifact.
Repo tree: `reactor_physics/`, `controls_ic/`, `reliability/`, `README.md` linking all three with a short explanation of how they relate to the same plant.
Acceptance criteria: (1) each artifact is tied to a specific plant system or engineering question, not a generic exercise, (2) all three use correct nuclear terminology and reference at least one real document or standard, (3) the README makes the connection between all three explicit.

**Advanced:**
`nuclear-digital-portfolio-architecture`
Deliverables: a full portfolio map document and three linked projects — one from reactor/thermal-hydraulics, one from data/digital, and one from safety/governance — presented as a coherent employment case for one specific target role.
Repo tree: `portfolio_map.md`, `project_1_reactor/`, `project_2_digital/`, `project_3_governance/`, `hiring_case.md`.
Acceptance criteria: (1) portfolio_map.md explains how all three projects demonstrate the specific competency combination required for the target role, (2) each project includes a validation or limitations section demonstrating nuclear-style engineering discipline, (3) hiring_case.md demonstrates that the candidate can articulate their value in plant and engineering terms, not only software terms.

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: cross-disciplinary nuclear-digital profiles are genuinely rare and genuinely valued. The curriculum exists to produce them.
- `2030`: life-extension and digital modernization programs will dominate fleet operator hiring. Both require broad systems understanding combined with specific digital depth.
- `2035`: advanced reactor programs (SMRs, microreactors, Gen IV concepts) will create demand for engineers who can transfer across reactor type boundaries — which requires the foundational plant-systems thinking the curriculum develops, not only reactor-specific expertise.
- `2045`: the skill set that ages least is the combination of physical-system understanding, engineering conservatism, and digital tool fluency. All three are in this curriculum and all three are still required by nuclear plants in 2045.

### Interview Questions

1. "Why is nuclear engineering described as a systems discipline in this curriculum, rather than as a collection of individual technical subjects?"
   Short answer: because real plant performance and safety depend on how reactor, thermal, electrical, chemical, and control systems interact — and engineers who only understand one layer make worse decisions about the others.

2. "What is the most common mistake that CS-background engineers make when entering nuclear work, and how does this curriculum address it?"
   Short answer: treating the digital layer as primary and the physical system as secondary. The curriculum addresses this by building physical-system understanding before digital application, not alongside it or after it.

3. "Describe the distinction between an advisory system and a safety system in a nuclear plant, and explain why this matters for someone writing data analytics code."
   Short answer: a safety system must be validated, qualified, and independent; an advisory system provides information to support human decisions without acting on them directly. Data analytics code that inadvertently influences a safety function without validation is a serious engineering and regulatory problem.

4. "Name three types of commercial roles where the curriculum's combination of plant-systems knowledge and digital skills creates direct hiring value."
   Short answer: nuclear I&C modernization engineer, plant historian and reliability analytics engineer, OT cybersecurity analyst for nuclear facilities.

5. "If you were hiring a new graduate for a nuclear digital engineering role, what would be the most important thing their portfolio could demonstrate?"
   Short answer: that they understand what the plant data they are working with actually represents physically — not only that they can process the data technically.

### Further Depth

- IAEA Nuclear Knowledge Management publications (iaea.org) — curriculum design and competency framework references
- US DOE Nuclear Energy University Program (NEUP) project database (available at energy.gov) — current research areas with industry alignment
- BARC Training School orientation materials — India-specific competency framework for public-sector nuclear engineering
- MIT OCW 22.01 and 22.06 — anchor technical content for reactor physics and plant systems
- NRC NUREG-1350 Annual Information Digest — publicly available fleet and regulatory orientation reference
- Lamarsh & Baratta, "Introduction to Nuclear Engineering" — the recommended foundational technical text for this curriculum
