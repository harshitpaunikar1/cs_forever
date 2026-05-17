# Curriculum Overview

## Overview

This curriculum is designed for someone who wants to become employable in serious drone software, UAV autonomy, or flight-stack engineering without wasting time on low-signal certificate collecting.

The operating idea is simple: optimize for the stack companies actually use and for artifacts you can ship. In practice that means `C++`, `Python`, Linux, `PX4` or `ArduPilot`, `ROS 2`, `Gazebo` or `JSBSim`, `MAVLink`, `QGroundControl`, logs, simulation, testing, and embedded fundamentals.

## Why This Topic Matters

Most people approaching drones get trapped in one of two weak patterns:

- they collect courses but never build anything inspectable
- they chase AI, swarms, or flashy autonomy before they can control one vehicle well

This roadmap corrects both problems.

## Core Principles

- master one autopilot deeply before trying to be bilingual
- use simulation early and often
- learn mission tooling and telemetry, not just control theory
- treat logs, failure cases, and safety checks as core engineering work
- produce repos and writeups that a hiring manager can evaluate quickly

## Best First Specialization

Start with:

```text
PX4 + ROS 2 + Gazebo + MAVLink + C++/Python
```

Then add:

```text
ArduPilot + QGroundControl + OpenCV + JSBSim + NuttX
```

## What This Curriculum Prioritizes

- open-source foundations still active in `2026`
- engineering-grade written resources
- practical system integration
- career signal, not certificate signal

## What This Curriculum De-Prioritizes

- shallow survey courses
- deep learning before systems basics
- learning several autopilots at once
- spending early months in tools that are not central to employability

## Next Step

Move to [Learning Roadmap](02_Learning_Roadmap.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

A curriculum overview is only as useful as the clarity it provides about who it is for and what it actually produces. In the UAV industry, roles do not cluster around "drone interest" — they cluster around specific technical lanes: autopilot firmware, offboard autonomy, perception and CV, mission software, GCS and operator tooling, test infrastructure, and embedded bring-up. This curriculum is designed to produce engineers who are hireable in at least one of those lanes with verifiable artifacts, not engineers who have "studied drones."

The stack framing matters because UAV failures cluster at boundaries. The boundary between autopilot firmware and companion compute is where safety-critical messaging contracts are broken. The boundary between simulation and flight test is where hidden assumptions surface. The boundary between telemetry and decision-making is where autonomy goes wrong quietly. Engineers who understand the full stack — even without being experts in every layer — diagnose these boundary failures faster than specialists who know only their own layer deeply.

This curriculum front-loads flight-stack fundamentals, simulation, and log discipline precisely because those are the tools that reveal boundary failures early, when they are still cheap to fix.

### Industry Tool Stack

- **PX4 Autopilot** — primary autopilot; used for research, startup, and defense-adjacent UAV development; strong ROS 2 integration path
- **ArduPilot** — secondary autopilot for broader vehicle coverage; practical for inspection, agriculture, and fixed-wing commercial operations
- **MAVLink + MAVSDK + pymavlink** — message protocol and SDK layers for commanding, monitoring, and scripting autopilot interactions
- **QGroundControl** — operator and developer tool for parameter management, mission planning, telemetry viewing, and field debugging
- **ROS 2 (Humble / Iron)** — middleware for companion-compute autonomy, sensor fusion, and offboard control pipelines
- **Gazebo / JSBSim** — simulation environments for SITL integration and flight-dynamics modeling
- **Python + C++** — scripting and performance-critical code respectively; both are required at any serious UAV engineering team
- **Git + CI** — version control and automated build/test infrastructure; expected to be used from the first week onward

### Step-by-Step Applied Workflow

1. **Choose your primary lane**: firmware/embedded, autonomy/companion-compute, perception/CV, mission software, or test infrastructure. This curriculum covers all five, but your portfolio emphasis should pick one to go deep on.
2. **Work through Foundation completely**: do not skip to autonomy demos until SITL, telemetry, and log reading are solid. This is the most common mistake and the most expensive one.
3. **Build a lane-appropriate artifact at each tier**: Foundation produces a SITL and log toolkit; Core produces an offboard or telemetry system; Advanced produces an embedded, multi-vehicle, or safety-focused artifact.
4. **Document every artifact with a reproducible README**: team hiring is partly about verifying that a candidate can explain and reproduce their own work.
5. **Connect simulation evidence to every claim**: "it worked in SITL" is a stronger claim than "I built an autonomy demo" only if the SITL is reproducible and logged.
6. **Contribute to upstream or produce a visible open artifact**: PX4, ArduPilot, MAVSDK, and QGC all accept contributions; a merged PR is the strongest possible hiring signal.
7. **Package the portfolio coherently**: a GitHub profile with five half-finished repos is weaker than two well-documented, end-to-end projects.

### AI Integration

AI belongs in the later tiers of this curriculum, not the early ones. That is not an ideological position — it is a practical sequencing observation. The value of onboard AI in UAV systems comes from its interaction with the flight stack: perception feeds into state estimation, route optimization depends on telemetry, anomaly detection requires a baseline of normal flight data. If you do not understand the flight stack, you cannot evaluate whether your AI-driven behavior is correct or dangerous.

At the curriculum level, AI integration points include: computer vision for precision landing and obstacle avoidance (Perception tier); reinforcement learning for flight control policy refinement (Advanced/Controls tier); swarm coordination algorithms (Multi-Vehicle tier); anomaly detection in flight logs (Operations tier). Each of these entry points is described in the relevant page. What this overview communicates is that all of them require flight-stack literacy as a prerequisite — not a suggestion, but a hard dependency.

### Case Studies

**Skydio (California, USA)**: Skydio's R&D to production path for autonomous follow-me and inspection drones demonstrates the curriculum's stack exactly. Their engineers work across firmware (custom flight controller), computer vision (onboard NVIDIA Jetson inference), and mission software (enterprise app integration). The job postings consistently describe a full-stack UAV engineer profile — exactly what this curriculum builds toward. Skydio's obstacle avoidance work is particularly relevant to the Perception and Autonomy tier of this course.

**Auterion (Switzerland/USA)**: Auterion builds enterprise software (Auterion Enterprise PX4) on top of PX4 and offers Skynode — an onboard compute platform that integrates PX4 with a companion Linux environment. Their product directly demonstrates the Foundation → Core → Advanced progression of this curriculum: PX4 firmware at the base, ROS 2 and payload software in the middle, fleet management and enterprise API at the top. Their open-source contributions to PX4 are a model for the contribution path this curriculum targets.

**Zipline (USA/Rwanda/Ghana/Nigeria)**: Zipline operates high-speed fixed-wing delivery drones at scale for medical supply logistics in East Africa and US suburban delivery. Their engineering job descriptions require exactly the profile this curriculum produces: flight software engineers who can work across autopilot, mission software, and GCS tooling simultaneously, with rigorous testing and log discipline. Their operations at scale (millions of autonomous flights) demonstrate what the Career and Industry Readiness tier targets as a production outcome.

### Failure Modes & Safety

**Learning tool breadth before depth**: the most common curriculum mistake is spending time on eight different autopilot platforms, four GCS tools, and three simulators while building zero serious artifacts in any of them. Tool breadth is valuable after depth. Before depth it is expensive distraction.

**Skipping the boundary analysis**: UAV system failures rarely happen entirely inside one component. They happen at the interface between the autopilot and companion, between the simulator and actual hardware dynamics, between mission planning and actual terrain. The curriculum is organized to force engineers to work at these interfaces repeatedly. Skipping Foundation and jumping to perception or autonomy short-circuits exactly this boundary training.

**Treating simulation as a demo medium**: SITL is not a place to record screenshots. It is a controlled environment for discovering what your system actually does. Engineers who only run SITL when they want to show something — rather than running it to test hypotheses and capture log evidence — miss most of its safety value.

**No reproducibility discipline**: if you cannot reproduce your own demo from a clean checkout, hiring managers and collaborators cannot either. Reproducibility is a safety property in UAV work, not just a convenience. It is also the primary differentiator between a portfolio and a collection of screenshots.

### Business & Commercial Layer

The commercial map for UAV software engineers in 2026 runs across five major verticals, each with distinct hiring profiles:

**Inspection and mapping** (Skydio Enterprise, Percepto, Flyability, Pix4D, DJI Enterprise): largest employer count globally; needs engineers who can integrate autopilots with payload software, GCS, and data processing pipelines. India-specific growth driven by infrastructure surveys, power line inspection, and DGCA-compliant operations.

**Logistics and delivery** (Zipline, Wing, Amazon Prime Air, Swiggy drone delivery): highest engineering bar; demands flight software reliability, multi-vehicle operations, and deep log-driven safety culture. Very few open positions but extremely high-value.

**Defense and surveillance** (Shield AI, ideaForge, Garuda Aerospace, AeroVironment, Joby/Uber Elevate adjacents): fastest hiring growth in India following DGCA PLI scheme; requires certifiable software, safety-case documentation, and field-rugged integration.

**Agriculture** (precision agriculture drones in India via Garuda Aerospace, IdeaForge SWITCH for agri): growing domestic market driven by DGCA Kisan Drone certification path; needs autopilot configuration, spray-system integration, and GCS operability.

**Research and academia** (TU Delft MAVLab, MIT CSAIL aerial robotics, IISc, IIT Bombay UAV labs): needs PX4/ArduPilot contributors, algorithm-to-flight-test pipelines, and open-source publication habits.

### Hiring Signal

**Job titles that this curriculum's full completion targets:**
- **Flight Software Engineer** — mid-level role at Wing, Zipline, Joby, Shield AI; requires full-stack UAV engineering literacy including firmware, offboard, and test infrastructure
- **UAV Autonomy Engineer** — at Skydio, Aurora Flight Sciences, Auterion; requires ROS 2, perception, offboard control, and safety-aware architecture
- **Perception Engineer (UAV)** — at Skydio, DJI Enterprise, emerging Indian autonomy teams; requires OpenCV, depth estimation, and integration with autopilot state
- **Mission Software Engineer (MAVLink / MAVSDK)** — at GCS companies, enterprise drone integrators; requires mission scripting, telemetry tooling, and MAVSDK-level fluency
- **Ground Station Software Engineer** — at QGC-adjacent companies and enterprise integrators; requires understanding of all autopilot interfaces, operator workflow design, and telemetry reliability

**Specific interview screens this curriculum prepares you for:**
1. "Describe the end-to-end message path from a QGC mission upload command to the autopilot executing the first waypoint — at the MAVLink level."
2. "Given a PX4 log where the EKF switched to GPS-denied mode mid-flight, walk me through how you would identify the trigger and assess the navigation impact."
3. "Write a MAVSDK Python script that arms a simulated drone, takes off to 10 m, flies a square, and lands. Handle the case where arming fails."
4. "Explain the uORB publish/subscribe model in PX4. How does it differ from ROS 2 DDS, and why does PX4 use it instead?"
5. "What is the minimum set of safety behaviors you would implement before deploying a companion-compute offboard controller to a real vehicle for the first time?"

### Portfolio Projects

**Beginner: `uav-stack-map`**
- Deliverables: annotated architecture diagram of the full UAV stack (autopilot, companion, GCS, simulator, telemetry link), SITL run demonstrating each interface, and a written explanation of each boundary in plain language
- Suggested repo tree: `README.md`, `docs/stack_diagram.svg`, `sitl/run.sh`, `scripts/inspect_messages.py`, `notes/boundary_analysis.md`
- Acceptance criteria: (1) diagram is correct and identifies all five major components; (2) SITL run is reproducible from the README; (3) boundary analysis correctly identifies what happens when each link fails

**Intermediate: `lane-choice-portfolio`**
- Deliverables: one artifact in your chosen specialization lane (firmware module, offboard controller, perception pipeline, mission script, or test harness), fully documented, with a 300-word rationale for the lane choice and the tools selected
- Suggested repo tree: `README.md`, `src/`, `tests/`, `docs/rationale.md`, `logs/` or `outputs/`
- Acceptance criteria: (1) artifact runs end-to-end without additional dependencies beyond README setup; (2) rationale explains the trade-off against other lane choices; (3) at least one logged or measured output shows correctness

**Advanced: `full-stack-integration-demo`**
- Deliverables: complete integration demo across at least three stack layers (e.g., PX4 + ROS 2 offboard + perception pipeline, or ArduPilot + MAVSDK + custom GCS), with CI, logged evidence, safety analysis note, and architecture writeup
- Suggested repo tree: `README.md`, `.github/workflows/`, `autopilot/`, `companion/`, `gcs/`, `docs/architecture.md`, `docs/safety_assumptions.md`, `logs/`
- Acceptance criteria: (1) CI workflow passes on a clean runner; (2) safety assumptions document lists at least three explicit failure modes and mitigations; (3) architecture document explains every inter-component interface

### Future Trends

- **2026**: The curriculum's emphasis on PX4, ROS 2, MAVLink, and SITL reflects the current industry standard. BVLOS normalization globally will increase the hiring demand for engineers who combine flight-stack depth with test infrastructure rigor.
- **2030**: Onboard AI (edge inference on Jetson Orin class hardware) becomes mainstream in commercial UAVs. This does not replace the curriculum's fundamentals — it adds a perception and ML layer on top of them. Engineers who have both will dominate hiring.
- **2035**: Certification-grade software (DO-178C-style evidence for UAV software in urban airspace) becomes a commercial requirement in key markets. Engineers who have learned log discipline, safety analysis, and systematic testing as habits will adapt to this requirement faster than those who learned only features.
- **2045**: The UAV stack will have evolved significantly in tooling but not in physics. The fundamentals of state estimation, actuator control, telemetry, and failsafe logic remain — even in highly automated or AI-native aircraft. Foundation literacy remains a career-length asset.

### Interview Questions

1. **Why does this curriculum de-prioritize deep learning in the early stages?**
   *Answer*: Because deep learning in UAV systems interacts with autopilot state, sensor data, and safety logic — none of which you can reason about correctly without understanding the flight stack first. An engineer who adds a neural network to a flight system they do not understand creates risks they cannot identify. Flight-stack literacy is the prerequisite, not a nice-to-have.

2. **What makes a drone software portfolio credible to a hiring manager who has seen many drone portfolios?**
   *Answer*: Reproducibility (can I clone and run it?), evidence (are there logs, plots, or test outputs?), and honest scope (does the writeup match what the code actually does?). The most credible portfolios show controlled SITL experiments with logged outcomes, not impressive-looking demos with no rerun path.

3. **Explain the difference between an autopilot, a companion computer, and a GCS — and where each one can fail independently.**
   *Answer*: The autopilot runs safety-critical flight control at hard real-time rates (1–8 kHz) and owns arming, failsafe, and actuator output. The companion computer runs higher-level software (ROS 2, perception, mission logic) at soft real-time rates and sends commands to the autopilot via MAVLink. The GCS is the operator-facing tool for configuration, monitoring, and mission management. Each fails independently: autopilot failure means loss of control; companion failure means loss of autonomy (autopilot continues in a safe mode); GCS loss means loss of operator visibility (vehicle continues on its current mission or failsafe).

4. **What is the correct order of capability development in UAV engineering, and why?**
   *Answer*: (1) Toolchain and dev environment → (2) flight-stack and telemetry literacy → (3) simulation and log discipline → (4) companion-compute and offboard control → (5) perception and autonomy → (6) embedded and production readiness. Each tier depends on the one below it for correct behavior and for the ability to diagnose failures.

5. **Which lane (firmware, autonomy, perception, mission software, test infra) is the easiest to enter from this curriculum, and which is the hardest?**
   *Answer*: Mission software and GCS tooling are the easiest entry points — they require MAVLink fluency and Python scripting but do not require embedded or real-time expertise. Autopilot firmware is the hardest — it requires C++, RTOS/NuttX understanding, hardware knowledge, and the ability to write and validate safety-critical code. Autonomy and perception sit in the middle.

### Further Depth

- **PX4 Developer Guide** (docs.px4.io/main/en/) — the primary technical reference for this curriculum's autopilot layer
- **ArduPilot Developer Wiki** (ardupilot.org/dev/) — equivalent coverage for the ArduPilot-track content
- **MAVSDK Documentation** (mavsdk.mavlink.io) — SDK for Python, C++, and Swift clients; covers mission scripting, offboard control, and telemetry
- **ROS 2 Documentation** (docs.ros.org) — covers DDS, nodes, topics, actions, lifecycle nodes; the companion-compute middleware used throughout the Core and Advanced tiers
- **Dronecode Foundation** (dronecode.org) — the umbrella organization governing PX4, MAVSDK, QGroundControl, and MAVLink; good orientation to the open ecosystem
- **"Small Unmanned Aircraft: Theory and Practice"** — Beard and McLain; theory grounding for dynamics, estimation, and control chapters of this curriculum
