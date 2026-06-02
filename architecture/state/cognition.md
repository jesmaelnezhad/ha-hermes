# Cognitive State Model

## Overview

Hermes-on-K8s maintains a distributed cognitive layer.

This layer is distinct from:
- Git (declarative intent)
- Kubernetes etcd (runtime truth)

Hermes cognition represents operational thinking, memory, coordination, and adaptive perception.

## Concept Before Persistence

The cognition model is defined conceptually before storage or schema decisions.

Core cognitive artifacts include:
- Perception (adaptive attention mechanism)
- Observation (selected, context-relevant signals)
- Session (bounded active reasoning)
- Task (executable work unit)
- Memory (durable cognition)
- Skill (reusable operational capability)
- Intent (desired operational expectations)

## Cognitive Flow

```
Perception Policy → Observation → Session → Task → Execution → Memory
                                               ↑                    |
                                               └────────────────----+
                                          (feedback loop)
```

Skill and Intent influence reasoning and execution at every stage.

## Cognition Store Role

The cognition store is NOT passive memory. It is an **active feedback mechanism**:

- influences future perception policies
- adapts observation behavior over time
- enables forgetting of irrelevant signals
- reinforces useful historical patterns

## Persistence

Storage strategy is implementation specific and defined later.

Possible approaches include:
- Kubernetes-backed state
- RWX storage
- object storage
- database-backed cognition

## Signal Hierarchy Constraint

Hermes does NOT ingest raw telemetry into the cognitive layer.

Raw signals (logs, metrics, traces, events) stay in external systems. Only meaningful, selected signals become Observations through each agent's adaptive perception policy.

## Purpose

Cognitive state enables Hermes agents to:
- remember
- investigate
- coordinate
- learn
- reason collectively
- adapt their attention over time

## Summary

Cognitive state enables Hermes agents to behave as a coordinated cognitive system with adaptive perception, rather than static observability-powered executors.
