# Intermediate Project Path

## Overview

Intermediate projects should look like small pieces of plant or industrial-digital infrastructure rather than like isolated homework problems.

## Recommended Projects

1. Tank-level or heat-exchanger control simulator with PID
1. Modbus polling tool in Python or C
1. Ignition-style dashboard with trends and alarms
1. Cooling-loop digital twin with measured-versus-expected comparison

## Quality Bar

- system diagram
- code and README
- basic verification
- alarm or state logic
- explanation of operational relevance

## Skills Reinforced

- control concepts
- protocols
- dashboards
- historian-style data handling

## Common Pitfalls

- beautiful UI with weak engineering logic
- no explanation of failure modes
- mixing all concerns into one unreadable codebase

## Next Step

Move to [Advanced Project Path](../Advanced/01_Advanced_Project_Path.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Intermediate projects should feel like small plant-digital subsystems: dashboard logic, alarm-state handling, historian parsing, equipment-health review, or control-loop interpretation. The key upgrade from beginner level is that the project now has state, failure modes, and operating consequences.

### Industry Tool Stack

- synthetic historian or event data
- dashboards and plots
- alarm/state logic
- structured repo layout with docs and test data

### Step-by-Step Applied Workflow

1. Define one operating scenario, not only one formula.
2. Build the data path and the state logic first.
3. Add the visualization or reporting layer second.
4. Document what happens when the data goes bad or the operating mode changes.

### AI Integration

AI can appear here as anomaly ranking or explanation support, but the project should still work without AI magic.

### Case Studies

- historian analytics and alarm review are good intermediate industrial patterns.
- condition-monitoring demos are a strong bridge into reliability work.

### Failure Modes & Safety

- attractive UI with weak underlying state logic
- no explanation of abnormal cases
- no separation between advisory output and operator action

### Business & Commercial Layer

These projects start looking commercially relevant because they resemble the first slice of a real dashboard, analytics, or reliability tool.

### Hiring Signal

Interviewers want to see that you can structure a system, not only a notebook.

### Portfolio Projects

- Beginner bridge: retain one simple calculation module.
- Intermediate core: add state logic, alarm reasoning, and validation cases.
- Advanced bridge: add architecture note, user workflow, and uncertainty section.

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: intermediate projects that look like small plant tools are highly employable.
- `2030+`: maintainability and evidence trail matter as much as functionality.

### Interview Questions

1. What makes an intermediate nuclear project different from a beginner one?
   Short answer: state handling, operating context, and failure-case reasoning.
2. Why is alarm or state logic valuable?
   Short answer: because real plant-support tools interpret changing conditions, not only static values.
3. What is the common mistake here?
   Short answer: building front-end polish before engineering logic.
4. How should AI appear?
   Short answer: as one layer inside a usable system.
5. What makes the repo readable?
   Short answer: clean separation of data, logic, visualization, and docs.

### Further Depth

- historian and dashboard tooling docs
- alarm-management references
