# Image Index

This folder is intentionally light on bundled images. The curriculum prefers text diagrams, official manuals, and plant-system explanations that remain readable in plain markdown.

## Recommended Use

- Use ASCII diagrams inside topic pages for first-pass understanding.
- Use official plant schematics, vendor manuals, or course figures only when you need exact geometry or component layouts.
- Keep copied assets inside `Images/` only if they are necessary for local navigation.

## High-Value Visuals To Add Later

- PWR primary-secondary loop schematic
- PHWR system map
- turbine-condenser-feedwater loop
- safety-system independence diagram
- control-room alarm and trip logic map

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

In nuclear engineering learning materials, the highest-value visuals are not decorative. They are diagrams that answer a specific question the text cannot answer as efficiently: where does the flow go, which barriers separate which systems, what does the protection logic look like as a ladder, and how does an alarm-to-trip sequence actually unfold in time. Every image in a nuclear curriculum should exist because removing it would force the reader to work harder to understand the engineering decision the image makes obvious.

The curriculum's text-first preference reflects real plant engineering practice: system descriptions, procedures, and technical specifications are written in text, and the visual layer supplements them for topology, independence, and layout understanding. ASCII diagrams embedded directly in topic pages are the minimum viable visualization. Full schematics, redraw-quality loop diagrams, and logic maps are the higher tier, added only when they save meaningful comprehension time.

### Industry Tool Stack

- `ASCII art (in-page)` — used for quick topology understanding without any external tooling; ideal for flow paths and protection-layer relationships
- `draw.io (diagrams.net)` — used for clean, reviewable system diagrams, cause-and-effect matrices, and logic maps without proprietary dependencies
- `Excalidraw` — used for fast hand-drawn-style system sketches suitable for README files and documentation
- `Matplotlib / Plotly` — used for data-driven visuals such as pump curves, heat-balance plots, trend comparisons, and transient timelines
- `Graphviz / Mermaid` — used for architecture and logic-flow diagrams that can be version-controlled and reviewed as code
- Official plant schematics and IAEA/NRC regulatory figures — used as authoritative topology references when exact component layout matters

### Step-by-Step Applied Workflow

1. Decide whether the image explains topology, logic, data, or a physical process — different question types need different diagram formats.
2. Start with an ASCII diagram inside the relevant topic page; it costs nothing to revise and works in all rendering environments.
3. Upgrade to a draw.io or Excalidraw diagram only when ASCII cannot capture the level of layout or component-count detail needed.
4. Label every component, flow direction, and boundary condition on the diagram — an unlabeled system diagram creates false confidence that the reader understood something they only recognized.
5. Add a one-line caption explaining what engineering decision this diagram supports, not just what it shows.
6. Source external figures explicitly and check that reproduction is permitted; IAEA and NRC figures are generally public-domain for educational use.

### AI Integration

AI image generation can create plausible-looking system diagrams, but it will invent component positions, invent barrier labels, and generate safety-system boundaries that do not reflect any real regulatory or design standard. For nuclear learning materials, AI-generated visuals carry a specific risk: a student who uses an AI-generated plant schematic as their mental model of a real plant may learn incorrect layout topology that is later hard to unlearn. The safer pattern is to use AI to draft an ASCII or descriptive text version of a diagram, then manually convert it into a draw.io figure, preserving engineering accuracy at each step.

### Case Studies

- `IAEA nuclear safety and plant system publications`: The IAEA Safety Reports and TECDOC series contain publicly available system diagrams and flow-path illustrations for PWR, BWR, PHWR, and advanced reactor types that represent authoritative layout references. These are a better source for learning-material schematics than any AI-generated alternative.
- `NRC Inspection Manual and NUREG figures`: NRC-published figures for control-room layout, protection system independence, and I&C architecture are publicly available and provide the most credible visual reference for US-regulatory-context nuclear learning materials.

### Failure Modes & Safety

- Decorative images that look technical but carry no engineering information slow learners down by suggesting depth that does not exist.
- Unlabeled or under-labeled diagrams are one of the most common failures in self-study nuclear materials: a flow path without direction arrows, or a schematic without barrier labels, teaches recognition rather than understanding.
- Copied visuals with unclear copyright status create legal and credibility problems in public course materials.
- AI-generated schematics that invent safety-system boundaries are a specific nuclear-learning risk because students may not detect the inaccuracy.

### Business & Commercial Layer

In nuclear training, consulting, and onboarding deliverables, visual clarity directly reduces time-to-competency and reduces the probability of misunderstanding system boundaries. Vendors selling nuclear digital tools, utilities onboarding new engineers, and consultancies preparing technical proposals all use system diagrams as the fastest route to shared mental models. An engineer who can produce clean, accurate nuclear system diagrams is demonstrably more useful at the start of a project than one who cannot.

### Hiring Signal

**Five job titles where diagram quality appears in interview or work-sample evaluation:**
- Plant Systems Engineer — expected to read and annotate P&IDs and system flow diagrams
- I&C Engineer (Nuclear) — expected to work with logic diagrams, cause-and-effect matrices, and control-room HMI schematics
- Reactor Engineer — expected to interpret core layout and primary-system flow diagrams
- Reliability and Maintenance Engineer — expected to read one-line electrical diagrams and exchanger performance schematics
- Nuclear Training Specialist — expected to create and maintain accurate system overview diagrams for operator training

**Five interview screens for diagram competency:**
1. "Draw the primary coolant path in a pressurized water reactor from the reactor vessel outlet to the steam generator and back." Tests basic topology retention.
2. "On a simplified P&ID for a pump and discharge valve, mark where the permissive signal would originate and where the trip actuation would act." Tests logic-plus-topology linkage.
3. "What is shown by a system independence diagram, and why does it matter in nuclear design?" Tests understanding of defence-in-depth visualization.
4. "How would you confirm that a schematic you found online accurately represents the actual plant configuration?" Tests source-critical thinking.
5. "Walk me through the symbols on a cause-and-effect matrix and explain what a filled cell means." Tests I&C diagramming literacy.

### Portfolio Projects

**Beginner:**
`nuclear-loop-diagram-set`
Deliverables: ASCII and draw.io version of the PWR primary and secondary flow paths, with all major components labelled and flow directions marked.
Acceptance criteria: (1) primary loop and secondary loop clearly separated and both complete, (2) all components labelled with correct nuclear terminology, (3) brief markdown note explaining what each loop boundary represents and why it exists.

**Intermediate:**
`alarm-trip-logic-visual`
Deliverables: cause-and-effect matrix and trip logic diagram for one operating event (e.g., high reactor coolant temperature trip), with permissive inputs and actuated outputs labelled.
Acceptance criteria: (1) matrix distinguishes initiating condition, permissive, alarm, and trip action, (2) diagram verified against a textbook or NRC document description rather than invented from scratch, (3) one worked example showing how the sequence unfolds during the modeled event.

**Advanced:**
`nuclear-system-architecture-board`
Deliverables: integrated architecture diagram showing reactor system, I&C system, historian/DCS data path, and advisory analytics layer as separate bounded zones with data flows and security boundaries marked.
Acceptance criteria: (1) safety, control, supervisory, and analytics layers correctly separated and labelled, (2) diagram matches the layering described in IEC 62645 or IAEA I&C guidance at a conceptual level, (3) README explains what each boundary represents and what crossing it without authorization would mean.

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: the best nuclear learning materials are still diagram-sparse but precise — a few high-accuracy visuals outperform many generic ones.
- `2030`: more interactive and versioned system diagrams appear in digital plant documentation and operator support tools.
- `2035`: augmented-reality maintenance support and digital-twin visualizations begin to integrate with traditional P&ID-style representations.
- `2045`: the fundamental need for accurate system topology understanding persists regardless of visualization technology — the engineering question drives the diagram, not the other way around.

### Interview Questions

1. What is the primary purpose of a system schematic in a nuclear engineering context?
   Short answer: to communicate accurate topology — where things are, how they connect, and where the boundaries are — not to look impressive.

2. Why is an unlabelled diagram more dangerous than no diagram at all?
   Short answer: because it creates recognition without understanding, which is a specific failure mode in safety-critical work.

3. What makes an ASCII diagram acceptable for a learning-material context?
   Short answer: it is fast to produce, easy to version-control, and reviewable without specialized tooling.

4. When should you upgrade from ASCII to a draw.io or vector diagram?
   Short answer: when the layout complexity, component count, or boundary precision required cannot be captured accurately in ASCII without becoming unreadable.

5. What is the risk of using AI to generate nuclear system diagrams?
   Short answer: AI will invent plausible-looking but incorrect safety boundaries and component arrangements that are difficult for a learner to identify as wrong.

### Further Depth

- IAEA Safety Reports Series and TECDOC publications (publicly available plant-system diagrams for PWR, BWR, PHWR, and advanced reactor types)
- NRC NUREG reports and Inspection Manual public figures (authoritative US regulatory context schematics)
- Lamarsh & Baratta, "Introduction to Nuclear Engineering" (contains accurate conceptual system diagrams suitable for study reference)
- draw.io / diagrams.net documentation (free diagramming tool used widely in engineering documentation)
