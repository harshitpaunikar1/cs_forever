# Learning Roadmap

## Overview

This roadmap converts the UAV stack into a practical sequence you can actually execute. The goal is not to read everything. The goal is to build compounding capability.

## Study Sequence

### Phase 1: Tooling and Fundamentals

- Linux daily workflow
- Git and GitHub
- C++ and Python
- aerodynamics intuition
- electronics basics

### Phase 2: Flight-Stack Literacy

- PX4 or ArduPilot
- MAVLink messages and protocols
- QGroundControl basics
- SITL and logs

### Phase 3: Companion and Autonomy Work

- ROS 2
- offboard control
- Gazebo or JSBSim
- estimation and control
- perception

### Phase 4: Production Thinking

- embedded systems and NuttX
- safety-minded testing
- multi-vehicle workflows
- polished portfolio and upstream contribution

## Recommended Weekly Pattern

1. Read one serious topic page.
2. Build one small related artifact.
3. Capture one written note about what failed or what you learned.
4. Keep one main repo clean and reproducible.

## Quality Bar

Every month should end with at least one visible output:

- code
- logs
- plots
- design notes
- architecture diagrams
- or a reproducible simulator workflow

## Next Step

Continue to [Linux Git C++ Python and Aerodynamics Foundations](../02_Engineering_Workflow/01_Linux_Git_Cpp_Python_and_Aerodynamics_Foundations.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

UAV engineering teams do not hire by elapsed weeks or certificate count. They hire by demonstrated capability: can you build and debug a dev environment from scratch, run SITL and read the resulting log, understand autopilot mode logic and failsafe behavior, and ship one coherent artifact in your chosen lane? The question is always "what can you build and explain?" not "how long have you been studying?"

This means a useful UAV learning roadmap must be organized as a **capability tree**, not a calendar. Each branch of the tree represents a set of skills that unlock downstream branches. You cannot do real companion-compute offboard work if you do not understand MAVLink message contracts. You cannot do meaningful perception work if you do not understand vehicle state and estimation. You cannot do production-grade embedded work if you do not understand the RTOS and hardware bring-up. The tree structure forces you to be honest about which branches you have actually earned versus which ones you have read about.

In industry, capability gates are verified through code review, debugging exercises, and live system operation — not quizzes. The roadmap below reflects that reality.

### Industry Tool Stack

- **Linux CLI + build toolchains** — the prerequisite substrate; used daily at every gate
- **Git + GitHub / GitLab + CI** — version control and automated verification used from the first artifact onward
- **PX4 or ArduPilot SITL** — the primary practice environment; unlocked at Gate 1 and used continuously
- **pymavlink / MAVSDK** — MAVLink scripting tools; unlocked at Gate 2 and extended through Gate 4
- **QGroundControl** — operator and developer tool; used at every gate for inspection, configuration, and mission verification
- **ROS 2** — companion-compute middleware; unlocked at Gate 3 for offboard and autonomy work
- **Gazebo / JSBSim** — physics simulation; Gazebo used from Gate 2 onward, JSBSim specifically at Gate 4 for fixed-wing/VTOL FDM work
- **NuttX RTOS + cross-compilation toolchain** — embedded bring-up tooling; unlocked at Gate 5 for firmware-level work

### Step-by-Step Applied Workflow

The workflow below maps to the five capability gates described in the main roadmap.

1. **Verify Gate 1 (Tooling)**: clean Ubuntu install → PX4 or ArduPilot SITL builds successfully → one pymavlink script prints live telemetry → Git repo is initialized and first commit is pushed. If any of these fail without knowing why, Gate 1 is not earned.
2. **Verify Gate 2 (Flight-Stack Literacy)**: upload a waypoint mission via QGC → inspect the `MISSION_ITEM_INT` MAVLink messages during upload → explain what happens to the vehicle if it loses GPS during a mission → read a `.ulg` or `.bin` log and identify the mode transition sequence.
3. **Verify Gate 3 (Companion-Compute)**: write a ROS 2 node that subscribes to vehicle state over PX4-ROS2 bridge or MAVSDK → command an offboard position setpoint and verify the vehicle responds in SITL → implement a watchdog that returns vehicle to HOLD if offboard heartbeat is lost.
4. **Verify Gate 4 (Autonomy or Perception)**: build one functional module — precision landing using ArUco detection, obstacle field from depth camera, or mission replanning from telemetry — in SITL with logged evidence of correct behavior.
5. **Verify Gate 5 (Production or Embedded)**: choose one: (a) NuttX driver or PX4 module with unit tests merged or review-ready; (b) multi-vehicle test harness with assertions and CI; (c) safety case document for one specific flight mode with identified failure modes and mitigations.
6. **Package the evidence portfolio**: every gate must have a reproducible artifact — code + README + logs or test outputs. The portfolio is the gate verification.
7. **Choose a contribution path**: identify one upstream project (PX4, ArduPilot, MAVSDK, QGC, or a related library) where you can submit a meaningful change; a merged contribution is the strongest single hiring signal.

### AI Integration

AI tools enter the capability tree at specific branches where they add genuine leverage without masking the underlying skill.

**At Gate 2 (Flight-Stack Literacy)**: LLM assistants can explain MAVLink message fields, parse parameter documentation, and suggest pymavlink code patterns. This is legitimate use — it speeds up routine lookup without replacing understanding. The test is whether you can verify the suggestion against the MAVLink spec without just trusting it.

**At Gate 4 (Perception and Autonomy)**: AI/ML is the core subject matter. Computer vision models for ArUco detection, depth estimation for obstacle avoidance, and learned flight policies all live here. This is the primary AI branch of the capability tree. The prerequisite is Gate 2 (understanding the vehicle state that perception must respect) and Gate 3 (understanding the command interface that autonomy sends through).

**Across all gates**: Copilot-style code assistance speeds up boilerplate writing but creates a known trap — code that compiles but is semantically wrong for the flight stack context (wrong coordinate frames, wrong message types, wrong rate assumptions). Gate verification closes this trap by requiring demonstrated understanding, not just working code.

### Case Studies

**Wing Operations (capability-ladder evidence at scale)**: Wing's flight software teams operate with strict gate discipline — engineers do not touch flight-critical code paths until they have verified competence in telemetry, log analysis, and SITL testing. Their internal onboarding reflects almost exactly the capability ladder described here: tooling, telemetry literacy, simulation discipline, and only then production flight software. Wing's emphasis on log-based evidence of every change is a direct commercial manifestation of Gate 2 and Gate 5 discipline.

**Garuda Aerospace (India)**: India's largest drone-as-a-service operator (agricultural spraying, surveillance, logistics) hires engineers who can move rapidly from SITL to field deployment because their operation cycles are short. The practical implication is that Gate 1 and Gate 2 must be very solid — field debugging without a good log habit and a robust dev environment is extremely expensive. Their domestic focus means India-specific regulatory (DGCA Digital Sky, Remote Pilot Licences, UIN registration) awareness is part of the Gate 5 production readiness picture.

**Auterion Enterprise PX4 Platform**: Auterion's Skynode product requires engineers who have earned Gate 3 at minimum — they need to understand PX4 firmware, companion compute architecture, and ROS 2 or payload SDK integration simultaneously. Their public GitHub (github.com/Auterion) shows exactly the kind of Gate 3–5 artifacts that this capability ladder is designed to produce.

### Failure Modes & Safety

**Gate-skipping**: the most destructive failure mode for a self-directed learner. Gate-skipping typically happens by watching a demo that makes Gate 4 look accessible without Gate 2, and then spending three months on a perception demo that fails mysteriously in ways that Gate 2 would have diagnosed in an afternoon. The symptom of gate-skipping is autonomy code that works in controlled demos but fails unpredictably in varied conditions.

**Demo-without-evidence**: reaching Gate 4 but building demos that are not reproducible and have no logged evidence of what actually happened. Demo-without-evidence creates a portfolio that looks impressive but cannot survive technical review. Interviewers at Wing, Skydio, and serious UAV companies do ask "can I run this and reproduce it?" The answer must be yes.

**Artificial urgency**: setting time deadlines ("I will finish Gate 3 in 4 weeks") that create pressure to call a gate done before the artifacts are actually solid. Gate 2 is not complete when you can run SITL once. It is complete when you can debug a SITL anomaly from the log without help. The tree does not move until the branch is actually stable.

**Safety habit gaps**: building autonomy or offboard control without explicitly designing and testing the failsafe return-to-home or HOLD behavior. Every Gate 3 and Gate 4 artifact must include a demonstrated answer to "what happens when the companion compute crashes?" If the answer is "I don't know," Gate 3 is not earned for production purposes.

### Business & Commercial Layer

The capability ladder maps to salary and responsibility tiers directly in the UAV job market.

**Gate 1–2 completion**: qualifies for UAV test operator, field integration engineer, and junior GCS/mission-software roles. Salary range in India (2026): ₹6–12 LPA for experienced profiles. In US/Europe: $70–100k for entry-level flight software and integration roles.

**Gate 1–3 completion**: qualifies for autonomy engineer (junior), ROS 2 developer (UAV context), and offboard control roles. This is the target gate for most engineers completing the Core UAV section. India: ₹12–20 LPA; US: $100–130k.

**Gate 1–5 completion**: qualifies for senior flight software engineer, autopilot firmware engineer, and technical lead roles. This is the target gate for engineers completing the full Advanced section. India: ₹20–40 LPA for senior roles; US: $130–180k for senior Flight Software Engineer roles at Wing or Zipline level.

The commercial ROI of each gate is real and measurable. This is not a motivational framing — it reflects actual job posting requirements and compensation data from UAV industry job boards.

### Hiring Signal

**Job titles organized by the gate that makes you eligible:**

Gates 1–2 (Tooling + Flight-Stack Literacy):
- **Systems Test Engineer (UAV)** — writes and runs SITL-based test cases; requires Gate 1 tooling and Gate 2 log analysis
- **Field Integration Engineer** — configures autopilots, verifies missions, and debugs field issues; requires Gate 2 telemetry and parameter fluency

Gates 1–3 (adding Companion-Compute):
- **ROS 2 / Robotics Engineer (Aerial)** — builds companion-compute pipelines for offboard control, payload integration, or sensor fusion
- **Mission Software Engineer (MAVLink/MAVSDK)** — scripts missions, builds GCS integrations, and manages autopilot command interfaces

Gates 1–4 (adding Perception/Autonomy):
- **UAV Autonomy Engineer** — builds perception, planning, and decision pipelines integrated with the flight stack; requires Gate 3 prerequisite
- **Perception Engineer (UAV)** — specializes in CV, depth, or learned representations for navigation and landing assistance

Gates 1–5 (full stack):
- **Flight Software Engineer** — works across firmware, offboard, and test infrastructure; requires all five gates
- **Autopilot Firmware Engineer (PX4/ArduPilot)** — writes C++ firmware modules, NuttX drivers, and submits upstream contributions

**Interview screens by gate:**

Gate 2 screen: "Given this `.ulg` log, tell me what caused the vehicle to switch from Position Control to Altitude Control at timestamp 47 seconds. What data tells you that?"

Gate 3 screen: "Describe the exact message and rate your companion computer must send to maintain OFFBOARD mode in PX4. What happens if the rate drops below the threshold?"

Gate 4 screen: "Your precision landing pipeline is working in simulation but the vehicle misses the pad in field testing by 0.5 m consistently. List five possible causes and how you would diagnose each from logs."

Gate 5 screen: "Write the safety assumptions document for your offboard controller: what are the three most likely failure modes and what does your system do in each case?"

### Portfolio Projects

**Gate 1–2 artifact: `px4-sitl-log-audit`**
- Deliverables: SITL environment setup, one documented mission run, Python log analysis tool extracting mode transitions and attitude error, comparative note across two parameter configurations
- Suggested repo tree: `README.md`, `setup/`, `missions/`, `scripts/log_audit.py`, `logs/`, `notes/param_comparison.md`
- Acceptance criteria: (1) setup reproducible on clean Ubuntu in under 45 min; (2) log audit script produces labeled plots; (3) param comparison note identifies measurable difference between configs

**Gate 3 artifact: `ros2-offboard-controller`**
- Deliverables: ROS 2 node commanding PX4 offboard position setpoints in SITL, with heartbeat watchdog, mode management, and logged position error; documented with interface diagram
- Suggested repo tree: `README.md`, `ros2_ws/src/offboard_ctrl/`, `docs/interface_diagram.svg`, `logs/`, `tests/`
- Acceptance criteria: (1) vehicle holds commanded setpoint in SITL within 0.5 m; (2) watchdog triggers HOLD within 2 seconds of simulated companion crash; (3) interface diagram correctly shows all MAVLink and ROS 2 message flows

**Gate 4–5 artifact: `precision-landing-demo`**
- Deliverables: ArUco-based precision landing pipeline in Gazebo SITL, with detection node, offboard descent logic, landing accuracy statistics across 10 runs, and safety analysis doc
- Suggested repo tree: `README.md`, `ros2_ws/src/aruco_detector/`, `ros2_ws/src/precision_land/`, `docs/safety_analysis.md`, `data/accuracy_stats.csv`, `logs/`
- Acceptance criteria: (1) landing accuracy within 0.3 m CEP across 10 reproducible SITL runs; (2) safety analysis doc explicitly addresses what happens if ArUco marker is lost at each descent stage; (3) all runs are logged and stats are computed from actual log data, not manual observation

### Future Trends

- **2026**: The five-gate capability ladder structure reflects current industry hiring reality. BVLOS expansion (India DGCA Type Certification, FAA BVLOS ARC, EASA U-Space) is adding new Gate 5-level requirements around safety cases and operational documentation to commercial UAV engineering.
- **2030**: AI-native flight stacks (neural network policies for flight control, learned world models for planning) begin to appear in research and advanced commercial products. Gate 4 (Perception/Autonomy) expands to cover reinforcement learning and sim-to-real transfer. Gates 1–3 remain necessary prerequisites because the physics does not change.
- **2035**: Urban Air Mobility (eVTOL) creates a new Gate 6 equivalent: DO-178C-adjacent software qualification, formal safety cases, and airspace integration software. Engineers who have built Gate 5 discipline adapt to this requirement faster than those who have not.
- **2045**: The capability tree structure is more durable than any specific tool. Python, C++, ROS 2, and PX4 will have evolved significantly, but the gates — tooling fluency, protocol literacy, companion integration, perception, production safety — remain because they reflect the physics and safety requirements of flight, not any particular implementation.

### Interview Questions

1. **What is the difference between a calendar-based roadmap and a capability-based ladder for UAV learning, and why does the distinction matter in practice?**
   *Answer*: A calendar roadmap says "spend 4 weeks on Foundation." A capability ladder says "earn the Foundation gate by demonstrating X, Y, and Z." The calendar creates pressure to call a gate done by a date regardless of artifact quality. The capability ladder tells you whether you have actually earned the skill. In UAV work, the distinction matters because the failures that hurt people happen when gates are called complete by time rather than by demonstrated capability.

2. **What specific skills must you demonstrate before you have earned Gate 2 (Flight-Stack Literacy) on this ladder?**
   *Answer*: You must be able to: (1) upload a mission and explain the MAVLink message sequence; (2) read a `.ulg` or `.bin` log and identify the mode sequence and any anomalies; (3) explain what happens under at least three different failsafe triggers (GPS loss, RC loss, battery low); (4) inspect and compare two different parameter configurations and articulate the behavioral difference.

3. **Why is Gate 3 (Companion-Compute) a prerequisite for Gate 4 (Perception/Autonomy) rather than a parallel track?**
   *Answer*: Because perception and autonomy systems running on the companion computer must interact with the autopilot through MAVLink OFFBOARD mode, which requires heartbeat maintenance, mode management, and understanding of the autopilot's response to setpoint errors. If you build perception without Gate 3, you will not know how to send the output to the vehicle safely, how to handle mode switches that interrupt your autonomy pipeline, or how to recover when the vehicle rejects your offboard commands.

4. **Describe what "demonstrating" Gate 5 (Production/Embedded) looks like — what artifacts are required?**
   *Answer*: At minimum, one of: (a) a PX4 or ArduPilot firmware module with unit tests that could pass code review; (b) a multi-vehicle SITL test harness with CI integration and assertion-based pass/fail logic; or (c) a safety case document for a specific flight mode, with named failure modes, trigger conditions, mitigations, and evidence. The key is that Gate 5 requires a production-quality artifact with explicit safety reasoning — not just working code.

5. **How does contributing to an upstream project (PX4, ArduPilot, MAVSDK, QGC) function as gate verification?**
   *Answer*: Upstream contribution requires you to understand the codebase well enough to make a correct change, write a description that the maintainers accept, handle review feedback, and produce something that passes CI. This is harder than building a private project because the bar is set by experienced engineers, not by yourself. A merged PR in PX4 or ArduPilot is the single strongest indicator that Gate 4 or Gate 5 is genuinely earned.

### Further Depth

- **PX4 Developer Guide** (docs.px4.io/main/en/) — authoritative reference for all PX4 gates
- **ArduPilot Developer Wiki** (ardupilot.org/dev/) — equivalent for ArduPilot track
- **MAVSDK Documentation** (mavsdk.mavlink.io) — Gate 2–4 scripting reference
- **ROS 2 Documentation** (docs.ros.org) — Gate 3 middleware reference
- **"Small Unmanned Aircraft: Theory and Practice"** — Beard and McLain; the theory grounding for Gate 4 estimation and control content
- **PX4 Flight Review** (review.px4.io) — log analysis tool used in Gate 2 verification; run your logs here as a baseline comparison
- **Dronecode Foundation** (dronecode.org) — upstream contribution entry points across PX4, MAVSDK, QGC, and MAVLink
