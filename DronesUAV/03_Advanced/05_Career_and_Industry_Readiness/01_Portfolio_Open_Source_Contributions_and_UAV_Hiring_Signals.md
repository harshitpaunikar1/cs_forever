# Portfolio Open Source Contributions and UAV Hiring Signals

## Overview

This page turns the roadmap into employability. The goal is to present work in a way a hiring manager can evaluate quickly and trust.

## What Employers Notice

- clean repos
- reproducible builds
- logs and metrics
- architecture diagrams
- upstream contributions
- clarity about what is simulated versus hardware-backed

## What Matters Most

- one autopilot deeply
- strong `C++`
- practical `Python`
- ROS 2 competence
- simulation-first workflow
- finished systems, not half-built ideas

## What Matters Less Than Students Think

- certificates
- jumping to deep learning too early
- learning every autopilot at once
- spending months in low-signal side tools first

## Best Portfolio Targets

1. flight-stack integration project
2. telemetry or mission tooling project
3. perception or precision-landing project
4. simulation or JSBSim project
5. one upstream contribution

## Resume Translation

Write bullets that emphasize:

- built
- integrated
- debugged
- measured
- documented

Avoid bullets that only say:

- completed
- learned
- followed

## Next Step

Move to [Projects](../../04_Projects/00_Overview.md).

---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

Career readiness in UAV engineering is not about credentials — it is about demonstrated capability in the form of reproducible artifacts that a technical hiring manager can evaluate in 20 minutes. The gap between engineers who get hired at Wing, Skydio, or ideaForge and engineers who do not is almost never about coursework completion or certifications. It is about whether the engineer's portfolio contains work that a senior engineer recognizes as technically honest, reproducible, and representative of the actual job.

Portfolio hardening — the process of converting demo-grade work into evidence-grade work — is the core activity of this section. A demo-grade artifact shows that something worked once under favorable conditions. An evidence-grade artifact shows that something works reproducibly under defined conditions, with measurements that support or contradict the claims made about it, and honest documentation of what was not tested.

Upstream contribution to PX4, ArduPilot, MAVSDK, or ROS 2 is the most powerful portfolio signal available to a UAV engineer. A merged PR demonstrates: (1) technical competence sufficient to understand and modify a professional codebase; (2) communication skill sufficient to get a PR through code review; (3) judgment sufficient to choose a contribution that the community wanted; and (4) persistence sufficient to address review feedback and iterate to merge. None of these properties are demonstrated by a self-contained personal project.

The trajectory from first contribution to recognizable community member takes 6–18 months of consistent effort. The fastest path is: find a `good first issue` on PX4 or ArduPilot GitHub, reproduce it in SITL, write a minimal fix, write a regression test if applicable, and submit. The community is generally welcoming to engineers who have done the work to understand the issue before submitting a solution.

### Industry Tool Stack

- **GitHub** — the surface where upstream contributions happen; pull requests, issue tracker, code review; PX4 is at github.com/PX4/PX4-Autopilot; ArduPilot at github.com/ArduPilot/ardupilot; MAVSDK at github.com/mavlink/MAVSDK
- **Git branching workflow** — fork → feature branch → PR → review → merge; squash commits before PR; rebase on main regularly; conventional commit message format (`fix:`, `feat:`, `docs:`) for PX4 submissions
- **PX4 CI system** — GitHub Actions runs unit tests, SITL integration tests, and build checks on every PR; understanding why a CI failure is blocking is a required skill; logs are public on GitHub Actions
- **Dronecode Forum (discuss.px4.io)** — where PX4 contributions begin; search for the issue, discuss the approach, get maintainer buy-in before spending a week writing code
- **ArduPilot developer mailing list (ardupilot-discuss@googlegroups.com)** — equivalent community channel for ArduPilot contributions; long threads with technical depth
- **Portfolio hosting** — GitHub for code; a personal site (GitHub Pages, Notion, or a lightweight static site) for narrative portfolio with embedded log screenshots and metrics; video demos on YouTube (unlisted or public)
- **Resume LaTeX/Markdown** — PDF resume for applications; Markdown version in repo for easy updating; keep it to 1 page for < 5 years experience
- **LinkedIn** — where recruiters at Wing, Zipline, Skydio, and ideaForge search for candidates; ensure skills (PX4, ROS 2, MAVSDK, C++17, UAV) are in the Skills section and endorsed; connect with engineers at target companies
- **PlotJuggler + Flight Review** — portfolio projects should include log screenshots from these tools as evidence; a repo README with a Flight Review screenshot showing a clean EKF innovation plot signals that the engineer reads their own logs

### Step-by-Step Applied Workflow

1. **Audit your existing portfolio against a hiring manager checklist** — for each project: (a) does it have a README with a one-paragraph description of what it does? (b) does it build from a fresh clone with documented steps? (c) does it include a log or metric showing it worked? (d) does it state what conditions were tested and what was not? Grade each project pass/fail; the fails are the work items.

2. **Harden one project to evidence grade** — pick your strongest existing project; add: a `docs/safety_assumptions.md`, a `results/metrics.md` auto-generated from the log, a `docs/failure_modes.md` listing at least 3 failure cases (tested or not), and a CI badge (GitHub Actions running a smoke test). Update the README to include a Quickstart that a stranger can follow.

3. **Write three portfolio narrative bullets** — for each of your three best projects, write a 3-sentence resume bullet: sentence 1 = what you built and what technical approach you used; sentence 2 = how you tested it and what the measured outcome was; sentence 3 = what this demonstrates about your engineering judgment. Test: read it as if you are a senior engineer who has never met you. Does it tell you anything specific?

4. **Find one upstream contribution opportunity** — go to github.com/PX4/PX4-Autopilot/issues and filter by `good first issue` and `help wanted`; read 10 issues; pick one you can reproduce in SITL; reproduce it; write one sentence in the issue thread confirming you can reproduce it and proposing your fix approach.

5. **Implement and submit the contribution** — fork PX4, create a feature branch, implement the fix, run the CI locally (`make tests`), write a minimal test if applicable, push, and open a PR with a description following PX4's PR template; be explicit about what you tested and what you did not.

6. **Iterate through code review** — respond to every reviewer comment within 24 hours; treat review comments as questions the reviewer is asking you to answer, not criticisms to defend against; update the PR until it passes CI and reviewers approve; getting to merge takes patience.

7. **Document the contribution for your portfolio** — whether or not the PR merges, document it: what the issue was, what your investigation found, what your fix did, what feedback you received, and what you would do differently. A PR that was closed with good feedback is still a portfolio signal — it shows you attempted a real contribution.

8. **Prepare for a technical screen** — for each project in your portfolio, prepare to: (a) walk a technical interviewer through the architecture in 5 minutes, (b) explain one specific bug you hit and how you diagnosed it, (c) state one thing the demo does not handle and what you would do to address it. Practice these verbally, not just in writing.

### AI Integration

AI tools have specific, bounded utility in portfolio and career work. LLMs are good at: (1) drafting initial README text from a bullet list of what the project does — the engineer must verify technical accuracy; (2) improving resume bullet phrasing — the engineer must ensure the bullets accurately reflect the work; (3) preparing for behavioral interview questions by generating likely follow-up questions and letting the engineer practice responses; (4) explaining unfamiliar code in a PR before contributing — LLMs can explain what a PX4 module does at a high level, reducing the time to understand a new codebase.

LLMs are poor at: (1) generating accurate technical content for safety assumptions or failure mode documents — these require engineering knowledge of the specific system; (2) writing code contributions that will pass PX4 code review — PX4's codebase has specific patterns, style requirements, and safety constraints that LLMs frequently violate; (3) assessing whether a portfolio project is actually good — LLMs cannot evaluate whether a technical approach is correct or whether a log shows healthy flight behavior.

The productive use pattern: LLM for communication artifacts (README, resume, PR description), engineer for technical content (safety assumptions, failure modes, code logic, log interpretation).

### Case Studies

**Tridge (Andrew Tridgell) and ArduPilot Upstream Culture**: Andrew Tridgell (creator of Samba, rsync) is also the primary maintainer of ArduPilot. His approach to code review in the ArduPilot community is well-documented: thorough, technical, and focused on whether the proposed change actually improves the system's reliability. Engineers whose contributions are merged by Tridge have a career credential that is recognized globally by aerospace and defense UAV hiring teams. The ArduPilot community is one of the most active open-source aerospace engineering communities, with weekly dev calls documented on YouTube and a transparent code review process on GitHub.

**Auterion's Upstream-First Engineering Culture**: Auterion has built their entire business on PX4 and is one of the largest contributors to PX4 upstream. Their engineering policy is explicit: features should be developed upstream in PX4 first, not in a private fork, because maintaining a private fork diverges from the community over time and becomes a liability. Engineers at Auterion who contribute to PX4 upstream are therefore directly serving both Auterion's commercial interest and the community. This is the commercial case for upstream contribution — it is not purely altruistic.

**ideaForge Portfolio to Product**: ideaForge's engineering team built their internal capabilities through a combination of PX4 customization for specific Indian regulatory requirements and upstream contribution where their changes were generalizable. Their Q-series VTOL platform uses a custom PX4 fork for mission-critical changes (fuel cell integration, custom failsafes for DGCA BVLOS operations) but contributes general improvements upstream. This represents the mature commercial model: fork minimally, contribute generously.

### Failure Modes & Safety

**Portfolio breadth without depth**: Building 7 projects that each demonstrate 60% completion is worse than building 3 projects that demonstrate 95% completion. Hiring managers at Wing or Skydio are evaluating whether you can finish things — a half-built precision landing system tells them you cannot. The most common portfolio failure is accumulating breadth to appear impressive rather than depth to appear trustworthy.

**Claiming work you cannot defend**: If you list "built a PX4 EKF state estimator" on a resume and the interviewer asks you to explain the innovation gate calculation, you need to be able to do it. Over-claiming in portfolio narratives is immediately exposed in technical screens. The correct approach is precise scoping: "integrated PX4 EKF2 for GPS-denied operation using a downward optical flow sensor, validated in SITL with GPS disabled" is defensible; "worked on EKF" is not.

**Not tracking PX4 version in portfolio projects**: A SITL demo that worked on PX4 v1.13 may not work on PX4 v1.15. If a recruiter tries to clone your repo and run it and it fails because of a version mismatch, this is a significant negative signal — it means you do not understand reproducibility. All portfolio projects must specify the PX4 version, Gazebo version, and ROS 2 version used, and ideally provide a Docker container or installation script that reproduces the environment.

**Submitting an upstream PR without reading the contributor guide**: PX4's and ArduPilot's contributor guides specify code style (clang-format for C++, specific naming conventions), commit message format, PR description requirements, and test evidence requirements. A PR that ignores these conventions is immediately identified as a first-time contributor who did not do the homework. Reading the contributor guide before writing a single line of code is the baseline.

**Treating upstream contribution as a numbers game**: A portfolio with 10 trivial PRs (typo fixes, unused variable removals) is worth less than one substantive PR that fixes a real bug or adds a genuinely useful feature. The contribution should be chosen for its technical merit — something that other developers want — not for adding a PR count to a resume.

### Business & Commercial Layer

The market for skilled UAV software engineers has a clear tiered structure. Foundation + Core competence is becoming commoditized by the proliferation of online courses, YouTube tutorials, and accessible hardware (Pixhawk, ROS 2 on Raspberry Pi). Advanced specialization — in any of the five Advanced-tier domains — remains scarce because it requires sustained engagement with complex, real engineering problems that online courses do not produce.

Career positioning in 2026 requires demonstrating at least one Advanced-tier specialization alongside a solid Core foundation. The specific Advanced specialization should align with the target company's engineering focus: embedded firmware depth for Holybro, Cube Pilot, or ideaForge hardware teams; GNC/FDM depth for eVTOL companies (Joby, Archer); fleet software depth for Wing or Zipline; safety case depth for BVLOS-certified operators; swarm coordination depth for defense UAV companies.

In India, the combination of PX4 depth + DGCA regulatory awareness is a differentiating profile that very few engineers currently hold. As DGCA BVLOS certification scales, this combination will be in demand specifically at Indian UAV OEMs and operators — a career opportunity that requires positioning now.

### Hiring Signal

**Job titles that specifically reward portfolio-and-contribution signals:**
- **Senior UAV Software Engineer** — at Wing, Zipline, Skydio; expects upstream contribution history, reproducible portfolio projects, and ability to explain technical decisions under examination
- **Autopilot Firmware Engineer (PX4)** — at Auterion, Holybro, Cube Pilot; upstream PX4 contribution is the strongest possible signal for this role
- **UAV Autonomy Engineer** — at Skydio, Shield AI; expects demonstrated autonomy stack work with measured performance, not just theoretical knowledge
- **Mission Software Engineer (MAVLink/MAVSDK)** — at ground software companies and fleet operators; expects open-source contribution to MAVSDK or pymavlink alongside portfolio mission scripting projects
- **GNC Engineer** — at eVTOL companies; expects simulation-validated control law work with measured performance against defined metrics, not just "implemented PID"

**Specific interview screens for career-readiness focused evaluation:**
1. "Walk me through your most technically complex portfolio project. What was the hardest debugging problem you hit? How did you diagnose it? What did you learn?"
2. "You have 3 hours to contribute something useful to PX4 today. What issue would you look at first and why? What would your investigation process look like?"
3. "Read this PX4 flight log. Tell me whether the EKF was healthy during the entire flight, whether there were any mode transitions that should not have happened, and whether you would feel comfortable flying this vehicle again tomorrow."
4. "A senior engineer reviewing your PR says your fix is correct but the test coverage is insufficient. What does sufficient test coverage mean in the context of a PX4 autopilot change, and what would you add?"
5. "Describe a technical decision you made in one of your projects that you would make differently now. What did you learn that changed your view?"

### Portfolio Projects

**Beginner: `portfolio-audit-and-hardening`**
- Deliverables: A documented audit of your existing 3+ portfolio projects against a 10-item checklist (README completeness, reproducible build, log evidence, metrics, failure modes, safety assumptions, version pinning, CI badge, architecture diagram, honest limitation statement); for each project that fails 3+ checklist items, a specific remediation plan with tasks
- Suggested repo tree: `README.md`, `docs/portfolio_audit.md`, `docs/remediation_plan.md`, `checklists/portfolio_checklist.md`
- Acceptance criteria: (1) the audit correctly identifies specific checklist failures for each project (not generic "needs improvement"); (2) the remediation plan has specific tasks, not goals ("add `docs/safety_assumptions.md` listing 3 tested conditions and 2 untested conditions" not "improve documentation"); (3) at least one project is fully hardened based on the remediation plan before the audit document is committed

**Intermediate: `upstream-contribution-attempt`**
- Deliverables: A documented attempt at an upstream contribution to PX4, ArduPilot, or MAVSDK — either a merged PR or a closed PR with a post-mortem explaining what happened; includes: the issue chosen and why, the investigation findings, the fix or proposed fix, the CI output, any review feedback received, and a reflection on what was learned
- Suggested repo tree: `README.md`, `docs/issue_investigation.md`, `docs/fix_rationale.md`, `docs/review_feedback.md`, `docs/reflection.md`, (link to the actual GitHub PR)
- Acceptance criteria: (1) the issue is real (a GitHub issue link is provided, not a fabricated problem); (2) the investigation document shows evidence of actually running the code (SITL output, log snippet, or build error) — not just reading the issue description; (3) the reflection is honest about what went wrong (review rejection, approach error, scope misjudgment) if the PR was not merged

**Advanced: `career-ready-portfolio-package`**
- Deliverables: A fully production-hardened portfolio: 3 projects each with complete documentation (README, safety assumptions, failure modes, metrics, CI badge, version pinning); one upstream merged PR; three polished resume bullets following the "built / tested / demonstrates" format; a personal portfolio site or GitHub profile README that surfaces all three projects with one-paragraph narratives; a 15-minute rehearsed technical walkthrough of the strongest project
- Acceptance criteria: (1) all three projects build from a fresh clone in a documented environment with no errors; (2) the upstream PR is merged (not just submitted); (3) the 15-minute walkthrough was practiced with at least one person who gave feedback, and the feedback was incorporated

### Future Trends

- **2026**: AI-assisted code review tools (GitHub Copilot code review, Cursor) become standard in PX4 and ArduPilot CI; contributors who do not use these tools work slower than those who do; the barrier to a technically clean first PR drops slightly
- **2030**: UAV engineering becomes a licensed engineering profession in some jurisdictions (analogous to PE licensure for civil engineers in the US); portfolio and contribution history becomes part of the licensure evidence portfolio
- **2035**: Open-source UAV flight stack ecosystems (PX4, ArduPilot) have integrated so many commercial contributions that the line between "open source contributor" and "commercial UAV engineer" is indistinct; upstream contribution is the expected baseline, not the differentiator
- **2045**: The specific flight stack and tools in this roadmap are replaced by systems that do not exist yet; the portfolio discipline — finish things, measure them, document honestly, contribute to the community — remains the career signal

### Interview Questions

1. **What makes a UAV portfolio project production-credible rather than demo-grade?**
   *Answer*: Five properties: reproducibility (a defined procedure that another engineer can follow to get the same result); measurement (quantitative metrics against defined specifications, not just "it worked"); explicit failure modes (what was tested, what was not, and what the consequences of untested failure modes would be); safety assumptions (what must be true for the system to behave as shown); and version control (exact software versions and parameter configuration recorded). A project that lacks any of these is a demo. A project that has all five is evidence.

2. **How do you find a good upstream contribution opportunity in PX4?**
   *Answer*: (1) Filter GitHub issues by `good first issue` and `help wanted` labels; read 10 issues and pick one you can reproduce in SITL. (2) Search for issues in the module you know best from previous work — if you have spent time with EKF2, an EKF2 issue is a better target than a random driver issue. (3) Look for issues where the maintainer has described the expected behavior and the actual behavior but has not committed to a specific fix — this signals they want a contributor to investigate and propose. (4) Post in discuss.px4.io to confirm your reproduction and proposed approach before writing code — maintainer buy-in before a PR saves wasted effort.

3. **Why does an upstream merged PR carry more weight than a self-contained portfolio project?**
   *Answer*: A merged upstream PR demonstrates properties that a self-contained project cannot: (1) the code was reviewed by engineers who did not write it and who have domain expertise; (2) the change was deemed valuable by the community (which has implicit requirements about quality and scope); (3) the contributor was able to communicate their technical approach in writing clearly enough for reviewers to evaluate it; (4) the contributor iterated on feedback — a real engineering skill that does not appear in solo projects. A self-contained project demonstrates what the engineer built; a merged PR demonstrates how they work with other engineers.

4. **How do you write a resume bullet that accurately represents a SITL project without overstating or understating?**
   *Answer*: The formula: "Built [specific artifact using specific technical approach] that [measured result]; validated in [specific simulation environment] under [specific conditions]." Example: "Built a precision landing system using ArUco marker detection with OpenCV and PX4 offboard control that achieves 0.3 m median landing error; validated in Gazebo SITL across 50 trials under 0–5 m/s simulated wind." This is specific (the tool names), honest (SITL, not flight tested), and measured (0.3 m, 50 trials, wind range). Compare to the generic version: "Implemented computer vision for autonomous landing" — which says nothing about scale, accuracy, or test discipline.

5. **What is the difference between a `fix:` and a `feat:` commit message and why does it matter for a PX4 upstream contribution?**
   *Answer*: PX4 uses conventional commit message format: `fix:` indicates a bug correction (no new capability, existing behavior corrected); `feat:` indicates a new feature (new capability added that did not exist before); `docs:` is documentation only. This matters because it drives the changelog and semantic versioning; maintainers use it to categorize PR impact. A bug fix submitted as `feat:` is immediately flagged in review as miscategorized. Getting the commit message type correct signals that the contributor understands the project's conventions — which signals broader professionalism.

### Further Depth

- **PX4 Contribution Guide** (docs.px4.io/main/en/contribute/) — required reading before submitting any PR; code style, commit message format, test requirements, and PR process
- **ArduPilot Developer Wiki — Contributing** (ardupilot.org/dev/docs/contributing.html) — equivalent guide for ArduPilot; includes the PR submission checklist
- **Dronecode Forum (discuss.px4.io)** — where PX4 engineering discussions happen; search before posting; follow `dev` and `EKF` tags for relevant technical threads
- **"The Architecture of Open Source Applications"** — essays on how large open-source codebases are structured and maintained; provides context for navigating PX4 and ArduPilot at architectural level
- **MAVSDK repository** (github.com/mavlink/MAVSDK) — more accessible than PX4 core for a first contribution; Python and C++ SDKs; active issue tracker with `good first issue` labels
- **GitHub Actions documentation** (docs.github.com/en/actions) — understanding CI pipelines is required for contributing; PX4's CI runs on GitHub Actions with public logs
- **"Cracking the Coding Interview" adapted for embedded/robotics** — technical interview preparation resource; supplement with PX4 and ROS 2 specific practice; most UAV interviews include both systems design and coding components
