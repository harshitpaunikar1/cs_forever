# Gazebo JSBSim SITL and Log-Driven Development

## Overview

Simulation is how serious UAV teams learn faster and break less hardware. This page covers the practical role of Gazebo, JSBSim, SITL, and logs in a development workflow.

## Why This Topic Matters

Students who only read theory or only fly hardware move too slowly. Simulation gives you repetition, safer failure, and better debugging leverage.

## Core Concepts

### Gazebo
- strong for robotics-style simulation and ROS 2 integration
- officially maintained releases still matter in `2026`

### JSBSim
- strong for flight-dynamics modeling, especially fixed-wing and VTOL reasoning

### SITL
- essential for autopilot development, parameter testing, and mission rehearsal

### Logs
- flight software work improves when every experiment leaves evidence

## Decision Framework

```text
robotics-style integration -> Gazebo
flight-dynamics depth -> JSBSim
autopilot development -> SITL
all of the above -> logs
```

## Hands-On Example / Mini Project

Build a mission rehearsal stack with:

- one SITL autopilot
- one simulator
- one ROS 2 or Python control tool
- one ground station
- one log review note

## Best Practices

- simulate before field testing
- save parameters with each run
- keep logs and screenshots tied to experiments
- document exact versions

## Common Pitfalls

- running simulation without recording evidence
- mixing incompatible versions casually
- treating “it armed once” as validation

## Next Step

Move to [Core UAV](../../02_Core_UAV/00_Overview.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Simulation is not a demo medium — it is a controlled environment for discovering what your system actually does before it costs hardware or safety margins. Every serious UAV team has a sim-first discipline. At Zipline, every flight software change runs through thousands of SITL scenarios before reaching hardware. At Auterion, PX4's CI pipeline runs automated SITL tests on every commit. At MAVLab TU Delft, researchers validate swarm behaviors in Gazebo for weeks before a single real flight.

The practical discipline is: each simulator in the stack serves a different purpose. **Gazebo** provides physics-backed 3D simulation with sensor models (IMU, GPS, camera, rangefinder) and tight ROS 2 integration — use it when you need the robot to exist in a simulated environment with realistic sensor noise and physics. **JSBSim** provides flight-dynamics fidelity — use it when you need the aerodynamics to be accurate for fixed-wing, VTOL, or dynamics-heavy multirotor work. **SITL** is the autopilot running as a software process — use it whenever you need to test autopilot behavior (modes, failsafes, parameters, mission execution) without involving hardware. These three are complementary, not substitutes: a rigorous simulation stack uses all three together.

The log discipline is what turns simulation from demos into engineering evidence. Every run produces a log. Every parameter change is versioned. Every comparison is made between two runs — not between memory and the current run.

### Industry Tool Stack

- **PX4 SITL** — `make px4_sitl gazebo-classic` or `make px4_sitl jmavsim`; runs PX4 firmware as a Linux process; connects to Gazebo or jMAVSim for physics
- **ArduPilot SITL** — `sim_vehicle.py -v ArduCopter -f gazebo-iris`; supports Gazebo, JSBSim, X-Plane, and built-in FlightGear models
- **Gazebo Classic (Gazebo 11)** — used with PX4 and ROS 2; includes the `px4_gazebo` plugin set for multirotor and fixed-wing models
- **Gazebo Ignition / Fortress / Harmonic** — newer release series; integrated with ROS 2 via `ros_gz_bridge`; PX4 v1.14+ supports it natively
- **JSBSim** — flight-dynamics model (FDM) engine with Python and C++ APIs; used for high-fidelity fixed-wing and VTOL simulation
- **MAVProxy** — CLI GCS and MAVLink router; useful for scripted mission testing, message rate monitoring, and multi-link routing
- **pyulog** — PX4 ULog file parser; generates CSV, matplotlib plots, and pandas DataFrames from `.ulg` files
- **ArduPilot DataFlash Log Viewer / Mission Planner** — ArduPilot post-flight log analysis; also supports `.bin` log parsing in Python via `pymavlink.DFReader`

### Step-by-Step Applied Workflow

1. **Pin your versions before any run**: `git log --oneline` for the autopilot commit; note the Gazebo or JSBSim release; save the parameter file. A run without version metadata is not reproducible.
2. **Launch SITL with the target simulator**: `make px4_sitl gazebo-classic` for PX4+Gazebo; wait for the SITL process to print the vehicle's HEARTBEAT on UDP 14550.
3. **Connect QGC or MAVProxy**: confirm vehicle readiness, arm state, and GPS fix simulation. Upload the test mission or script the test via MAVSDK.
4. **Run the scenario once and save the full log**: `.ulg` (PX4) or `.bin` (ArduPilot); also save a QGC telemetry screenshot at each phase transition.
5. **Change exactly one variable**: a single controller parameter, a mission waypoint altitude, a simulated wind speed, or one line of companion code. Document the change in a `CHANGES.md` in the run folder.
6. **Run the scenario again and capture the second log**: name runs systematically (`run_001_baseline`, `run_002_pitch_p_plus20pct`).
7. **Compare the two logs**: load both in `pyulog` or pandas, overlay attitude error traces, position error traces, or motor output. Quantify the difference — do not describe it from memory.
8. **Write a one-paragraph engineering note**: what changed, what got better, what got worse, what questions remain for hardware testing.

### AI Integration

AI is specifically useful at two points in the simulation workflow — test scenario generation and log comparison — without replacing the core evidence-capture discipline.

**Test scenario generation**: LLM-based tools can help generate Gazebo world files, MAVSDK mission scripts, or ArduPilot SITL parameter configurations for specific test scenarios (GPS denied at 45 degrees heading, wind gust at 6 m/s from NW, battery simulation dropping to 15% at waypoint 3). This is additive — the human still has to verify that the generated scenario is physically meaningful and the pass/fail criteria make sense.

**Log comparison and anomaly flagging**: tools like PX4 Flight Review (review.px4.io) use statistical models to flag runs where vibration levels, EKF innovation ratios, or motor balance exceed typical envelopes. More advanced ML-based log analysis tools — being built by several aerospace companies — cluster flight logs by failure mode and suggest probable root causes. The human still makes the final diagnostic judgment.

What AI cannot replace: the discipline of running a controlled experiment (one change per run), the engineering judgment of what to measure and what counts as success, and the verification that a simulation result generalizes to hardware.

### Case Studies

**PX4 Continuous Integration Pipeline**: PX4's open-source CI pipeline (visible on GitHub Actions at github.com/PX4/PX4-Autopilot/actions) runs SITL-based tests on every pull request. Tests include mission execution, mode transition verification, and EKF health checks — all in Gazebo. This is the industry standard for autopilot development: no firmware change ships to users without SITL evidence. Contributing to PX4 means understanding and extending this test infrastructure.

**Zipline's Simulation-First Culture**: Zipline's fixed-wing delivery drones (which have flown millions of autonomous delivery miles in Rwanda, Ghana, and the US) use a simulation-first development culture where every flight software change is tested against thousands of simulated scenarios before reaching hardware. Their approach — described in engineering blog posts — includes Monte Carlo runs over wind and sensor-noise distributions, not just nominal scenarios. This is the professional extension of the log-driven development discipline described on this page.

**MAVLab TU Delft — Swarm Simulation**: TU Delft's MAVLab validates swarm algorithms (their Crazyflie-based micro-drone work and larger swarming platforms) in simulation for weeks before field deployment. Their Paparazzi UAV simulator and Gazebo-based multi-agent setups demonstrate how simulation scales from single-vehicle testing to fleet-level behavioral validation. Their research papers consistently cite simulation hours as the basis for physical safety confidence.

### Failure Modes & Safety

**Unversioned simulation runs**: running SITL without recording which firmware commit, which parameter file, which Gazebo release, and which world file was used. When a behavior changes between runs, there is no way to identify what caused it. The fix: treat every SITL session the same way you would a flight test — log and version everything before pressing play.

**One-run validation**: treating a single successful SITL run as evidence that a behavior is correct. One run catches obvious failures. It does not catch failures that occur 15% of the time in slightly different initial conditions, or failures triggered by a specific sequence of events that your one run happened not to trigger. Minimum validation is 5–10 runs with the same configuration; safety-critical behaviors need Monte Carlo coverage.

**Sim-to-real assumption mismatch**: assuming that behaviors validated in Gazebo or JSBSim will transfer to hardware without modification. Gazebo's aerodynamic models are simplified; real motors have latency and nonlinearity not captured in the default sim; real GPS has noise patterns different from the Gaussian simulation model. Good sim discipline includes explicit documentation of which behaviors have been validated in sim and which assumptions are yet to be tested on hardware.

**Ignoring EKF innovations in logs**: running simulations without ever checking the EKF innovation magnitudes in the log. High innovations indicate the estimator is rejecting sensor measurements — which may be a sign of a model mismatch or an incorrectly configured sensor simulation. Checking EKF health in every SITL log is a non-negotiable habit for engineers doing any controls or estimation work.

**Treating Gazebo Classic and Gazebo Ignition as interchangeable**: they share a name and general concept but have different APIs, plugin systems, and ROS bridge packages. PX4 support for each version is specific. Mixing tutorials written for different Gazebo versions is a common source of subtle physics differences that invalidate comparison between runs.

### Business & Commercial Layer

Simulation competence is commercially valuable in two distinct ways: as a development accelerator and as a regulatory compliance tool.

As a **development accelerator**: UAV hardware costs anywhere from $500 for a hobbyist frame to $50,000+ for a defense-grade platform. Each hardware crash is expensive in money, schedule, and sometimes legal risk. Teams that can resolve 80% of bugs in simulation before hardware testing spend dramatically less on hardware loss and have faster iteration cycles. This is a direct business cost argument for hiring engineers with simulation discipline.

As a **regulatory compliance evidence**: DGCA in India, EASA in Europe, and FAA in the US are moving toward accepting simulation evidence as part of certification packages for certain airspace authorizations (BVLOS, beyond-visual, urban operations). An engineering team that has maintained systematic SITL evidence — versioned runs, pass/fail criteria, anomaly logs — is positioned to produce that evidence on demand. Teams that have only unlogged flight hours are not. This is a hiring argument for engineers who treat simulation as engineering infrastructure, not as a convenience.

### Hiring Signal

**Job titles where SITL and log-driven development are primary hiring screens:**
- **Systems Test Engineer (UAV)** — at Wing, Zipline, Joby, Shield AI, and UAV OEMs; primary job function is designing SITL test scenarios, running them in CI, and analyzing logs to identify regressions
- **Flight Software Engineer** — at any serious UAV company; SITL is the expected daily development environment; log analysis is a core diagnostic skill
- **Autopilot Firmware Engineer (PX4)** — contributes to PX4's CI-integrated SITL tests; expected to write new test scenarios for new features and run them before submitting PRs
- **UAV Integration Engineer** — field-integration teams use SITL for pre-deployment mission rehearsal and for reproducing field issues in a controlled environment

**Specific interview screens for this topic:**
1. "Describe how you would set up a SITL test that validates a new waypoint-following algorithm. What is the pass/fail criterion and how do you measure it from the log?"
2. "A PX4 log from a SITL run shows the EKF switching from GPS-aided to GPS-denied mode at the 45-second mark. The mission continues successfully. What does this mean and what would you investigate?"
3. "What is the difference between Gazebo Classic and JSBSim as simulation backends for PX4 SITL, and when would you use each?"
4. "You run the same mission in SITL twice, 10 minutes apart, with no parameter changes. The position error is 0.8 m in run 1 and 1.9 m in run 2. How do you diagnose this?"
5. "Write pseudocode (or outline the structure) for a Python script that launches PX4 SITL, waits for the vehicle to arm, executes a mission, captures the log, and returns a pass/fail result based on maximum altitude deviation from the planned path."

### Portfolio Projects

**Beginner: `sitl-baseline-experiment`**
- Deliverables: 3 SITL runs of the same waypoint mission with different `MC_PITCH_P` values, logged and named systematically; Python script loading all three `.ulg` files and overlaying attitude error; written comparison note
- Suggested repo tree: `README.md`, `runs/run_001_baseline/`, `runs/run_002_pitch_p_low/`, `runs/run_003_pitch_p_high/`, `analysis/compare_runs.py`, `analysis/plots/`, `notes/comparison.md`
- Acceptance criteria: (1) all three runs are reproducible from the README; (2) overlay plot clearly shows the effect of the parameter change; (3) comparison note quantifies the difference (not just describes it)

**Intermediate: `sitl-ci-test-suite`**
- Deliverables: a SITL test suite with at least 5 different scenarios (normal mission, GPS denied recovery, battery failsafe trigger, geofence breach, wind disturbance); each scenario produces a pass/fail result from log analysis; runs headlessly
- Suggested repo tree: `README.md`, `scenarios/`, `runner/run_suite.py`, `assertions/`, `logs/`, `reports/`
- Acceptance criteria: (1) suite runs all 5 scenarios in under 15 minutes; (2) each scenario produces a named log and a pass/fail output; (3) at least one failure scenario produces a deliberate fail result correctly

**Advanced: `sim-to-real-transfer-harness`**
- Deliverables: documented experiment comparing simulation and hardware flight for the same mission, with quantitative comparison of attitude error and position tracking; explicit sim-to-real assumption list; protocol for what gets re-tested on hardware after sim validation
- Suggested repo tree: `README.md`, `sim_runs/`, `hardware_runs/`, `analysis/compare_sim_real.py`, `docs/assumptions.md`, `docs/transfer_protocol.md`
- Acceptance criteria: (1) comparison plot shows both sim and hardware traces; (2) assumptions document lists at least 5 sim-to-real gaps; (3) transfer protocol specifies which failures in hardware trigger a return to sim investigation

### Future Trends

- **2026**: PX4's SITL pipeline moves further toward Gazebo Ignition (Fortress / Harmonic), with deprecation of Gazebo Classic imminent. Engineers who understand the Ignition plugin system and `ros_gz_bridge` will be ahead of the migration.
- **2030**: Simulation-as-a-service platforms (AWS RoboMaker for UAVs, NVIDIA Omniverse Isaac Sim aerial, or similar) may make high-fidelity parallel SITL runs accessible to smaller teams. Monte Carlo simulation becomes a standard pre-flight practice even for smaller operators.
- **2035**: Regulatory bodies begin accepting formally documented SITL evidence as part of airworthiness submissions for certain UAV classes. Teams with systematic simulation archives are positioned for faster certification timelines.
- **2045**: Physics simulation fidelity approaches real-world accuracy for most flight regimes, making sim-to-real transfer dramatically easier. The log-driven development discipline — which is software methodology, not a simulator feature — remains equally applicable.

### Interview Questions

1. **What is the difference between SITL, HIL (Hardware-In-the-Loop), and real flight for the purposes of software testing?**
   *Answer*: SITL runs the entire flight software stack as a software process with simulated sensors and physics — fastest and cheapest. HIL runs the actual flight controller hardware with simulated sensor inputs injected via hardware interfaces — tests the full hardware layer including I/O timing and interrupt behavior, but slower and requires hardware. Real flight tests the full system including real aerodynamics, real sensor noise, and real environmental conditions — most expensive and highest risk, but necessary for final validation.

2. **Why should you pin your Gazebo version, PX4 commit, and parameter file before running a SITL test, even informally?**
   *Answer*: Because simulation behavior changes with every Gazebo physics engine version, every PX4 commit, and every parameter value. If you change more than one thing between runs, you cannot attribute a behavioral change to a specific cause. Pinning creates a reproducible baseline that makes every subsequent run comparable.

3. **What does a high EKF velocity innovation ratio in a SITL log indicate, and what would you investigate?**
   *Answer*: High EKF velocity innovations mean the estimator is seeing large discrepancies between predicted and measured velocity — suggesting either sensor noise that is higher than the model assumes, a GPS simulation model that does not match the real GPS noise characteristics, or an IMU model mismatch. In SITL, first check if the simulated GPS noise parameters in Gazebo match real hardware specs. In hardware, check for vibration, GPS antenna placement, and multipath.

4. **Describe a situation where JSBSim would be more appropriate than Gazebo for PX4 SITL testing.**
   *Answer*: JSBSim is more appropriate when the test is specifically about aerodynamic behavior — e.g., testing a fixed-wing aircraft's behavior in a crosswind landing, validating VTOL transition dynamics at different airspeeds, or testing pitch-stiffness response at different trim conditions. JSBSim's flight-dynamics models are more physically rigorous than Gazebo's default aerodynamic plugins. Gazebo is more appropriate when the test requires a 3D environment with obstacles, terrain, or sensor occlusion.

5. **You want to test a geofence violation scenario in SITL. Walk through how you would set it up and what you would assert in the log.**
   *Answer*: Set up a QGC mission with a geofence boundary that the mission plan would cross if the fence were not enforced. Enable geofence failsafe in PX4 parameters (`GF_ACTION = 1` for RTL on breach). Run the mission in SITL and let it approach the fence boundary. In the log, assert: (1) the `vehicle_land_detected` topic does not show a crash; (2) a mode transition to RTL is visible in the `vehicle_status` topic at the expected geofence boundary position; (3) the vehicle position at the fence trigger is within the expected geofence radius (±10 m given GPS accuracy simulation).

### Further Depth

- **PX4 SITL Documentation** (docs.px4.io/main/en/simulation/) — covers all SITL backends (Gazebo, jMAVSim, JSBSim, X-Plane), setup, and test automation
- **ArduPilot SITL Documentation** (ardupilot.org/dev/docs/sitl-simulator-software-in-the-loop.html) — ArduPilot's equivalent guide; includes sim_vehicle.py documentation
- **Gazebo Documentation** (gazebosim.org/docs) — covers Ignition/Harmonic series; plugin development guide relevant for adding custom sensor models
- **JSBSim Reference Manual** (jsbsim.sourceforge.net/JSBSimReferenceManual.pdf) — the authoritative FDM reference; covers aircraft configuration files and FDM architecture
- **pyulog** (github.com/PX4/pyulog) — the primary tool for reading and plotting PX4 `.ulg` logs programmatically
- **PX4 Flight Review** (review.px4.io) — web-based log upload and analysis tool; useful for quick health checks and as a reference for what "good" log traces look like
