# k8s-hermes-collective

## A Distributed Cognitive Operator for Kubernetes and Beyond

---

**Version:** 0.1 (Draft)  
**Date:** June 2026  
**Status:** Architecture Definition

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [The Problem](#2-the-problem)
3. [What k8s-hermes-collective Is](#3-what-k8s-hermes-collective-is)
4. [What k8s-hermes-collective Is Not](#4-what-k8s-hermes-collective-is-not)
5. [Foundational Principles](#5-foundational-principles)
6. [Architecture](#6-architecture)
   - 6.1 [The Fabric](#61-the-fabric)
   - 6.2 [Distributions](#62-distributions)
   - 6.3 [The Distribution Formula](#63-the-distribution-formula)
   - 6.4 [Fabric–Distribution Relationship](#64-fabricdistribution-relationship)
7. [Cognition](#7-cognition)
   - 7.1 [Cognitive Artifacts](#71-cognitive-artifacts)
   - 7.2 [The Cognitive Flow](#72-the-cognitive-flow)
   - 7.3 [The Cognitive Store](#73-the-cognitive-store)
   - 7.4 [Signal Hierarchy](#74-signal-hierarchy)
8. [Adaptive Perception](#8-adaptive-perception)
   - 8.1 [What Perception Is](#81-what-perception-is)
   - 8.2 [The Four Sources](#82-the-four-sources)
   - 8.3 [How Perception Is Computed](#83-how-perception-is-computed)
   - 8.4 [Perception Is Distributed](#84-perception-is-distributed)
   - 8.5 [Perception and Forgetting](#85-perception-and-forgetting)
9. [Roles](#9-roles)
   - 9.1 [Warden — Node Cognitive Executor](#91-warden--node-cognitive-executor)
   - 9.2 [Regent — Cluster Cognitive Authority](#92-regent--cluster-cognitive-authority)
   - 9.3 [Steward — Application Cognitive Role](#93-steward--application-cognitive-role)
   - 9.4 [Emissary — External System Cognitive Role](#94-emissary--external-system-cognitive-role)
10. [Inter-Distribution Communication](#10-inter-distribution-communication)
11. [Infrastructure Integration](#11-infrastructure-integration)
    - 11.1 [The Interface–Adapter Pattern](#111-the-interfaceadapter-pattern)
    - 11.2 [Capability Catalog](#112-capability-catalog)
    - 11.3 [Fabric Installation Principle](#113-fabric-installation-principle)
12. [Installation](#12-installation)
    - 12.1 [Installation Model](#121-installation-model)
    - 12.2 [Distribution Independence](#122-distribution-independence)
    - 12.3 [Required Kubernetes Primitives](#123-required-kubernetes-primitives)
    - 12.4 [Cognitive Layer Setup](#124-cognitive-layer-setup)
13. [State Model](#13-state-model)
    - 13.1 [The Three Planes of State](#131-the-three-planes-of-state)
    - 13.2 [Cognitive State](#132-cognitive-state)
    - 13.3 [Persistence](#133-persistence)
    - 13.4 [Cognition Durability Invariant](#134-cognition-durability-invariant)
14. [Security Model](#14-security-model)
    - 14.1 [Trust Boundaries](#141-trust-boundaries)
    - 14.2 [Arbitration and Human Authority](#142-arbitration-and-human-authority)
15. [Use Cases](#15-use-cases)
    - 15.1 [Single-Node Kubernetes with Warden](#151-single-node-kubernetes-with-warden)
    - 15.2 [Production Cluster with Full Stack](#152-production-cluster-with-full-stack)
    - 15.3 [Multi-Tenant Platform with Stewards](#153-multi-tenant-platform-with-stewards)
    - 15.4 [Hybrid Infrastructure with Emissaries](#154-hybrid-infrastructure-with-emissaries)
    - 15.5 [Edge Cluster with Minimal Footprint](#155-edge-cluster-with-minimal-footprint)
16. [Architecture Decision Records](#16-architecture-decision-records)
17. [Open Questions and Future Work](#17-open-questions-and-future-work)
18. [Appendix: Glossary](#18-appendix-glossary)

---

## 1. Introduction

Infrastructure operations are caught in a bind. Kubernetes gave the industry a powerful reconciliation engine — declarative intent, self-healing workloads, rolling updates, autoscaling. But operating production Kubernetes remains a fundamentally human activity: diagnosing cryptic pod failures at 3 AM, understanding why a canary deployment stalled, correlating a spike in 5xx errors across three microservices, deciding whether a node with memory pressure should be drained or tolerated. The control plane reconciles *declared state*. It does not *understand* what is happening, *reason* about what to do, or *learn* from what happened before.

Observability tools compound the problem rather than solving it. They generate dashboards, alerts, and traces — more signals, more noise, more pages. An on-call engineer does not need another dashboard. They need a system that understands the operational context, can investigate, reason, and act — or at least prepare a diagnosis and a remediation plan — without requiring a human to read twelve logs and correlate six metrics first.

k8s-hermes-collective is a distributed cognitive operator designed to address this gap. It layers cognition, memory, adaptive perception, and operational coordination on top of Kubernetes and surrounding infrastructure. It does not replace Kubernetes. It does not compete with Kubernetes controllers. It adds a layer of operational intelligence that observes, reasons, remembers, coordinates, and acts — while respecting Kubernetes as the authoritative reconciliation substrate.

The system is built on a modular architecture. A shared cognitive substrate — the **Fabric** — provides the reusable machinery. Independently installable **Distributions** operationalize responsibility domains as deployable systems. You install the Fabric, then choose the distributions you need. You can run one distribution alone, or several, or all of them. Integration is optional. Independence is required.

This document introduces k8s-hermes-collective, explains its architecture, principles, components, and work flows, and discusses the design decisions that shape it.

---

## 2. The Problem

Kubernetes automates reconciliation. Given declared intent, it converges reality toward that intent. This is powerful, but it addresses only one phase of operations: *convergence*. The operational lifecycle is broader:

1. **Perception** — What is happening? What signals matter? What has changed?
2. **Reasoning** — Why is this happening? What are the dependencies? Is this a symptom or a cause?
3. **Decision** — What should be done? Is intervention needed? What remediation is appropriate?
4. **Action** — Execute the chosen remediation. Orchestrate the steps. Verify the outcome.
5. **Learning** — Was the remediation effective? Should the diagnosis be remembered? Should the perception policy change?

Kubernetes handles steps 1 (partially, via events) and 4 (via controllers). Steps 2, 3, and 5 are left to humans — or to runbooks, which are fragile, static, and disconnected from operational context.

Meanwhile, the observability ecosystem generates enormous signal volume. Teams instrument everything, collect everything, and then struggle to find the relevant signal in a flood of noise. Alert fatigue is endemic. Context is lost between incidents. The same failure is diagnosed from scratch every time.

The problem is not a lack of data. It is a lack of *cognition* — a system that can perceive selectively, reason about what it perceives, remember what it learned, and adapt its attention over time.

---

## 3. What k8s-hermes-collective Is

k8s-hermes-collective is a **distributed cognitive system with adaptive perception**. It is not a static observability pipeline, not a controller framework, and not a monolithic operations platform.

It is a system where:

- **Each agent independently computes what to observe** — perception policy is not centralized but distributed and adaptive.
- **Agents reason about observations** — they open sessions, form hypotheses, correlate signals, and diagnose.
- **Agents remember what they learn** — cognitive memory is durable, active, and feeds back into perception.
- **Agents act within controlled boundaries** — they execute tasks via permitted mechanisms, not unrestricted shells.
- **Agents coordinate when multiple distributions are present** — but every distribution can operate alone.

The system is organized around three concepts:

| Concept | Definition |
|---------|-----------|
| **Fabric** | Shared cognitive substrate — the reusable cognitive engine |
| **Role** | Responsibility domain — defines what an agent cares about |
| **Distribution** | Independently installable assembly — Fabric + role personality + tools + persistence + deployment form |

Roles are abstract. Distributions are concrete. The Fabric is the foundation.

---

## 4. What k8s-hermes-collective Is Not

Important negative constraints that shape the system:

- **Not a Kubernetes replacement.** Kubernetes remains the authoritative reconciliation substrate. k8s-hermes-collective observes, reasons, and coordinates — it does not reimplement scheduling, reconciliation, or healing.
- **Not a competing controller framework.** Existing operators and controllers remain enabled and authoritative. k8s-hermes-collective composes and orchestrates them; it does not replace them.
- **Not a monolith.** Every distribution is independently installable and independently useful. You do not need the entire system to get value from a single part.
- **Not a centralized observability pipeline.** There is no global observation filter. Each agent computes its own perception policy. Two agents with the same role may perceive differently.
- **Not a static rule engine.** Perception is adaptive. Agents learn what is valuable, deprioritize what is noisy, and evolve their attention over time. The same agent may observe differently today than it did a week ago.
- **Not a raw telemetry store.** Raw signals stay in external systems. Only meaningful, context-relevant observations enter the cognitive layer.

---

## 5. Foundational Principles

These principles are immutable architectural commitments, recorded as Architecture Decision Records (ADRs).

### Kubernetes as Substrate

Kubernetes provides the distributed execution and reconciliation substrate. k8s-hermes-collective operates as a cognitive operator layered on top. It observes, reasons, coordinates, remembers, and automates. It does not replace Kubernetes-native reconciliation. (ADR 0001)

### Non-Duplication of Reconciliation

Kubernetes operators and controllers already implement reconciliation loops and healing logic. Creating parallel reconciliation systems would risk conflict and duplicated authority. k8s-hermes-collective observes existing reconciliation, diagnoses failures, coordinates remediation, adjusts policy and intent when needed, and composes existing controllers. It is a meta-operational and cognitive layer, not a competing controller framework. (ADR 0002)

### Fabric and Independent Distributions

The shared cognitive machinery (the Fabric) is separated from the independently installable assemblies that operationalize roles (Distributions). A user who needs only application cognition should install only the Steward Distribution — not the entire system. Integration between distributions is optional. Independence is required. (ADR 0003)

### Leverage Existing Infrastructure

k8s-hermes-collective provides the option to integrate with existing infrastructure rather than always bundling its own. Users who already run CephFS, PostgreSQL, or Kafka should be able to connect them. Users who need a self-contained install should also be supported. The Fabric installation must be lightweight. Every bundled default must be optional and replaceable. (ADR 0004)

---

## 6. Architecture

### 6.1 The Fabric

The Fabric is the shared cognitive substrate — the reusable engine that every distribution is built on. It is not a role, not a distribution, and not a Kubernetes resource. It is the foundation.

The Fabric provides five capability areas: 

**Cognition** — The core cognitive machinery:
- Cognition store and memory persistence
- Adaptive perception engine
- Session and task persistence — the Fabric stores and serves sessions and tasks; agents create, maintain, and drive their lifecycles
- Reasoning lifecycle and skill execution
- Cognition feedback loops

**Adaptive Perception** — The attention mechanism:
- Perception policy computation
- Observable interpretation
- Attention scheduling and observation prioritization
- Adaptive learning and forgetting
- Perception history and signal relevance evolution

**Execution Framework** — How work gets done safely:
- Task execution lifecycle
- Tool abstraction and isolated execution
- Permission boundary support
- Executor coordination and sidecar integration

**Communication** — Inter-agent coordination (detailed semantics TBD):
- Inter-agent communication
- Coordination transport
- Cognition synchronization
- Distributed awareness
- Conflict reporting

**Persistence** — Durability of cognitive state:
- Memory persistence and cognition durability
- Learned perception history
- Task and session history
- Adaptive state continuity

The Fabric is installed first. It is always required. It must be as lightweight as possible and must not force-install heavy infrastructure solely for its own use.

### 6.2 Distributions

A Distribution is an independently installable assembly built on top of the Fabric. It is a deployable system. While a role defines a responsibility domain, a distribution operationalizes that role into something you can install, configure, and run.

Each distribution must be:
- **Independently deployable** — can be installed and run on its own
- **Independently useful** — provides operational value without other distributions
- **Self-cognitive** — maintains its own cognitive state
- **Self-persistent** — each distribution configures its own persistence through the Fabric's persistence interfaces
- **Operationally meaningful** — does something useful without requiring other distributions

Four distributions are recognized:

| Distribution | Role | Scope | Deployment Form |
|---|---|---|---|
| **Regent Distribution** | Regent | Cluster-wide singleton | Deployment (HA) |
| **Warden Distribution** | Warden | Node-level | DaemonSet |
| **Steward Distribution** | Steward | Namespace / service domain | Deployment (HA) |
| **Emissary Distribution** | Emissary | VM / bare metal / external | Agent / container |

Two categories of concern:

- **Cluster health distributions** — Regent and Warden, concerned with the health and operation of the cluster itself.
- **Application and external distributions** — Steward and Emissary, concerned with applications, namespaces, service domains, and external infrastructure.

### 6.3 The Distribution Formula

Every distribution is an assembly of five components:

```
Fabric  +  Personality  +  Tools  +  Persistence  +  Deployment Form  =  Distribution
```

- **Fabric** — the shared cognitive substrate (always present)
- **Personality** — the role-specific behavior, responsibility focus, and operational heuristics
- **Tools** — the role-applicable execution tools and integrations
- **Persistence** — the distribution's persistence configuration (which Fabric-provided persistence adapters to use, storage sizing, retention policies)
- **Deployment Form** — how the distribution is deployed (DaemonSet, Deployment, agent, etc.)

The Fabric provides several capabilities that distributions consume but do not bring themselves: persistence engines, perception record storage, cognition store, communication interfaces, and execution framework. What differs between distributions is personality, tools, persistence configuration, and deployment form.

### 6.4 Fabric–Distribution Relationship

The Fabric owns cognition. Distributions own responsibility. Tools own action.

This separation means:
- The Fabric provides perception engines, memory persistence, session and task persistence, and execution framework — the machinery that stores, serves, and runs cognitive operations
- Agents (within distributions) create, maintain, and drive sessions, tasks, and reasoning — they are the active participants that use the Fabric's machinery
- A distribution provides the personality that determines *what* to perceive, *what* to reason about, and *what* actions are appropriate
- Tools provide the concrete execution mechanisms

Infrastructure adapter interfaces belong in the Fabric. Distributions reference them but do not reimplement them. This ensures consistency across distributions and avoids duplicating infrastructure integration code.

---

## 7. Cognition

Cognition is the core of k8s-hermes-collective. It is what makes the system a *cognitive operator* rather than a static automation engine.

The cognition model is defined conceptually before implementation schemas or CRDs. The model exists; persistence and implementation follow.

### 7.1 Cognitive Artifacts

| Artifact        | Purpose                                  | Nature                         |
| --------------- | ---------------------------------------- | ------------------------------ |
| **Perception**  | Adaptive attention mechanism             | Continuous computation         |
| **Observable**  | Declarative perception-guidance artifact | Declarative to be used as hint |
| **Observation** | Selected, context-relevant signals       | Perceived output               |
| **Session**     | Bounded active reasoning                 | Temporary, active cognition    |
| **Task**        | Executable work unit                     | Action-oriented                |
| **Memory**      | Durable cognition                        | Persistent, active feedback    |
| **Skill**       | Reusable operational capability          | Reusable procedure             |
| **Intent**      | Desired operational expectations         | Declarative guidance           |

These are conceptual artifacts. They are not automatically Kubernetes resources.

### 7.2 The Cognitive Flow

Cognition flows through a defined pipeline with a feedback loop:

```
Perception Policy (adaptive)
    ↓
Observation (selected signals)
    ↓
Session (active reasoning)
    ↓
Task (execution unit)
    ↓
Execution (delegated)
    ↓
Memory (durable knowledge)
    ↓
[feeds back into Perception Policy]
```

**Intent** and **Skill** influence reasoning and execution at every stage. They are not steps in the pipeline — they are influences that shape the pipeline's behavior.

The flow works as follows:

1. **Perception** decides what to observe right now, considering four sources: native knowledge, declarations, Observable hints, and memory.
2. **Observation** produces the selected, context-relevant signals that enter cognition. These are not raw logs — they are shaped by each agent's perception policy.
3. **Session** opens bounded active reasoning when an observation is interesting enough — an investigation, incident analysis, or maintenance activity.
4. **Task** is created when the session determines that action is needed — a concrete, executable work unit.
5. **Execution** delegates the task to a permitted execution mechanism (sidecar, tool, or controlled operation).
6. **Memory** stores what was learned — the diagnosis, the remediation outcome, whether the signal was useful. This feeds back into perception, making future perception smarter.

### 7.3 The Cognitive Store

The cognition store is not passive memory. It is an **active feedback mechanism**:

- It influences future perception policies — what the agent pays attention to
- It adapts observation behavior over time — reinforcing useful signals, suppressing noise
- It enables forgetting of irrelevant signals — operational attention has finite capacity
- It reinforces useful historical patterns — what worked before should be tried again

This is what makes k8s-hermes-collective adaptive rather than static. The same agent may observe differently after a hundred incidents than it did on day one.

### 7.4 Signal Hierarchy

Three layers of signal:

**Raw Infrastructure Layer** — logs, metrics, traces, Kubernetes events. These are external. k8s-hermes-collective does not ingest all raw signals.

**Cognitive Observation Layer** — only meaningful signals become Observations. Observations are NOT raw logs. They are selected, context-relevant signals shaped by each agent's adaptive perception policy. This is the entry point into cognition.

**Cognitive Layer** — Sessions, Tasks, Intent, Memory updates. These are the cognitive artifacts that flow through reasoning and execution.

The key constraint: k8s-hermes-collective does NOT ingest raw telemetry into the cognitive layer. Raw signals stay in their source systems. Only observations — signals that perception has selected as context-relevant — enter cognition.

---

## 8. Adaptive Perception

Perception is the mechanism that determines what an agent observes. In k8s-hermes-collective, perception is not a static filter, not a centralized pipeline, and not a configuration file. It is a dynamic, adaptive attention mechanism that each agent computes independently.

### 8.1 What Perception Is

Each agent continuously computes a **perception policy**:

> What to observe + how often + under what conditions

This policy is not static. It evolves as the agent learns which signals are valuable, which are noisy, and which are no longer relevant.

Perception answers questions like:
- Should I watch this metric, or has it been uninformative for weeks?
- Is this log pattern worth observing, or is it always benign?
- Has the topology changed such that I should now observe a new dependency?
- Did the last incident I diagnosed start with this signal? If so, prioritize it.

### 8.2 The Four Sources

Each perception policy is computed from four independent sources:

**Source 1: Agent-Native Knowledge** — The baseline. Every agent carries embedded domain expertise: DevOps and Kubernetes understanding, role-specific heuristics (a Warden knows about node health; a Steward knows about application topology), built-in operational patterns. This is the perception that exists before any runtime adaptation — the knowledge the system was designed with.

**Source 2: Declaration Data** — CRDs and role specifications define scope boundaries, role-specific focus, and Observable configuration. Declaration data constrains and focuses perception but does not rigidly enforce it. A Steward declared in namespace `production` knows that is its scope, but it can still observe cross-namespace signals that affect its domain.

**Source 3: Observable / Emissary Hints** — External guidance: suggested signal sources, recommended thresholds, sampling frequency guidance, environment constraints, Emissary-provided context about external systems. These are hints, not commands. Observable is a declarative perception-guidance artifact — it influences perception but does not centrally control it.

**Source 4: Cognition Memory (Adaptive Layer)** — The feedback loop that makes perception adaptive:
- **Learned signal importance** — signals that historically led to useful cognition are reinforced
- **Historical relevance** — patterns from past Sessions and Tasks inform what to watch
- **Signal decay** — irrelevant signals are gradually deprioritized over time
- **Reinforcement** — useful observations are strengthened
- **Forgetting** — irrelevant signals are actively suppressed

Source 4 is what turns perception from a configured filter into an adaptive attention mechanism.

### 8.3 How Perception Is Computed

At its core, perception computation is a selection process. For each agent, at each attention cycle, the system determines which signals to observe, how frequently, and under what conditions.

At this stage of the architecture, perception can be understood as a **perception record database** — a set of records that specify, for each agent, what it should perceive and how. These records are influenced by the four sources and evolve as memory feeds back.

A sketch of a perception record:

| Field | Description | Source |
|-------|-------------|--------|
| `agent` | Which agent this record applies to | Declaration |
| `signal_source` | What to observe (metric name, log pattern, event type, etc.) | Native knowledge, Observable hints, Memory |
| `frequency` | How often to check (continuous, periodic, on-change) | Observable hints, Memory |
| `priority` | How important this signal is (influences attention allocation) | Native knowledge, Memory |
| `conditions` | Under what conditions to observe (always, on-anomaly, above-threshold) | Observable hints, Memory |
| `last_useful` | When this signal last led to useful cognition (for decay computation) | Memory |
| `reinforcement_count` | How many times this signal proved useful (for reinforcement) | Memory |

The perception record database is populated initially from native knowledge (Source 1) and declarations (Source 2). Observable hints (Source 3) add or adjust records. Cognition memory (Source 4) updates records over time — raising priority for signals that proved useful, lowering priority for signals that were noise, and adjusting frequency based on observed patterns.

At each attention cycle, the agent:
1. Reads its perception records
2. Applies decay: signals that have not been useful for a long time are deprioritized
3. Applies reinforcement: signals that recently led to useful cognition are prioritized
4. Selects the top-priority signals within its attention budget
5. Observes the selected signals
6. Feeds observations into cognition
7. Updates perception records based on the cognitive outcome (was this observation useful?)

This is a simple, understandable model. It can be implemented with a database table and a periodic attention scheduler. More sophisticated models (multi-armed bandits, learned embeddings, reinforcement learning) are possible future directions, but the fundamental model is a selectable, adaptive record set.

### 8.4 Perception Is Distributed

There is no global centralized observation filter. Each agent independently computes its own perception policy using all four sources.

This means:
- Two Wardens on different nodes may observe different things — one may focus on disk I/O because that node has a history of disk issues; the other may focus on network latency because its workload is network-bound.
- A Steward in namespace `payments` may observe payment-specific signals, while a Steward in namespace `auth` observes authentication signals — even if they share the same cluster.
- An Emissary on a legacy VM may observe SSH login patterns and service health, while an Emissary on a database server observes query latency and replication lag.

Perception evolves through local experience, not global configuration.

### 8.5 Perception and Forgetting

Forgetting is an active process, not a bug. An agent that observes everything observes nothing usefully. Operational attention has finite capacity. Signals that were once relevant but are no longer must be deprioritized to make room for signals that are.

Forgetting works through **signal decay**: if a signal has not led to useful cognition for a configurable period, its priority is gradually reduced. If it remains irrelevant, it may eventually be removed from the active perception set entirely — though it remains in memory, so it can be re-promoted if circumstances change.

This is similar to how an experienced on-call engineer develops intuition: they learn to ignore the noise that never matters and focus on the patterns that reliably signal trouble. k8s-hermes-collective agents do the same — not through rules, but through experience.

---

## 9. Roles

Roles define responsibility domains. They determine what an agent cares about, what it reasons about, and what actions are appropriate within its scope. Roles are not runtime states, not deployment forms, and not emergent from one another.

No role is an emergent state of another role. No promotion or election-based identity transitions exist. A Warden does not become a Regent. A Steward does not become a Warden. Responsibility emerges from role type, placement, and declared scope.

### 9.1 Warden — Node Cognitive Executor

**Responsibility domain:** The Kubernetes node.

Warden is the node-local brain and hands. It is a privileged, node-resident cognitive executor that understands what is happening on its node and can act on it.

**What Warden does:**
- **Node health:** Monitors node conditions, resource pressure, disk and network health. Diagnoses node-level failures.
- **Node recovery:** Performs host inspection, system repair, and recovery operations. Can execute privileged operations when needed.
- **Kubernetes awareness:** Watches cluster resources, reads logs and events, inspects workload behavior, interacts with the Kubernetes API.
- **Local cognition:** Maintains reasoning context for its node. Contributes observations to the collective. Participates in shared memory.

**Deployment:** DaemonSet when deployed to all nodes; Deployment with node selectors or affinity when deployed to selected nodes. One or many Wardens may exist.

**Independence:** Warden alone is a valid, useful, operational distribution. A single-node Kubernetes cluster with only Warden gets a node-local cognitive operator that can diagnose and recover node-level issues.

### 9.2 Regent — Cluster Cognitive Authority

**Responsibility domain:** The Kubernetes cluster as a whole.

Regent is the cluster's cognitive brain. It is a singleton role responsible for cluster-wide cognition and orchestration. It thinks about the cluster. It coordinates cross-domain work. It arbitrates conflicts.

**What Regent does:**
- **Cluster lifecycle:** Node add, remove, recovery. Cluster lifecycle orchestration.
- **Cross-distribution coordination:** Coordinates with Wardens and Stewards when they are present. Maintains collective state awareness. Orchestrates cross-domain work.
- **Arbitration:** Resolves operational disagreements, coordinates competing priorities, arbitrates cross-scope decisions.
- **Cluster reporting:** Cluster-wide reporting and administrative CLI interface for operators.
- **Secure orchestration:** Manages secure orchestration workflows, accesses protected credentials when authorized, bootstraps infrastructure.

**What Regent does not do:**
- Does not delegate execution to other distributions — execution goes to sidecar executors and controlled operational tools
- Does not collapse cognition and execution into a single trust boundary

**Execution model:** Regent delegates execution to sidecar executors and controlled operational tools. It uses permitted execution mechanisms rather than unrestricted execution. It may possess isolated or tool-mediated execution capability. It does NOT delegate to Warden, Steward, or Emissary — it is an independent distribution.

**Deployment:** Singleton. HA-aware. Cluster-scoped.

**Independence:** Regent alone is a valid, useful, operational distribution. A cluster with only Regent gets a cluster-wide cognitive authority that can reason about the cluster, coordinate lifecycle events, and provide cluster reporting — without any node-level executors.

**Arbitration:** When Regent is absent, conflicts are surfaced and deferred to human authority. Human authority remains final.

### 9.3 Steward — Application Cognitive Role

**Responsibility domain:** Applications, namespaces, and service domains.

Steward understands and coordinates application operations within a defined scope. It is the application's cognitive operator — the agent that knows about your services, your topology, your incidents, and your operational context.

**What Steward does:**
- **Application awareness:** Observes workloads and services, inspects logs and metrics, understands topology and dependencies, reasons about application health.
- **Incident analysis:** Diagnoses failures, correlates incidents across services, coordinates remediation.
- **Reporting:** Service-level reporting, operational guidance, optional cluster-wide reporting participation.
- **Configuration:** CLI-based product configuration interface for the applications it manages.
- **Memory and context:** Maintains application knowledge, records operational context, contributes cognitive state to the collective.

**Declaration:** Stewards are user-declared via CRDs and configuration after installing the Fabric. Typical scope: namespace, service domain, or shared application boundary.

**Deployment:** Highly available. Replicated runtime. Durable cognition. Resilient operational continuity.

**Independence:** Steward alone is a valid, useful, operational distribution. A namespace with only Steward gets an application-scoped cognitive operator that can observe, diagnose, and report on application health — without cluster-wide coordination or node-level execution.

### 9.4 Emissary — External System Cognitive Role

**Responsibility domain:** External infrastructure — VMs, bare metal hosts, SSH-accessible systems, non-Kubernetes environments.

Emissary extends cognition and execution beyond the Kubernetes cluster. It is the agent that knows about your legacy VMs, your bare-metal database servers, your external monitoring systems — the infrastructure that Kubernetes doesn't manage but your operations depend on.

**What Emissary does:**
- **External awareness:** Inspects external systems, collects operational state, analyzes logs and services.
- **Execution:** Executes system commands, manages services, performs diagnostics and recovery, handles VM/bare-metal operations.
- **External integration:** Integrates external system findings with the Hermes collective.
- **Coordination:** Assists Wardens and Stewards when present, participates in operational workflows.

**Declaration:** Emissaries are intentionally declared after installing the Fabric. Typical scope: VM, bare metal host, SSH-accessible Linux environment, external infrastructure system.

**Deployment:** Agent or container on the external system.

**Independence:** Emissary alone is a valid, useful, operational distribution. A VM with only Emissary gets an external-system cognitive operator that can inspect, diagnose, and act — without any Kubernetes presence.

---

## 10. Inter-Distribution Communication

TBD

When multiple distributions coexist in the same cluster or environment, they may benefit from coordination. The communication model for inter-distribution interaction is not yet defined.

Open questions:
- What transport? (Publish-subscribe channel, direct API, shared cognition store, etc.)
- What semantics? (Event notification, request-response, shared state, etc.)
- What security boundary? (Do distributions trust each other's cognition? How is authentication handled?)
- What failure mode? (If the communication channel fails, each distribution must remain independently operational.)
- What is the coordination protocol between Regent and other distributions when present?

---

## 11. Infrastructure Integration

k8s-hermes-collective requires infrastructure capabilities to operate: persistent storage, highly available state, databases, distributed file systems, messaging. Many organizations already run these. Forcing every installation to bring its own would increase operational cost, add failure modes, and make adoption expensive — contradicting ADR 0004 (Leverage Existing Infrastructure).

### 11.1 The Interface–Adapter Pattern

When k8s-hermes-collective requires an infrastructure capability, it follows a three-step approach:

1. **Define a clear interface** for that capability within the Fabric
2. **Provide adapters** for common existing systems
3. **Allow users to connect their own installations** behind the interface

When the user does not have an existing system, k8s-hermes-collective may provide a lightweight default — but this must never be the only option.

This means:
- The Fabric defines *what it needs* (e.g., "a key-value store with watch semantics")
- Adapters provide *how to connect* to specific systems (etcd, PostgreSQL, Redis, SQLite)
- Users can bring *their own* system behind the interface

The pattern applies equally inside and outside Kubernetes. An Emissary on an external VM can connect to an existing PostgreSQL instance for perception state just as a Warden can use an in-cluster etcd.

### 11.2 Capability Catalog

| Capability | Interface | Common Adapters |
|---|---|---|
| Persistent storage | PVC / POSIX / object storage API | CephFS, NFS, MinIO, S3, local PV |
| Cognitive state / memory | Key-value / document API | etcd, PostgreSQL, Redis, SQLite |
| Distributed file system | RWX volume | CephFS, NFS, GlusterFS |
| Messaging / events | Pub-sub channel | NATS, Kafka, Redis Streams |
| Observability signals | OTLP / Prometheus | Prometheus, OpenTelemetry, Elasticsearch |

### 11.3 Fabric Installation Principle

The Fabric installation must be as lightweight as possible. It must not force-install heavy infrastructure solely for its own use. Every bundled default must be optional and replaceable.

This principle ensures that:
- Small installations (single-node, edge, development) can run with minimal infrastructure
- Large installations can leverage existing enterprise infrastructure
- The Fabric does not become an implicit infrastructure requirement that dominates the installation

---

## 12. Installation

### 12.1 Installation Model

Installing k8s-hermes-collective is a two-step process:

**Step 1: Install the Fabric.** This is always required. The Fabric provides the shared cognitive substrate. On Kubernetes, this means deploying the Fabric's runtime components, configuring persistence and communication systems, and establishing RBAC.

**Step 2: Install Distributions.** Choose which distributions you need. Each distribution is independently deployable and independently useful. You can install one, several, or all.

```
Fabric → choose → [Regent] [Warden] [Steward] [Emissary]
```

There is no prescribed order for distribution installation. There is no requirement to install all distributions. There is no dependency between distributions — each operates independently.

### 12.2 Distribution Independence

Each distribution is independently deployable and independently useful:

- **Regent alone** — valid, useful, operational. Cluster-wide cognitive authority.
- **Warden alone** — valid, useful, operational. Node-local cognitive executor.
- **Steward alone** — valid, useful, operational. Application-scoped cognitive operator.
- **Emissary alone** — valid, useful, operational. External system cognitive operator.

Integration between distributions is **optional**. Independence is **required**.

This is not a theoretical property — it is an architectural constraint. Every distribution must be tested and validated in isolation. A distribution that fails to operate without other distributions present violates this constraint.

### 12.3 Required Kubernetes Primitives

For distributions deployed on Kubernetes:

- Deployments
- DaemonSets
- Leases (coordination.k8s.io)
- Persistent Volumes (RWX recommended)
- RBAC roles for Hermes agents

### 12.4 Cognitive Layer Setup

A shared storage layer must be provisioned for cognitive artifacts (tasks, memory, sessions, skills). Options include:

- A dedicated Persistent Volume (e.g., `/hermes-on-k8s` volume)
- An object storage bucket
- A database-backed cognition store (per ADR 0004)

Every fabric-backed distribution maintains persistent cognition. Loss of pod identity does not imply loss of cognition.

---

## 13. State Model

### 13.1 The Three Planes of State

k8s-hermes-collective operates alongside two existing state planes in a Kubernetes environment:

| Plane                  | Store           | What It Holds                                                                                                                                           |
| ---------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Declarative intent** | Git             | What should exist — desired state                                                                                                                       |
| **Runtime truth**      | Kubernetes etcd | What currently exists — actual state, plus distribution declarations, agent configuration, and operational hints |
| **Cognitive state**    | Cognition store | What was learned, observed, reasoned — operational intelligence                                                                                         |

These planes are distinct. Git stores what should happen. etcd stores what is happening. The cognition store stores what was learned about what happened — and feeds that learning back into future perception and reasoning.

### 13.2 Cognitive State

Cognitive state includes:
- **Perception adaptation** — how each agent's attention has evolved
- **Operational memory** — incidents diagnosed, remediations attempted, outcomes observed
- **Session and task history** — what reasoning occurred, what actions were taken
- **Learned relevance** — which signals proved useful, which proved noisy
- **Skill evolution** — how operational capabilities have been refined

### 13.3 Persistence

Storage strategy is implementation-specific and defined per distribution. Possible approaches include:

- Kubernetes-backed state (ConfigMaps, Secrets, custom resources)
- RWX persistent volumes
- Object storage (S3, MinIO, etc.)
- Database-backed cognition (PostgreSQL, etcd, Redis, SQLite)

Per ADR 0004, the choice of persistence backend is determined by what the user already has, not by what k8s-hermes-collective mandates.

### 13.4 Cognition Durability Invariant

**Loss of pod identity does not imply loss of cognition.**

This is a fundamental invariant. Pods are ephemeral. Cognition must survive pod restarts, rescheduling, node failures, and deployment rollouts. When a Warden pod is rescheduled to a different node, its cognitive state — its memory, its learned perception, its operational history — must be available when it restarts. Cognition is separate from process identity.

---

## 14. Security Model

### 14.1 Trust Boundaries

Each distribution maintains a distinct trust boundary:

- **Regent** holds cluster-wide authority and sensitive orchestration credentials. This authority is isolated.
- **Warden** holds node-level privileged execution capability. This is scoped to the node.
- **Steward** holds application-level cognition and configuration capability. This is scoped to the namespace or service domain.
- **Emissary** holds external-system access capability. This is scoped to the declared external scope.

Distribution independence implies trust independence. A distribution does not need to trust another distribution to operate.

### 14.2 Arbitration and Human Authority

When multiple distributions coexist, operational disagreements can arise — two Stewards may disagree on remediation for a shared dependency, or a Steward and Warden may have conflicting priorities.

When Regent is present, it performs arbitration: resolves disagreements, coordinates competing priorities, and arbitrates cross-scope decisions.

**When Regent is absent, conflicts are surfaced and deferred to human authority.** No distribution assumes arbitration power in Regent's absence. Human authority remains final — even when Regent is present, a human operator can override Regent's arbitration.

---

## 15. Use Cases

### 15.1 Single-Node Kubernetes with Warden

**Scenario:** A small team runs a single-node Kubernetes cluster for development or lightweight production. They don't need cluster-wide coordination, but they want a node-level cognitive operator.

**Installation:** Fabric + Warden Distribution.

**What they get:** A node-local brain that monitors node health, diagnoses node-level issues, performs recovery operations, and learns which signals matter on this specific node. Adaptive perception means Warden learns over time which node conditions are benign and which signal real trouble.

**What they don't need:** Regent, Steward, Emissary, heavy infrastructure.

### 15.2 Production Cluster with Full Stack

**Scenario:** A production Kubernetes cluster running multiple services. The team wants comprehensive operational cognition: node health, cluster coordination, application awareness, and external infrastructure visibility.

**Installation:** Fabric + Regent Distribution + Warden Distribution + Steward Distribution(s) + Emissary Distribution(s) (as needed).

**What they get:** Wardens monitor each node. Regent coordinates cluster-wide cognition and arbitrates conflicts. Stewards, one per service domain, understand application topology, diagnose incidents, correlate cross-service failures. Emissaries extend cognition to external systems like database servers and load balancers. The distributions coordinate voluntarily through the inter-distribution communication layer (when implemented).

**What they leverage:** Existing infrastructure (CephFS for persistent storage, PostgreSQL for cognition state, Kafka for inter-distribution events) per ADR 0004.

### 15.3 Multi-Tenant Platform with Stewards

**Scenario:** A platform team operates a multi-tenant Kubernetes cluster. Each tenant gets a namespace and a dedicated Steward. The platform team uses Regent for cluster-wide coordination but does not expose it to tenants.

**Installation:** Fabric + Regent Distribution (platform team) + one Steward Distribution per tenant namespace.

**What they get:** Each tenant gets an application-scoped cognitive operator that understands their services, diagnoses their incidents, and provides operational guidance — scoped to their namespace. The platform team gets cluster-wide visibility and coordination through Regent. Tenants don't need to know about Wardens or Regent — their Steward is independently useful.

**What they don't get:** Cross-tenant visibility (Stewards are scoped to their namespace). The platform team retains cluster-wide authority through Regent.

### 15.4 Hybrid Infrastructure with Emissaries

**Scenario:** An organization runs Kubernetes for containerized workloads but also has legacy VMs, bare-metal database servers, and external monitoring systems that Kubernetes doesn't manage.

**Installation:** Fabric + Emissary Distribution(s) on external systems (optionally with Warden/Regent/Steward on the Kubernetes cluster).

**What they get:** Cognitive agents on each external system that can inspect, diagnose, and act on non-Kubernetes infrastructure. An Emissary on a database server can monitor query latency, replication lag, and disk usage. An Emissary on a legacy VM can monitor SSH access patterns and service health. All without requiring Kubernetes to manage those systems.

**What they leverage:** SSH-based access, existing monitoring infrastructure, and local execution on the external system.

### 15.5 Edge Cluster with Minimal Footprint

**Scenario:** An edge Kubernetes cluster with limited resources. The team wants cognitive operations but cannot afford a full installation.

**Installation:** Fabric (lightweight defaults) + Warden Distribution (selected nodes only).

**What they get:** Node-level cognition on critical edge nodes. Adaptive perception tuned for edge conditions (network intermittency, resource constraints). Minimal infrastructure footprint — SQLite for cognition state, local PV for persistence, no external dependencies.

**What they leverage:** ADR 0004 — lightweight defaults, no forced infrastructure. The Fabric stays minimal.

---

## 16. Architecture Decision Records

The following ADRs are accepted and govern the architecture:

| ADR | Title | Core Decision |
|-----|-------|---------------|
| 0001 | Kubernetes as Substrate | Operate as a cognitive operator layered on Kubernetes; do not replace Kubernetes reconciliation |
| 0002 | Non-Duplication of Reconciliation | Do not reimplement Kubernetes reconciliation; observe, diagnose, coordinate, compose existing controllers |
| 0003 | Fabric and Independent Distributions | Separate shared cognitive machinery (Fabric) from independently installable assemblies (Distributions); integration optional, independence required |
| 0004 | Leverage Existing Infrastructure | Provide the option to integrate with existing infrastructure; define interfaces in the Fabric, provide adapters, allow custom backends; every default must be optional and replaceable |

These ADRs are not independent — they form a coherent set:

- ADR 0001 establishes the relationship with Kubernetes
- ADR 0002 extends 0001 to all reconciliation concerns
- ADR 0003 establishes the modular structure that makes incremental adoption possible
- ADR 0004 extends 0002's "don't duplicate" principle to infrastructure, and works with 0003 by keeping the Fabric lightweight

---

## 17. Open Questions and Future Work

The architecture is defined. Implementation is not. The following areas need further design and development:

### Inter-Distribution Communication

The communication model between distributions is undefined. When Regent and Warden coexist, how do they coordinate? When two Stewards share a dependency, how do they avoid conflicting remediation? This is a critical design area that will be addressed in a future ADR.

### CRD Surface

What Kubernetes custom resource definitions does k8s-hermes-collective introduce? Which artifacts become CRDs and which remain internal? Observable is a candidate, but the full CRD surface — distribution declarations, role specifications, Observable, Intent, Skill, and others — needs design work. This determines the operator API surface and how users interact with the system declaratively.

### Perception Policy Mechanics

The perception record model described in this document is a starting point. The mechanics of decay, reinforcement, and attention scheduling need formalization — decay functions, reinforcement algorithms, attention budgets, and the interaction between the four perception sources need precise specification.

### Execution Framework

The execution framework — sidecar integration, tool abstraction, permission boundaries, isolated execution — is defined as a Fabric capability but needs detailed design. How are execution permissions declared? How are sidecars managed? How is execution isolation enforced?

### Cognition Persistence Schema

Cognitive artifacts need storage schemas. The concept-before-persistence principle means the information model is defined first, but at some point, concrete CRD schemas, database schemas, or storage formats need to be specified.

### Security Model Details

Trust boundaries are defined at the distribution level, but the details of authentication, authorization, credential management, and cross-distribution trust need formal specification.

### Fabric Component Model and Distribution Wiring

Several architectural questions remain about the boundary between the Fabric and distributions:

- **What components does the Fabric consist of?** The Fabric is defined as a set of capability areas, but its concrete component structure — what processes run, what APIs are exposed, what services exist — is not yet specified.
- **What components does each distribution bring?** Beyond personality and tools, what does a distribution deploy that the Fabric does not? Is a distribution a single process, a set of processes, or a Helm chart?
- **What exactly does the Fabric configure and provide?** When the user provides infrastructure (e.g., a PostgreSQL instance), does the Fabric configure the connection and expose it to distributions? Or do distributions connect directly?
- **How is user-provided infrastructure wired to distributions?** If the user provides storage, is it given to distributions through Fabric-managed interfaces, or through distribution-specific declarations (CRDs)? This determines whether the Fabric is a passthrough or a broker.
- **What is the Fabric's operational footprint?** How many pods does the Fabric need? What resources does it consume? This affects the minimal installation size and edge viability.

These questions will be addressed in a future design document.

### Testing and Validation

Distribution independence is an architectural constraint that must be validated. Each distribution needs test suites that verify correct operation in isolation — no other distributions present, no inter-distribution communication available.

---

## 18. Appendix: Glossary

| Term | Definition |
|------|-----------|
| **Adaptive Perception** | The mechanism by which each agent computes what to observe, adaptively evolving its attention policy over time through cognition memory feedback |
| **Cognition Store** | The active feedback mechanism that stores and serves cognitive state — not passive memory but a system that influences future perception and reasoning |
| **Cognitive Artifact** | A conceptual unit of cognition: Perception, Observable, Observation, Session, Task, Memory, Skill, Intent |
| **Cognitive Flow** | The pipeline through which cognition moves: Perception → Observation → Session → Task → Execution → Memory → (feedback) |
| **Decay** | The process by which irrelevant signals are gradually deprioritized in perception, making room for more useful signals |
| **Distribution** | An independently installable assembly: Fabric + Personality + Tools + Persistence + Deployment Form |
| **Emissary** | The external system cognitive role — extends cognition and execution beyond Kubernetes to VMs, bare metal, and external systems |
| **Fabric** | The shared cognitive substrate — the reusable cognitive engine that all distributions are built on |
| **Forgetting** | The active suppression of irrelevant signals in perception — a feature, not a bug |
| **Intent** | Desired operational expectations that influence reasoning and perception — what *should* happen |
| **Memory** | Durable cognition — knowledge that persists beyond active Sessions and feeds back into perception |
| **Observable** | A declarative perception-guidance artifact — influences how agents compute perception policy but does not control it |
| **Observation** | A selected, context-relevant signal that has entered cognition — not a raw log, but a signal shaped by perception |
| **Perception Policy** | An agent's current computation of what to observe, how often, and under what conditions |
| **Perception Record** | A record in the perception database specifying what an agent should perceive and how |
| **Personality** | The role-specific behavior, responsibility focus, and operational heuristics that distinguish one distribution from another |
| **Reconciliation** | The Kubernetes mechanism that converges actual state toward declared intent — k8s-hermes-collective does not duplicate this |
| **Regent** | The cluster cognitive authority — singleton role responsible for cluster-wide cognition, orchestration, and arbitration |
| **Reinforcement** | The process by which useful signals are strengthened in perception based on historical cognitive outcomes |
| **Role** | A responsibility domain — defines what an agent cares about, not how it is deployed |
| **Session** | Bounded active reasoning — an investigation, incident analysis, or maintenance activity |
| **Skill** | Reusable operational capability — a procedure that can guide or automate execution |
| **Steward** | The application cognitive role — understands and coordinates application operations within a namespace or service domain |
| **Task** | An executable work unit created through cognition — action-oriented, may be delegated |
| **Warden** | The node cognitive executor — privileged, node-local brain and hands |

---

*k8s-hermes-collective — A distributed cognitive operator for Kubernetes and beyond.*
