# Perception System

## Overview

Perception in Hermes-on-K8s is NOT a static filter or a centralized observability pipeline.

It is a dynamic, adaptive attention mechanism that each agent computes independently.

## Definition

Each agent continuously computes a perception policy:

> What to observe + how often + under what conditions

## The Four Sources

### Source 1: Agent-Native Knowledge

Every agent carries embedded domain expertise:
- DevOps and Kubernetes understanding
- Role-specific heuristics (Warden vs Steward vs Emissary)
- Built-in operational patterns

This is the baseline perception that exists before any runtime adaptation.

### Source 2: Declaration Data

CRDs and role specifications define:
- Scope boundaries (what an agent is responsible for)
- Role specifications (what a Warden vs Steward should focus on)
- Observable configuration (declarative perception hints)

Declaration data constrains and focuses perception but does not rigidly enforce it.

### Source 3: Observable / Emissary Hints

External guidance influences perception:
- Suggested signal sources
- Recommended thresholds
- Sampling frequency guidance
- Environment constraints
- Emissary-provided context about external systems

### Source 4: Cognition Memory (Adaptive Layer)

This is the feedback loop that makes perception adaptive:

- **Learned signal importance**: signals that historically led to useful cognition are reinforced
- **Historical relevance**: patterns from past Sessions and Tasks inform what to watch
- **Signal decay**: irrelevant signals are gradually deprioritized
- **Reinforcement**: useful observations are strengthened over time
- **Forgetting**: irrelevant signals are actively suppressed

## Perception Is Distributed

No global centralized observation filter exists.

Each agent independently computes its own perception policy using all four sources. Two agents with the same role may have different perception policies due to different cognition memory and placement.

## Key Principles

- Perception is distributed and adaptive
- No raw telemetry ingestion into the cognition layer
- Observable is declarative guidance, not a strict filter
- The cognition store is an active feedback mechanism, not passive memory

## Relationship to Other Artifacts

| Artifact    | Relationship                                                                      |
| ----------- | --------------------------------------------------------------------------------- |
| Observation | Output of perception — selected signals that enter cognition                      |
| Session     | Consumes observations, may update perception policy via memory                    |
| Task        | May be triggered by observations                                                  |
| Memory      | Stores perception learnings — feeds back into future perception                   |
| Intent      | Influences what an agent should prioritize observing                              |
| Skill       | May encode perception patterns or known behavior for specific operational domains |
