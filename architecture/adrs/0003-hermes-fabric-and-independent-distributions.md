# ADR 0003: Hermes Fabric and Independent Distributions

## Status

Accepted.

## Context

hermes-on-k8s defines four roles: Regent, Warden, Steward, and Emissary. These roles are **responsibility domains**, not deployment units. The current architecture lacks a clear separation between:

- the shared cognitive machinery all roles need
- the independently installable assemblies that operationalize those roles

Without this separation, a user who needs only Steward-level application cognition must install the entire system — including Regent, Warden, and all associated infrastructure. This contradicts the principle that hermes-on-k8s should be modular and adoptable incrementally.

## Decision

Introduce a multi-tier architectural model:

```
Fabric  +  Personality  +  Tools  +  Persistence  +  Deployment Form  =  Distribution
```

### 1. Hermes Fabric (Shared Cognitive Substrate)

All distributions share a common **Hermes Fabric** — the reusable cognitive engine. The fabric is NOT a role, NOT a distribution, and NOT a Kubernetes resource. It provides:

- **Cognition**: cognition store, memory persistence, adaptive perception engine, session handling, task lifecycle, reasoning lifecycle, skill execution, cognition feedback
- **Adaptive Perception**: perception policy computation, Observable interpretation, attention scheduling, observation prioritization, adaptive learning and forgetting, perception history, signal relevance evolution
- **Execution Framework**: task execution lifecycle, tool abstraction, isolated execution, permission boundary support, executor coordination, sidecar integration
- **Communication**: inter-agent communication, coordination transport, cognition synchronization, distributed awareness, conflict reporting (detailed semantics TBD)
- **Persistence**: memory persistence, cognition durability, learned perception history, task/session history, adaptive state continuity

Loss of pod identity MUST NOT imply loss of cognition.

### 2. Distributions (Independently Installable Assemblies)

A **Distribution** is an independently installable assembly built on top of the fabric. Distributions are deployable systems; roles are conceptual responsibility domains.

Each distribution MUST be:

- independently deployable
- independently useful
- self-cognitive
- self-persistent
- operationally meaningful without requiring other distributions

The following distributions are recognized:

| Distribution              | Personality | Scope                                        |
| ------------------------- | ----------- | -------------------------------------------- |
| **Regent Distribution**   | Regent      | Cluster-wide singleton                       |
| **Warden Distribution**   | Warden      | Node-level (one per node, or selected nodes) |
| **Steward Distribution**  | Steward     | Namespace / service domain                   |
| **Emissary Distribution** | Emissary    | VM / bare metal / external systems           |

Integration between distributions is **optional**. Independence is **required**.

Examples:
- Regent alone: valid, useful, operational
- Warden alone: valid, useful, operational
- Steward alone: valid, useful, operational
- Emissary alone: valid, useful, operational

## Consequences

### Benefits
- Users install only what they need — lower barrier to entry
- Each distribution can be versioned, tested, and upgraded independently
- Clear separation: fabric owns cognition, personality owns responsibility, tools own action
- Consistent with existing ADRs (0001, 0002) — does not change role semantics or Kubernetes authority
- Repository can be restructured later into `fabric/` and `distributions/` without architectural change

### Trade-offs
- More packages/artifacts to build, version, and distribute
- Each distribution must bundle or reference the shared fabric — dependency management must be explicit
- Inter-distribution communication is still TBD — independent deployments must function without it, but coordinated deployments need a communication model
- Persistence must be provisioned per distribution (each is self-persistent), which may increase storage requirements
- Install documentation must clearly explain: fabric first, then choose distributions