# Beginner Project Path

## Overview

These projects convert early UAV and simulation knowledge into working artifacts with clear deliverables and modest scope.

## Projects

### Project 1: Telemetry Parser Starter
- parse MAVLink packets or logs
- print readable summaries
- document assumptions

### Project 2: SITL Mission Rehearsal
- one SITL vehicle
- one QGroundControl mission
- one log review note

### Project 3: ROS 2 UAV State Monitor
- simulated vehicle state feed
- one ROS 2 status node
- one launch or run script

### Project 4: Parameter Diff Tool
- compare two parameter sets
- highlight risky changes
- add one simple report output

### Project 5: Precision Landing Prototype
- camera or simulated target feed
- simple detection pipeline
- pose estimate output

## Completion Standard

Pick any `2-3` and finish them cleanly rather than starting all five.

## Next Step

Move to [Intermediate Project Path](../Intermediate/01_Intermediate_Project_Path.md) when these start feeling routine.

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Beginner projects in UAV engineering serve a specific function: they prove that the engineer can interact fluently with the UAV software stack without requiring tutorial hand-holding for every step. The five projects in this path are calibrated to establish that proof across five distinct skill areas — MAVLink parsing, SITL operation, ROS 2 integration, parameter management, and basic perception — each of which appears in almost every professional UAV job description.

The key discipline at the beginner level is scope honesty. Each project should be small enough to finish completely — not 80% of an ambitious project, but 100% of a modest one. A Telemetry Parser that correctly parses the 5 most common MAVLink messages and prints them clearly, with a documented test showing it works on a real SITL log, is a better portfolio artifact than a "comprehensive MAVLink analyzer" that handles 30 message types but crashes on any message it doesn't recognize.

In industry, beginner-equivalent work appears in two professional contexts: (1) intern and new-grad onboarding projects, where teams use small, bounded tasks to assess how engineers approach unfamiliar codebases; and (2) test infrastructure work, where tools like a parameter diff utility or a telemetry parser are actual production tools used daily by operations teams. Understanding this context helps calibrate the quality bar: these projects are not toy exercises, they are scaled-down versions of real tools.

### Industry Tool Stack

- **pymavlink** — Python library for MAVLink message parsing; `mavutil.mavlink_connection()` for log and serial connections; `master.recv_match()` for message filtering; the core tool for the Telemetry Parser project
- **PX4 SITL** — `make px4_sitl_default gazebo-classic` for simulation; required for the SITL Mission Rehearsal and all log-based projects
- **QGroundControl** — GUI GCS for mission planning; `Plan > File > Save Plan` exports mission JSON; `Analyze > Mavlink Inspector` for live message inspection
- **MAVSDK Python** — `pip install mavsdk`; `System()`, `Mission`, `Action`, `Telemetry` classes; higher-level than pymavlink for mission projects
- **ROS 2 Humble/Jazzy** — `ros2 topic echo`, `ros2 node list`, lifecycle node basics; for the ROS 2 UAV State Monitor project
- **pyulog** — `ulog2csv` for converting PX4 ULog files to CSV; `ulog_info` for metadata; used in the SITL Mission Rehearsal log review step
- **Flight Review** (review.px4.io) — upload `.ulg` files and generate EKF health, vibration, and flight path plots; embed screenshots in project README
- **pytest** — `pip install pytest`; write 3–5 test functions that verify your parser or tool produces correct output on a known input; run in CI via GitHub Actions

### Step-by-Step Applied Workflow

1. **Project 1 (Telemetry Parser): Set up pymavlink and parse a SITL log** — run a SITL flight and save the MAVLink tlog file; write a Python script using `mavutil.mavlink_connection()` to open the log; filter for `HEARTBEAT`, `GPS_RAW_INT`, `ATTITUDE`, `VFR_HUD`, and `BATTERY_STATUS` messages; print a human-readable summary for each; add a `--message-type` CLI argument to filter interactively.

2. **Project 2 (SITL Mission): Build, run, log, analyze** — create a 4-waypoint mission in QGC; upload and fly in SITL; download the ULog file using QGC's log download; open in Flight Review; take a screenshot of the EKF innovation plot and the position tracking plot; embed both in the README.

3. **Project 3 (ROS 2 State Monitor): Write a subscriber node** — connect ROS 2 to SITL via MAVSDK or px4_ros_com; subscribe to `VehicleLocalPosition` and `BatteryStatus`; publish a custom `UAVStatus` message containing mode, armed state, position, altitude, and battery percentage; log a warning when battery drops below 20%.

4. **Project 4 (Parameter Diff): Load two parameter files and compare** — PX4 parameter files are tab-separated text (`Name \t Value`); write a Python script that loads two files, identifies added, removed, and changed parameters, and produces a markdown table with the diff; flag parameters whose change exceeds a safety-relevant threshold (e.g., any `EKF2_*` or `MC_*` change).

5. **Project 5 (Precision Landing Prototype): Detect an ArUco marker in a still image** — use OpenCV's `cv2.aruco.ArucoDetector` to detect a dictionary 4×4 marker; compute the 2D centroid; simulate a `LANDING_TARGET` MAVLink message with the detected pixel coordinates; do not require actual SITL integration at the beginner level — that is the intermediate version.

6. **Write the README for each project following the standard** — for each completed project: one paragraph describing what it does and why; a `Quickstart` section with copy-paste commands to run it from a fresh clone; a `Results` section with a screenshot or output sample; a `Limitations` section listing 2 things it does not handle.

### AI Integration

At the beginner level, LLMs are most useful for explaining unfamiliar APIs (pymavlink message fields, MAVLink message ID tables, ROS 2 message types) and for generating boilerplate (argparse setup, CSV output formatting, test function skeletons). The engineer's job is to direct the LLM precisely and verify the output — a hallucinated pymavlink API call will produce a confusing error, not an obvious syntax error, so verification requires actually running the code and checking against the pymavlink documentation.

Specific high-value prompts for beginner projects: "Explain what the `HEARTBEAT.base_mode` bitmask represents in MAVLink" (factual lookup, LLM is reliable); "Generate a Python argparse setup for a script that takes a log file path and an optional message type filter" (boilerplate, fast to verify); "What does `estimator_status.solution_status_flags` mean in a PX4 ULog?" (LLM may be partially correct — verify against PX4 docs).

### Case Studies

**Wing Operations Tools Team**: Wing's ground software team maintains a suite of Python tools for log analysis, mission planning, and fleet status monitoring — many of which started as beginner-level utilities (parse a MAVLink log, print battery events, compare parameter files) before being scaled to fleet infrastructure. The engineering culture of building small, correct tools and scaling them is more common in professional UAV teams than building comprehensive frameworks from scratch. A beginner Telemetry Parser is not a toy — it is the first iteration of a production tool.

**ArduPilot Mission Planner Analyzer**: ArduPilot's Mission Planner includes a log analysis tool (`Logs > Review Log`) that reads DataFlash binary logs and produces tabular and graphical summaries — functionally, a production-scale version of Project 1 and Project 2 combined. Looking at Mission Planner's open-source code base (C#, GitHub: ArduPilot/MissionPlanner) shows what the professional version of a beginner log parser looks like at maturity. This is useful context for understanding the trajectory of beginner project work.

**Garuda Aerospace Internal Tooling**: Garuda Aerospace (India's largest commercial drone operator by fleet size) uses internal Python tooling for flight log batch processing, parameter compliance checking before each flight, and fleet health monitoring. Their parameter diff tool is a production artifact that checks every vehicle's parameters against a company-approved baseline before each flight day. This is exactly Project 4's scope, deployed at production scale.

### Failure Modes & Safety

**Scope expansion mid-project**: Starting with "Telemetry Parser for 5 message types" and expanding to "comprehensive GCS replacement" mid-project is the most common beginner failure. The expansion feels productive but produces an unfinished, undocumented artifact that is worse for the portfolio than a clean, small tool. The fix: finish to the original scope, document it, then start a new project for the expanded scope.

**Not testing on a real log**: A pymavlink parser that works on a manually constructed test message but crashes on a real SITL log is not a working parser. The realistic failure mode is that real logs contain messages with malformed fields, zero-length payloads from failed transmissions, or message types the parser does not handle. Always test on a real SITL log, not just on synthetic data.

**README that describes intent, not reality**: "This tool parses all MAVLink messages" when the tool actually only handles 5 message types is a common beginner README error. Reviewers who run the tool on a different message type immediately discover the gap. Accurate scope description builds trust; overclaiming destroys it. Write what the tool actually does, not what you plan to eventually make it do.

**Missing the `requirements.txt`**: A Python project without a `requirements.txt` (or `pyproject.toml`) cannot be reproduced on another machine. This is the single most common reason a recruiter cannot run a portfolio project. Always `pip freeze > requirements.txt` after getting the project working and commit it.

### Business & Commercial Layer

Beginner-level UAV tooling skills are commercially relevant in two job categories that are often overlooked by candidates targeting flight software roles: **flight operations support** (tools for log analysis, mission planning, parameter management at fleet operators) and **UAV test engineering** (automated test infrastructure for SITL regression testing at OEMs). These roles are filled by engineers with Foundation + Core competence and strong software tooling skills — the beginner project skill set is a direct match.

In India, the rapid scaling of DGCA-registered commercial drone operators (agriculture, surveillance, delivery) is creating demand for operations support engineers who can build and maintain the Python tooling for log review, compliance checking, and fleet monitoring. This is entry-level UAV software engineering work that does not require embedded firmware experience — making it the right entry point for engineers coming from software backgrounds.

### Hiring Signal

**Beginner project portfolio for early-career UAV roles:**
- **UAV Test Engineer** — beginner-level tooling projects (log parser, parameter diff) are directly relevant to test infrastructure work; many test engineering roles are the entry point to UAV companies
- **UAV Operations Software Engineer** — SITL mission rehearsal and telemetry parsing skills are immediately applicable; Wing and Zipline hire operations support engineers who build the fleet monitoring tools
- **Junior Autopilot Software Engineer** — beginner projects demonstrate that the engineer can use the stack before being asked to modify it

**What interviewers look for in beginner project discussions:**
1. "Walk me through how your Telemetry Parser handles a message type it has not seen before. What does it do?" — tests error handling thinking
2. "You added a feature to your parameter diff tool. How did you verify it produced correct output?" — tests test discipline
3. "Your SITL Mission Rehearsal README says the demo runs on PX4 v1.14. What would break if I tried to run it on v1.15?" — tests version awareness

### Portfolio Projects

**Project 1 hardened: `mavlink-telemetry-parser`**
- Deliverables: Python CLI tool that parses a MAVLink tlog file, filters by message type, and outputs a CSV summary; includes 5 unit tests using pytest with known input-output pairs; GitHub Actions CI that runs the tests; README with Quickstart, Results (screenshot of output on a real SITL log), and Limitations
- Acceptance criteria: (1) `pip install -r requirements.txt && python parser.py sample.tlog` produces a CSV with correct values; (2) all 5 pytest tests pass in CI; (3) Limitations section lists at least 2 message types not handled and explains why

**Project 2 hardened: `sitl-mission-rehearsal`**
- Deliverables: A documented SITL mission run with: the QGC mission file (`.plan` JSON), the PX4 ULog file, a Flight Review screenshot showing GPS position tracking and EKF innovations, and a one-page log review note (what was healthy, what would have been concerning if real)
- Acceptance criteria: (1) the `.plan` file loads correctly in QGC without errors; (2) the Flight Review screenshot is labeled with callouts identifying the flight mode transitions; (3) the log review note explicitly mentions EKF innovation quality and GPS satellite count

**Project 5 hardened: `aruco-landing-target-detector`**
- Deliverables: Python script that reads a static image or camera frame, detects a 4×4 ArUco marker, draws the detected corners and ID, computes the 2D centroid, and prints the simulated `LANDING_TARGET` MAVLink message fields; includes a test image in the repo and a CI step that runs detection on it
- Acceptance criteria: (1) detection succeeds on the provided test image with correct marker ID and centroid; (2) CI runs the detection script without errors; (3) README explains what information would be needed to convert from 2D pixel centroid to 3D pose (previewing the intermediate project)

### Future Trends

- **2026**: Beginner UAV project tooling is increasingly built on MAVSDK rather than raw pymavlink; MAVSDK's type-safe API and async patterns make it the recommended beginner entry point as its Python documentation improves
- **2030**: Cloud-hosted SITL environments (GitHub Codespaces, AWS RoboMaker) eliminate the local setup barrier for beginner projects; a SITL Mission Rehearsal can be run in a browser without installing anything; the engineering value shifts entirely to the analysis and documentation
- **2035**: AI-assisted log analysis (upload a ULog, get a plain-language health report) becomes standard; the beginner project skill shifts from "how to parse a log" to "how to validate what the AI's log analysis says"
- **2045**: The specific tools change; the habit of capturing evidence and documenting honestly — established at the beginner project level — persists as the foundational engineering discipline

### Interview Questions

1. **What MAVLink message would you use to monitor whether a vehicle's EKF is healthy in real time?**
   *Answer*: `EKF_STATUS_REPORT` (MAVLink message ID 193) contains EKF health flags and variance estimates for velocity, position, and heading. In PX4 via pymavlink, you would subscribe to this message and check `flags` for the `EKF_ATTITUDE`, `EKF_VELOCITY_HORIZ`, `EKF_POS_HORIZ_ABS`, and `EKF_POS_VERT_ABS` bits. A full health check would also monitor `GPS_RAW_INT.fix_type` (should be ≥ 3 for 3D fix) and `GPS_RAW_INT.satellites_visible` (should be ≥ 6).

2. **What is the difference between a MAVLink tlog file and a PX4 ULog file?**
   *Answer*: A tlog file (`.tlog`) is recorded by QGroundControl from the MAVLink telemetry stream — it contains only the MAVLink messages that were transmitted over the radio or USB link, at the GCS-configured telemetry rates. A ULog file (`.ulg`) is recorded onboard the vehicle by PX4 at much higher rates (hundreds of Hz for IMU data) and contains the full internal state of the autopilot, including uORB topics that are never transmitted over MAVLink. For flight analysis, ULog is authoritative; tlog is useful for GCS-level event reconstruction.

3. **A parameter diff between two flights shows that `EKF2_GPS_P_NOISE` changed from 0.5 to 0.1. Should you flag this as a safety-relevant change?**
   *Answer*: Yes. `EKF2_GPS_P_NOISE` is the EKF2 assumed GPS position measurement noise in meters. Changing it from 0.5 m to 0.1 m makes the EKF treat GPS measurements as 5× more accurate than before. If the actual GPS accuracy is worse than 0.1 m (which is typical for consumer-grade GPS), the EKF will weight GPS too heavily and be too slow to compensate for GPS errors. This can cause the EKF position estimate to track GPS noise more aggressively, potentially degrading attitude estimation and position hold. Any change to EKF2 noise parameters warrants review.

4. **What is `cv2.aruco.ArucoDetector` and what inputs does it need to detect a marker in an image?**
   *Answer*: `cv2.aruco.ArucoDetector` is OpenCV's ArUco marker detection class (introduced in OpenCV 4.7, replacing the older `cv2.aruco.detectMarkers` function). It requires: (1) an `ArucoDetectorParameters` object specifying detection algorithm parameters (corner refinement method, adaptive threshold settings); (2) a `Dictionary` object specifying which ArUco marker dictionary to use (e.g., `cv2.aruco.DICT_4X4_50` for 50 unique 4×4 markers). Given these, `detector.detectMarkers(gray_image)` returns corner coordinates and IDs for all detected markers in the image.

5. **Why should a beginner project include a `requirements.txt` rather than just mentioning the required packages in the README?**
   *Answer*: A `requirements.txt` with pinned versions (`pymavlink==2.4.40`, `opencv-python==4.9.0.80`) ensures that a fresh `pip install -r requirements.txt` installs exactly the versions the project was tested with. Without it, a user who runs `pip install pymavlink` gets the latest version, which may have breaking API changes from the version used in development. A `requirements.txt` is a reproducibility contract — it converts "I assume you have the right packages" into a verified, deterministic dependency specification.

### Further Depth

- **pymavlink documentation** (mavlink.io/en/mavgen_python/) — official Python MAVLink library reference; message parsing, connection types, and message field definitions
- **MAVLink message specifications** (mavlink.io/en/messages/common.html) — complete list of common MAVLink messages with field descriptions; required reading for the Telemetry Parser project
- **PX4 ULog format documentation** (docs.px4.io/main/en/dev_log/ulog_file_format.html) — binary format specification; pyulog implements this format; reading the spec builds intuition for what the parsed data represents
- **OpenCV ArUco documentation** (docs.opencv.org/4.x/d5/dae/tutorial_aruco_detection.html) — official tutorial for marker detection; covers `ArucoDetector`, `Dictionary`, `DetectorParameters`, and pose estimation
- **MAVSDK Python Mission example** (github.com/mavlink/MAVSDK-Python/blob/main/examples/mission.py) — reference implementation for mission upload and monitoring; the starting point for Project 2 variants using MAVSDK
- **pytest documentation** (docs.pytest.org) — testing framework setup; fixture patterns for test data; parameterized tests for multiple input cases
