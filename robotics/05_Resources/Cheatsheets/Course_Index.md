# Course Index

## Highest-ROI Robotics Resources

1. [ROS 2 Tutorials](https://docs.ros.org/en/jazzy/index.html)
1. [ROS-Industrial Training](https://rosindustrial.org/training)
1. [Nav2 Docs](https://docs.nav2.org/getting_started/index.html)
1. [MoveIt 2 Tutorials](https://moveit.picknik.ai/main/doc/tutorials/tutorials.html)
1. [ros2_control Docs](https://control.ros.org/)
1. [Gazebo Docs](https://gazebosim.org/docs)
1. [micro-ROS Tutorials](https://micro.ros.org/docs/tutorials/core/overview/)
1. [PythonRobotics](https://github.com/AtsushiSakai/PythonRobotics)
1. [Introduction to Robotics and Perception](https://www.roboticsbook.org/intro.html)
1. [Modern Robotics](https://modernrobotics.northwestern.edu/)
1. [MIT Robotic Manipulation](https://manipulation.csail.mit.edu/)
1. [Underactuated Robotics](https://underactuated.mit.edu/)
1. [PX4 ROS 2 User Guide](https://docs.px4.io/main/en/ros2/user_guide)
1. [Bootlin Embedded Linux](https://bootlin.com/docs/)
1. [Pro Git](https://git-scm.com/book/en/v2)
1. [Docker Get Started](https://docs.docker.com/get-started/)
1. [OpenCV Docs](https://docs.opencv.org/)
1. [Hugging Face Robotics Course](https://huggingface.co/robotics-course)
1. [LeRobot Docs](https://huggingface.co/docs/lerobot)

## ROS 2 Status Note

Official ROS docs checked on `2026-04-17` show:

- `Kilted Kaiju` is the latest stable release.
- `Jazzy Jalisco` is the current supported LTS release.
- Studying `Jazzy` first remains a practical learning choice for broader package compatibility, then validating `Kilted` support when needed.
---
## 🔧 Industry Enrichment (Appended)
---

### Real-World Implementation

An index page matters professionally when it saves decision time. Real robotics teams use internal indexes to route people toward the right docs, repos, standards, and debugging references without forcing them to rediscover the whole knowledge graph every time. This course index should be used the same way: not as something to read top to bottom, but as the control panel for choosing the next resource, backfilling a missing concept, or finding the canonical reference when a project exposes a weak spot.

### Industry Tool Stack

- `Course index`: used for routing from problem type to the best next source instead of random searching.
- `Official docs`: used for API truth when tutorials conflict.
- `Books and long-form notes`: used for conceptual depth when tool docs explain only usage.
- `Open-source repos`: used to inspect real package structure and deployment patterns.

### Step-by-Step Applied Workflow

1. Identify the current bottleneck: setup, navigation, manipulation, perception, deployment, or learning.
2. Open the corresponding section of the index instead of searching broadly.
3. Read one canonical source first, then one implementation source.
4. Apply the idea in code or simulation immediately.
5. Return to the index only when the next bottleneck is clear.
6. Save the exact source that resolved the issue in project notes.

### AI Integration

AI is useful here as a routing helper. It can summarize which source is likely best for a specific problem, but it should not replace the source itself. For robotics, the safest workflow is still: use AI to narrow the search, then read the official docs, repo, or book chapter that defines the behavior you are about to rely on.

### Case Studies

Open Robotics documentation is the clearest example of why indexes matter: engineers repeatedly return to the docs, examples, and API references because one layer explains concepts while another explains exact behavior. The same pattern appears in `Nav2` and `MoveIt 2`, where strong engineers keep both the conceptual docs and the implementation references close at hand.

### Failure Modes & Safety

The failure mode for index pages is passive collecting. If the index becomes a long list of links without a usage pattern, it stops being useful. Another failure is relying on secondary tutorials when the official source is required for a decision that affects runtime behavior, compatibility, or safety assumptions. The safe rule is simple: use the index to route quickly, then anchor important choices in the most primary source available.

### Business & Commercial Layer

Commercially, a good index reduces onboarding time and debugging waste. Teams lose money when engineers spend hours rediscovering the same references or build on stale tutorials. A compact, well-prioritized index is a force multiplier because it improves decision speed across the whole learning and delivery pipeline.

### Hiring Signal

Job titles supported by this page:

- Robotics Software Engineer
- Robotics Platform Engineer
- Robotics Applications Engineer

Interview screens it helps with:

- choosing the right reference for a ROS 2, Nav2, or MoveIt problem
- explaining why official docs beat tutorial fragments for critical decisions
- naming the first source you would consult for a broken subsystem

### Portfolio Projects

Beginner: build a `resource map` README for one robotics topic with primary vs secondary sources.  
Intermediate: create a `debugging playbook` linking common failures to the exact docs or repos that resolve them.  
Advanced: build a `team onboarding index` for a full robotics stack with role-specific reading paths.

### Future Trends

- `2026`: stronger reliance on curated internal indexes as robotics stacks widen.
- `2030`: more indexes combine docs, logs, and fleet playbooks rather than static reading lists.
- `2035`: AI-assisted retrieval improves routing, but primary-source judgment stays valuable.
- `2045`: knowledge operations become a formal robotics platform function, not an informal side task.

### Interview Questions

1. When should you prefer official docs over tutorials?
   Short answer: when behavior, compatibility, or configuration correctness matters.

2. Why keep books in an index if repos already exist?
   Short answer: because repos show structure while books explain the concepts behind the structure.

3. What makes an index actually useful?
   Short answer: prioritization, clear routing, and repeated use in real debugging workflows.

4. What is the main risk of link-heavy index pages?
   Short answer: they become collections instead of decision tools.

5. How should AI be used with an index?
   Short answer: to narrow search, not to replace source validation.

### Further Depth

- `ROS 2` official docs
- `Nav2` docs
- `MoveIt 2` docs
- `Modern Robotics`
- `Foxglove` docs
