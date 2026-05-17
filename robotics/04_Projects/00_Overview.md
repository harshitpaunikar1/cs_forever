# Projects

## Overview

Projects are where this curriculum stops being aspirational and becomes inspectable engineering work. A robotics project proves that you can integrate software, launch systems, debug frames, structure code, document setup, and finish a coherent system.

The project paths are split by difficulty so you can choose a starting point that is ambitious without becoming vague or unfinishable.

## How To Use the Project Paths

### Beginner
Choose this if you are still building confidence with ROS 2 basics, simulation, and simple robot descriptions.

### Intermediate
Choose this if you can already build and launch small ROS 2 systems and want navigation, perception, or control depth.

### Advanced
Choose this if you want an industrial, drone, embedded, or robot-learning capstone.

## Quality Bar for Every Project

Every project should include:

- a short design note or README
- setup and run instructions
- tests or clear verification steps
- screenshots, bag captures, or architecture diagrams
- one limitations section and one next-steps section

## Next Step

Choose one of the paths:

- [Beginner Project Path](Beginner/01_Beginner_Project_Path.md)
- [Intermediate Project Path](Intermediate/01_Intermediate_Project_Path.md)
- [Advanced Project Path](Advanced/01_Advanced_Project_Path.md)
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Project pages are where the robotics course stops being a reading sequence and becomes evidence. In hiring and in real engineering, a list of topics studied has limited value unless it becomes a reproducible artifact that someone else can inspect. That is why this overview page matters. The beginner, intermediate, and advanced paths are not simply “easy, medium, hard.” They represent different proof standards. A beginner path proves you can assemble a clean ROS 2 or simulation workflow and ship something understandable. An intermediate path proves you can integrate subsystems and debug cross-component behavior. An advanced path proves you can make design decisions under realism, constraints, and imperfect data.

Professionally, good robotics projects tend to have the same shape even when the robot type changes. There is a scoped task, a repo that a reviewer can actually run, an architecture boundary that makes sense, logs or plots that demonstrate behavior, and a written explanation of what still breaks. That makes this page operationally important. It prevents the common failure mode where a learner accumulates disconnected demos that look busy but do not add up to an engineering narrative. Used correctly, this page helps you convert course coverage into a portfolio with progression: first command of tools, then system integration, then independent technical judgment.

### Industry Tool Stack

- `GitHub`: used for public history, issue tracking, reviewable documentation, and visible engineering iteration.
- `ROS 2`: used as the common runtime and package model that makes project work legible to robotics employers.
- `Gazebo` or `Isaac Sim/Lab`: used to build credible projects when hardware access is limited or unsafe.
- `Foxglove` or `PlotJuggler`: used to show topic flow, timing, and run-time evidence instead of relying on demo videos alone.
- `rosbag2` with `MCAP`: used to capture experiments, replay bugs, and preserve proof of behavior over project revisions.
- `Docker`: used to make setup reproducible and prevent “works only on my machine” portfolio repos.
- `CI pipelines`: used to prove that the project still builds and passes basic checks after changes.
- `Markdown docs` and diagrams: used to explain scope, architecture, tradeoffs, and known limitations to reviewers.

### Step-by-Step Applied Workflow

1. Pick a project tier based on what you can already debug independently, not what sounds most prestigious.
2. Write a one-page project brief with task, robot class, success metric, software stack, and a realistic final demo artifact.
3. Create the repo skeleton early so source, launch files, configs, tests, logs, and docs do not become mixed together.
4. Build the smallest end-to-end loop first and make it visible with one measurable output rather than building every subsystem at once.
5. Record evidence from the first working version onward: screenshots, short clips, bag files, metrics, and notes on what changed.
6. Add a limitations section as the project evolves so unresolved gaps are visible and technically honest.
7. Package the project for review with setup instructions, a runnable demo path, and a short architecture explanation aimed at a hiring manager.
8. Map the finished project to roles and interview screens so the artifact becomes targeted evidence rather than a generic side project.

### AI Integration

AI belongs in projects when it clarifies the engineering story, not when it hides weak fundamentals. On lower-tier projects, AI may appear as a bounded perception component, data-analysis support for logs, or an auxiliary classifier that does not dominate the system architecture. On mid-tier and advanced projects, AI can become central: object detection in a navigation loop, learned grasp scoring, visual-language interfaces for task specification, or a deployed policy trained in simulation. The important point is that AI should still sit inside an explainable robotics workflow with inputs, outputs, fallback conditions, and operational metrics.

The strongest project portfolios use AI selectively. They keep the sensor path, timing, failure handling, and evaluation visible. If a model is used, the project should show how data was chosen, how latency was measured, and what happens when the model fails or confidence drops. Reviewers do not reward AI buzzwords by themselves. They reward engineers who can combine modern ML tools with disciplined robotics integration.

### Case Studies

Open Robotics is a useful benchmark because projects based on ROS 2 gain credibility when the package layout, launch flow, and tooling feel native to the ecosystem instead of improvised. Clearpath Robotics is another strong reference because its platforms and educational examples shaped what many teams consider a clean mobile-robot project baseline. Picknik Robotics is equally relevant for manipulation-oriented work: projects become much more believable when they reflect the interface discipline and integration habits seen in `MoveIt`-based application stacks.

### Failure Modes & Safety

The most common portfolio failure is shallow breadth. Many learners build several demos copied from tutorials, but they cannot explain topic timing, transforms, controller assumptions, or why the system fails. Another failure is missing evidence. A repo may contain code, but no bag files, no metrics, no diagrams, and no account of what changed between revisions. That makes the project hard to trust and easy to dismiss as assembled work rather than owned work.

Safety also matters, even for study projects. A simulation-only repo can still teach bad habits if it ignores watchdogs, collision assumptions, or recovery behavior. Hardware projects make this more serious. An arm demo without clear workspace limits or a mobile robot project without a stop condition teaches the wrong engineering reflex. Good project discipline therefore includes operating boundaries, safe test conditions, and a clear statement of what would need to improve before the work could leave the lab. Mature projects do not hide failure; they show controlled failure, diagnosis, and correction.

### Business & Commercial Layer

Projects matter commercially because employers use them as a compressed forecast of how you will behave on their systems. A warehouse robotics company reads a project differently than a manipulation startup or industrial integrator, but all three are looking for the same traits: scoping discipline, clear interfaces, visible testing, and honest discussion of operational limits. This overview page helps you shape projects so they signal those traits instead of reading like disconnected experiments.

In India, project quality often matters even more because visible portfolio evidence can compensate for a thin local specialization pipeline in robotics roles. In the US and Europe, the same principle holds, but the bar on reproducibility and documentation is often higher. Remote-friendly roles depend heavily on project clarity because the repo must show that you can leave a usable engineering trail without constant live explanation. This page therefore has direct commercial value even though it is not tied to a single robot subsystem.

### Hiring Signal

Job titles supported by this page:

- Robotics Software Engineer
- Robotics Systems Integrator
- Robotics Test Engineer
- Production Robotics Engineer
- Research Engineer (Robotics)

Interview screens this page prepares you for:

- walk through one project architecture and defend why the subsystem boundaries exist
- open a recorded run or bag file and explain what it says about system behavior
- identify the top three technical risks preventing a project from moving from simulation to hardware
- describe what should be tested automatically versus manually in a robotics repo
- compare two portfolio projects and explain which one is stronger evidence for a specific role

### Portfolio Projects

Beginner track package:

- Deliverables: one complete beginner project, demo clip, architecture diagram, setup guide, and issue log.
- Suggested repo structure:

```text
robotics-projects-beginner/
├── project_01/
│   ├── src/
│   ├── launch/
│   ├── config/
│   ├── tests/
│   └── README.md
├── media/
└── docs/
```

- Acceptance criteria:
  - a reviewer can run the project from the README without guessing missing steps
  - at least one logged failure and fix is documented
  - the artifact shows one real robotics concept working end to end

Intermediate track package:

- Deliverables: one subsystem-integration project, metrics or plots, replay data, and one design tradeoff note.
- Suggested repo structure:

```text
robotics-projects-intermediate/
├── bags/
├── project_02/
│   ├── src/
│   ├── launch/
│   ├── rviz/
│   ├── analysis/
│   └── README.md
└── docs/
```

- Acceptance criteria:
  - at least two subsystems interact in a reproducible way
  - evidence includes metrics or logs, not just screenshots
  - the write-up explains why one integration choice was rejected

Advanced track package:

- Deliverables: one capstone-grade project, deployment or safety story, benchmarking, and a hiring-focused technical summary.
- Suggested repo structure:

```text
robotics-projects-advanced/
├── capstone/
│   ├── src/
│   ├── docker/
│   ├── ci/
│   ├── logs/
│   ├── evaluation/
│   └── README.md
└── portfolio_summary.md
```

- Acceptance criteria:
  - the project demonstrates ownership of architecture, debugging, and validation
  - evidence includes constraints, failure analysis, and next-step engineering work
  - the repo maps cleanly to at least one target job family

### Future Trends

- `2026`: hiring teams keep moving away from tutorial familiarity toward reproducible project evidence with metrics, tests, and visible iteration.
- `2030`: simulation-backed portfolios become more accepted as long as they include realistic constraints and measurable outcomes.
- `2035`: embodied-AI portfolio work only stands out when paired with deployment, observability, and failure-analysis evidence.
- `2045`: the best portfolios look like miniature product programs, with release discipline, log-driven debugging, and lifecycle thinking built into the repo.

### Interview Questions

1. What makes a robotics project more credible than a tutorial clone?
   Short answer: clear ownership, reproducibility, measured outcomes, and honest discussion of limitations and fixes.

2. Why should a project include logs or bag files?
   Short answer: they let reviewers reproduce behavior, inspect failures, and see more than a polished demo clip.

3. When is a simulation-only project acceptable as hiring evidence?
   Short answer: when the simulation is well scoped, technically honest, and backed by real architecture, metrics, and transfer reasoning.

4. What separates a beginner project from an advanced project?
   Short answer: advanced work shows independent engineering judgment, subsystem tradeoffs, and operational constraints rather than assembly alone.

5. Why include rejected design choices in project docs?
   Short answer: because engineering maturity is visible in tradeoff reasoning, not just in the final implementation.

### Further Depth

- `ROS 2` official docs for package, launch, and testing conventions
- `Nav2` docs for what a mature navigation project stack looks like
- `MoveIt 2` docs for manipulation-oriented project structure and interfaces
- `Foxglove` docs for evidence-rich debugging and review
- `rosbag2` and `MCAP` docs for reproducible experiment capture
