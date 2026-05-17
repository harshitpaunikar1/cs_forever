# Projects

## Overview

Projects are where this curriculum stops being aspirational and becomes inspectable engineering work. A UAV project proves that you can integrate simulation, autopilot software, telemetry, logs, mission tooling, and documentation into one coherent system.

The project paths are split by difficulty so you can choose a starting point that is ambitious without becoming vague or unfinishable.

## How To Use the Project Paths

### Beginner
Choose this if you are still building confidence with SITL, telemetry, and small tools.

### Intermediate
Choose this if you can already run simulation cleanly and want deeper integration with ROS 2, MAVLink, or control logic.

### Advanced
Choose this if you want an embedded, multi-vehicle, fixed-wing, or autonomy-heavy capstone.

## Quality Bar for Every Project

Every project should include:

- a short design note or README
- setup and run instructions
- tests or clear verification steps
- logs, screenshots, plots, or architecture diagrams
- one limitations section and one next-steps section

## Next Step

Choose one of the paths:

- [Beginner Project Path](Beginner/01_Beginner_Project_Path.md)
- [Intermediate Project Path](Intermediate/01_Intermediate_Project_Path.md)
- [Advanced Project Path](Advanced/01_Advanced_Project_Path.md)

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

UAV project work is the mechanism by which self-study converts into hiring credibility. The transition happens at the point where a project moves from "I followed a tutorial and it ran" to "I designed a system, validated it against measurable criteria, understood its failure modes, and can defend every decision I made." The Projects section of this curriculum defines that standard explicitly so that learners have a clear target, not a vague sense that they should "do more."

In practice, UAV engineering hiring teams use portfolio projects as a proxy for on-the-job performance in two ways. First, technical correctness: does the project demonstrate that the engineer understands the underlying systems (PX4 architecture, MAVLink protocol, ROS 2 communication model, EKF state estimation) deeply enough to have made non-obvious design choices? A project that uses the default parameters for everything and follows a tutorial exactly tells the hiring manager nothing. A project that documents why specific parameters were chosen, what the alternative was, and what tradeoff was made is evidence of engineering judgment.

Second, production discipline: does the project include logs, metrics, safety assumptions, and failure modes? An engineer who builds a precision landing system and can show you the distribution of landing errors across 50 SITL trials, with the wind conditions specified for each trial, and three identified failure modes they tested and three they did not, is demonstrating the operational rigor that production UAV programs require.

The three project paths in this section are calibrated to real hiring benchmarks: beginner projects demonstrate that the engineer can set up and use the UAV software stack; intermediate projects demonstrate that they can integrate multiple components into a coherent system; advanced projects demonstrate that they can design and validate a system with production-grade discipline.

### Industry Tool Stack

- **PX4 SITL + Gazebo** — the primary simulation environment for all project paths; version-pin both PX4 and Gazebo in the project README
- **MAVSDK Python** — the recommended SDK for mission scripting projects at beginner and intermediate levels; async Python patterns, `System()`, `Mission`, `Offboard`, `Telemetry` APIs
- **pymavlink** — for lower-level MAVLink projects where MAVSDK's abstraction is too high; direct message construction and parsing
- **ROS 2 Humble/Jazzy** — for intermediate and advanced projects involving sensor integration, perception, or multi-node architectures; namespace your nodes for portability
- **OpenCV** — for perception-based projects (ArUco detection, optical flow, camera calibration); `cv2.aruco`, `cv2.solvePnP`, `cv2.calibrateCamera`
- **pyulog** — required for every project that captures flight logs; post-flight metric extraction and log comparison
- **pytest + GitHub Actions** — recommended test framework for SITL smoke tests; GitHub Actions free tier runs CI on open repos; a passing CI badge signals reproducibility
- **Docker** — for packaging the development environment so the project is reproducible outside the author's machine; Dockerfile in the repo root with `docker run` instructions in the README
- **mkdocs or Sphinx** — for advanced projects that warrant structured documentation beyond a README; generates a browsable docs site from Markdown or RST
- **PlotJuggler or Flight Review** — for generating log screenshots used in project documentation and portfolio; a Flight Review plot embedded in the README is a strong quality signal

### Step-by-Step Applied Workflow

1. **Choose a project based on your current demonstrated capability, not your aspirational capability** — if you cannot reliably run a 4-waypoint PX4 SITL mission, an intermediate project will expose gaps rather than build on them. Assess honestly by running the gating skill for each level before choosing.

2. **Write the design document before writing any code** — what problem does this project solve, what approach will you use, what are the acceptance criteria, what are three known limitations going in? This forces clarity about scope and prevents scope creep once you start building.

3. **Set up CI first** — create `.github/workflows/ci.yml` that runs a smoke test (at minimum: the project builds without errors from a fresh clone) before writing project-specific code. This ensures CI is never an afterthought.

4. **Build to the minimal acceptance criteria first** — get the basic behavior working before adding features. A precision landing system that reliably detects an ArUco marker and lands within 1 m in SITL is complete for a beginner project; add wind simulation and outdoor lighting only after the baseline works.

5. **Capture logs before optimizing** — run the baseline with logging enabled and save the ULog file. This is your before-measurement. Without it, you cannot demonstrate that any subsequent changes improved anything.

6. **Test failure cases explicitly** — for each project, define at least 2 failure injection tests: what happens when GPS is disabled mid-mission, when the ArUco marker is out of frame during the landing approach, when the battery voltage drops below threshold during a waypoint mission. Run them. Document the results.

7. **Write the safety assumptions document** — list what must be true for the project to work as shown. This is the hardest document to write honestly because it requires naming things you are not sure about. An honest limitations section is worth more than a polished demo.

8. **Generate the metrics report** — compute at least 3 quantitative metrics from the log and put them in a `results/metrics.md` file: landing error in meters, maximum altitude deviation, EKF innovation RMS, mission completion time, or whatever is relevant to your project's acceptance criteria.

### AI Integration

AI tools provide differentiated value at each project tier. At the beginner level, LLMs can explain PX4 log messages that are unfamiliar, suggest debugging approaches for common SITL setup errors, and help draft a README or design document from a bulleted outline. At the intermediate level, AI tools can generate boilerplate code for MAVSDK mission scripting patterns, suggest test case structures for SITL integration testing, and draft the safety assumptions document from a description of the project's design. At the advanced level, GitHub Copilot and Cursor accelerate C++ development for custom PX4 modules or ROS 2 nodes, but the safety-critical logic must be written and reviewed by the engineer — AI-generated autopilot code is not production-safe without explicit review.

The meta-skill is using AI to accelerate scaffolding (CI configuration, boilerplate, documentation structure) while investing the saved time in the technical content that cannot be delegated: understanding why the EKF behaves a specific way, designing the coordinate frame chain for a perception pipeline, reasoning about failure modes at the system level.

### Case Studies

**Skydio Engineering Internship Project Standards**: Skydio's internship program expects interns to produce projects that meet professional quality standards — reproducible, documented, with quantitative results. Interns who arrive with portfolio projects at or above this standard are more effective from day one because they already understand the engineering discipline. The most common gap in UAV intern portfolios at companies like Skydio is not technical knowledge — it is evidence collection and failure analysis. Interns who have done one project with genuine failure injection testing are meaningfully ahead of those who have only done happy-path demos.

**PX4 Google Summer of Code Projects**: The PX4 organization participates in Google Summer of Code annually, producing student projects that are evaluated by PX4 maintainers. The projects that become upstreamed (merged to PX4 main) share common properties: they defined acceptance criteria before starting, they included SITL test evidence, and the students iterated on maintainer feedback. These projects are public on GitHub and serve as concrete examples of the quality bar for Advanced-tier portfolio projects.

**ideaForge Q-Series VTOL Development Timeline**: ideaForge's engineers described their internal project structure in conference talks at IASC (Indian Aeronautical Society Conference): each subsystem (autopilot integration, BVLOS telemetry, landing system) is treated as an internal portfolio project with defined acceptance criteria, a SITL validation phase, and a hardware validation phase with log evidence. This mirrors the beginner → intermediate → advanced progression in this section, scaled to a professional team. Their internal standard for "hardware-ready" aligns with what this curriculum calls "advanced project" quality.

### Failure Modes & Safety

**Choosing a project scope that is too large**: The most common beginner project failure is choosing a scope (multi-vehicle swarm, full SLAM navigation, custom fixed-wing controller) that requires Advanced-tier foundation before it is achievable. The project stalls, produces nothing presentable, and wastes weeks. The fix: define the minimum viable version of the project (what is the smallest coherent thing this could be?) and complete that version before expanding scope.

**No version pinning**: A project that works on PX4 main as of the day it was built but has no version constraint will silently break when PX4 is updated. A recruiter who clones the repo 3 months later and cannot run it draws the conclusion that the project was never really working. Always pin: `git checkout v1.15.0` or specify the commit hash; document this in the README.

**Metrics without baselines**: Stating "landing error was 0.35 m" is meaningless without context — is that good or bad for this system? Metrics are only meaningful relative to a specification (target: < 0.5 m) or a comparison (before tuning: 0.8 m, after tuning: 0.35 m). Every metric should have a reference point.

**Safety assumptions that are actually safety claims**: Writing "the system safely handles GPS denial" in a safety assumptions document when you have not tested GPS denial is an error. Safety assumptions state what must be true for the system to work, not what the system can handle. "GPS denial handling is not tested; behavior under GPS denial is unknown" is the correct form if you have not tested it.

**No `next steps` section**: A project without a next steps section looks abandoned rather than complete. "What would make this better" is a signal that the engineer understands the limits of their work and has a plan for addressing them — a positive hiring signal, not an admission of failure.

### Business & Commercial Layer

The commercial UAV market is creating demand for engineers who can demonstrate product-level discipline in their portfolio work. The transition from "hobbyist UAV community" to "professional UAV engineering community" has raised the baseline — a PX4 SITL tutorial completion is table stakes, not a differentiator. Projects built to the standards in this section are the differentiator.

In India specifically, the startup funding landscape for drone companies (2024–2026 wave: ideaForge, Garuda Aerospace, Omnipresent Robotics, AgriDrones India) means that early-stage hiring is happening rapidly and teams are small. Engineers who arrive with portfolio projects that demonstrate production discipline are immediately useful on day one — they do not require mentorship in the basics of simulation-first development, log analysis, or safety assumption documentation. This is a rare and valuable quality in a small team.

For university students in aerospace or computer science engineering programs in India, the Projects section of this curriculum provides a structured path to portfolio projects that are significantly more sophisticated than typical final-year projects — and therefore significantly more differentiated in job applications.

### Hiring Signal

**How projects are used in UAV hiring interviews:**
- **Technical screen**: the interviewer reviews your project repo before the call; the interview focuses on questions your project raises, not generic knowledge questions — "I see you used an EKF2-based position estimate for your precision landing. What were the innovation statistics for the EKF during the landing approach?" This is why logs and metrics in the repo matter.
- **Whiteboard extension**: "Given your precision landing project, how would you extend it to handle 5 m/s crosswind? What would you change in the controller and what would you test?" Advanced project experience gives you something to extend.
- **Pair debugging**: "Here is a ULog from a similar precision landing system with a problem. Walk me through your diagnostic process." Having analyzed your own logs prepares you for this.

**Specific signals that distinguish tier levels:**
- **Beginner project**: demonstrates the engineer can set up and use the stack; adequate for internship applications and junior roles
- **Intermediate project**: demonstrates integration and debugging competence; competitive for junior/associate engineer roles at commercial UAV companies
- **Advanced project**: demonstrates system design, validation discipline, and production readiness; required for mid-level roles at Wing, Zipline, Skydio, or equivalent

### Portfolio Projects

**The portfolio IS the project section**: This section's deliverables are the beginner, intermediate, and advanced project paths themselves. Each is defined in detail in the sub-pages. The three-level structure maps to three hiring tiers — choose the highest level where you can produce complete, honest work.

**Cross-section portfolio coherence**: The strongest portfolios show a coherent technical narrative: a beginner SITL mission project that scales up to an intermediate precision landing project that scales up to an advanced multi-vehicle landing coordination project. Interviewers who see this progression understand that the engineer builds systematically, not randomly.

**Minimum portfolio for a competitive application:**
- One project at the intermediate level or higher, fully hardened (safety assumptions, metrics, failure modes, CI badge)
- One upstream contribution attempt (merged or documented attempt)
- A GitHub profile that makes it easy to find both of the above in 2 minutes

### Future Trends

- **2026**: Video demos on YouTube become expected rather than impressive; the differentiator shifts to quantitative log evidence and CI-verified reproducibility — what you can prove, not what you can show
- **2030**: AI-assisted project scaffolding (GitHub Copilot, Cursor) reduces the time to produce a working prototype by 50%; the engineering value shifts entirely to the design, validation, and safety analysis that AI cannot automate
- **2035**: UAV engineering portfolio reviews may include live system operation (similar to how flight test evaluations are conducted) — "here is a SITL environment, debug this vehicle" in the interview rather than reviewing pre-built work
- **2045**: The specific software stack (PX4, ROS 2, MAVSDK) is replaced by systems yet to be built; the portfolio discipline — design first, measure everything, document honestly — remains unchanged

### Interview Questions

1. **What is the difference between a beginner UAV project and an intermediate one?**
   *Answer*: A beginner project demonstrates correct use of the stack: the engineer can set up SITL, run a mission, connect a GCS, and capture a log. An intermediate project demonstrates integration and diagnosis: the engineer has connected multiple components (e.g., ROS 2 + PX4 SITL + MAVSDK), encountered and resolved a non-trivial technical problem (e.g., coordinate frame mismatch between ROS 2 ENU and PX4 NED), and produced quantitative evidence that the integrated system works. The key test: in a beginner project, the engineer followed a tutorial; in an intermediate project, the engineer had to solve a problem the tutorial did not address.

2. **What does a `results/metrics.md` file in a UAV portfolio project signal to a hiring manager?**
   *Answer*: It signals that the engineer understands the difference between "it worked" and "it worked within specification." Metrics force the engineer to define what success means before measuring it, which is a core engineering discipline. A metrics file with a 0.35 m landing error across 50 SITL trials under 0–5 m/s wind tells the hiring manager: the engineer ran enough trials to compute a distribution, not just a single cherry-picked result; they tested under varying conditions; they have a standard (the 50-trial threshold) that is repeatable.

3. **Why is a project limitations section a positive signal, not a weakness?**
   *Answer*: Because it demonstrates self-awareness, technical depth, and honesty — three properties hiring managers prize. An engineer who writes "this system has not been tested under GPS-denied conditions; behavior in GPS-denied environments is unknown" is demonstrating that they understand what GPS denial is and that it is a meaningful failure mode — this is more impressive than an engineer who does not mention it because they did not think about it. A missing limitations section suggests either the engineer does not know the limitations (bad) or is hiding them (worse).

4. **How does a CI badge on a portfolio project repo change how a hiring manager perceives it?**
   *Answer*: A CI badge shows that the project builds and passes its tests on an independent machine (GitHub Actions), not just on the author's laptop. This is the minimum bar for "reproducible." Without it, the hiring manager must assume the project may not run in any environment other than the one it was built in. A green CI badge is not a high bar — but its absence is a red flag. The presence of a well-configured CI pipeline also signals that the engineer understands automated testing, which is a required skill in any production engineering role.

5. **What is the recommended scope for a beginner UAV portfolio project?**
   *Answer*: A 4-waypoint SITL mission with MAVSDK, complete with: a README explaining what it does and how to run it, a log file showing a successful run with the EKF innovation plot visible in Flight Review, a metrics file with 3 quantitative results (mission completion time, max altitude error, GPS satellite count throughout), a safety assumptions document listing 3 tested conditions and 2 untested ones, and a CI badge. This scope is achievable in a weekend of focused work once SITL is set up, is technically honest about what simulation can demonstrate, and shows the production discipline that differentiates it from a tutorial follow-through.

### Further Depth

- **PX4 SITL documentation** (docs.px4.io/main/en/simulation/) — setup guides for Gazebo, JSBSim, and multi-vehicle SITL; version-specific instructions
- **MAVSDK Python examples** (github.com/mavlink/MAVSDK-Python/tree/main/examples) — reference implementations for mission, offboard, telemetry, and multi-vehicle patterns
- **PX4 Flight Review** (review.px4.io) — upload logs here to generate EKF health and flight path visualizations for portfolio documentation
- **GitHub Actions for Python** (docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-python) — CI setup guide; adapt for SITL smoke tests
- **pyulog** (github.com/PX4/pyulog) — log parsing for metric extraction; `ulog2csv` for CSV export, `ULog` class for programmatic access
- **"The Pragmatic Programmer" — Thomas and Hunt** — general engineering discipline reference; the concepts of "tracer bullets" (minimum viable working system) and "don't assume, prove it" apply directly to UAV project work
