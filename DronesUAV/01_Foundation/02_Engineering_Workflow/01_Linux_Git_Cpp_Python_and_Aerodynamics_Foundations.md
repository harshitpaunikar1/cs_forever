# Linux Git C++ Python and Aerodynamics Foundations

## Overview

This page covers the lowest layer of employable UAV engineering. Before you touch autonomy, you need to be comfortable with Linux, Git, C++, Python, basic debugging, and the aerodynamics intuition that makes flight behavior less mysterious.

## Why This Topic Matters

Drone software work is not just writing one node or script. It is building, debugging, profiling, logging, and reasoning about software that interacts with real physics.

## Real-World Context / Industry Relevance

Every serious drone team expects fluency with terminals, version control, compiled code, scripting, and enough flight intuition to discuss lift, drag, thrust, stability, and actuator behavior without hand-waving.

## History / Evolution of the Topic

Modern UAV engineering moved from isolated firmware hacking toward a broader systems workflow: Linux laptops, CI, simulations, field logs, companion computers, and mixed-language codebases.

## Prerequisites

- willingness to use the terminal daily
- basic programming exposure

## Core Terminology

- `RAII`: C++ resource management style that ties cleanup to object lifetime.
- `Virtualenv`: isolated Python environment for tooling and scripts.
- `PWM`: pulse-width modulation used for actuator control.
- `ESC`: electronic speed controller between flight controller and motor.
- `UART`, `I2C`, `SPI`: common embedded communication buses.

## Mental Model / Big Picture

```text
Linux + Git + C++/Python + hardware intuition
    -> faster debugging
    -> cleaner tools
    -> better flight-stack understanding later
```

## Main Concepts / Core Concepts

- Linux workflow for builds, logs, package management, and debugging
- Git discipline for reproducible work and collaboration
- C++ for flight-stack and performance-sensitive code
- Python for telemetry, tooling, and data analysis
- aerodynamics and electronics as engineering context, not separate theory

## Subtopics Breakdown

- shell, files, processes, package managers
- CMake and build troubleshooting
- Python packaging and scripts
- basic forces and stability
- power, buses, and sensors

## Architecture / Components / Building Blocks

- development machine
- repo and branch workflow
- compiler and debugger
- tool scripts
- sensor and actuator chain

## Process Flow / Lifecycle

```text
code -> build -> run -> inspect logs -> debug -> document -> repeat
```

## Practical / Design / Operational Sections

Use these foundations every day. They are not pre-work you “finish.” They are the substrate of all later UAV work.

## Step-by-Step Implementation Guide

1. Set up Linux, Git, compiler toolchains, and Python environments.
2. Write one small C++ project and one small Python project.
3. Review lift, drag, thrust, moments, and common electrical interfaces.

## Hands-On Example / Mini Project

Build a Python telemetry parser for mock MAVLink packets and a small C++ complementary-filter demo on synthetic IMU data.

## TWO Case Study / Real Scenario

### Case Study 1 / Real Scenario

A developer who can inspect logs, rebuild tools, and reason about IMU noise fixes a flight-test issue in hours instead of days.

### Case Study 2 / Real Scenario

A developer with weak Linux and hardware basics spends days blaming the autopilot for a problem caused by bad environment setup and misunderstood sensor wiring.

## Best Practices

- keep one clean build path
- document setup commands
- separate experiment scripts from reusable tools
- learn enough physics to sanity-check behavior

## Performance / Optimization Considerations

Build speed, debug speed, and log inspection speed matter early because they control iteration quality.

## Security / Reliability Considerations

Undocumented setup and fragile scripts create avoidable field failures.

## Scalability Considerations

Good workflow habits matter more as projects gain more packages, boards, logs, and contributors.

## Common Pitfalls

- trying to learn five tools at once
- avoiding C++ because Python feels easier
- skipping aerodynamics entirely

## Debugging / Troubleshooting Guide

- verify compiler and Python versions first
- isolate environment issues from code issues
- use plots and logs instead of guessing sensor behavior

## Common Misconceptions

- “I only need Python for drones”
- “The autopilot hides the physics anyway”
- “Git matters later”

## Tradeoffs / Decision Frameworks

The main trade-off is speed of getting started versus depth of engineering understanding. Optimize for durable depth.

## Metrics / KPIs / What to Measure

- clean rebuild success
- time to reproduce an issue
- code readability
- ability to explain sensor and actuator pathways

## Tools Commonly Used Around This Topic

- `git`
- `gdb`
- `cmake`
- `colcon`
- `python`
- `clang-format`

## Ecosystem / Platforms / Vendors

- Ubuntu
- GitHub
- GCC / Clang
- common autopilot hardware buses

## Automation Opportunities

Linting, formatting, CI builds, and log parsing are high-value early automations.

## AI Impact on This Topic

AI can help write small utilities faster, but it cannot replace environment discipline or physical intuition.

## Recommended Resources

- official Python docs
- C++ references
- NASA aerodynamics primers as support reading
- the UAV stack docs listed in the local course index

## Practice Exercises

- write a CLI that parses and summarizes mock telemetry packets
- implement a small filter in C++
- explain the difference between UART, I2C, and SPI from memory

## Reflection Questions

- Which tool failure still slows you down most?
- Can you explain why a drone pitches forward to accelerate?

## Interview Questions

- Why is C++ prioritized over Python for flight-stack work?
- What would you inspect first after an IMU-related anomaly?

## Portfolio / Resume Application

Show one clean tooling repo, one C++ systems artifact, and one Python telemetry or analysis tool.

## Cross-Disciplinary Connections

This topic connects software engineering, embedded systems, controls, and hardware integration.

## Future Trends

Developer workflows are becoming more sim-first, CI-driven, and traceable.

## 2026+ Focus Areas

- reproducible environments
- mixed C++ and Python workflows
- better log analysis and tooling

## Next Step

Continue to [PX4 ArduPilot MAVLink and QGroundControl Foundations](../03_Flight_Stack_Fundamentals/01_PX4_ArduPilot_MAVLink_and_QGroundControl_Foundations.md).

## Advanced Next Step

Tie this workflow into ROS 2, SITL, and autopilot source builds.

## Industry Readiness Layer

If you cannot build and debug locally, you are not ready for serious UAV software work yet.

## Terms to Remember

`RAII`, `PWM`, `ESC`, `UART`, `I2C`, `SPI`, `IMU`

## Where Companies Use This

Everywhere in UAV software, autonomy, firmware, and test tooling.

## Roles That Need This Skill

- drone software engineer
- autonomy engineer
- embedded engineer
- robotics engineer

## Hands-On Checklist

- Linux environment installed
- Git workflow used daily
- one C++ utility
- one Python tool
- one debugging session completed with logs

## Common Production Mistakes

- undocumented setup
- brittle scripts
- weak hardware assumptions

## What Beginners Usually Miss

How much of drone work is debugging, not just feature writing.

## What Senior Professionals Focus On

Fast diagnosis, clean interfaces, and dependable tooling.

## How This Appears in Real Projects

Through build scripts, CI, log tooling, interface definitions, and issue triage.

## How to Talk About This in Interviews

Explain one concrete bug you found and how your tools and reasoning exposed it.

## Portfolio Proof You Can Build

A telemetry parser, an IMU filter demo, and a documented Linux-based dev workflow.

## Red Flags Employers Notice

- no Git history
- no setup instructions
- no evidence of debugging discipline

## Decision-Making Scenarios

When should a quick Python tool stay a tool, and when should it become a maintained subsystem?

## Industry Standards / Compliance Notes

Even early tooling choices affect traceability and testability in regulated or safety-sensitive environments.

## Team Collaboration Considerations

Shared build steps and logging conventions reduce wasted time.

## Cost / Budget Awareness

Good simulation and tooling habits save field-test time and hardware risk.

## Speed vs Quality Tradeoffs

Move fast in experiments, but keep mainline workflows clean and reproducible.

## Production Readiness Checklist

- documented setup
- stable build
- versioned dependencies
- logs and debug path

## Maintenance Mindset

Prefer boring tools that teammates can run and fix.

## Scaling Mindset

Assume more vehicles, more logs, and more contributors later.

## Leadership Perspective

Strong foundations lower onboarding cost across the team.

## Freelance / Startup Perspective

You will often be both developer and integration engineer, so these basics compound quickly.

## Enterprise Perspective

Larger teams care about traceability, reproducibility, and shared tooling contracts.

## Global Market Relevance

These skills transfer across drones, aerospace software, robotics, and embedded systems globally.

## Career Leverage Score

`10/10`

## Adjacent Skills to Learn Next

ROS 2, SITL, and autopilot architecture.

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Every UAV software team — from two-person startups to Zipline or Shield AI — operates on the same toolchain substrate: a Linux laptop or server, a Git workflow, a C++ or Python codebase, and enough physics intuition to reason about why the vehicle did what it did. The specific autopilot, simulator, and mission software change by company. The substrate does not.

In practice this page's skills show up daily in the following ways. Build system fluency (CMake, colcon, cross-compilation) determines how quickly you can get a new firmware module or ROS 2 package building and running. Git discipline (clean branches, meaningful commits, parameter diff in version control) determines whether your team can understand what changed between a good flight and a bad one. Python scripting fluency determines how quickly you can build a log parser, a parameter diff tool, or a MAVLink replay harness. C++ fluency determines whether you can read autopilot source, contribute a module, or write a performance-sensitive onboard component. Aerodynamics intuition determines whether you can tell a physics-plausible explanation from a physics-impossible one when debugging a strange flight behavior.

Senior UAV engineers at companies like Auterion, ideaForge, and Garuda Aerospace are explicitly asked in interviews to demonstrate these basics before any discussion of autonomy or perception. The assumption is that everyone who gets past the technical screen already has this foundation solid. If they do not, the interview ends there.

### Industry Tool Stack

- **Ubuntu 22.04 / 24.04 + APT** — the standard development OS; package management is used daily for build dependencies, ROS 2 packages, and toolchain updates
- **GCC / Clang + CMake / Ninja** — C++ compilation for flight stack, firmware modules, and cross-compiled targets; `cmake --preset sitl` style build invocations are standard PX4 workflow
- **`gcc-arm-none-eabi` / `arm-linux-gnueabihf`** — cross-compilation toolchains for Cortex-M (bare metal) and Cortex-A (Linux companion) targets respectively
- **Git + GitHub / GitLab + `git log --follow -p`** — version control with full history tracing; teams use `git bisect` to trace parameter and behavior regressions
- **Python 3 + `venv` / `pip`** — scripting, log analysis, telemetry tooling, test harnesses; `pymavlink`, `pyulog`, `matplotlib`, `numpy` are standard dependencies
- **GDB + `addr2line` + Valgrind** — debugging C++ crashes, firmware faults, and memory issues; `gdb` is used on both host and cross-compile targets via gdbserver
- **`clang-format` / `cpplint`** — code style enforcement matching the PX4 or ArduPilot contribution requirements
- **`strace` / `lsof` / `top`** — Linux process inspection tools used daily for debugging simulation, driver, and IPC issues

### Step-by-Step Applied Workflow

1. **Build the flight stack from source**: clone PX4-Autopilot or ArduPilot, run the full build for SITL target, confirm zero warnings in your patch paths. If the build fails, diagnose using CMake output, not by guessing.
2. **Write a Python log parser**: use `pyulog` to load a `.ulg` file, extract `vehicle_attitude` and `vehicle_local_position` topics, and plot commanded vs. actual roll over a 30-second window. Export to PNG. Put it in a git repo with a clear README.
3. **Write a C++ filter utility**: implement a simple complementary filter or moving-average on synthetic IMU data (generated in Python, read via stdin or file). Compile with `-O2`, add a `CMakeLists.txt`, and write a test that verifies output bounds for known input.
4. **Explain a flight behavior from physics**: given a multirotor that pitches forward aggressively at full-throttle hover, estimate whether the CG offset, motor asymmetry, or wind drag is a plausible cause based on basic force and moment balance. Write a two-paragraph note in your repo.
5. **Build a parameter diff tool**: write a Python CLI that loads two QGC parameter files (`.params` format) and outputs only the changed parameters with before/after values. This is a real team tool — parameter regressions are common.
6. **Set up Git discipline**: create a branch-per-experiment pattern in your local repo. Each SITL experiment gets a branch with a commit message that records the parameter set, the scenario, and the outcome. This is the foundation of traceable development.
7. **Profile a build**: time a full PX4 SITL rebuild from clean, then add `-j$(nproc)` and compare. Understand why parallel builds sometimes create linking race conditions.

### AI Integration

AI code assistants (GitHub Copilot, Cursor, Claude) add genuine productivity at this foundation tier for specific tasks: generating CMakeLists.txt boilerplate, writing Python log-parsing scaffolding, explaining unfamiliar compiler error messages, and suggesting pymavlink connection patterns. These are legitimate uses because they reduce time on mechanical tasks without replacing engineering judgment.

Where AI fails dangerously at this level: it will suggest physically impossible aerodynamic claims with high confidence, it will hallucinate CMake flags that do not exist for a specific target, and it will generate C++ that compiles but uses wrong coordinate frames or wrong data types for the autopilot's message interface. The only protection against these failures is being able to verify the suggestion manually — which requires the human to actually know the topic. This is why Foundation competence is non-negotiable even in an AI-assisted workflow.

A useful discipline: when an AI writes a line of flight-stack code for you, ask yourself if you could have written it from the documentation. If the answer is no, treat it as a draft to verify rather than a solution to accept.

### Case Studies

**PX4-Autopilot codebase (GitHub)**: PX4's open-source repository is the best single example of professional C++ and CMake discipline in the UAV domain. The build system, module structure (`src/modules/`), uORB message definitions, and contribution guide all reflect the standards that real companies apply. Reading PX4 source code and attempting to contribute a simple change teaches more about this page's content than any tutorial because it enforces the same standard a real code reviewer would apply.

**ArduPilot's Python-based test suite (`autotest/`)**: ArduPilot's `autotest` framework in their repository is a large Python test harness that launches SITL, flies programmed missions, and asserts on outcomes. It is an excellent real-world example of Python scripting for flight-stack testing. Reading and running individual `autotest` scripts teaches both Python tooling patterns and ArduPilot's internal behavioral contracts simultaneously.

**Garuda Aerospace field deployment workflow**: Garuda Aerospace (India) operates agricultural and surveillance drones at scale across multiple Indian states. Their field engineering teams use Python scripting for log processing and mission analysis, Git for versioning waypoint files and parameter configs, and Linux CLI tools for onboard debugging. The operational context — often with connectivity constraints and hardware iteration pressure — makes the "works on one machine only" failure mode acutely costly.

### Failure Modes & Safety

**Fragile development environment**: a setup that requires manual steps not captured in any script or README, depends on a specific undocumented Ubuntu version quirk, or breaks when a package is upgraded. This creates a hidden operational risk: every new team member's first week is debugging setup rather than building flight software. In a small team deploying hardware, this is dangerous because it means field issues cannot be reproduced quickly on a fresh machine.

**Undocumented parameter changes**: changing autopilot parameters during development without recording the before/after state in version control. UAV tuning history is a safety artifact — if a vehicle crashes after a tuning session, the investigation needs the full parameter trajectory. Teams that do not track parameters are regularly unable to answer "what changed between the last good flight and this crash?"

**C++ code that compiles but is physically wrong**: the most insidious failure mode at this level. Common examples: using wrong coordinate frame (NED vs. ENU vs. body frame) for position offsets sent to the autopilot, computing heading in degrees when the autopilot expects radians, assuming GPS altitude when the autopilot is using barometric altitude. These compile cleanly and may work in some conditions while failing dangerously in others.

**Aerodynamics ignored, "software first"**: treating the autopilot's attitude response as purely a software problem when it is actually a combination of motor mapping, airframe geometry, CG position, and PID tuning. Engineers with no physical intuition chase parameter changes that cannot help because they are solving a software problem that does not exist while the real physics constraint goes unexamined.

**Weak Git hygiene**: working on main, committing "fix" and "update" without detail, and never using branches for experiments. When flight behavior changes unexpectedly, the team needs to bisect their history. Clean Git history is a safety tool, not a style preference.

### Business & Commercial Layer

The engineering workflow skills on this page are the commercial substrate for every UAV product and service. Their commercial value is not optional. An inspection drone company (Percepto, Flyability, Skydio Enterprise) with a fragile build system and no parameter version control carries hidden operational risk that eventually surfaces as a field incident. A delivery drone company (Wing, Zipline) with weak log tooling cannot diagnose anomalies fast enough to maintain operational safety margins.

In India, the growing DGCA compliance requirements for commercial drone operations (UIN, RPAS permit, type certification for BVLOS) are beginning to impose documentation and traceability obligations that directly reward teams with strong Git, build reproducibility, and log discipline. The PLI scheme for domestic drone manufacturing rewards production-grade engineering practices, and the companies receiving PLI funding need engineers who can work at that level.

Globally, defense-adjacent UAV work (Shield AI, AeroVironment, ideaForge defense track) adds safety-critical software requirements that make the engineering workflow habits on this page mandatory rather than best-practice.

### Hiring Signal

**Job titles where this page's skills are an explicit screen (not just a prerequisite):**
- **Autopilot Firmware Engineer (PX4/ArduPilot)** — requires C++ and CMake fluency at contribution level; code review is part of the interview
- **Flight Software Engineer (Entry/Mid)** — requires ability to set up toolchain, run SITL, read logs, and write small tools independently; this is verified during technical screen
- **Embedded Systems Engineer (UAV)** — requires C++ for bare-metal or RTOS targets, cross-compilation understanding, and hardware-interface awareness (UART, SPI, I2C, PWM)
- **UAV Test Engineer / Systems Test Engineer** — requires Python scripting for test harnesses, log analysis, and SITL-based test case writing

**Interview screens specific to this page's content:**
1. "Walk me through how you would diagnose a PX4 SITL build failure where cmake finds the wrong version of a dependency — what tools do you use, in what order?"
2. "Write a Python script that loads a `.ulg` file using pyulog, computes the RMS attitude error between commanded and actual roll over the entire flight, and prints the result. You have 10 minutes."
3. "Explain the difference between using GDB on a native Linux binary versus using GDB with gdbserver for a cross-compiled ARM target. When would you use each in UAV work?"
4. "A multirotor is pulling left consistently during forward flight. List three physical causes and three software causes. For each, what log field or physical measurement would you check first?"
5. "What is RAII in C++ and give one example of where it matters in flight software — specifically in a scenario where exception safety or early return is relevant."

### Portfolio Projects

**Beginner: `uav-log-toolkit`**
- Deliverables: Python CLI that loads a `.ulg` PX4 log, extracts user-specified topics, outputs a timestamped CSV, and generates labeled time-series plots; tested on at least two different log files with different flight profiles
- Suggested repo tree: `README.md`, `src/log_toolkit.py`, `tests/test_log_toolkit.py`, `data/sample_logs/`, `outputs/`, `requirements.txt`
- Acceptance criteria: (1) CLI accepts `--log` and `--topics` arguments and fails gracefully for invalid inputs; (2) output plots are labeled with axis names and units; (3) test suite passes on a clean `venv` install

**Intermediate: `cpp-complementary-filter`**
- Deliverables: C++ implementation of a complementary filter for attitude estimation, reading synthetic IMU data from stdin, outputting roll/pitch estimates; built with CMake, includes unit tests using a known-input test vector, and a Python script to generate and visualize test data
- Suggested repo tree: `README.md`, `CMakeLists.txt`, `src/comp_filter.cpp`, `include/comp_filter.h`, `tests/`, `scripts/generate_imu_data.py`, `data/`
- Acceptance criteria: (1) builds cleanly with `cmake .. && make`; (2) unit tests pass; (3) Python visualization shows filter output converging to ground truth within 5 seconds on the provided synthetic data

**Advanced: `aero-aware-debug-case`**
- Deliverables: a documented case study of a real or realistic SITL anomaly — vehicle oscillating, unexpected mode switch, or sensor rejection — including the log evidence, the physical or software diagnosis, the parameter change that resolved it, and a before/after log comparison tool in Python
- Suggested repo tree: `README.md`, `logs/before/`, `logs/after/`, `scripts/compare_runs.py`, `notes/diagnosis.md`, `notes/physics_analysis.md`
- Acceptance criteria: (1) diagnosis note correctly identifies the root cause with log evidence cited; (2) physics analysis note explains whether the cause is aerodynamic, electronic, or software; (3) compare_runs.py produces a side-by-side plot of the relevant metric in both runs

### Future Trends

- **2026**: The C++ and Python workflow on this page is stable and expected. What changes is the tooling around it: Dev Containers (VSCode + devcontainer.json) are becoming the standard way to share reproducible development environments, replacing manual setup docs. Engineers who adopt this pattern early reduce onboarding friction significantly.
- **2030**: Cross-language tooling (Rust in flight-critical paths, Python for glue) may begin appearing in next-generation autopilot developments, but C++ remains dominant in PX4 and ArduPilot. Python's role in simulation, log analysis, and test harnesses grows rather than shrinks.
- **2035**: Formal verification tools (model checking, static analysis, bounded model checking of C++ flight software) begin appearing in certification-grade UAV development processes. Engineers who have strong C++ and can work with MISRA-C++ style constraints are positioned for this shift.
- **2045**: The Linux + Git + compiled language + scripting layer remains structurally stable because it reflects computer science fundamentals, not a specific tool fashion. The exact tools evolve; the underlying disciplines do not.

### Interview Questions

1. **Why is C++ the primary language for autopilot firmware rather than Python, and what specifically makes it necessary rather than just conventional?**
   *Answer*: C++ compiles to machine code with predictable execution time, no garbage collection pauses, and deterministic memory layout — all properties required for hard real-time flight control loops running at 400–8000 Hz. Python's GIL, garbage collector, and dynamic dispatch latency make it unsuitable for inner control loops. Python is appropriate for scripting, tooling, and non-real-time companion-compute tasks.

2. **What does `gcc-arm-none-eabi` compile for, and how does it differ from `arm-linux-gnueabihf`?**
   *Answer*: `gcc-arm-none-eabi` targets bare-metal ARM Cortex-M microcontrollers — no operating system, no standard library I/O, no Linux syscalls. `arm-linux-gnueabihf` targets ARM Cortex-A processors running Linux with hardware floating-point support. In UAV work: the first is for the flight controller MCU (STM32 family), the second is for the companion computer (Raspberry Pi, Jetson Nano, etc.).

3. **Explain how CMake's `find_package` works and what happens when a dependency is found in the wrong location.**
   *Answer*: `find_package` searches a set of predefined directories (and paths specified via `CMAKE_PREFIX_PATH` or `<PackageName>_DIR`) for a package config file (`<PackageName>Config.cmake`) or find module. When the wrong version is found — common in ROS 2 environments where multiple workspace overlays exist — the build fails at link time with version mismatch errors or at runtime with ABI incompatibilities. Resolution: explicitly set `CMAKE_PREFIX_PATH` to point to the correct workspace, or use `CMAKE_FIND_PACKAGE_PREFER_CONFIG` to force config-mode search.

4. **A multirotor in SITL shows persistent clockwise yaw drift even with yaw setpoint fixed. What are the three most likely causes, and how would you distinguish them using logs?**
   *Answer*: (1) Motor asymmetry or mixer mismatch — check actuator outputs in the log; all four should sum to equal torque. (2) IMU gyro Z-axis bias not calibrated — check `estimator_status` for gyro bias magnitude; if it is large and stable, recalibrate. (3) Airframe geometry mismatch in the mixer (wrong arm positions or prop-spinning-direction mapping) — compare the mixer file against the actual airframe and check if the yaw correction actuator output saturates.

5. **What is the purpose of `aerodynamics intuition` for a software engineer, and give one concrete example where it prevents a bug.**
   *Answer*: Aerodynamics intuition gives software engineers a physical sanity check on vehicle behavior that prevents mistaking physics-caused behavior for software bugs. Example: an engineer notices the vehicle pitches nose-down when throttle is reduced abruptly. Without aerodynamics intuition, they might suspect a PID bug and chase parameter changes. With intuition, they recognize this as the expected response of a multirotor CG slightly forward of the geometric center — the pitch is proportional to the throttle reduction and requires a CG adjustment or trim, not a PID change.

### Further Depth

- **PX4 Developer Guide — Development Environment Setup** (docs.px4.io/main/en/dev_setup/) — authoritative build environment reference for this curriculum's PX4 track
- **ArduPilot Developer Wiki — Setting Up the Build Environment** (ardupilot.org/dev/docs/building-the-code.html) — equivalent for ArduPilot track
- **"Small Unmanned Aircraft: Theory and Practice"** — Beard and McLain; chapters on aerodynamics, coordinate frames, and forces are directly relevant to the physics intuition layer of this page
- **pyulog** (github.com/PX4/pyulog) — the standard Python log parsing library for PX4 ULog files
- **Scott Meyers, "Effective Modern C++"** — the closest thing to a canonical C++ style guide relevant to safety-conscious flight software development; covers RAII, smart pointers, and move semantics
- **NASA Aerodynamics Primer** (grc.nasa.gov/www/k-12/airplane/) — accessible aerodynamics reference appropriate for the physical intuition layer of this page
