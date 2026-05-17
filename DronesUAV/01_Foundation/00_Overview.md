# Foundation

## Overview

The Foundation section exists to make the rest of the UAV curriculum possible. It teaches the tooling, flight-stack, and simulation basics that prevent later confusion: Linux workflow, Git discipline, Python and C++, basic aerodynamics, PX4 or ArduPilot concepts, MAVLink, QGroundControl, and first SITL loops.

A common mistake in drone self-study is jumping straight into flashy autonomy demos. That produces surface familiarity without durable skill. This section starts lower on purpose. By the end of Foundation, you should be able to set up a development environment, explain the role of the autopilot and companion computer, launch simulation, inspect telemetry, and move between Python and C++ comfortably.

## What This Section Covers

### 1. Start Here
- A map of the curriculum and the order in which to study it.
- The role of open-source flight stacks, simulation, and portfolio projects.
- A realistic expectation for how to study UAV software independently.

### 2. Engineering Workflow
- Linux command line, files, processes, Git workflow, C++, Python, and basic aerodynamics intuition.

### 3. Flight Stack Fundamentals
- PX4, ArduPilot, MAVLink, QGroundControl, and how the major pieces fit together.

### 4. Simulation and Testing
- Gazebo, JSBSim, SITL, logs, and sim-first development habits.

## Suggested Study Order

1. Curriculum Overview
2. Learning Roadmap
3. Linux, Git, C++, Python, and Aerodynamics Foundations
4. PX4, ArduPilot, MAVLink, and QGroundControl Foundations
5. Gazebo, JSBSim, SITL, and Log-Driven Development

## Milestones

You are ready to leave Foundation when you can do all of the following without heavy hand-holding:

- set up a Linux-based UAV development environment
- explain the difference between an autopilot, a companion computer, and a ground control station
- run one SITL workflow
- inspect messages, parameters, and logs
- write one small Python or C++ tool around UAV telemetry or simulation

## Time Guidance

A realistic range is `6-8 weeks` at `8-12 hours per week`.

## Next Step

Start with [Curriculum Overview](01_Start_Here/01_Curriculum_Overview.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

The Foundation tier is the literal first week of onboarding at every professional UAV engineering team. New engineers at companies like ideaForge, Garuda Aerospace, Skydio, and Shield AI spend their first days setting up toolchains, confirming they can build autopilot firmware, running SITL, and inspecting MAVLink telemetry through QGroundControl or pymavlink scripts. The purpose is not instant productivity — it is confirming that the engineer understands which layer owns which behavior.

Foundation competence manifests in three concrete ways. First, the engineer can reproduce the development environment from scratch in under an hour and explain every tool in the chain. Second, they can run a PX4 or ArduPilot SITL session, upload a waypoint mission, and read the resulting `.ulg` or `.bin` log without hand-holding. Third, they can explain why a given vehicle behavior — uncommanded pitch, sensor rejection, arming refusal — is plausible or suspicious based on lift, drag, and actuator authority physics.

Without this layer, engineers become bottlenecks who depend on senior teammates to diagnose what should be routine issues. Engineers who skip Foundation and jump to autonomy or perception work typically hit a wall six months in when the first real telemetry anomaly appears and they have no diagnostic vocabulary for it.

### Industry Tool Stack

- **Ubuntu 22.04 / 24.04** — primary development OS across PX4 and ArduPilot toolchains; WSL2 on Windows is supported but adds friction
- **Git + GitHub / GitLab** — version control for firmware forks, CI integration, parameter history, and reproducible build configs
- **PX4 Autopilot** — dominant open-source autopilot for research and startup-grade UAV systems; strong ROS 2 adjacency
- **ArduPilot** — broader vehicle coverage (plane, copter, rover, boat); favored in inspection, agriculture, and field-heavy deployments
- **MAVLink + pymavlink** — message introspection, mission scripting, and telemetry tooling around the autopilot
- **QGroundControl** — parameter management, mission planning, and operator-facing telemetry during development and field testing
- **Gazebo / Ignition Fortress** — 3D simulation integrated with PX4 SITL; used for multirotor and fixed-wing runs
- **pyulog / FlightPlot** — parse and visualize PX4 `.ulg` log files; `ardupilot/Tools/autotest/pysim` for ArduPilot log work

### Step-by-Step Applied Workflow

1. **Bootstrap the OS**: install Ubuntu 22.04, configure terminal, install `git`, `cmake`, `gcc-arm-none-eabi`, Python 3 with `pip` and `venv` support.
2. **Clone and build the flight stack**: run `make px4_sitl gazebo-classic` (PX4) or `./waf configure --board sitl && ./waf sim_vehicle` (ArduPilot) to validate the toolchain end-to-end.
3. **Connect QGroundControl**: launch QGC, confirm it detects the SITL vehicle, inspect parameter list and telemetry readouts.
4. **Inspect a MAVLink message stream**: use `pymavlink` to subscribe to `HEARTBEAT`, `ATTITUDE`, and `GLOBAL_POSITION_INT` messages and print them in a Python script.
5. **Upload and run a waypoint mission**: build a 4-waypoint square mission in QGC, upload it to SITL, arm, auto-launch, and observe the vehicle complete it.
6. **Capture and read a log**: locate the `.ulg` or `.bin` log from the SITL session, load it in `pyulog` or FlightPlot, extract commanded vs. actual attitude trace.
7. **Document the build-to-log cycle**: write a README another developer can follow to reproduce the entire workflow on a clean machine in under 30 minutes.

### AI Integration

AI plays a minimal but legitimate role at the Foundation tier. The Foundation is about understanding deterministic, physics-constrained systems — autopilot modes, message semantics, sensor chains, and log formats — before adding probabilistic reasoning. Rushing AI in at this stage masks the gaps it is supposed to fill.

That said, adjacent AI applications exist here. LLM assistants can speed up toolchain setup by suggesting correct package versions, diagnosing build errors, and explaining unfamiliar compiler flags. For log analysis, tools like the open-source PX4 flight review platform (review.px4.io) use statistical baselines to flag anomalous IMU signatures or vibration levels. Copilot-style assistants can generate pymavlink boilerplate quickly. These are additive tools, not substitutes for understanding what you are looking at.

The key discipline to build at Foundation: before you trust an AI suggestion about flight behavior, you must be able to sanity-check it manually. If you cannot read a telemetry plot and say whether the attitude response looks physically plausible, you are not ready to let AI tell you whether a flight was safe.

### Case Studies

**ideaForge (India)**: India's largest domestically produced drone manufacturer operates SWITCH UAV systems for defense surveillance, precision agriculture, and infrastructure surveys. Their engineering teams work with ArduPilot-based stacks and expect all hires to arrive with strong telemetry discipline, log analysis familiarity, and field integration skills. Foundation competence is the hiring baseline, not a differentiator.

**Wing (Alphabet)**: Wing operates commercial last-mile delivery drones in Australia, the US, and Ireland. Their internal flight software is proprietary, but their engineering job postings consistently list Linux workflow, flight-stack debugging, and log analysis as baseline requirements even for junior Flight Software Engineer roles. They do not train this layer — they screen for it.

**MAVLab, TU Delft (Netherlands)**: The Micro Air Vehicle Laboratory at TU Delft runs one of the most active open UAV research groups globally. Their Paparazzi UAV platform and swarming micro-drone research demonstrate that Foundation-tier habits — simulation, log-driven development, controlled iteration — are the same at research scale as at commercial scale. Their public repos and papers show this discipline explicitly.

### Failure Modes & Safety

Foundation-tier failures are amplified later in the stack because they are structural, not cosmetic.

**Environment fragility**: a development setup that works on one machine but cannot be reproduced. Every new team member or CI runner becomes a debugging session. Configuration assumptions — Python versions, library paths, compiler flags — become undocumented load-bearing dependencies that break during the worst possible moments (pre-flight, field deployment).

**Mode and failsafe ignorance**: running SITL repeatedly without understanding what each flight mode actually guarantees. An engineer who has run SITL hundreds of times but cannot explain what happens when a GPS fix is lost in Position mode, when a geofence is breached, or when the RC link drops is building future field-safety risk. Failsafe configuration — LAND vs. RTL vs. hold vs. disarm — must be understood, not assumed.

**Log blindness**: treating the flight log as optional post-analysis rather than the primary evidence of what the system did. Most serious UAV incidents during development are recoverable if the log exists and is read promptly. Without the log, teams argue from memory. Developing the habit of always reading the log from the very first SITL run — and saving it — is the highest-leverage safety behavior at Foundation tier.

**Parameter version-blindness**: making autopilot parameter changes without tracking which version was used and what changed. This leads to situations where a vehicle behaves differently across sessions with no clear audit trail of what was modified.

### Business & Commercial Layer

The Foundation tier's commercial relevance lies in how it positions an engineer for every downstream UAV market segment.

In **inspection** (power lines, offshore oil platforms, cell tower surveys), teams need engineers who can rapidly diagnose field telemetry issues under time pressure — there is no lab fallback when a crew is on site 40 km from the nearest office. In **delivery** (Zipline, Wing, Swiggy's delivery drone programs in India), flight reliability depends on deep log reading and controlled iteration. In **defense** (Shield AI's V-BAT, ideaForge's SWITCH), software must be deterministic, auditable, and testable — exactly what strong Foundation habits produce.

India's drone market specifically is growing fast: DGCA's Digital Sky platform, the PLI scheme for domestic UAV manufacturing, and expanding BVLOS corridors through DGCA Type Certification mean the job market for Foundation-literate engineers is growing in Bengaluru, Pune, Hyderabad, and Nashik. Starting with Foundation-tier depth rather than surface feature knowledge is the fastest path to qualifying for these roles.

### Hiring Signal

**Job titles that directly hire for Foundation-level UAV skills:**
- **Flight Software Engineer (Associate / Entry)** — Wing, Zipline, Joby Aviation, Shield AI; expected to set up toolchains, run SITL, and read logs independently from day one
- **UAV Integration Engineer** — enterprise inspection vendors (Skydio for enterprise, Percepto, Flyability); expected to configure autopilots, script missions, and trace telemetry
- **Autopilot Firmware Engineer (Junior)** — companies building on PX4 or ArduPilot; requires Linux fluency, build system understanding, and log analysis capability
- **Systems Test Engineer (UAV)** — test organizations and UAV OEMs; Foundation skills are the explicit prerequisite for writing and running SITL-based test cases

**Specific interview screens for Foundation competence:**
1. "Walk me through setting up a PX4 SITL environment from scratch on Ubuntu — what do you install, in what order, and how do you confirm it works before doing anything else?"
2. "Open this `.ulg` log file. Tell me what flight mode the vehicle was in during the second waypoint leg and whether the attitude tracking looks nominal."
3. "What happens to a PX4 vehicle configured with RTL failsafe when it loses GPS while in Position Control mode? Walk me through the failsafe trigger logic step by step."
4. "Show me a pymavlink script that subscribes to `GLOBAL_POSITION_INT` and prints position every 2 seconds. Explain each line of the connection and subscribe pattern."
5. "I have a vehicle that refuses to arm. List five different possible root causes and what parameter or log field you would inspect first to diagnose each one."

### Portfolio Projects

**Beginner: `uav-foundation-bootstrap`**
- Deliverables: documented build environment setup (Ubuntu + PX4 or ArduPilot SITL), one SITL mission run with captured log, one pymavlink script that subscribes and prints three message types in real time
- Suggested repo tree: `README.md`, `setup/install.sh`, `missions/square_4wp.plan`, `scripts/telemetry_listen.py`, `logs/run_001.ulg`, `notes/flight_review.md`
- Acceptance criteria: (1) another developer can reproduce the SITL run in under 30 minutes using only the README; (2) the log is present and flight review note identifies takeoff, waypoint sequence, and landing phases; (3) the pymavlink script runs without errors and prints live telemetry from SITL

**Intermediate: `flight-stack-audit-toolkit`**
- Deliverables: Python CLI tool that loads a PX4 `.ulg` log, extracts attitude error and mode transitions, outputs a summary report with labeled plots; parameterizable via CLI args; tested on at least two different log files
- Suggested repo tree: `README.md`, `src/log_audit.py`, `tests/`, `data/sample_logs/`, `outputs/report_001.md`, `requirements.txt`
- Acceptance criteria: (1) tool runs on any well-formed `.ulg` without modification; (2) attitude error plot is readable and axis-labeled; (3) mode transitions are listed with timestamps and flight-phase context

**Advanced: `sitl-ci-harness`**
- Deliverables: CI-ready SITL test harness that launches PX4 SITL, uploads a waypoint mission, runs it to completion, captures the log, and asserts that 3D position error stays below a defined threshold throughout; documented with architecture diagram
- Suggested repo tree: `README.md`, `.github/workflows/sitl_test.yml`, `harness/run_mission.py`, `harness/assertions.py`, `missions/`, `logs/`, `docs/architecture.md`
- Acceptance criteria: (1) CI workflow passes on a clean GitHub Actions Ubuntu runner; (2) a threshold violation causes a non-zero exit code and a readable failure message; (3) architecture diagram explains the SITL UDP communication path and assertion hook

### Future Trends

- **2026**: Open-source flight stacks (PX4, ArduPilot) continue as the dominant onramp for commercial and research UAV software. BVLOS corridor expansion in India (DGCA Type-Certification paths), US (FAA BVLOS ARC recommendations), and EU (EASA U-Space) increases demand for engineers who can demonstrate systematic telemetry and log discipline rather than just piloting capability.
- **2030**: Simulation-based qualification for UAV operations becomes a regulatory expectation rather than a startup differentiator. Teams with rigorous SITL and log disciplines satisfy certification evidence requirements faster. Foundation skills become a gating requirement in regulated markets.
- **2035**: The Foundation stack — Linux, Git, MAVLink, SITL, log analysis — remains recognizable but is increasingly embedded in containerized (Docker, Dev Containers) and cloud-based (AWS RoboMaker, simulation-as-a-service) environments. Engineers who understand the underlying communication and data layers adapt more easily than those who only know IDE-level tooling.
- **2045**: As eVTOL certification processes mature and urban air mobility expands, the demand for engineers who can reason rigorously about flight system behavior from first principles increases rather than decreases. Foundation discipline is a career-length asset.

### Interview Questions

1. **What is the difference between PX4 and ArduPilot, and when would you choose one over the other?**
   *Answer*: PX4 has stronger ROS 2 and research-startup adjacency, cleaner module architecture (uORB pub/sub), and active Dronecode Foundation support. ArduPilot has broader vehicle coverage (plane, copter, rover, submarine), a larger operational user community, and more mature field-integration patterns. Choose PX4 for autonomy-heavy research and companion-compute work; choose ArduPilot for broader platform coverage and operational field integration with less ROS dependency.

2. **Describe what happens between the moment a developer presses "Takeoff" in QGroundControl and the moment the rotors spin up in SITL.**
   *Answer*: QGC sends a `MAV_CMD_NAV_TAKEOFF` command as a MAVLink `COMMAND_LONG` message over UDP to the SITL process. The autopilot verifies arming conditions (battery simulation, sensor health, GPS fix). If checks pass, it arms, transitions the flight mode to Takeoff, ramps motor outputs via the mixer, and begins climbing to the configured takeoff altitude. The SITL physics engine simulates the resulting forces and feeds back attitude and position.

3. **How would you confirm that your SITL environment is using the same PX4 version as the hardware you plan to deploy?**
   *Answer*: `git log --oneline` on the PX4-Autopilot repo gives the exact commit. Cross-reference against the firmware version visible in QGC's vehicle summary or the `autopilot_version` field in the `AUTOPILOT_VERSION` MAVLink message. On hardware, the bootloader version and `ver all` in the PX4 NuttX console confirm the tag.

4. **What does a `.ulg` log tell you that live MAVLink telemetry does not?**
   *Answer*: The log provides a complete, time-indexed record of every internal state — actuator outputs, estimator states, controller setpoints, mode transitions — at full internal sample rates (often 50–250 Hz), not at the reduced telemetry streaming rate (often 1–10 Hz). This enables post-flight root-cause analysis of anomalies that were too fast to see in the live stream.

5. **Name three things that can prevent a PX4 vehicle from arming and how you would diagnose each.**
   *Answer*: (1) Failed prearm check — inspect `STATUSTEXT` messages in QGC or the MAVLink inspector for the specific check name (e.g., `Preflight Fail: Gyros inconsistent`); check `PREFLIGHT_STATUS`. (2) Safety switch not pressed — look at `safety_button_available` parameter and confirm the hardware switch is wired and pressed. (3) RC calibration out of range — inspect `RC_MAP_*` parameters and verify channel min/max in QGC Radio setup cover the full stick travel.

### Further Depth

- **PX4 Developer Guide** (docs.px4.io/main/en/) — architecture, SITL setup, uORB messaging, and build system; the primary reference for this curriculum
- **ArduPilot Developer Wiki** (ardupilot.org/dev/) — equivalent for ArduPilot; covers SITL, parameter system, and vehicle-specific firmware
- **MAVLink Developer Guide** (mavlink.io/en/) — message definitions, protocol spec, and dialect documentation
- **QGroundControl Developer Guide** (docs.qgroundcontrol.com) — plugin architecture, mission planning API, telemetry integration
- **"Small Unmanned Aircraft: Theory and Practice"** — Randal Beard and Timothy McLain (Princeton University Press); rigorous treatment of UAV dynamics, autopilot design, and estimation; the closest thing to a canonical textbook for UAV software engineers
- **pyulog** (github.com/PX4/pyulog) — Python library for parsing PX4 ULog files; foundational for building log analysis tools
