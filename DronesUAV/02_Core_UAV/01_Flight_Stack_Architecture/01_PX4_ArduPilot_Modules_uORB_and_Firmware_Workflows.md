# PX4 ArduPilot Modules uORB and Firmware Workflows

## Overview

This page focuses on how autopilot software is actually organized. Knowing commands and parameters is useful. Knowing the internal architecture is what turns you into someone who can make meaningful changes safely.

## Why This Topic Matters

Most flight-stack bugs are not solved by adding another script. They are solved by understanding module boundaries, message flow, parameter coupling, logging, and build or test workflow.

## Real-World Context / Industry Relevance

Teams hiring for UAV software expect more than operator knowledge. They want engineers who can read firmware code, trace control flow, change behavior intentionally, and explain the effect in logs.

## Core Terminology

- `uORB`: PX4 publish-subscribe middleware used inside the flight stack.
- `module`: a unit of autopilot functionality such as estimation, control, or drivers.
- `parameter`: runtime-configurable setting that changes behavior.
- `driver`: code bridging hardware devices into the stack.

## Mental Model / Big Picture

```text
sensors -> drivers -> estimators -> controllers -> mixers / outputs
                      ^            |
                      |            v
                   parameters   logs / telemetry
```

## Main Concepts / Core Concepts

- internal publish-subscribe patterns
- controller and estimator layering
- parameter-driven behavior
- build, test, and SITL loops for firmware changes

## Architecture / Components / Building Blocks

- drivers
- estimators
- controllers
- vehicle-type logic
- logging
- parameters

## Step-by-Step Implementation Guide

1. Trace one signal path from sensor input to actuator output.
2. Inspect one estimator or controller module.
3. Change one small behavior in SITL.
4. Compare logs before and after.

## Hands-On Example / Mini Project

Add a small diagnostic or tune one behavior in PX4 or ArduPilot SITL, then write a note explaining the changed path and observed result.

## Best Practices

- change one variable at a time
- keep parameter diffs
- validate in SITL first
- write down the exact code path you touched

## Common Pitfalls

- changing multiple parameters and code paths at once
- not understanding vehicle-type differences
- editing behavior without a log-based comparison

## Debugging / Troubleshooting Guide

- start from logs and module boundaries
- confirm the estimator and controller states
- isolate whether the issue is firmware, simulator, or companion-side

## Metrics / KPIs / What to Measure

- stability of the changed behavior
- reproducibility in SITL
- clarity of before vs after evidence

## Tools Commonly Used Around This Topic

- `PX4` or `ArduPilot` source trees
- SITL
- log analyzers
- parameter tools

## Practice Exercises

- draw the PX4 signal path using uORB terms
- identify the equivalent high-level path in ArduPilot
- modify one non-safety-critical behavior in SITL

## Portfolio / Resume Application

One autopilot modification with logs and explanation is a strong hiring signal.

## Next Step

Continue to [ROS 2 Offboard Control and Companion Architecture](../02_ROS_2_and_Companion_Computers/01_ROS_2_Offboard_Control_and_Companion_Architecture.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Understanding autopilot internals is the skill that separates engineers who can tune parameters from engineers who can diagnose why a parameter does not work, write a new module, or trace an unexpected behavior through the firmware. In PX4, the uORB message bus carries data between every module — from sensor drivers through estimators to controllers and mixers — using a typed, asynchronous publish/subscribe model. In ArduPilot, the equivalent is a scheduler-based single-threaded architecture with AP_HAL abstractions over hardware.

In practice, firmware-level work shows up in these situations: a new sensor needs a driver; an estimator is rejecting measurements for an unknown reason (requires reading `estimator_status` and tracing back to the sensor driver); a custom vehicle type needs different mixing; a customer needs a diagnostic mode that logs additional internal state. None of these are solvable by script. They require reading source code, understanding module registration, and making controlled changes in SITL.

The build workflow matters equally. PX4's CMake-based build system, `nuttx` target builds, and SITL targets (`make px4_sitl gazebo-classic`) all follow specific conventions. ArduPilot's `waf` build system with `--board` targets for different hardware (Pixhawk 6C, Cube Orange, SITL) works differently. Engineers who understand the build system do not get blocked by mysterious build failures when they add a new file or change a header.

### Industry Tool Stack

- **PX4 source tree** — module registration in `CMakeLists.txt`; module entry via `px4_simple_app_main()`; build and flash with `make <board_target> upload`
- **uORB** — `uorb top` (realtime publish rate monitor in NuttX console); `listener <topic_name>` (live message print); `uorb status` (subscription counts); `orb_subscribe()` / `orb_publish()` APIs in C++
- **NuttX console** — accessible via UART or USB; `ps` shows active tasks; `free` shows memory; `perf reset && perf` captures timing benchmarks
- **ArduPilot AP_HAL** — hardware abstraction layer; `AP_Scheduler` drives the main loop; `DataFlash` handles logging; `GCS_Mavlink` handles external communication
- **SITL + GDB** — attach GDB to a running SITL process for live breakpoint debugging; `gdb --pid $(pgrep px4)` or `lldb` on macOS
- **ClangFormat + ClangTidy** — enforced by PX4's CI; format all modified files before submitting a PR or the CI will reject the patch
- **PX4 Flight Review** — upload SITL or hardware logs; automated health checks run on every uploaded log and flag anomalies

### Step-by-Step Applied Workflow

1. **Read one complete module**: start with `mc_pos_control` (PX4 multicopter position controller) or `ArduCopter/control_althold.cpp` (ArduPilot). Trace every uORB subscription it reads and every topic it publishes.
2. **Add a diagnostic publication**: create a new uORB topic (add a `.msg` file, register it, compile) that publishes one extra internal value from the position controller — e.g., the feed-forward term. Verify it appears in logs.
3. **Trace a signal through the full pipeline**: from `sensor_combined` (raw IMU) → `estimator_sensor_bias` (EKF output) → `vehicle_local_position` (estimator output) → `vehicle_local_position_setpoint` (controller input) → `actuator_controls` (controller output) → `actuator_outputs` (mixer output). Print each topic value at the same timestamp.
4. **Make one parameter change and validate in SITL**: change `MC_PITCH_P` by +50%, run a position hold in SITL, capture the log, and compare `vehicle_attitude.q` vs. `vehicle_attitude_setpoint.q` traces in pyulog.
5. **Submit a minimal PR to PX4**: fix a documentation error, add a unit test, or improve a comment in a module you have read. Follow the PX4 contribution guide: `git checkout -b my-fix`, `make format`, test in SITL, push, and open a draft PR.
6. **Build ArduPilot for SITL**: `./waf configure --board sitl && ./waf copter`. Run `sim_vehicle.py -v ArduCopter`. Identify the equivalent position control loop in ArduPilot's source and note the architectural differences from PX4.

### AI Integration

AI has limited but useful applications at the firmware level. LLM code completion tools (Copilot, Claude) can speed up boilerplate — uORB topic definitions, module registration CMakeLists entries, parameter macros — because these follow strict patterns that AI generates correctly. For novel control logic or safety-critical paths, AI suggestions require careful review against the PX4 contribution guidelines and SITL validation.

Log-based anomaly detection is more applicable: given a set of uORB topic logs from multiple flights, ML models can learn the typical relationship between `actuator_controls` and `vehicle_local_position` response and flag flights where the relationship diverges — indicating actuator degradation, parameter drift, or a structural change.

For ArduPilot, the AutoTune feature is a rule-based precursor to ML-assisted parameter tuning. Research groups are extending it toward learning-based approaches, but these are not yet in mainline ArduPilot.

### Case Studies

**PX4 Auterion Enterprise Stack**: Auterion's commercial PX4 fork (used in Skynode) includes several custom modules — enhanced logging, payload control interfaces, and fleet telemetry modules — built directly on top of the uORB architecture described here. Their engineering team contributes these improvements upstream to PX4. Reading their public PRs on github.com/PX4/PX4-Autopilot is one of the best ways to learn production-grade firmware module authoring.

**ArduPilot AutoTune**: ArduPilot's AutoTune feature — which automatically finds PID gains by analyzing vehicle response to step inputs — is implemented as a flight mode module that watches `ATTITUDE_ERROR` and `RATE` topics, applies test inputs, and adjusts parameters. It demonstrates how a complex firmware behavior is organized as a mode within the scheduler architecture. Its source in `ArduCopter/control_autotune.cpp` is readable and well-commented.

**ideaForge Custom Firmware Features**: ideaForge's engineering team has implemented custom ArduPilot features for their SWITCH UAV platform, including payload control interfaces and DGCA-specific compliance behaviors. These are not publicly available, but their job postings for Embedded/Firmware Engineers list ArduPilot module authoring and uORB-equivalent AP_HAL driver writing as explicit requirements — confirming that firmware internals knowledge is not optional for production UAV engineering in India.

### Failure Modes & Safety

**Module coupling without uORB contracts**: adding code that directly accesses another module's internal state rather than subscribing to its published uORB topic. This creates invisible dependencies that break when the source module changes its internal logic. The uORB interface contract exists precisely to prevent this.

**Timing violations in the control loop**: adding code to the position controller that takes too long (e.g., a string operation, a memory allocation, or a slow filesystem access). The NuttX real-time scheduler will allow this, but the control loop rate will degrade and the controller will skip cycles. In SITL this may not manifest; on hardware with real sensor noise it can cause oscillations. Profile with `perf` before and after adding code to the critical path.

**Parameter coupling without documentation**: adding a parameter that interacts with two other parameters in a non-obvious way. A pilot or engineer who changes only one of the three will get unexpected behavior with no error message. Every new parameter should have clear units, range, and dependency documentation in the `.yaml` metadata file.

**Flashback incompatibility**: flashing a firmware update that changes the parameter format or default values without documenting the change, causing field vehicles to behave differently after an update. PX4's parameter compatibility system handles some of this, but custom parameters require explicit migration code.

**ArduPilot vehicle type mismatch**: confusing the ArduCopter, ArduPlane, and ArduRover codebases. The scheduler rates, control loop structure, and failsafe behaviors differ significantly. Code that works for copter does not transfer to plane without understanding the plane-specific control architecture.

### Business & Commercial Layer

Autopilot firmware engineering is the most specialized — and typically highest-compensated — role in the UAV software industry. Teams cannot hire for it quickly; it requires 1–3 years of deliberate firmware study and contribution. This creates a supply shortage that makes firmware engineers extremely valuable.

In India, the PLI (Production-Linked Incentive) scheme for drones has created domestic demand for engineers who can modify and extend ArduPilot for DGCA-certified platforms. Companies like ideaForge, NewSpace Research, and several DRDO-adjacent startups are hiring specifically for firmware modification capability — not just operator skill.

Globally, the eVTOL industry (Joby, Archer, Lilium-successor ventures, Supernal) is a major demand driver for flight control firmware engineers who can work in both classical autopilot (PX4-based) and proprietary certified software (DO-178C compliant) contexts.

### Hiring Signal

**Job titles that require firmware/module-level autopilot knowledge:**
- **Autopilot Firmware Engineer (PX4)** — at Auterion, Dronecode-affiliated companies, and research institutions; primary job function is writing, testing, and maintaining PX4 modules in C++ with NuttX RTOS
- **Embedded Systems Engineer (Flight Controller)** — at UAV OEMs building on ArduPilot or PX4; requires driver writing, RTOS task management, and hardware bring-up
- **Flight Controls Engineer** — at defense-adjacent UAV companies and eVTOL startups; requires control loop understanding in the firmware context, not just simulation
- **UAV Software Engineer (ArduPilot)** — at inspection, agriculture, and field operations companies using ArduPilot; requires parameter system knowledge and custom feature development

**Specific interview screens for firmware competence:**
1. "Given a PX4 log where `actuator_controls[0].control[0]` is non-zero but `actuator_outputs.output[0]` is zero, what are the possible causes? Walk me through the module path between those two topics."
2. "Explain the uORB pub/sub model: how does a subscriber know when new data is available? What is the difference between `orb_check()` polling and `orb_set_interval()`, and when would you use each?"
3. "You need to add a custom PX4 module that reads `vehicle_local_position` and publishes a new topic `my_diagnostic`. Walk me through the files you create and the CMakeLists changes you make."
4. "What is the NuttX scheduler's role in PX4? How do module tasks get scheduled and what happens if one task takes longer than its expected cycle time?"
5. "ArduPilot and PX4 both implement multicopter position control. Name two architectural differences between them and explain when each approach has an advantage."

### Portfolio Projects

**Beginner: `uorb-signal-tracer`**
- Deliverables: Python script using pyulog that loads a PX4 SITL flight log, extracts the full signal chain (sensor → estimator → controller → output), plots each stage, and annotates the plot with topic names and publish rates; README explaining each topic's role
- Suggested repo tree: `README.md`, `scripts/trace_signal_chain.py`, `data/sample_flight.ulg`, `outputs/signal_chain_plot.png`, `docs/topic_reference.md`
- Acceptance criteria: (1) all six stages of the signal chain are present in the plot; (2) topic names and sample rates are correctly labeled; (3) README explains each stage in plain language

**Intermediate: `px4-diagnostic-module`**
- Deliverables: a minimal PX4 module that subscribes to `vehicle_local_position` and `actuator_controls`, computes position error vs. setpoint, and publishes a custom `position_diagnostic` uORB topic; SITL-tested and logged; PR-ready code quality
- Suggested repo tree: `README.md`, `src/modules/position_diagnostic/`, `msg/position_diagnostic.msg`, `CMakeLists.txt`, `test/sitl_test.sh`, `logs/`
- Acceptance criteria: (1) module compiles without warnings for `px4_sitl` target; (2) custom topic appears in SITL log; (3) position error computation is correct against a manually verified reference

**Advanced: `autopilot-module-contribution`**
- Deliverables: a real submitted (or merged) PR to PX4 or ArduPilot — could be a bug fix, test addition, documentation improvement, or new feature; accompanied by a writeup of the design decision, review feedback received, and how feedback was addressed
- Suggested repo tree: PR link as primary deliverable; `writeup/contribution_narrative.md`, `writeup/review_feedback.md`
- Acceptance criteria: (1) PR was actually submitted to the upstream repo; (2) it includes SITL test evidence; (3) writeup demonstrates understanding of the reviewers' feedback

### Future Trends

- **2026**: PX4 v1.15+ continues the migration from NuttX-only RTOS to supporting additional RTOS targets (VxWorks, eCos) for certification purposes. Engineers who understand the HAL abstraction layer are positioned for this transition.
- **2030**: DO-178C-adjacent verification practices begin appearing in the UAV firmware community as BVLOS markets require higher assurance. Engineers who have practiced test-driven firmware development and module-level unit testing will adapt more easily.
- **2035**: AI-assisted firmware generation (control law code from specifications, adaptive parameter tuning from flight data) becomes a real engineering tool. Firmware engineers who understand what correct control code looks like — and can validate AI-generated code — are the critical quality gate.
- **2045**: The NuttX/ArduPilot/PX4 architecture will likely be superseded, but the discipline of understanding the full signal chain from sensor to actuator in a real-time embedded system remains a permanent engineering skill.

### Interview Questions

1. **Explain the PX4 module architecture. What is a module, how is it registered, and how does it communicate with other modules?**
   *Answer*: A PX4 module is a self-contained software unit that runs as a NuttX task. It is registered by adding a `px4_add_module()` entry in `CMakeLists.txt` and implementing a `module_main()` entry point with start/stop/status subcommands. Communication with other modules happens exclusively through uORB: the module subscribes to topics it needs (`orb_subscribe()`) and publishes to topics it produces (`orb_advertise()` + `orb_publish()`). Direct function calls between modules are not used — everything goes through the message bus.

2. **What is the difference between `ORB_ID(vehicle_attitude)` and `ORB_ID(vehicle_attitude_setpoint)` and which modules publish each?**
   *Answer*: `vehicle_attitude` is the current estimated vehicle attitude from the EKF (published by the `ekf2` or `attitude_estimator_q` module). `vehicle_attitude_setpoint` is the desired attitude commanded by the position controller or the navigator (published by `mc_pos_control` or directly by the attitude controller in some flight modes). The attitude controller (`mc_att_control`) subscribes to both: it reads the setpoint and the current attitude and computes the attitude error that drives the rate controller.

3. **In ArduPilot, how does the scheduler differ from NuttX task scheduling in PX4?**
   *Answer*: ArduPilot uses a cooperative, single-threaded scheduler (`AP_Scheduler`) that calls registered functions in round-robin order. Each function runs to completion before the next starts — there is no preemption. Functions declare their expected max runtime; if a function overruns, the scheduler logs the overrun. PX4 uses NuttX's preemptive RTOS with multiple tasks at different priorities — the attitude controller runs at higher priority than the navigator, which runs at higher priority than logging. The PX4 model allows finer timing control but requires careful priority assignment; the ArduPilot model is simpler to reason about but less suitable for hard real-time guarantees.

4. **A PX4 vehicle is oscillating in roll. Walk me through your firmware-level diagnostic process.**
   *Answer*: (1) Open the log and plot `vehicle_angular_velocity.xyz[0]` (roll rate) against `vehicle_attitude.q` roll and `actuator_controls.control[0]` (roll rate setpoint). (2) Check if the oscillation is at the rate loop frequency (fast, > 10 Hz) or the position loop frequency (slow, 1–2 Hz). (3) If rate loop — `MC_ROLLRATE_P` is too high; check vibration in `sensor_combined.gyro_rad` for mechanical resonance. (4) If position loop — `MC_ROLL_P` is too high; check `vehicle_local_position` vs `vehicle_local_position_setpoint` for tracking error growth. (5) Reduce the offending gain by 20%, re-run SITL, compare logs.

5. **What happens in PX4 firmware when the autopilot loses the GPS signal during a position-controlled flight?**
   *Answer*: EKF2 detects the GPS absence via the `gps_check_fail_flags` in `estimator_status`. After the GPS timeout (`EKF2_GPS_DELAY` + check failure window), EKF2 marks GPS as inactive and falls back to dead-reckoning using IMU integration only. Position estimate quality degrades rapidly. The vehicle status module reads EKF health flags and may trigger the GPS loss failsafe (`COM_POSCTL_NAVL` parameter). Depending on the configured failsafe action (`COM_POSCTL_NAVL = 0` → no action in Position mode, `= 1` → RTL, `= 2` → land), the vehicle either tries to hold position (with growing error) or executes a recovery action.

### Further Depth

- **PX4 Module Architecture Documentation** (docs.px4.io/main/en/concept/architecture.html) — the definitive guide to modules, uORB, and the internal message bus
- **PX4 Contribution Guide** (docs.px4.io/main/en/contribute/) — PR workflow, coding style, test requirements, and review process
- **ArduPilot Developer Wiki — Coding** (ardupilot.org/dev/docs/apmcopter-programming-libraries.html) — covers the scheduler, library architecture, and AP_HAL
- **NuttX RTOS Documentation** (nuttx.apache.org) — the OS underlying PX4; task scheduling, memory management, and POSIX API coverage
- **PX4 ULog file format** (docs.px4.io/main/en/dev_log/ulog_file_format.html) — the binary format used by PX4 logs; useful for writing custom log parsers
- **"Small Unmanned Aircraft: Theory and Practice"** — Beard and McLain; the control loops implemented in PX4 and ArduPilot are explained rigorously in chapters 5–10
