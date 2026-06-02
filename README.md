# HA-Hermes

HA-Hermes is a distributed cognitive operator layered over Kubernetes and external systems.

Kubernetes remains the execution and reconciliation substrate.
Hermes provides cognition, coordination, and adaptive operational intelligence.

## Core Model

HA-Hermes is a **distributed cognitive system with adaptive perception**, not a static observability pipeline.

### Three Concepts

- **Runtime** — shared cognitive substrate (cognition, perception, execution, persistence)
- **Role** — responsibility domain (not a runtime state, not a deployment form)
- **Distribution** — independently installable assembly (Runtime + role personality + tools + persistence + deployment form)

### Structural Decomposition

- **Kubernetes** = execution substrate
- **Roles** = responsibility domains
- **Distributions** = operational deployments
- **Perception system** = adaptive attention mechanism
- **Cognition store** = active feedback loop
- **Tasks** = execution units

## Roles

### Native Roles (installed at bootstrap)

| Role | Domain | Scope |
|------|--------|-------|
| **Regent** | Cluster Cognitive Authority | Singleton, cluster-wide |
| **Warden** | Node Cognitive Executor | One per Kubernetes node |

### Declared Roles (created via CRDs after bootstrap)

| Role | Domain | Scope |
|------|--------|-------|
| **Steward** | Application Cognitive | Namespace / service domain |
| **Emissary** | External System Cognitive | VM / bare metal / external |

Roles define **responsibility domains**, not runtime states.
No role is emergent from another. No state transitions between roles.
Each distribution is independently deployable and independently useful.

## Distribution Independence

- Regent alone — valid, useful, operational
- Warden alone — valid, useful, operational
- Steward alone — valid, useful, operational

Integration is optional. Independence is required.

## Perception System

Each agent independently computes its own perception policy:

> What to observe + how often + under what conditions

Four sources influence perception:
1. Agent-native knowledge (domain expertise, heuristics)
2. Declaration data (CRDs, role specs, scope boundaries)
3. Observable guidance (signal sources, thresholds, sampling guidance)
4. Cognition memory (learned relevance, signal decay, reinforcement)

Key properties:
- Perception is distributed — no centralized observation filter
- Perception is adaptive — evolves via cognition memory feedback
- Observable influences but does not centrally control perception

## Principles

- Kubernetes remains authoritative for reconciliation
- HA-Hermes augments rather than replaces operators
- Git stores declarative intent
- etcd stores runtime truth
- Hermes stores cognitive state and memory
- Roles define responsibility, not runtime states
- Perception is adaptive and distributed
- Distribution independence

## Cognitive Artifacts

| Artifact | Purpose |
|----------|---------|
| Perception | Adaptive attention mechanism |
| Observable | Declarative perception-guidance artifact |
| Observation | Selected, context-relevant signals |
| Session | Bounded active reasoning |
| Task | Executable work unit |
| Memory | Durable cognition + perception feedback |
| Skill | Reusable operational capability |
| Intent | Desired operational expectations |

## Arbitration

When multiple distributions coexist, Regent performs arbitration.

When Regent is absent, conflicts are surfaced and deferred to human authority. Human authority remains final.

## Vision

A distributed cognitive and operational layer that helps maintain infrastructure and applications through reasoning, coordination, and adaptive perception.
