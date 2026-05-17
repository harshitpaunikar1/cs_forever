# Portfolio Checklist

## Strong Robotics Portfolio Signals

- one flagship repo with a clean README
- one architecture diagram
- one reproducible setup path
- one limitations section
- screenshots, bag captures, or demo media
- Docker or environment setup story
- test or verification instructions

## Best Project Types

- ROS 2 mobile robot starter stack
- Gazebo + Nav2 autonomous navigation demo
- MoveIt 2 manipulator project
- micro-ROS embedded bridge
- industrial workcell project
- PX4 or embodied-AI capstone

## Employer Red Flags

- tutorials copied without adaptation
- no setup steps
- no explanation of trade-offs
- no evidence the project actually runs
- no understanding of frames, QoS, or controller ownership

## How to Talk About Projects in Interviews

- start with the problem
- explain the system architecture
- describe one failure and how you fixed it
- explain one trade-off you made
- be clear about what is simulated versus real hardware
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

A portfolio checklist is a quality gate, not a motivational page. Professional robotics teams use similar checklists before demos, interviews, customer reviews, and internal design reviews because projects are judged on evidence, not effort. This page should be used as a pre-publish audit for every robotics repo you intend to show another engineer.

### Industry Tool Stack

- `Checklist`: used to catch missing evidence before a reviewer does.
- `README`: used to turn a project into a navigable artifact.
- `Bags, plots, screenshots`: used to prove the system really ran.
- `Issue log`: used to show iteration and engineering honesty.

### Step-by-Step Applied Workflow

1. Open the checklist before calling a project finished.
2. Verify setup, run, and verification steps are all present.
3. Confirm the repo contains evidence, not just source code.
4. Add one limitations section and one failure-analysis note.
5. Map the project to one target job family.
6. Re-read the repo as if you were a skeptical interviewer.

### AI Integration

AI is most useful here as a reviewer simulator. It can point out missing sections, unclear explanations, or weak structure. It should not invent claims or inflate the project. The checklist exists to keep the portfolio honest, especially when AI makes it easy to over-polish language around thin work.

### Case Studies

Foxglove is a good benchmark because teams that use strong data and visualization practices naturally produce better portfolio evidence. Picknik Robotics and Open Robotics are also relevant benchmarks: public-facing robotics artifacts from strong teams tend to be clear about structure, interfaces, and intended use rather than relying on vague claims.

### Failure Modes & Safety

Portfolio failure usually comes from omission. The project runs, but there is no setup path, no proof, no tradeoff note, and no explanation of what is simulated versus real. Another failure is overselling. A project described as production-ready without tests, logs, or limits damages trust quickly. The safe rule is to document capability and boundary together.

### Business & Commercial Layer

Commercially, this page matters because portfolios are often used as a low-cost proxy for work quality. A strong checklist reduces reviewer friction, improves signal density, and helps your best work survive a quick scan by a busy hiring team. It is one of the cheapest leverage points in the whole course.

### Hiring Signal

Job titles supported by this page:

- Robotics Software Engineer
- Robotics Test Engineer
- Robotics Systems Integrator

Interview screens it supports:

- presenting one project in five minutes with architecture, evidence, and limits
- answering what was self-built versus adapted
- naming the top risk still left in the project

### Portfolio Projects

Beginner: audit one repo against this checklist and fix every missing item.  
Intermediate: create a reusable `project-review-template.md` for future robotics repos.  
Advanced: run a comparative review across three projects and rank which one is strongest evidence for each target role.

### Future Trends

- `2026`: hiring reviews keep getting shorter, so checklist-driven clarity matters more.
- `2030`: portfolios increasingly need observability and deployment evidence, not just algorithm demos.
- `2035`: reviewers expect stronger honesty about hardware boundaries and AI claims.
- `2045`: portfolio artifacts look more like compact engineering dossiers than casual side-project pages.

### Interview Questions

1. What is the first thing missing in weak robotics portfolios?
   Short answer: reproducible setup and evidence of actual runtime behavior.

2. Why include limitations in a portfolio?
   Short answer: because honest boundaries increase trust.

3. What makes a project interview-ready?
   Short answer: clear problem, architecture, evidence, failure note, and tradeoff.

4. Why are screenshots alone not enough?
   Short answer: they show outcome without proving reproducibility or reasoning.

5. How should AI affect portfolio writing?
   Short answer: it should improve clarity, not inflate claims.

### Further Depth

- `Foxglove` docs
- `rosbag2` docs
- `ROS 2` testing docs
- `MoveIt 2` and `Nav2` examples for strong project structure
- `Modern Robotics` for technical framing depth
