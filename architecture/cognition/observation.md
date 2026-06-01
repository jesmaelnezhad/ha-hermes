# Observation

## Overview

Observation represents perception inside the Hermes collective.

Observations are NOT raw logs — they are **selected, context-relevant signals** derived from external substrates.

Examples include:
- Kubernetes events
- logs
- metrics
- topology changes
- node conditions
- external system signals

## Perception Model

Perception is NOT a static filter. It is a **dynamic, adaptive policy system**.

Each agent independently computes its own perception policy:

> What to observe + how often + under what conditions

### Sources Influencing Perception

#### (1) Agent-Native Knowledge
- embedded domain expertise
- DevOps/Kubernetes understanding
- role-specific heuristics

#### (2) Declaration Data
- CRDs
- role specifications
- scope boundaries

#### (3) Observable / Emissary Hints
- suggested signal sources
- thresholds
- sampling guidance
- environment constraints

#### (4) Cognition Memory (Adaptive Layer)
- learned signal importance
- historical relevance
- signal decay or suppression
- reinforcement of useful observations

## Key Corrections

- Observability is NOT centrally filtered
- Observability is NOT static
- Each agent independently computes perception policy using the four sources above

## Purpose

Observations provide raw inputs to cognition.

They may trigger:
- Sessions
- Tasks
- reasoning
- escalation

## Ownership

Observations are not owned.

They are perceived by agents operating within their scope, according to their adaptive perception policy.
