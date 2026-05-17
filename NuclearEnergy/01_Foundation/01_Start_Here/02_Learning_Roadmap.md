# Learning Roadmap

## Overview

This roadmap converts the curriculum into a practical 12-month sequence with outputs, not just topics.

## Phase Plan

### Phase 1: Months 0-3

- learn plant basics, reactor fundamentals, radiation basics, Python, and Linux
- output: one plant systems map and three small engineering calculators

### Phase 2: Months 3-6

- learn C, microcontrollers, sensors, PID, PLC logic, and basic SCADA ideas
- output: one sensor logger, one control-logic demo, one small dashboard

### Phase 3: Months 6-9

- learn thermal hydraulics, reactor transients, OpenMC, digital twins, and anomaly detection
- output: one serious simulation and one predictive-maintenance notebook

### Phase 4: Months 9-12

- package the work into four portfolio pieces
- prepare job documents for automation, embedded, simulation, or nuclear-digital roles

## Exit Criteria

By month 12, you should be able to:

- explain the plant as a system
- build software that touches plant-like data or controls
- discuss one serious project in operational terms
- target at least one hiring pathway with credible portfolio evidence

## Weekly Rhythm

- `2 sessions`: reading and annotated notes
- `2 sessions`: coding or modeling
- `1 session`: project integration and review

## Metrics / KPIs / What to Measure

- topic completion
- number of finished artifacts
- number of pages of notes written in your own words
- project quality, not just project count

## Common Pitfalls

- studying too many topics at once
- spending months only on content consumption
- skipping documentation writing

## Next Step

Start with [How Nuclear Power Plants Work](../02_Plant_and_Energy_Basics/01_How_Nuclear_Power_Plants_Work.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Utilities and nuclear vendors do not train people as "generic nuclear learners." They train them into role families: plant systems, reactor engineering, instrumentation and controls, reliability, outage planning, chemistry or radiation protection, and digital modernization. A useful roadmap therefore has to branch by capability, not by calendar.

For a software-heavy learner, the practical path is usually:

- first learn how the plant is measured and controlled
- then learn one operating-system view such as core monitoring, feedwater control, equipment reliability, or historian data
- then build one artifact that looks like engineering work rather than study notes

### Industry Tool Stack

- `Python`, `NumPy`, `pandas`, `matplotlib`: calculators, data cleanup, engineering plots, notebook studies
- `Linux`, `Git`, plain-text notes: reproducible engineering workflow
- `OpenMC`, `PyNE`: open reactor-analysis and nuclear-data learning stack
- historian exports, `OPC UA`, `Modbus`: plant-data integration and advisory analytics
- DCS / PLC / SCADA environments: control logic, operator display, alarm, and trend context
- CMMS or work-order systems: maintenance planning and evidence capture

### Step-by-Step Applied Workflow

1. Pick one target role lane: plant systems, controls, reactor analysis, or nuclear digital.
2. Build a plant mental model with one-page diagrams for reactor, steam cycle, electrical path, and protection boundaries.
3. Add one tool layer: Python calculators, trend analysis, control-loop sketch, or simple simulator work.
4. Convert one topic into an inspectable artifact: notebook, dashboard, engineering note, or alarm-response map.
5. Review the artifact against an operating question such as "what measurement changes first?" or "what action is advisory versus safety-critical?"
6. Package the result as a small portfolio unit with assumptions, limits, and next-step risk notes.

### AI Integration

AI enters the roadmap after you can already explain the plant in normal engineering terms. The right sequence is:

- start with interpretable rules, calculations, and plots
- add anomaly detection or surrogate models only when the measured signal and operating mode are already understood
- keep model output advisory unless a human can explain why the recommendation is credible

### Case Studies

- `MIT CRPG / OpenMC`: useful benchmark for how open tools can be turned into serious nuclear-analysis learning artifacts rather than black-box demos.
- `NPCIL`: useful benchmark for a structured India-facing nuclear career path that still depends on deep plant literacy before digital specialization.
- `IAEA`: strong benchmark for the way safety, operations, maintenance, and digital modernization must stay tied together instead of being studied as separate silos.

### Failure Modes & Safety

- The common failure mode is role confusion: learning reactor theory, controls, and AI in parallel without ever being able to explain one plant transient cleanly.
- Another failure mode is building only notebooks with no operating context, so the work never resembles outage, control-room, or reliability engineering.
- Safety risk appears when advisory analytics are treated as action authority instead of decision support.

### Business & Commercial Layer

This roadmap can feed several commercial paths:

- utility or fleet engineering roles
- EPC and vendor digitalization work
- reliability and asset-health consulting
- training and simulation tooling
- industrial data integration and dashboard work

India-facing roles remain strongest in public-sector and supplier ecosystems. US and Europe offer stronger vendor, digital, and advanced-reactor pathways.

### Hiring Signal

Interviewers usually look for evidence that you can:

- explain one plant subsystem without hand-waving
- work with data or controls in a disciplined way
- document assumptions and limits
- build something inspectable, not just summarize textbooks

Good evidence includes a plant-systems map, one core or thermal notebook, one control or alarm artifact, and one reliability-style analysis.

### Portfolio Projects

- Beginner: `plant-system-atlas`
  Deliverables: markdown system map, one heat-balance notebook, one sensor-tag glossary.
  Suggested structure: `docs/`, `notebooks/`, `figures/`, `sources/`.
- Intermediate: `nuclear-digital-lab`
  Deliverables: historian-style synthetic dataset, anomaly notebook, operator note on why alerts should stay advisory.
  Suggested structure: `data/`, `src/`, `dashboards/`, `reports/`.
- Advanced: `core-and-plant-decision-support`
  Deliverables: OpenMC-linked study, plant dashboard mockup, maintenance or operations review note, uncertainty register.
  Suggested structure: `models/`, `analysis/`, `ops_notes/`, `validation/`, `README.md`.

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: strong demand for engineers who can bridge plant systems and industrial data.
- `2030`: more modernization work around analytics, digital twins, outage optimization, and equipment health.
- `2035`: greater value in engineers who can combine reactor, grid, maintenance, and cyber thinking.
- `2045`: the durable skill is not one tool. It is the ability to explain a high-consequence physical system and attach trustworthy software to it.

### Interview Questions

1. Why is a capability ladder better than a calendar plan in nuclear engineering?
   Short answer: roles branch by plant function, and mastery is proved by artifacts and judgment, not elapsed time.
2. Where should a software-heavy learner enter the nuclear domain?
   Short answer: plant systems, controls, historian data, and reliability are usually the best bridge layers.
3. Why must AI stay advisory in most early nuclear portfolio work?
   Short answer: because explainability, validation, and safety review matter more than model novelty.
4. What makes a nuclear project portfolio credible?
   Short answer: reproducible calculations, plant context, clear assumptions, and evidence that decisions were reviewed conservatively.
5. What is the biggest roadmap mistake?
   Short answer: studying many topics shallowly without producing one inspectable engineering artifact.

### Further Depth

- MIT OCW `22.01` and `22.091`
- OpenMC documentation
- IAEA operations and maintenance guidance
- IAEA safety culture and human performance references
- EPRI material on equipment reliability and digital modernization
