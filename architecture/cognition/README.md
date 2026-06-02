# Cognition Model

## Overview

HA-Hermes is a distributed cognitive operator with **adaptive perception**.

This directory defines the information model used by the Hermes collective.

The model is defined before implementation schemas or CRDs.

## System Identity

HA-Hermes is a distributed cognitive system with adaptive perception, **not** a static observability pipeline.

## Cognitive Flow

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

Intent and Skill influence reasoning and execution at every stage.

## Signal Hierarchy

### Raw Infrastructure Layer (external systems)
- logs, metrics, traces, Kubernetes events

Hermes does NOT store all raw signals.

### Cognitive Observation Layer
Only meaningful signals become Observations.

Observations are NOT raw logs — they are selected, context-relevant signals shaped by each agent's adaptive perception policy.

### Cognitive Layer
- Sessions, Tasks, Intent, Memory updates

## Cognitive Artifacts

- Perception — adaptive attention mechanism
- Observable — perception guidance artifact
- Observation — selected, context-relevant signals
- Session — bounded active reasoning
- Task — executable work unit
- Memory — durable cognition
- Skill — reusable operational capability
- Intent — desired operational expectations

These are conceptual artifacts and are not automatically Kubernetes resources.

Observable is expected to evolve into a first-class CRD and cognition artifact.

Persistence and implementation are defined later.