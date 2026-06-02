# Request for Change — Hermes Runtime and Independent Distributions

## Purpose

This document describes a new architectural refinement for HA-Hermes.

The purpose of this request is to introduce a clean separation between:

- shared Hermes cognitive runtime
- independently installable Hermes distributions
- role semantics
- execution tooling

This is not merely a naming or packaging change.

It is a structural architectural clarification intended to make HA-Hermes:

- modular
- independently deployable
- easier to reason about
- reusable across multiple operational domains
- consistent with earlier decisions about cognition, perception, and role ownership.

---

# 1. Core Architectural Clarification

A new distinction must be introduced:

Role ≠ Distribution ≠ Runtime

These are separate concepts and should not be conflated.

Historically, the repository has defined:

- Regent
- Warden
- Steward
- Emissary

primarily as roles.

That remains correct.

However, the system now needs an additional layer:

> independently installable Hermes assemblies.

These are not roles.

They are operational assemblies built from:

- shared runtime
- role personality
- tools and permissions
- persistence model
- deployment form

This document proposes introducing this layer.

---

# 2. Hermes Runtime (Shared Cognitive Substrate)

A new architectural component should be formally introduced:

> Hermes Runtime

Hermes Runtime is NOT:

- a role
- a distribution
- a Kubernetes resource
- a deployment topology

Instead, it is:

> the reusable cognitive substrate shared by all Hermes distributions.

The runtime is the common foundation that allows Regent, Warden, and Steward to exist as independently installable systems while preserving coherent cognition behavior.

The runtime owns reusable cognitive and operational mechanisms.

---

## 2.1 Runtime Responsibilities

Hermes Runtime should own the common machinery used by all distributions.

This includes several major domains.

### Cognition

Runtime should provide:

- cognition store
- memory persistence
- adaptive perception engine
- session handling
- task lifecycle support
- reasoning lifecycle support
- skill execution model
- cognition feedback mechanisms

Runtime owns the cognitive substrate.

Role semantics do not reimplement cognition.

---

### Adaptive Perception

Runtime should provide:

- perception policy computation
- Observable interpretation
- attention scheduling
- observation prioritization
- adaptive learning and forgetting
- perception history
- signal relevance evolution

Adaptive perception remains consistent with previous architectural decisions:

Perception derives from:

- native knowledge
- declaration data
- Observable guidance
- cognition memory

The runtime should provide the machinery for this process.

Roles and distributions supply domain knowledge and priorities.

---

### Execution Framework

Runtime should provide:

- task execution lifecycle
- tool abstraction
- isolated execution model
- permission boundary support
- executor coordination
- sidecar integration model

Execution remains distinct from cognition.

The runtime provides execution infrastructure.

Roles determine when and why execution occurs.

---

### Communication

Runtime should eventually provide:

- inter-agent communication
- coordination transport
- cognition synchronization
- distributed awareness support
- conflict reporting support

Detailed communication semantics remain future work.

This document only identifies communication as a runtime concern.

---

### Persistence

Runtime should provide durable cognition support.

This includes:

- memory persistence
- cognition durability
- learned perception history
- task history
- session history
- adaptive state continuity

Every runtime-backed distribution should maintain persistent cognition.

Loss of pod identity should not imply loss of cognition.

---

# 3. Distribution Layer (Independent Installables)

A second architectural layer should be introduced:

> Hermes Distributions

The word "distribution" is intentionally used instead of "product" to avoid collision with Steward's business or application product domain.

A distribution is:

> an independently installable assembly built from Hermes Runtime and a role personality.

Distributions are deployable systems.

Roles are conceptual responsibility domains.

Distributions operationalize roles.

---

# 4. Runtime + Personality + Tools

The proposed model is:

Runtime + Personality + Tools + Persistence + Deployment Form = Distribution

This is the primary assembly rule.

Runtime provides shared cognition.

Personality provides:

- role-native knowledge
- priorities
- responsibility model
- perception priors
- operational semantics

Tools provide:

- permitted actions
- execution environment
- operational capability

Persistence provides:

- durable cognition
- continuity

Deployment form provides:

- Kubernetes topology
- placement
- lifecycle

---

# 5. Regent Distribution

A new independent distribution should be recognized:

> Regent Distribution

Regent Distribution consists of:

- Hermes Runtime
- Regent personality
- cluster orchestration tools
- secure execution tooling
- persistent cognition

Regent Distribution is independently installable.

It must remain useful even when no Warden or Steward exists.

---

## 5.1 Regent Responsibilities

Regent Distribution focuses on cluster concerns.

Examples include:

- node addition
- node recovery
- node deletion
- cluster reporting
- cluster health awareness
- coordination
- arbitration
- operational monitoring
- administrative assistance

Regent acts as:

- cluster cognitive authority
- administrator-facing operational CLI
- orchestration system

---

## 5.2 Regent Execution

Previous decisions remain valid.

Regent is primarily:

- brain
- orchestration authority

Execution should normally occur through:

- delegated executors
- isolated tooling
- permitted sidecars
- controlled operational tools

The phrase:

"Regent does not directly execute"

should be interpreted as:

> Regent uses permitted execution mechanisms rather than collapsing cognition and unrestricted execution into a single trust boundary.

Regent may possess isolated or tool-mediated execution capability.

---

## 5.3 Regent Persistence

Regent must preserve cognition.

This includes:

- cluster knowledge
- learned relevance
- operational history
- perception adaptation
- reporting history

Regent cognition is durable.

---

# 6. Warden Distribution

A second independent distribution should be introduced:

> Warden Distribution

Warden Distribution consists of:

- Hermes Runtime
- Warden personality
- privileged node tools
- persistent cognition

Warden Distribution is independently installable.

One or many Wardens may exist.

Wardens may be deployed to:

- one node
- selected nodes
- all nodes

depending on operational needs.

---

## 6.1 Warden Responsibilities

Warden focuses on:

- node health
- node recovery
- privileged execution
- node-local cognition
- Kubernetes awareness
- delegated execution
- operational assistance

Warden remains:

- guardian of nodes
- node-local brain and hands
- privileged cognitive executor

---

## 6.2 Warden Persistence

Warden must preserve:

- node memory
- learned relevance
- operational history
- perception adaptation
- cognition continuity

Warden cognition is durable.

---

# 7. Steward Distribution

A third independent distribution should be introduced:

> Steward Distribution

Steward Distribution consists of:

- Hermes Runtime
- Steward personality
- application tools
- persistent cognition
- highly available deployment model

Steward Distribution is independently installable.

Steward must remain useful without Regent or Warden.

---

## 7.1 Steward Responsibilities

Steward focuses on application and operational scope.

Examples:

- application maintenance
- optimization
- reporting
- operational guidance
- product or namespace cognition
- alerting participation
- product-facing CLI

Steward remains declarative and adaptive.

---

## 7.2 Steward High Availability

Steward is expected to support highly available deployment.

This includes:

- replicated runtime
- durable cognition
- resilient operational continuity

Detailed synchronization semantics remain future work.

---

# 8. Independence Principle

A major architectural principle should be introduced:

> Distribution Independence

Each distribution must be:

- independently deployable
- independently useful
- self-cognitive
- self-persistent
- operationally meaningful without requiring others

This is a deliberate design goal.

Examples:

Regent alone:

- valid
- useful
- operational

Warden alone:

- valid
- useful
- operational

Steward alone:

- valid
- useful
- operational

Integration is optional.

Independence is required.

---

# 9. Arbitration Without Regent

A new operational principle should be introduced.

When multiple distributions coexist:

- conflict may occur
- competing actions may arise
- disagreement may emerge.

Regent normally performs arbitration.

However:

Regent may be absent.

---

## 9.1 Human Fallback Arbitration

The system should follow:

> Human fallback arbitration

Hierarchy:

1. Human authority
2. Regent arbitration
3. Human escalation when Regent absent

Meaning:

If:

- Regent absent
- conflicting decisions detected
- tie breaking required

Then:

- conflict is surfaced
- action is deferred
- human intervention requested

Steward should shy away from conflict rather than assume authority.

Warden should not dominate simply due to local visibility.

Human authority remains final.

---

# 10. Repository-Level Implications

Repository organization may eventually require a new structure.

Potential future direction:

runtime/
  hermes-runtime.md

 distributions/
   regent/
   warden/
   steward/

This remains a future repository concern.

The present RFC focuses only on conceptual clarification.

---

# Summary

This RFC introduces a new architectural distinction:

- Runtime
- Distribution
- Role

Runtime:

- reusable cognition engine

Distribution:

- independently installable assembly

Role:

- responsibility domain

The goal is to preserve:

- modularity
- adaptive cognition
- independent deployment
- clean separation of concerns
- future scalability of HA-Hermes architecture.