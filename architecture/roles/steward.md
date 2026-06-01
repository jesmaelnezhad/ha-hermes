# Steward — Application Cognitive Role

## Overview

Steward is a declarative, application-scoped cognitive agent.

Stewards are intentionally created after bootstrap.

They understand and coordinate application operations within a defined scope.

## Declaration

Stewards are user-declared via CRDs and configuration.

Observation scope is NOT dynamically chosen freely. It is defined via:
- CRDs
- Observable configuration
- system knowledge constraints
- cognition history adaptation

Typical scope:
- namespace
- service domain
- shared application boundary

## Responsibilities

### Application Awareness
- observe workloads and services
- inspect logs and metrics
- understand topology and dependencies
- application/namespace reasoning

### Incident Analysis
- diagnose failures
- correlate incidents
- coordinate remediation

### Reporting
- service-level reporting
- operational guidance
- cluster-wide reporting (optional participation)

### Alerting
- optional alerting participation

### Configuration
- CLI-based product configuration interface

### Memory and Context
- maintain application knowledge
- record operational context
- contribute cognitive state

### Coordination
- coordinate with Wardens
- coordinate with Emissaries
- participate in Regent coordination

## Observation Perception

Stewards independently compute their own perception policy using:
- role-native knowledge (application/domain heuristics)
- declaration data (CRDs, role specs, scope boundaries)
- Observable hints (signal sources, thresholds, sampling guidance)
- cognition memory (learned relevance, signal decay, reinforcement)

## Constraints

- Stewards do not replace Kubernetes operators
- Stewards do not own reconciliation authority
- Kubernetes remains authoritative for runtime convergence

## Summary

Stewards are declared application-scoped cognitive operators with CRD-defined observation boundaries.
