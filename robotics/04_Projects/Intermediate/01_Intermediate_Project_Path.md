# Intermediate Project Path

## Overview

These projects focus on the robotics systems that employers inspect most often: navigation, control, perception, and manipulation in simulation-first workflows.

## Projects

### Project 1: Gazebo + Nav2 Autonomous Navigation Demo
- mapping or saved map
- localization
- goal following
- obstacle avoidance

### Project 2: MoveIt 2 Manipulator Demo
- planning scene
- obstacle-aware planning
- one pick-and-place routine

### Project 3: ros2_control Integration Demo
- controller manager
- one controller
- simulation validation

### Project 4: Robot Perception Starter Pack
- camera calibration
- fiducial or feature pipeline
- pose publication in ROS 2

### Project 5: Algorithm Comparison Notebook
- one planner
- one estimator
- one controller
- short engineering comparison

## Completion Standard

Finish at least `2` to a strong standard with docs, screenshots, and verification steps.

## Next Step

Move to [Advanced Project Path](../Advanced/01_Advanced_Project_Path.md) when you want one flagship portfolio piece.
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Intermediate projects are where robotics work starts looking like subsystem ownership rather than tutorial completion. At this stage, the important question is not whether you can use a tool in isolation. It is whether you can make two or three components cooperate and then diagnose what happens when they do not. A navigation demo with localization, planning, and controller tuning; a `MoveIt 2` stack tied to execution; a perception pipeline feeding pose estimates to another node; or an algorithm comparison that drives an engineering choice are all intermediate because they expose interface problems, timing problems, and system assumptions that do not appear in isolated examples.

This is very close to the kind of work early-career robotics engineers do in practice. They are handed a subsystem boundary, not a blank sheet. The task is to integrate, configure, validate, and document. That makes this page strongly hiring-relevant. Reviewers are watching for whether the project owner can define acceptance criteria, stand up subsystems independently, connect them cleanly, record evidence, and explain why one configuration or approach was chosen over another. The project does not need to be huge. It needs to be inspectable and defensible under technical questioning.

### Industry Tool Stack

- `Nav2`: used for mobile-robot localization, planning, control, and recovery integration work.
- `MoveIt 2`: used for manipulation planning and execution pipelines that must connect to robot models and controllers.
- `ros2_control`: used to expose hardware abstractions and controllers in a way other ROS 2 subsystems can use.
- `OpenCV`: used for calibration, feature extraction, and pose-estimation components that feed downstream robot logic.
- `Gazebo` or `Isaac Sim`: used to validate multi-component behavior before touching hardware.
- `rosbag2` with `MCAP`: used to capture integration failures and replay them later instead of guessing.
- `Foxglove`, `RViz`, and `PlotJuggler`: used to inspect graph state, timing, robot state, and controller behavior while debugging.
- `Docker` and CI: used to keep the project reproducible once dependencies and configuration start multiplying.

### Step-by-Step Applied Workflow

1. Choose one integration problem and define exactly which boundary the project is proving.
2. Write the acceptance metric first, such as repeatable goal reaching, stable execution of a planned motion, or pose estimates consumed downstream.
3. Validate each subsystem independently and record its baseline behavior before integration.
4. Connect interfaces one at a time, checking message types, frame assumptions, topic rates, and launch order at each step.
5. Record a bag or trace the first time the full system runs, so later regressions have a concrete reference.
6. Introduce one controlled perturbation such as delay, map inconsistency, parameter change, or payload variation.
7. Write an integration note that explains the real bottleneck rather than just listing parameter tweaks.
8. Package the repo with demo instructions, metrics, and a short statement of what still blocks credible hardware deployment.

### AI Integration

AI becomes more natural on intermediate projects because perception and decision-support components now feed other subsystems. An object detector may provide candidate targets to a manipulation pipeline. A learned classifier may filter events before a planner reacts. A pose-estimation model may feed a grasp or docking workflow. What matters is that the model output now crosses an interface boundary. That means the project owner must care about latency, confidence thresholds, coordinate frames, and fallback behavior, not just model accuracy in isolation.

This is where many otherwise strong projects become weak. The AI component looks modern, but the rest of the stack cannot explain how the output is trusted or what happens when it is wrong. A strong intermediate repo avoids that trap. It makes the contract explicit: input, output, timing, downstream consumer, failure behavior. If AI is present, it should make the project more capable while keeping the robotics system more measurable, not less.

### Case Studies

The `Nav2` team and Open Navigation LLC are strong references because navigation projects become much more credible when they mirror the configuration discipline and debugging workflow of real `Nav2` deployments. Picknik Robotics is equally relevant for manipulation integration because `MoveIt 2` projects rise or fall on clear scene setup, kinematics assumptions, and execution boundaries. Clearpath Robotics is another good benchmark because its mobile platforms and integration examples show what believable mid-tier subsystem work looks like when logs, configs, and interfaces are handled seriously.

### Failure Modes & Safety

Intermediate failures are usually interface failures. A planner expects one frame and receives another. A perception node publishes at a rate the consumer cannot handle. A controller assumes an update loop the rest of the graph cannot maintain. The project may “mostly work,” but only in one lucky configuration. Another common failure is parameter superstition: the engineer keeps tuning until the demo passes once, then cannot explain why. That signals weak system ownership even if the final video looks good.

Safety matters because these projects start resembling real operational stacks. A manipulation demo without bounded execution assumptions, a navigation project without a credible recovery story, or a controller bridge without command limits teaches bad engineering instincts. The right pattern is controlled realism: show the limits, expose the assumptions, and say clearly what must be fixed before hardware use would be responsible.

### Business & Commercial Layer

Intermediate projects line up closely with the work many robotics companies actually buy. AMR teams need engineers who can integrate localization, planning, and controller behavior. Manipulation teams need people who can connect calibration, planning, and execution. Integrators need engineers who can diagnose interface failures quickly and document exactly what changed. That makes this page commercially strong because it demonstrates productive integration behavior rather than just tool familiarity.

In India, this page is especially useful for startups and integrators where one engineer often spans multiple parts of the stack in the same project. In the US and Europe, it maps directly to roles in navigation, perception integration, controls integration, and robotics applications engineering. Remote work is viable here when the artifact quality is high, because the evidence lives in repos, bags, metrics, and diagrams. Commercially, intermediate projects are often where a portfolio starts looking employable rather than merely promising.

### Hiring Signal

Job titles that fit this page:

- Robotics Software Engineer
- Navigation Software Engineer
- Manipulation Integration Engineer
- Robotics Applications Engineer
- Robotics Test and Validation Engineer

Interview screens these projects prepare you for:

- debug a ROS 2 graph where two subsystems compile independently but fail when integrated because of frame or timing mismatch
- explain how `Nav2` or `MoveIt 2` would be configured differently for a changed robot or task assumption
- inspect a bag or metrics plot and identify the true bottleneck in an integration failure
- compare two algorithms or configurations and justify one using evidence rather than preference
- describe what additional checks would be needed before the project could leave simulation and touch hardware

### Portfolio Projects

Beginner bridge project: `Navigation Stack Bring-Up`

- Deliverables: simulated robot, localization setup, goal execution demo, and one debug note on a failure case.
- Suggested repo structure:

```text
navigation-stack-bringup/
├── maps/
├── params/
├── launch/
├── rviz/
├── bags/
└── README.md
```

- Acceptance criteria:
  - the robot reaches declared goals repeatedly in the same environment
  - one recovery or failure case is logged and explained
  - configuration files are documented well enough for another engineer to modify them

Intermediate core project: `Perception-to-Action Demo`

- Deliverables: one perception pipeline, one downstream consumer node, latency notes, and a replayable bag.
- Suggested repo structure:

```text
perception-to-action-demo/
├── src/
│   ├── perception_pkg/
│   └── consumer_pkg/
├── config/
├── launch/
├── data/
└── docs/
```

- Acceptance criteria:
  - perception output drives another subsystem in a measurable way
  - latency or confidence handling is documented explicitly
  - one interface mismatch encountered during development is explained and fixed

Advanced stretch project: `MoveIt 2 or ros2_control Integration Study`

- Deliverables: planning/execution pipeline, hardware or simulated controller interface, metrics on execution behavior, and a system diagram.
- Suggested repo structure:

```text
integration-study/
├── src/
├── config/
├── launch/
├── analysis/
├── tests/
└── README.md
```

- Acceptance criteria:
  - the project shows end-to-end motion or control behavior beyond isolated planning
  - evidence includes logs or plots, not just final poses
  - the write-up names the top risks for real hardware deployment

### Future Trends

- `2026`: intermediate robotics work is increasingly expected to include replayable logs, metrics, and reproducible simulation instead of one-shot demos.
- `2030`: perception, planning, and learned components blend more tightly, increasing the value of interface-debugging skill.
- `2035`: fleet-scale robotics companies rely even more on engineers who can connect subsystem evidence across integration boundaries.
- `2045`: mid-tier robotics engineering becomes less about owning one algorithm and more about proving that multi-component systems behave predictably under change.

### Interview Questions

1. What makes an integration project stronger than a standalone algorithm demo?
   Short answer: it proves interface reasoning, debugging ability, and system ownership instead of isolated implementation.

2. Why record bag files during integration?
   Short answer: because they let you reproduce timing, data, and failure conditions instead of guessing from a demo video.

3. What is the first thing to check when two ROS 2 subsystems fail together?
   Short answer: interface assumptions such as topic names, message types, frame alignment, and timing.

4. Why is configuration management important on intermediate projects?
   Short answer: because integration failures often come from parameters and environment assumptions rather than code defects.

5. When should an intermediate project remain in simulation?
   Short answer: when the owner still cannot explain the failure envelope or bound unsafe behavior on hardware.

### Further Depth

- `Nav2` docs and configuration guides
- `MoveIt 2` docs for planning and execution interfaces
- `ROS 2` launch and testing docs
- `Foxglove` docs for graph and data inspection
- `rosbag2` and `MCAP` docs for replay-based debugging
