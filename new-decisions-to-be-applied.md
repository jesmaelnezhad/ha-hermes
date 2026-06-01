# HA-Hermes — Consolidated Architectural Decisions & New System Understanding

This document captures the **latest refined architectural decisions, clarifications, and corrections** derived from iterative design discussions of the HA-Hermes system.

It is intended as a **single source of truth for updating and reconciling the repository structure, role semantics, and cognition model**.

---

# 1. Core System Identity Shift

## 1.1 From static agent system → adaptive cognitive operator system

HA-Hermes is no longer defined as a set of independent agents.

It is a:

> Distributed cognitive operator layered over Kubernetes and external systems.

Kubernetes remains the execution substrate.
Hermes provides cognition, coordination, and adaptive operational intelligence.

---

# 2. Role System (Finalized Semantics)

## 2.1 Core Principle

Roles define **responsibility domains**, not implementation forms or runtime states.

No role is an emergent state of another role.
No promotion or election-based identity transitions exist.

---

## 2.2 Regent (Cluster Cognitive Authority)

### Definition
Regent is a **native singleton role** responsible for cluster-wide cognition and orchestration.

### Responsibilities
- cluster lifecycle management (node add/remove/recovery)
- cross-agent conflict resolution
- cluster-wide reporting
- orchestration coordination
- administrative CLI interface for operators

### Execution model
- Regent is brain + orchestration authority
- Execution is delegated (not directly performed)
  - Wardens
  - Emissaries
  - sidecar executors

### Critical constraints
- NOT emergent
- NOT elected
- NOT derived from Warden state
- NOT a runtime role transition

---

## 2.3 Warden (Node Cognitive & Execution Role)

### Definition
Warden is a Kubernetes node–resident cognitive executor.

### Responsibilities
- node health and recovery
- privileged system execution
- Kubernetes API interaction
- workload and node observation
- execution of delegated tasks

### Constraints
- does not become Regent
- no election or promotion semantics
- operates within node scope

---

## 2.4 Steward (Application / Namespace Cognitive Role)

### Definition
Steward is a declarative, application-scoped cognitive agent.

### Responsibilities
- application/namespace reasoning
- incident analysis
- service-level reporting
- operational guidance
- optional alerting participation
- CLI-based product configuration interface

### Key property
- observation scope is NOT dynamically chosen freely
- it is defined via:
  - CRDs
  - Observable configuration
  - system knowledge constraints
  - cognition history adaptation

---

## 2.5 Emissary (External System Cognitive Role)

### Definition
Emissary is a declarative external-infrastructure cognitive agent.

### Responsibilities
- SSH-based system control
- VM/bare-metal operations
- external system integration
- non-Kubernetes operational execution

### Scope difference from Steward
- Steward: Kubernetes / namespace domain
- Emissary: external systems / machines

---

# 3. Perception Model (Critical Revision)

## 3.1 Core principle

Perception is NOT a static filter.

It is a dynamic, adaptive policy system.

---

## 3.2 Perception Definition

Each agent continuously computes a perception policy:

> What to observe + how often + under what conditions

---

## 3.3 Sources influencing perception

### (1) Agent-native knowledge
- embedded domain expertise
- DevOps/Kubernetes understanding
- role-specific heuristics

### (2) Declaration data
- CRDs
- role specifications
- scope boundaries

### (3) Observable / Emissary hints
- suggested signal sources
- thresholds
- sampling guidance
- environment constraints

### (4) Cognition memory (adaptive layer)
- learned signal importance
- historical relevance
- signal decay or suppression
- reinforcement of useful observations

---

## 3.4 Key correction

- Observability is NOT centrally filtered
- Observability is NOT static

Instead:

> Each agent independently computes perception policy using the four sources above.

---

# 4. Signal Hierarchy (Scalability Constraint)

## 4.1 Raw infrastructure layer (external systems)
- logs
- metrics
- traces
- Kubernetes events

Hermes does NOT store all raw signals.

---

## 4.2 Cognitive observation layer
Only meaningful signals become Observations.

Observations are NOT raw logs.
They are **selected, context-relevant signals**.

---

## 4.3 Cognitive layer
- Sessions
- Tasks
- Intent
- Memory updates

---

# 5. Observable Concept (Reframed)

Observable is NOT a strict filter.

It is:

> Declarative guidance influencing perception behavior.

It provides:
- hints for signal relevance
- suggested observation frequency
- domain boundaries
- thresholds

But:

- does NOT enforce perception
- does NOT centrally control observation

---

# 6. Cognition Store Role

The cognition store is not passive memory.

It is an active feedback mechanism:

- influences future perception policies
- adapts observation behavior over time
- enables forgetting of irrelevant signals

---

# 7. System-Level Principle

## 7.1 Key principle

> HA-Hermes is a distributed cognitive system with adaptive perception, not a static observability pipeline.

---

## 7.2 Structural decomposition

- Kubernetes = execution substrate
- Roles = responsibility domains
- Perception system = adaptive attention mechanism
- Cognition store = feedback loop
- Tasks = execution units

---

# 8. Stability Constraints

- No role is derived from another via state transition
- No global centralized observation filter exists
- No raw telemetry ingestion into cognition layer
- Perception is distributed and adaptive

---

# 9. Intended Use

This document should be used to:

- update all architecture documentation
- reconcile role definitions
- adjust cognition and observation models
- guide implementation of execution layer
- ensure consistency across system design
