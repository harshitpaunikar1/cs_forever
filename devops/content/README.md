# DevOps Roadmap

DevOps is a discipline that bridges the gap between software development and IT operations,
with the goal of delivering software faster, more reliably, and with tighter feedback loops.
Rather than treating "writing code" and "running code" as separate responsibilities owned by
separate teams, DevOps encourages shared ownership of the entire software lifecycle -- from
the first commit all the way through production monitoring. The practices, tools, and cultural
shifts that make up DevOps have become essential knowledge for anyone building or operating
modern software systems.

This roadmap lays out a structured learning path. Each topic builds on the ones before it,
so working through them in order will give you the most coherent experience. That said, you
can jump to any topic that matches your current needs.

---

## Visual Learning Path

```
                        +----------------------------+
                        |  1. Programming Languages  |
                        +-------------+--------------+
                                      |
                        +-------------v--------------+
                        | 2. Operating Systems &     |
                        |    Linux Fundamentals      |
                        +-------------+--------------+
                                      |
                        +-------------v--------------+
                        | 3. Terminal & Bash          |
                        |    Scripting               |
                        +-------------+--------------+
                                      |
                        +-------------v--------------+
                        | 4. Version Control (Git)   |
                        +-------------+--------------+
                                      |
                        +-------------v--------------+
                        | 5. Networking & Protocols  |
                        +-------------+--------------+
                                      |
                  +-------------------+-------------------+
                  |                                       |
    +-------------v--------------+          +-------------v--------------+
    | 6. Web Servers & Proxies   |          | 7. Containers (Docker)     |
    +-------------+--------------+          +-------------+--------------+
                  |                                       |
                  +-------------------+-------------------+
                                      |
                        +-------------v--------------+
                        | 8. Cloud Providers         |
                        +-------------+--------------+
                                      |
                        +-------------v--------------+
                        | 9. CI/CD Pipelines         |
                        +-------------+--------------+
                                      |
                  +-------------------+-------------------+
                  |                                       |
    +-------------v--------------+          +-------------v--------------+
    | 10. Infrastructure as Code |          | 11. Configuration Mgmt     |
    +-------------+--------------+          +-------------+--------------+
                  |                                       |
                  +-------------------+-------------------+
                                      |
                        +-------------v--------------+
                        | 12. Container Orchestration |
                        |     (Kubernetes)           |
                        +-------------+--------------+
                                      |
                  +-------------------+-------------------+
                  |                                       |
    +-------------v--------------+          +-------------v--------------+
    | 13. Monitoring & Logging   |          | 14. Security & Secrets     |
    +-------------+--------------+          +-------------+--------------+
                  |                                       |
                  +-------------------+-------------------+
                                      |
                        +-------------v--------------+
                        | 15. Serverless             |
                        +----------------------------+
```

---

## Topic Overview

### 1. Programming Languages

At minimum one general-purpose language is required to write automation scripts, build
internal tools, extend CI/CD pipelines, and contribute to application code. Python and Go
are the most common choices in the DevOps world today.

### 2. Operating Systems & Linux

The vast majority of production servers run Linux. Understanding how the kernel manages
processes, memory, file systems, and permissions is foundational to everything that follows
in this roadmap.

### 3. Terminal & Bash Scripting

The terminal is the primary interface for interacting with servers. Being productive in
Bash (or a comparable shell) means you can automate repetitive tasks, chain commands
together with pipes, and write robust startup and deployment scripts.

### 4. Version Control (Git)

Git is the universal version control system. Every piece of work in DevOps -- application
code, infrastructure definitions, CI/CD configurations, documentation -- lives in a Git
repository. Understanding branching strategies, merge workflows, and history management
is non-negotiable.

### 5. Networking & Protocols

Software systems communicate over networks. You need a working mental model of TCP/IP,
DNS resolution, HTTP/HTTPS, TLS handshakes, load balancing, and firewall rules to debug
production issues and design resilient architectures.

### 6. Web Servers & Proxies

Nginx, Apache, HAProxy, and Caddy sit between the internet and your applications. They
handle TLS termination, request routing, static file serving, rate limiting, and load
distribution. Knowing how to configure and troubleshoot them is a daily DevOps skill.

### 7. Containers (Docker)

Containers package an application together with its dependencies into an isolated,
reproducible unit. Docker popularized this model and remains the standard tool for
building, sharing, and running containers. Understanding images, layers, volumes,
networks, and multi-stage builds is essential.

### 8. Cloud Providers

AWS, Google Cloud, and Azure provide the compute, storage, networking, and managed
services that most modern systems run on. Familiarity with at least one major provider --
its console, CLI, IAM model, and core services -- is expected of any DevOps practitioner.

### 9. CI/CD Pipelines

Continuous Integration and Continuous Delivery automate the path from code commit to
production deployment. Tools like GitHub Actions, GitLab CI, Jenkins, and CircleCI
let you define build, test, security-scan, and deploy stages as code.

### 10. Infrastructure as Code

Instead of clicking through a cloud console, you describe your infrastructure in
declarative files (Terraform, Pulumi, CloudFormation) and let a tool converge real
resources to match. This makes infrastructure reviewable, versioned, and repeatable.

### 11. Configuration Management

Once servers exist, their software and settings need to be kept in a desired state.
Ansible, Chef, Puppet, and SaltStack let you express that desired state in code and
apply it across fleets of machines idempotently.

### 12. Container Orchestration (Kubernetes)

When you have hundreds of containers across dozens of machines, you need an orchestrator.
Kubernetes handles scheduling, scaling, self-healing, service discovery, and rolling
updates. It has become the de facto standard for running containerized workloads at scale.

### 13. Monitoring & Logging

You cannot improve what you cannot observe. Prometheus and Grafana handle metrics,
the ELK stack (Elasticsearch, Logstash, Kibana) or Loki handle logs, and Jaeger or
Tempo handle distributed traces. Together they give you visibility into system health.

### 14. Security & Secret Management

Security is not a phase -- it is woven into every step. This topic covers secret storage
(Vault, AWS Secrets Manager), image scanning, network policies, role-based access
control, supply-chain security, and the principle of least privilege applied to
infrastructure.

### 15. Serverless

Serverless platforms (AWS Lambda, Google Cloud Functions, Azure Functions) let you run
code without provisioning or managing servers. They charge per invocation, scale to
zero, and are well-suited for event-driven workloads, APIs, and glue logic between
services.

---

## How to Use This Roadmap

1. **Start at the top.** Each topic assumes knowledge from the ones above it.
2. **Build projects.** Reading alone does not build competence. For every topic, set up a
   small project that forces you to use the tools in a realistic scenario.
3. **Go deep on one cloud provider first.** Trying to learn AWS, GCP, and Azure
   simultaneously will slow you down. Pick one, get comfortable, then branch out.
4. **Revisit earlier topics.** As you learn Kubernetes, you will understand Linux networking
   at a deeper level. Circle back and fill in gaps.
5. **Stay current.** The DevOps tooling landscape evolves quickly. Follow release notes for
   the tools you use in production and evaluate new options periodically.

---

## Companion Files

Each topic has its own detailed page:

| # | Topic | File |
|---|-------|------|
| 1 | Programming Languages | [01-programming-languages.md](01-programming-languages.md) |
| 2 | Operating Systems & Linux | 02-operating-systems.md |
| 3 | Terminal & Bash Scripting | 03-terminal-bash.md |
| 4 | Version Control (Git) | 04-version-control-git.md |
| 5 | Networking & Protocols | 05-networking-protocols.md |
| 6 | Web Servers & Proxies | 06-web-servers-proxies.md |
| 7 | Containers (Docker) | 07-containers-docker.md |
| 8 | Cloud Providers | 08-cloud-providers.md |
| 9 | CI/CD Pipelines | 09-cicd-pipelines.md |
| 10 | Infrastructure as Code | 10-infrastructure-as-code.md |
| 11 | Configuration Management | 11-configuration-management.md |
| 12 | Container Orchestration | 12-container-orchestration-k8s.md |
| 13 | Monitoring & Logging | 13-monitoring-logging.md |
| 14 | Security & Secrets | 14-security-secrets.md |
| 15 | Serverless | 15-serverless.md |

---

## Prerequisites

Before diving in, you should be comfortable with:

- Basic programming concepts (variables, loops, functions, data structures)
- Using a computer's terminal or command prompt
- Reading technical documentation

No prior DevOps experience is assumed. The roadmap is designed to take you from
general software development knowledge to production-grade DevOps skills.

---

## Key Principles to Keep in Mind

**Automate everything repeatable.** If you do something more than twice, script it.
Manual processes are error-prone and do not scale.

**Treat infrastructure like code.** Version it, review it, test it, and deploy it
through the same pipelines as application code.

**Shift left on security.** Integrate security checks early in the development
process rather than bolting them on at the end.

**Measure, then optimize.** Collect data before making changes. Intuition about
performance bottlenecks is frequently wrong.

**Embrace failure.** Design systems that degrade gracefully. Practice incident
response. Run chaos experiments. Systems will fail -- your job is to make failures
small, detected quickly, and recoverable.

---

*Work through each topic at your own pace. Depth matters more than speed.*
