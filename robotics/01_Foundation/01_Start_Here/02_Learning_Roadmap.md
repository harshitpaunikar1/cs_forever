# Learning Roadmap

## Overview

This roadmap converts the robotics curriculum into a realistic `12-month` learning sequence. It assumes part-time self-study with consistent project work. The order is designed for the highest employment value in `2026`: ROS 2 first, then simulation, control, navigation, manipulation, perception, embedded systems, and one polished capstone.

## Month 1

- Linux CLI, shell basics, filesystems
- Git and GitHub workflow
- Python refresh
- Basic C++ refresh
- Start ROS 2 installation

Build:

- `robotics-dev-notes`
- shell cheat sheet
- simple Python sensor log parser
- small C++ CLI for pose or vector math

## Month 2

- ROS 2 fundamentals
- nodes, topics, services, actions, parameters
- launch and tf2
- URDF basics

Build:

- turtlesim mini-projects
- pub/sub sensor dashboard
- differential-drive URDF

## Month 3

- ROS 2 in Python and C++
- workspace structure
- Docker for ROS development
- testing and documentation

Build:

- Dockerized ROS dev workspace
- mixed Python and C++ project
- rosbag record and replay experiment

## Month 4

- Gazebo
- robot modeling
- ros2_control basics
- sensors and actuators in simulation

Build:

- simulated diff-drive robot
- controller configuration
- joint-state and velocity-controller demo

## Month 5

- localization
- mapping and SLAM
- Nav2
- behavior trees

Build:

- map a simulated environment
- AMCL localization
- goal navigation demo
- compare A*, DWA, and RRT style planners in Python

## Month 6

- OpenCV
- camera calibration
- feature detection
- simple perception pipelines

Build:

- calibration tool
- ArUco pose estimation
- object detection publisher
- basic sensor fusion demo

## Month 7

- MoveIt 2
- kinematics
- manipulation planning
- collision scenes

Build:

- `6-DOF` arm in simulation
- pick-and-place pipeline
- planning scene with obstacles
- one C++ MoveIt node

## Month 8

- micro-ROS
- RTOS concepts
- serial, CAN, I2C, SPI, GPIO
- embedded Linux device interaction

Build:

- micro-ROS pub/sub on MCU or emulator
- IMU or encoder bridge
- CAN sensor test app
- SBC bus experiment

## Month 9

- ROS-Industrial workflows
- workcells
- maintainability and documentation
- scan-and-plan ideas

Build:

- industrial workcell mockup
- reproducible documentation site
- deployment notes and diagrams

## Month 10

- PX4
- ROS 2 offboard control
- mission flow
- state estimation basics

Build:

- PX4 SITL with ROS 2
- waypoint mission node
- marker-based navigation prototype

## Month 11

- LeRobot or Isaac Lab
- imitation learning
- RL workflow in simulation
- LLM-enabled task planning ideas

Build:

- imitation-learning mini-project
- embodied-AI demo
- planner that outputs ROS 2 goals or actions

## Month 12

- system integration
- packaging and deployment
- interview prep
- capstone polish

Capstone choices:

- autonomous mobile robot
- industrial pick-and-place workcell
- drone offboard autonomy stack
- embedded ROS 2 sensor-actuator platform

## Next Step

Move to [Linux Git Python C++ for Robotics](../02_Engineering_Workflow/01_Linux_Git_Python_Cpp_for_Robotics.md).


<!-- FULL_TOPIC_EXPANSION_START -->
## Why This Topic Matters

A roadmap turns broad ambition into weekly execution and prevents resource sprawl.

## Real-World Context / Industry Relevance

Robotics hiring rewards finished systems, not broad but shallow exposure.

## History / Evolution of the Topic

As open-source robotics matured, viable self-study pathways became much more practical because the core stack became more accessible.

## Core Terminology

- `SITL`: Software in the loop simulation.
- `Capstone`: A project that integrates several curriculum areas into one system.
- `Polish`: The layer of docs, tests, and packaging that makes work inspectable.
- `Hiring signal`: Evidence that your skills can transfer into production work.

## Mental Model / Big Picture

```text
monthly focus -> build artifact -> portfolio proof -> stronger interview readiness
```

## Main Concepts / Core Concepts

This page already contains the primary concept material above. The appended sections below extend it into industry and implementation context.

## Subtopics Breakdown

- sequencing
- monthly goals
- portfolio integration
- capstone planning

## Architecture / Components / Building Blocks

- learning month
- build artifact
- portfolio update
- interview prep

## Process Flow / Lifecycle

```text
learn -> build -> document -> review -> apply
```

## Practical / Design / Operational Sections

Treat the roadmap like an engineering delivery plan with milestones and review points.

## Step-by-Step Implementation Guide

1. Pick one month and define one core deliverable
1. Keep scope tight enough to finish
1. Publish notes and screenshots with every major build

## Hands-On Example / Mini Project

At the end of Month 2, publish a `my-first-ros2-packages` repo with launch files, screenshots, and a short architecture note.

## TWO Case Study / Real Scenario

### Case Study 1 / Real Scenario

A learner who ships one focused repo per month has much better interview material than someone who only reads.

### Case Study 2 / Real Scenario

A learner who constantly restarts with new tools never accumulates proof of depth.

## Best Practices

- finish smaller scopes
- document what broke
- keep each month tied to one portfolio artifact

## Performance / Optimization Considerations

The roadmap works best when context switching is limited and the next step is obvious.

## Security / Reliability Considerations

Deployment and testing should enter the workflow before the final capstone, not only at the end.

## Scalability Considerations

You can compress or expand the schedule, but the dependency order should stay similar.

## Common Pitfalls

- spending a month only reading
- no screenshots or diagrams
- no cleanup after demos work once

## Debugging / Troubleshooting Guide

- If you fall behind, cut features instead of cutting documentation.
- If a month becomes too broad, split it into one skill and one project.
- If projects stall, reduce the hardware dependency and continue in simulation.

## Common Misconceptions

- You need expensive hardware immediately.
- You should wait to build until you feel ready.
- One giant capstone is better than several smaller finished repos.

## Tradeoffs / Decision Frameworks

The main trade-off is between ambitious breadth and consistently shippable milestones.

## Metrics / KPIs / What to Measure

- monthly project completion
- README quality
- issue closure rate
- interview explainability

## Tools Commonly Used Around This Topic

- `GitHub Projects`
- `README`
- `Docker`
- `rosbag`

## Ecosystem / Platforms / Vendors

- ROS 2
- Gazebo
- PX4
- Hugging Face Robotics

## Automation Opportunities

CI, formatting, workspace bootstrapping, and dev containers can reduce repeated setup work.

## AI Impact on This Topic

AI can help you start faster, but it will not create real portfolio proof unless you validate and explain every subsystem yourself.

## Recommended Resources

Use the local Course Index to map each month to one primary resource and one secondary reference.

## Practice Exercises

- convert the 12-month plan into a 24-week plan
- choose a capstone and define the minimum viable version
- write one interview-ready summary for each completed month
-->
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

The original roadmap above is time-based, but industry does not promote people by calendar. It promotes them when they can demonstrate capabilities repeatedly. In practice, robotics teams think in gates: can this engineer bring up a ROS 2 workspace alone, can they debug a tf mistake, can they stabilize a Nav2 stack in simulation, can they trace a controller issue into hardware interfaces, can they ship a reproducible repo another engineer can extend? That is the framing this page should carry in real use. A strong learning roadmap is a capability ladder that turns vague ambition into evidence-backed milestones.

For a self-directed learner, this matters because robotics is full of hidden dependency chains. If you cannot explain message flow, frame trees, parameters, and build tooling, you do not yet have the right to trust a SLAM demo or a learned control policy. Real organizations often onboard people with internal checklists that sound simple but are capability rich: build from source, inspect runtime graphs, interpret logs, tune a subsystem, document failure modes, and hand off work cleanly. That is the right mental model for this roadmap. The page should therefore be used as a progression from prerequisite literacy to subsystem ownership to system integration, not as a promise that “after month eight you are job ready.”

### Industry Tool Stack

- `GitHub Projects` or issue trackers: used to convert learning goals into inspectable capability checkpoints.
- `ROS 2 CLI` and `rviz2`: used as evidence tools to prove you can inspect a live system rather than just run it.
- `Gazebo`, `Nav2`, `MoveIt 2`, `ros2_control`: used as capability gates for the major robotics branches.
- `Docker`: used to show that your environment setup is transferable and not trapped on one machine.
- `rosbag2`: used to record evidence of system behavior and to revisit bugs methodically.
- `Markdown docs` and architecture diagrams: used to turn build effort into hiring evidence and handoff quality.

### Step-by-Step Applied Workflow

1. Rewrite each time-based milestone into a capability statement such as “can build and inspect a ROS 2 graph from scratch.”
2. Group those capabilities into tiers: prerequisites, foundation, subsystem fluency, integration, specialization, and portfolio proof.
3. For each tier, define one artifact that proves the capability, such as a repo, diagram, bag replay, or simulator runbook.
4. Do not advance because the calendar moved; advance only after another engineer could inspect the evidence and agree the capability is real.
5. Keep a gap log of what still feels scripted, such as QoS tuning, frame debugging, controller configuration, or perception latency.
6. Use one capstone idea as a through-line and keep mapping newly acquired skills back into that future system.
7. At the end of each capability tier, do an interview-style review: explain the architecture, failure modes, and trade-offs without reading notes.
8. Freeze strong tiers into portfolio artifacts and keep weaker tiers open for deliberate remediation.

### AI Integration

AI can help turn a roadmap into an adaptive capability tracker. A language model can review your notes, point out repeated blind spots, turn shell history into study gaps, and suggest targeted drills based on the last bug you hit. It can also simulate lightweight interview screens by asking you to explain why a service should be an action, how tf affects localization, or why a controller failed after a URDF change. That is useful because the real bottleneck in self-study is often not content access but calibration.

The misuse is obvious: AI can create the illusion of progress by summarizing topics you never operationalized. In robotics, the only roadmap that matters is the one backed by working artifacts. So the adjacent AI role is best treated as a coach around evidence, not a replacement for evidence. It can help you score your repo quality, detect repeated weak spots, or propose the next drill. It cannot certify that you can commission a robot, debug latency, or recover from a bad transform in a live stack. This page’s remediation is therefore to shift from “months completed” to “capabilities proven.”

### Case Studies

Organizations that train robotics engineers internally rarely rely on calendars alone. Industrial automation teams, mobile robot startups, and research labs all use some form of gated progression: first environment bring-up, then subsystem debugging, then supervised integration, then partial ownership. The exact tools differ, but the common lesson is that capability review beats time served. That is the right benchmark for this roadmap.

### Failure Modes & Safety

The main failure mode in a roadmap is false progression. A learner moves from topic to topic because the schedule says so, but the earlier layer was never stabilized. In robotics that creates cascading errors. Someone who did not really understand launch files will struggle to debug multi-node bring-up. Someone who did not really understand frame semantics will waste time “tuning” localization. Someone who did not learn to document assumptions will produce capstones that cannot be reviewed or reproduced. The result is a portfolio that looks broad but collapses under technical questioning.

Safety enters because robotics errors are physical, not just logical. A bad roadmap encourages people to touch hardware before their simulation and introspection habits are mature. That is how wheel directions get inverted, collision objects are ignored, or controller limits are misunderstood. A capability-based roadmap reduces this risk by requiring visible evidence before escalation. The safe rule is simple: no new complexity without proof that the current layer is controlled. That principle matters in mobile robots, manipulators, aerial systems, and embodied AI alike.

### Business & Commercial Layer

Capability ladders matter commercially because they reduce onboarding waste. A manager does not care that a new hire “spent three months learning ROS 2.” They care whether the person can own a bug, close an integration task, or produce a reproducible simulation result that de-risks hardware time. The same is true for freelancers and remote candidates. Customers and employers buy evidence of reliability, not elapsed study time.

For the learner, this is also a market positioning tool. In India, a capability-first roadmap helps frame yourself for industrial robotics, warehouse systems, inspection, and robotics software roles where demonstrable integration skill matters more than prestige signaling. In the US and Europe, it aligns well with roles in AMRs, manipulation, autonomy infrastructure, and simulation-heavy robotics teams. A roadmap written this way turns into a commercial narrative: here is what I can set up, what I can debug, what I can deploy, and what I can hand off.

### Hiring Signal

Job titles that respond well to a capability-based roadmap:

- Robotics Software Engineer (Entry Level)
- ROS 2 Integration Engineer
- Navigation Engineer
- Manipulation Software Engineer
- Robotics Simulation Engineer

Interview screens that test whether this roadmap produced real skill:

- walk through a personal repo and explain which capability gate it proves and which it does not
- debug a partially broken demo and identify which earlier skill gate was actually missing
- convert a vague capstone idea into subsystem milestones with explicit evidence artifacts
- explain why you would not move from simulation to hardware yet on a given robot task
- compare two weak portfolio projects and decide which one is more hireable based on reproducibility and integration depth

### Portfolio Projects

Beginner: `robotics-capability-ladder`
Deliverables: one table of capability tiers, one artifact for each foundation gate, one reflective gap log.
Suggested repo structure:

```text
robotics-capability-ladder/
├── tiers/
├── artifacts/
├── gap-log/
└── README.md
```

Acceptance criteria:

- each tier names a concrete capability instead of a time block
- every capability links to a real artifact
- the README explains what still remains unproven

Intermediate: `capability-reviewed-robot-stack`
Deliverables: one simulator-based robot project with checkpoints for bring-up, inspection, debugging, and documentation.
Suggested repo structure:

```text
capability-reviewed-robot-stack/
├── src/
├── docs/checkpoints/
├── bags/
├── scripts/
└── README.md
```

Acceptance criteria:

- each checkpoint has evidence, not just prose
- at least one failed attempt and fix are documented
- the progression from foundation to subsystem ownership is explicit

Advanced: `robotics-skill-tree-portfolio`
Deliverables: integrated capstone mapped to a tiered skill tree, interview questions, and role-fit analysis.
Suggested repo structure:

```text
robotics-skill-tree-portfolio/
├── capstone/
├── skill-tree/
├── interview-prep/
├── evidence/
└── README.md
```

Acceptance criteria:

- the capstone uses skills from at least three tiers
- the skill tree identifies hard gaps honestly
- a reviewer can understand the candidate’s current level in under ten minutes

### Future Trends (2026 / 2030 / 2035 / 2045)

- `2026`: skill-tree framing is becoming more useful than calendar framing because robotics roles are splitting across platform, autonomy, and learning tracks.
- `2030`: capability evidence will increasingly include simulator traces, CI history, and structured evaluation rather than only videos and READMEs.
- `2035`: organizations will expect engineers to move across classical robotics and learned systems, making dependency-aware progression more important.
- `2045`: durable roadmaps will still revolve around capabilities, but they will include stronger evaluation around data quality, fleet behavior, and human-robot operations.

### Interview Questions

1. Why is a calendar-based roadmap weak for robotics?
   Short answer: because finishing time blocks does not prove you can build, debug, or integrate real systems.
2. What is a better milestone than “studied Nav2 for one month”?
   Short answer: “can configure, run, inspect, and troubleshoot a Nav2 stack in simulation with documented trade-offs.”
3. Why should a capstone appear early in roadmap thinking?
   Short answer: because it gives later learning a system context and prevents disconnected study.
4. How do you know a capability gate is real?
   Short answer: another engineer can inspect the artifact and see that the task was actually completed and explained.
5. What is the safety benefit of capability-based progression?
   Short answer: it reduces the chance of escalating to hardware before the lower-level assumptions are under control.

### Further Depth

- ROS 2 documentation
- Nav2 documentation
- MoveIt documentation
- `Modern Robotics` by Kevin Lynch and Frank Park
- `Underactuated Robotics` by Russ Tedrake
