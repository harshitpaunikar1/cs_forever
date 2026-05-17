# MAVLink QGroundControl Missions and Telemetry

## Overview

This page focuses on the communication and operator side of the UAV stack: message semantics, missions, parameters, telemetry, and the practical importance of ground-control tooling.

## Why This Topic Matters

Real UAV debugging often happens through telemetry, message inspection, and mission review before anyone opens a control-theory notebook.

## Core Concepts

### MAVLink
- telemetry streams
- parameter protocol
- mission protocol
- command routing
- dialects and message generation

### QGroundControl
- vehicle setup
- mission planning
- MAVLink inspection
- log download
- multi-vehicle monitoring

## Decision Framework

```text
need protocol visibility -> MAVLink understanding
need operator and test workflow -> QGroundControl understanding
need automation -> Python or C++ tooling on top
```

## Hands-On Example / Mini Project

Build a mini ground-station tool that can:

- arm or disarm in simulation
- change mode
- upload a mission
- display a live telemetry summary

## Best Practices

- document packet flow
- save mission files and parameter sets
- inspect telemetry before changing code
- keep one repeatable GCS workflow

## Common Pitfalls

- treating the ground station as a black box
- not understanding message rates or units
- skipping telemetry recording during tests

## Metrics / KPIs / What to Measure

- command success rate
- telemetry completeness
- mission reproducibility
- time to isolate a link or protocol issue

## Tools Commonly Used Around This Topic

- `pymavlink`
- `QGroundControl`
- MAVLink Inspector
- telemetry logs

## Portfolio / Resume Application

One telemetry or mission tool is a strong differentiator because many students ignore the operator-facing side of the stack.

## Next Step

Continue to [UAV Dynamics Control and State Estimation](../04_Dynamics_Control_and_Estimation/01_UAV_Dynamics_Control_and_State_Estimation.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

MAVLink is the connective tissue of the open UAV stack. Every parameter change, mission waypoint, arming command, and telemetry reading flows over it. QGroundControl is the operator and developer window into the vehicle — the place where missions are built, parameters are tuned, telemetry is watched, and logs are downloaded. Engineers who treat these as black-box tools miss most of their diagnostic value; engineers who understand the protocol layer can build custom GCS tools, mission automation scripts, and telemetry pipelines.

In field operations, telemetry discipline is what separates safe, repeatable operations from operations that produce unexplained incidents. A field team that records full MAVLink telemetry logs from every flight has complete evidence for every post-incident analysis. A team that relies only on QGC's live display loses that evidence the moment the session closes.

Mission planning is also engineering, not just logistics. A well-designed mission file specifies not just waypoints but acceptance radii, flight speeds, loiter times, camera triggers, and contingency behaviors. Understanding the `MISSION_ITEM_INT` message structure — which encodes command type, frame, latitude, longitude, altitude, and parameters 1–7 — allows engineers to generate missions programmatically for survey coverage, inspection grids, or delivery routes.

### Industry Tool Stack

- **pymavlink** — Python library for constructing, parsing, and routing MAVLink messages; the primary tool for custom GCS development and mission scripting
- **MAVSDK Python** — higher-level Python SDK wrapping common MAVLink operations (upload mission, arm, offboard setpoints, telemetry subscription) in a clean async API
- **QGroundControl** — operator GCS with MAVLink Inspector for live message viewing, parameter editor, mission planner with coverage and survey modes, and log download
- **MAVProxy** — CLI GCS and MAVLink router; supports scripted missions, message rate monitoring, multi-link routing, and module plugins (`module load map`, `module load console`)
- **MAVLink message definitions** — `.xml` files at mavlink.io defining all message IDs, field names, types, and units; understanding these is required for building custom tools
- **Wireshark + mavlink-udp dissector** — network-level packet inspection for debugging link issues; use when MAVProxy/pymavlink-level inspection is not enough
- **QGC Survey and Corridor Scan** — QGC's built-in coverage mission generators for agricultural, inspection, and mapping operations; outputs `MISSION_ITEM_INT` waypoint sequences

### Step-by-Step Applied Workflow

1. **Run MAVProxy against a SITL vehicle** and observe the raw MAVLink output: `mavproxy.py --master=udp:127.0.0.1:14550 --console`. Identify the `HEARTBEAT`, `ATTITUDE`, and `GLOBAL_POSITION_INT` messages in the console output.
2. **Monitor message rates**: use `link rate` in MAVProxy to see bytes/sec and message counts per second for each message type. Identify which messages consume the most bandwidth.
3. **Upload a mission via pymavlink**: write a Python script using `pymavlink` that connects to SITL, constructs `MISSION_ITEM_INT` messages for a 4-waypoint square, uploads them with the `MISSION_COUNT` / `MISSION_ITEM_INT` / `MISSION_ACK` handshake, and verifies the upload with `MISSION_REQUEST_LIST`.
4. **Subscribe to a telemetry stream and log to CSV**: write a pymavlink script that subscribes to `ATTITUDE` at 4 Hz and `GLOBAL_POSITION_INT` at 2 Hz, prints both, and writes them to a CSV with timestamps.
5. **Change a parameter via MAVLink**: send `PARAM_SET` to change `MPC_XY_VEL_MAX` (PX4) or `WPNAV_SPEED` (ArduPilot). Confirm with a `PARAM_REQUEST_READ` that the value changed.
6. **Build a minimal custom GCS**: a Python script with a terminal UI (`curses` or `rich`) that shows live `ATTITUDE`, `BATTERY_STATUS`, and `MISSION_CURRENT` in a dashboard format; supports a single keypress to trigger RTL.
7. **Test link-loss behavior**: while SITL is executing a mission, kill the MAVProxy process. Observe in QGC what mode the vehicle transitions to and at what time — verify this against the GCS failsafe configuration.

### AI Integration

AI has natural applications in mission planning and telemetry analysis at this layer:

**Natural-language mission generation**: LLM-based tools can convert natural-language descriptions ("inspect all four sides of the building at 20 m altitude, 10 m standoff, 5 m/s") into structured waypoint sequences that are then uploaded via MAVSDK or pymavlink. This is an active area of research at robotics labs and a practical tool for non-expert operators.

**Telemetry anomaly detection**: time-series models (LSTM, transformer-based) can learn the expected relationship between `BATTERY_STATUS`, `ATTITUDE`, and `WIND_COV` messages and flag flights where the pattern deviates — indicating actuator degradation, unexpected wind, or battery cell imbalance. Fleet operators (Wing, Zipline) use similar systems at scale.

**Post-flight report generation**: LLMs can take a structured telemetry CSV and generate a plain-language post-flight report — mode transitions, max deviation from planned path, battery consumption rate, any anomalous events — faster than manual analysis. This is useful for operators who need to submit compliance logs.

### Case Studies

**Wing Delivery Operations**: Wing's delivery drone operations in Australia and the US require real-time telemetry to a remote operations center, automated mission generation for delivery routes, and post-flight log analysis for safety reporting. Their GCS infrastructure is proprietary but built on MAVLink semantics — mission upload, telemetry streaming, and parameter management are the same protocol operations described on this page.

**Garuda Aerospace Agricultural Operations**: Garuda Aerospace's agricultural drone operations in India use QGroundControl and custom mission planning tools for spray mission generation over pre-surveyed field polygons. Their operators generate survey grid missions using QGC's coverage planner, adjust spray parameters via the QGC parameter editor, and review flight logs post-mission for spray coverage verification. This is the mission planning and telemetry workflow at commercial scale in India.

**Dronecode MAVSDK Mission Scripting**: the Dronecode Foundation maintains MAVSDK as the standard high-level SDK for mission automation above MAVLink. Their example repositories (github.com/mavlink/MAVSDK-Python/tree/main/examples) demonstrate production-ready mission upload, offboard control, and telemetry subscription patterns that are used directly by integrators building commercial UAV applications.

### Failure Modes & Safety

**Link budget misconfiguration**: sending too many telemetry message subscriptions at too high a rate over a radio telemetry link (SiK radio at 57.6 kbps or RFD900 at 115.2 kbps). Symptoms are GCS disconnections, missed heartbeats, and telemetry freezes at altitude or distance. Diagnostic: use MAVProxy's `link rate` command to check bytes/sec; reduce high-rate subscriptions (`ATTITUDE` at 50 Hz is almost never needed over radio).

**Mission upload race condition**: sending the first mission waypoint before the `MISSION_REQUEST` acknowledgement arrives, causing the handshake to fail and the vehicle to retain the old mission. Always use the MAVSDK or pymavlink mission upload APIs that handle the full handshake protocol — do not implement raw MAVLink mission upload without understanding the MISSION_COUNT / MISSION_REQUEST / MISSION_ITEM / MISSION_ACK sequence.

**Parameter change without reboot**: some parameters in PX4 and ArduPilot require a reboot to take effect (sensor calibration parameters, EKF configuration). Changing them via QGC without rebooting creates a state where the displayed parameter differs from the active behavior. Always check the parameter's reboot requirement in the QGC parameter description.

**Unsaved telemetry**: relying only on QGC's live telemetry display without enabling MAVLink telemetry logging. If a flight anomaly occurs, there is no evidence to analyze post-flight. Enable GCS-side telemetry logging in QGC (Application Settings → Log Replay / Telemetry Logs) before every flight or test session.

**Mission coordinate system mismatch**: creating a mission in QGC using global (latitude/longitude) coordinates but uploading to a SITL vehicle whose origin is at a different geographic location. The vehicle will attempt to fly to the absolute coordinates from the mission file, which may be thousands of kilometers away. Verify that the mission home position matches the SITL or vehicle home position before uploading.

### Business & Commercial Layer

Mission software and GCS tooling is one of the most commercially accessible entry points in the UAV industry. Unlike firmware (which requires deep embedded knowledge) or perception (which requires ML and CV expertise), GCS and mission software development requires Python or C++ fluency, MAVLink protocol understanding, and software engineering discipline — skills that transfer from adjacent software engineering backgrounds.

The commercial applications are broad: **survey and mapping** (DJI Terra, Pix4Dcapture, QGC survey missions), **inspection** (custom GCS overlays for point cloud generation, defect tagging, and report generation), **agriculture** (spray coverage missions, variable rate prescription maps), and **delivery** (route optimization, dynamic rerouting, handoff coordination). Each of these requires building on top of the MAVLink mission and telemetry layer.

In India, the DGCA's operational requirements for BVLOS and remote operations specify telemetry logging and real-time link monitoring as compliance requirements. Engineers who can build these capabilities into GCS software are directly employable by DGCA-certified operators.

### Hiring Signal

**Job titles where MAVLink/GCS/Mission skills are primary:**
- **Mission Software Engineer (MAVLink / MAVSDK)** — at enterprise UAV operators, delivery companies, and GCS software vendors; primary job function is building mission automation, telemetry pipelines, and operator interfaces above the MAVLink layer
- **Ground Station Software Engineer** — at QGC-adjacent companies and enterprise integrators; requires Qt/QML development, MAVLink stream handling, and telemetry reliability
- **UAV Integration Engineer** — at inspection operators and enterprise deployers; requires QGC proficiency, mission planning, parameter management, and field telemetry diagnosis
- **Flight Test Operator / Engineer** — at UAV OEMs and test organizations; QGC and MAVProxy are the primary daily tools

**Specific interview screens:**
1. "Walk me through the complete MAVLink message sequence when a QGC operator uploads a 5-waypoint mission to a PX4 vehicle. Name every message type in the handshake, in order."
2. "Write a pymavlink script that connects to a SITL vehicle, subscribes to `BATTERY_STATUS`, and triggers a warning print when the battery drops below 30%. Handle the case where the vehicle is not connected."
3. "A field operator reports that QGC shows a successful mission upload but the vehicle immediately returns home when the mission starts. What are the three most likely causes and how do you diagnose each?"
4. "Explain what `MAV_FRAME_GLOBAL_RELATIVE_ALT` means for a mission waypoint altitude, and what happens if a waypoint is accidentally uploaded in `MAV_FRAME_GLOBAL` (absolute altitude) when the home position is at sea level but the field is at 1500 m MSL."
5. "Design a minimal custom GCS in Python that can: show live attitude, upload a preset mission, trigger RTL with a keypress, and save a telemetry log. What libraries do you use and what are the first 10 lines of your main loop?"

### Portfolio Projects

**Beginner: `mavlink-gcs-dashboard`**
- Deliverables: Python terminal dashboard (using `rich` or `curses`) showing live `ATTITUDE`, `BATTERY_STATUS`, `GLOBAL_POSITION_INT`, and `MISSION_CURRENT` from a SITL vehicle; color-coded health status; single-key RTL trigger
- Suggested repo tree: `README.md`, `src/gcs_dashboard.py`, `requirements.txt`, `screenshots/`
- Acceptance criteria: (1) dashboard updates at ≥ 2 Hz without user input; (2) RTL key press sends the correct MAVLink command and mode transition is visible in QGC; (3) README includes a demo screenshot

**Intermediate: `mission-scripting-library`**
- Deliverables: Python library wrapping MAVSDK that can generate rectangular survey grid missions from a center point, bearing, and dimensions; upload them to a SITL vehicle; monitor execution; and produce a CSV report of actual waypoint arrival times and positions
- Suggested repo tree: `README.md`, `src/mission_gen.py`, `src/mission_runner.py`, `tests/`, `examples/`, `reports/`
- Acceptance criteria: (1) survey grid generation is parameterizable and produces valid waypoint sequences; (2) mission runs in SITL without manual intervention; (3) CSV report contains planned vs. actual positions for all waypoints

**Advanced: `custom-operator-gcs`**
- Deliverables: web-based GCS using Flask + Leaflet (or similar) showing live vehicle position on a map, mission waypoints, battery status, and mode; supports mission upload from a drawn polygon; exportable telemetry logs in CSV
- Suggested repo tree: `README.md`, `backend/`, `frontend/`, `missions/`, `logs/`, `docs/`
- Acceptance criteria: (1) live position updates on the map at ≥ 1 Hz from SITL; (2) mission drawn and uploaded via the map UI executes correctly in SITL; (3) telemetry log downloaded from the UI is valid CSV with timestamps

### Future Trends

- **2026**: Remote ID compliance (FAA, DGCA, EASA mandates) adds a new mandatory telemetry broadcast layer that all GCS tools must handle. MAVLink's `OPEN_DRONE_ID_*` messages carry Remote ID data; GCS tools that understand and display this become compliance tools, not just developer toys.
- **2030**: BVLOS operations at scale require automated pre-flight telemetry checks, in-flight anomaly monitoring, and post-flight compliance reporting — all built on the MAVLink layer. Mission software engineers who build these systems are a key part of the regulatory certification infrastructure.
- **2035**: MAVLink 3 or its successor may replace the current framing and serialization format, but the mission and telemetry concepts remain. Engineers who understand the current protocol at the message level adapt most easily to protocol evolution.
- **2045**: Fleet-scale operations (hundreds of vehicles simultaneously) require distributed telemetry processing and mission coordination infrastructure. The MAVLink message semantics scale poorly to this; new protocols may emerge, but the engineering discipline of understanding what every message means does not.

### Interview Questions

1. **What is the MAVLink mission upload protocol, and what happens if any step in the handshake is dropped?**
   *Answer*: The uploader sends `MISSION_COUNT` (total waypoint count); the vehicle responds with `MISSION_REQUEST` for item 0; the uploader sends `MISSION_ITEM_INT` for item 0; the vehicle responds with `MISSION_REQUEST` for item 1; this continues until all items are sent; then the vehicle sends `MISSION_ACK` with `MAV_MISSION_ACCEPTED`. If any request is dropped, the uploader should retransmit the item after a timeout. If the `MISSION_ACK` is dropped, the uploader may retry the entire upload, which may cause the vehicle to clear and re-accept the mission. Incomplete uploads leave the vehicle with a partial or old mission.

2. **Explain the difference between `MAV_FRAME_GLOBAL_RELATIVE_ALT` and `MAV_FRAME_LOCAL_NED` for waypoint frames.**
   *Answer*: `MAV_FRAME_GLOBAL_RELATIVE_ALT` specifies waypoints in latitude, longitude, and altitude relative to the home position (takeoff point). A waypoint at altitude 30 means 30 m above where the vehicle armed. `MAV_FRAME_LOCAL_NED` specifies waypoints in meters North, East, and Down from the origin (also typically the arm position). GLOBAL_RELATIVE_ALT is more intuitive for operator-created missions; LOCAL_NED is used for programmatic setpoints in offboard control. Confusing the two when building custom tools can result in wildly incorrect waypoint altitudes.

3. **How would you diagnose a MAVLink telemetry link that works at short range but fails at 300 m distance?**
   *Answer*: First, check the radio hardware: SiK radio RSSI (visible in QGC's toolbar) — if RSSI drops below -100 dBm at 300 m, the radio link is the issue. Check antenna orientation (omnidirectional vs. directional), gain, and interference. Second, check message rate: if RSSI is adequate but telemetry still fails, the link may be saturated — reduce subscription rates. Third, check MAVProxy's `link rate` output. Fourth, test with a different radio channel if 2.4 GHz ISM band interference is suspected. Finally, verify serial baud rate matches between the radio and the autopilot UART.

4. **Write pseudocode for the mission waypoint generation algorithm for a rectangular survey grid given center lat/lon, heading, width, height, and row spacing.**
   *Answer*: (1) Compute corner positions by projecting width/2 and height/2 from the center in the heading direction and its perpendicular. (2) Generate row start/end pairs by sweeping from one side to the other in steps of `row_spacing`. (3) Alternate row direction for a boustrophedon (lawn-mower) pattern. (4) Project each row point from the local Cartesian grid back to lat/lon using a flat-earth approximation valid for small areas (< 50 km). (5) For each point, create a `MISSION_ITEM_INT` with `MAV_CMD_NAV_WAYPOINT`, the computed lat/lon, the specified survey altitude, and the desired acceptance radius and speed parameters.

5. **What is the GCS failsafe in PX4 and how is it configured?**
   *Answer*: The GCS failsafe triggers when the GCS heartbeat is lost for longer than `COM_DL_LOSS_T` seconds (default 10 s). The response is configured by `NAV_DLL_ACT`: 0 = disabled, 1 = Hold, 2 = RTL, 3 = Land, 5 = Terminate (immediate motor stop). The failsafe is separate from the RC failsafe and the OFFBOARD failsafe; all three can be configured independently. In typical field operations, `NAV_DLL_ACT = 2` (RTL) is the safest choice. The failsafe only applies when the vehicle is flying — if it is on the ground, losing the GCS link does not trigger the failsafe.

### Further Depth

- **MAVLink Developer Guide** (mavlink.io/en/) — message definitions, serialization format, and dialect documentation
- **pymavlink source and examples** (github.com/ArduPilot/pymavlink) — the primary Python MAVLink library; `examples/` directory contains mission upload, parameter change, and telemetry subscription scripts
- **MAVSDK Python Documentation** (mavsdk.mavlink.io/main/en/python/) — mission scripting, offboard control, and telemetry subscription examples
- **QGroundControl Source Code** (github.com/mavlink/qgroundcontrol) — Qt/QML codebase; the `src/MissionManager/` directory shows how QGC implements the mission upload protocol
- **MAVLink Mission Protocol** (mavlink.io/en/services/mission.html) — the authoritative specification for the mission upload and download handshake
- **Dronecode Forum** (discuss.px4.io) — active community for MAVLink, MAVSDK, and QGC integration questions
