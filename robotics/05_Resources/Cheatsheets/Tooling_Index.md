# Tooling Index

## Core Tooling

- `ROS 2`
- `Gazebo`
- `RViz`
- `colcon`
- `ros2 cli`
- `Git`
- `Docker`

## Mobile Robotics

- `Nav2`
- `AMCL`
- `SLAM tools`
- `rosbag`

## Manipulation

- `MoveIt 2`
- `ros2_control`
- planning scene tools

## Perception

- `OpenCV`
- camera calibration tools
- fiducial libraries

## Embedded

- `micro-ROS`
- RTOS toolchains
- `SocketCAN`
- `i2c-tools`
- `spidev`

## Drones

- `PX4`
- `QGroundControl`
- SITL simulators

## Robot Learning

- `LeRobot`
- `Isaac Lab`
- `PyTorch`
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

A tooling index is useful when it helps an engineer choose the right instrument for the job instead of installing everything at once. In practice, robotics work moves faster when tooling choices are made by task: inspect a bag, visualize a graph, simulate a world, deploy a container, profile a node, or tune a controller. This page should therefore be used as a task-to-tool lookup, not as a giant shopping list.

### Industry Tool Stack

- `Visualization tools`: used to inspect state, frames, and behavior quickly.
- `Simulation tools`: used to test ideas before hardware risk is introduced.
- `Build and packaging tools`: used to keep environments reproducible.
- `Profiling and debugging tools`: used to explain latency, drops, and failures.

### Step-by-Step Applied Workflow

1. Start from the engineering task, not the tool category.
2. Pick the minimum tool set needed for that task.
3. Verify that the tool fits the stack you already use.
4. Capture one repeatable workflow with the tool before moving on.
5. Record what the tool is best at and where it is weak.
6. Keep the index updated when a better default emerges.

### AI Integration

AI helps here mainly as a recommender and explainer. It can narrow options or summarize tradeoffs, but tool choice still needs real stack awareness. In robotics, a tool that is excellent in isolation can be a poor fit if it breaks the existing simulation, deployment, or observability workflow.

### Case Studies

Open Robotics is a clear example of why tooling ecosystems matter: ROS 2 becomes productive because build, launch, bagging, and visualization tools fit together. NVIDIA's `Isaac ROS` is another useful benchmark because it shows how GPU-accelerated tooling only becomes valuable when the integration path with ROS 2 and deployment targets is coherent.

### Failure Modes & Safety

The failure mode for tooling pages is cargo-cult installation. Engineers collect tools they never operationalize, or they pick a powerful tool that nobody else on the team can support. Another risk is tool overlap that creates duplicated workflows and inconsistent debugging habits. The safe pattern is task-first selection and explicit defaults.

### Business & Commercial Layer

Tool choices affect delivery cost directly. Good defaults reduce onboarding time, debugging waste, and environment entropy. Bad tooling decisions increase maintenance burden and make the stack harder to hand over. That is why mature robotics teams treat tool selection as an operational decision, not a personal preference.

### Hiring Signal

Job titles supported by this page:

- Robotics Platform Engineer
- Robotics Software Engineer
- Tools Engineer (Robotics)

Interview screens it supports:

- choosing the right tool for a specific debugging or deployment problem
- comparing overlapping tools and naming the better default
- explaining when a tool should not be added to the stack

### Portfolio Projects

Beginner: write a `tool-choice note` explaining why one visualization and one simulation tool were selected.  
Intermediate: create a `debugging workflow` document mapping common robotics problems to specific tools.  
Advanced: publish a `stack-defaults guide` for a full robotics project with reasoning for each chosen tool.

### Future Trends

- `2026`: toolchains keep converging around reproducibility and observability.
- `2030`: GPU-aware and edge-deployment tools become normal even outside AI-heavy teams.
- `2035`: more robotics stacks standardize on tighter internal tool catalogs rather than open-ended tool sprawl.
- `2045`: platform tooling becomes a formal competitive advantage for robotics organizations.

### Interview Questions

1. What is the right way to choose a robotics tool?
   Short answer: start from the task, constraints, and existing stack.

2. Why is tool overlap dangerous?
   Short answer: it fragments debugging and increases maintenance cost.

3. When should a powerful tool still be rejected?
   Short answer: when it adds complexity without improving the main workflow.

4. Why keep a tooling index updated?
   Short answer: because stale defaults waste time and cause avoidable drift.

5. What is the value of a task-to-tool map?
   Short answer: it turns the index into an operational resource instead of a list.

### Further Depth

- `ROS 2` official docs
- `Foxglove` docs
- `rosbag2` and `MCAP` docs
- `Isaac ROS` repositories
- `LeRobot` documentation
