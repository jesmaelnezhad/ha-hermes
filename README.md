# HA-Hermes

HA-Hermes is a distributed cognitive operator layered over Kubernetes and external systems.

Kubernetes remains the execution and reconciliation substrate.
Hermes provides cognition, coordination, and adaptive operational intelligence.

## Core Model

HA-Hermes is a **distributed cognitive system with adaptive perception**, not a static observability pipeline.

### Structural Decomposition

- **Kubernetes** = execution substrate
- **Roles** = responsibility domains (not runtime states)
- **Perception system** = adaptive attention mechanism
- **Cognition store** = active feedback loop (not passive memory)
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

Roles define **responsibility domains**, not implementation forms or runtime states.
No role is an emergent state of another role. No promotion or election-based identity transitions exist.

## Perception System

Each agent independently computes its own perception policy:

> What to observe + how often + under what conditions

Four sources influence perception:
1. Agent-native knowledge (domain expertise, heuristics)
2. Declaration data (CRDs, role specs, scope boundaries)
3. Observable / Emissary hints (signal sources, thresholds, guidance)
4. Cognition memory (learned relevance, signal decay, reinforcement)

Key properties:
- Perception is distributed — no centralized observation filter
- Perception is adaptive — evolves via cognition memory feedback
- No raw telemetry ingestion into the cognition layer

## Principles

- Kubernetes remains authoritative for reconciliation
- HA-Hermes augments rather than replaces operators
- Git stores declarative intent
- etcd stores runtime truth
- Hermes stores cognitive state and memory
- Roles define responsibility, not runtime states
- Perception is adaptive and distributed

## Cognitive Artifacts

| Artifact | Purpose |
|----------|---------|
| Perception | Adaptive attention mechanism |
| Observation | Selected, context-relevant signals |
| Session | Bounded active reasoning |
| Task | Executable work unit |
| Memory | Durable cognition + perception feedback |
| Skill | Reusable operational capability |
| Intent | Desired operational expectations |

## Vision

A distributed cognitive and operational layer that helps maintain infrastructure and applications through reasoning, coordination, and adaptive perception.
