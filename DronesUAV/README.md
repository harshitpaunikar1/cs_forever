# Drones and UAV Study Guide

This study guide is organized as a practical UAV curriculum rather than a loose collection of links. The goal is to move from engineering workflow fluency into flight stacks, simulation, telemetry, ROS 2 companion software, controls, perception, embedded systems, and portfolio-grade UAV projects.

The material is intentionally layered. Foundation builds Linux, C++, Python, and flight-stack familiarity. Core UAV explains how real drone software systems are structured across PX4 or ArduPilot, MAVLink, QGroundControl, ROS 2, dynamics, and perception. Advanced topics extend into NuttX, JSBSim, multi-vehicle systems, safety-minded testing, and industry readiness. Projects convert the reading path into inspectable engineering proof.

## How to Use This Guide

1. Start with `Foundation` unless you already work comfortably with Linux, Git, Python, C++, ROS 2 basics, and simulation workflows.
2. Move through `Core UAV` in order. The sections were arranged so that flight-stack architecture, telemetry, companion compute, control, and perception reinforce each other.
3. Treat `Advanced` as specialization material. You do not need every topic immediately, but the sequence is designed for employable UAV software work in `2026`.
4. Use `Projects` as the proof layer. If you cannot build something from a topic, you do not fully own it yet.
5. Use `Resources` for the ranked source stack, tooling map, and portfolio checklist when you want a fast reference.

## Section Map

- `Foundation`: curriculum map, roadmap, Linux/Git/C++/Python workflow, aerodynamics intuition, autopilot concepts, and simulation basics.
- `Core UAV`: PX4 or ArduPilot internals, MAVLink and QGroundControl, ROS 2 companion systems, dynamics, estimation, control, and perception.
- `Advanced`: NuttX and embedded bring-up, fixed-wing and VTOL modeling, multi-vehicle workflows, logs, reliability, safety, and career readiness.
- `Projects`: beginner, intermediate, and advanced UAV project paths.
- `Resources`: ranked resource index, tooling index, and portfolio checklist.

## Recommended Starting Points

- [Curriculum Overview](01_Foundation/01_Start_Here/01_Curriculum_Overview.md)
- [Learning Roadmap](01_Foundation/01_Start_Here/02_Learning_Roadmap.md)
- [Foundation](01_Foundation/00_Overview.md)
- [Core UAV](02_Core_UAV/00_Overview.md)
- [Advanced](03_Advanced/00_Overview.md)
- [Projects](04_Projects/00_Overview.md)
- [Navigation Map](NAVIGATION.md)

---
## 🔧 Industry Enrichment (Appended)
---

## What This Curriculum Prepares You For

This curriculum is calibrated to the actual hiring bar for UAV software engineering roles in 2026, not to what looks impressive in a YouTube tutorial. The distinction matters because the UAV software engineering job market has stratified: Foundation and Core competence is increasingly table stakes (attainable through online courses), while Advanced specialization and portfolio evidence are the differentiators. This curriculum addresses all three levels.

**Commercial UAV companies hiring from this skill set** (non-exhaustive):
- **Wing (Alphabet)** — delivery drone operations and autonomy engineering; strong GNC, MAVLink, and reliability engineering demand
- **Zipline** — fixed-wing delivery; fixed-wing GNC, embedded firmware, and simulation-first engineering culture
- **Skydio** — autonomous drone; visual navigation, ROS 2, and onboard perception engineering
- **Joby Aviation** — eVTOL; flight dynamics, embedded certification-track software, and safety engineering
- **Shield AI** — defense UAV; multi-vehicle coordination, GPS-denied autonomy, and swarm systems
- **Auterion** — commercial PX4 enterprise; PX4 firmware, fleet management, and upstream open-source contribution
- **ideaForge (India)** — defense and surveillance UAV; PX4 integration, DGCA regulatory navigation, and domestic hardware bring-up
- **Garuda Aerospace (India)** — agricultural and mapping UAV fleet; MAVLink, fleet operations software, and ground support tooling

## Technical Depth Map

Each section of this curriculum corresponds to a specific layer of the professional UAV stack:

```
[Hardware: Pixhawk, STM32H7, sensors, actuators]
    ↓
[Embedded RTOS: NuttX, drivers, BSP]          ← Advanced: Embedded
    ↓
[Flight Stack Core: PX4 / ArduPilot]          ← Foundation + Core
    - Modules: EKF2, position controller, failsafe
    - Communication: uORB publish/subscribe
    - Protocol: MAVLink (pymavlink, MAVSDK)
    ↓
[Simulation Layer: Gazebo Classic/Harmonic, JSBSim SITL]
    ↓                                          ← Foundation + Advanced: FDM
[Companion Compute: Jetson Orin, RPi]
    - OS: Ubuntu 22.04 + ROS 2 Jazzy
    - Bridge: Micro-XRCE-DDS (PX4↔ROS 2)
    - Perception: OpenCV, VIO (ORB-SLAM3)
    - Autonomy: ROS 2 offboard nodes
    ↓
[Ground Control: QGC, pymavlink, mission scripting]
    ↓
[Fleet / Operations: log analysis, safety cases, UTM]   ← Advanced: Safety
```

## Curriculum Scope — What Is and Isn't Covered

**In scope:**
- Open-source flight stack depth (PX4 and ArduPilot to module/driver level)
- Simulation-first engineering workflow (SITL, log analysis, parameter validation)
- ROS 2 companion software architecture and offboard control
- MAVLink protocol and mission scripting (pymavlink, MAVSDK)
- Camera perception and precision landing (OpenCV, ArUco, coordinate frames)
- Embedded flight firmware (NuttX, drivers, board bring-up concepts)
- Fixed-wing and VTOL simulation (JSBSim, TECS, FDM modeling)
- Multi-vehicle simulation and coordination
- Safety case methodology and production-readiness discipline
- Portfolio hardening and upstream contribution

**Out of scope (deliberately):**
- Hardware manufacturing, PCB design, or physical drone assembly
- FAA/EASA certification engineering (requires a separate dedicated curriculum)
- Deep learning for perception (covered in separate ML modules in this learning system)
- Proprietary flight stacks (DJI SDK, Autel, Parrot)
- Drone regulations for hobbyist flying (covers professional engineering only)

## Industry Context for 2026

The UAV software engineering market in 2026 is characterized by three concurrent trends:

**1. Regulatory-driven demand**: BVLOS certification requirements in India (DGCA), Europe (EASA SORA), and the US (FAA BVLOS waiver) are creating structured demand for engineers who can author safety cases, analyze flight logs at scale, and design operationally reliable systems. This is the fastest-growing demand segment.

**2. eVTOL investment wave**: The 2024–2027 eVTOL commercialization phase (Joby, Archer, Beta, Wisk) is driving demand for GNC engineers with fixed-wing/VTOL simulation experience (JSBSim), embedded certification-track experience, and safety engineering backgrounds. These roles are the highest-compensated in the UAV market.

**3. Fleet-scale autonomy**: Wing, Zipline, Amazon Prime Air, and Manna Drone Delivery are scaling to thousands of concurrent flights per day. The engineering challenges at fleet scale — coordination, reliability, log anomaly detection, UTM integration — require a new tier of fleet software engineering competence that does not yet have a standardized training path. This curriculum's Advanced tier addresses this directly.

**India-specific context**: The PLI scheme for domestic drone manufacturing, DGCA's BVLOS Type Certification pathway, and defense UAV procurement programs (TAPAS, DRDO ARCHER) are creating demand for Advanced-tier UAV engineers at Indian OEMs and defense contractors. Engineers who combine open-source flight stack depth with DGCA regulatory awareness are a rare and valuable profile in this market.

## How to Navigate This Guide Efficiently

**If you are coming from a software engineering background** (web, mobile, systems): Start at Foundation/02 (Engineering Workflow), then Foundation/03 (Flight Stack Fundamentals), then proceed through Core UAV in order. You already have the programming fundamentals; your gaps are flight-stack architecture and UAV-specific tooling.

**If you are coming from an aerospace/mechanical engineering background**: Start at Foundation/01 (Curriculum Overview), skim Foundation/02 (you may already know Git and C++), focus on Foundation/03 and Foundation/04 (flight stack and simulation), then prioritize Core/01 (PX4 architecture) and Core/04 (dynamics and EKF) deeply before proceeding.

**If you want embedded firmware roles**: After Foundation, go directly to Core/01 (flight stack architecture) and then Advanced/01 (NuttX/RTOS). Return to the other Core sections after completing the embedded path.

**If you want GNC/eVTOL roles**: Core/04 (dynamics and EKF) + Advanced/02 (JSBSim and FDM) is your priority path; build up from Foundation/03 if flight stack familiarity is weak.

**If you want autonomy/perception roles**: Core/02 (ROS 2) + Core/05 (perception and landing) is your priority; Advanced/02 and Advanced/03 extend this.

## Estimated Capability Gates

Each gate represents a verifiable competency milestone, not a calendar target:

**Gate 1 — Toolchain**: Can clone and build PX4 from source; can run a SITL mission in Gazebo; can open the resulting ULog in Flight Review and identify the flight mode transitions and EKF innovation plot.

**Gate 2 — Protocol**: Can write a pymavlink script that arms a vehicle, uploads a 4-waypoint mission, monitors battery telemetry, and saves a log file; can explain the MAVLink message sequence for mission upload.

**Gate 3 — Integration**: Can set up PX4 SITL + Micro-XRCE-DDS + a ROS 2 offboard node; can explain the coordinate frame transform between PX4 NED and ROS 2 ENU; can describe what happens when the offboard node crashes.

**Gate 4 — Diagnosis**: Given a PX4 ULog file with a flight anomaly (GPS denial, high vibration, EKF switch), can identify the anomaly, explain its cause, and propose a mitigation — without looking anything up.

**Gate 5 — Production discipline**: Can present a SITL project with: a safety assumptions document, a metrics report auto-generated from the log, at least 2 failure injection test results, and a passing CI badge — and defend every design decision under examination.

## Further Reading and Community

- **Dronecode Foundation** (dronecode.org) — the non-profit that governs PX4 and MAVSDK development; community structure overview
- **PX4 discuss** (discuss.px4.io) — primary community forum; search before posting; `dev` tag for engineering questions
- **ArduPilot discuss** (discuss.ardupilot.org) — ArduPilot community; technical depth comparable to PX4 forum
- **ROS Discourse** (discourse.ros.org) — ROS 2 community; `nav2` and `perception` categories most relevant to UAV work
- **Hackster.io UAV** — project showcases; useful for seeing what beginner and intermediate projects look like in practice
- **LinkedIn UAV Engineering groups** — industry news and job postings; connecting with engineers at target companies before applying is a high-ROI activity
