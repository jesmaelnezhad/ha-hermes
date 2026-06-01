# Steward Role

## Overview

A Steward is a declared Hermes role responsible for application cognition and operational assistance.

Stewards are intentionally created after bootstrap.

They help understand and coordinate application operations.

## Declaration

Stewards are user-declared and scoped.

Typical scope:

- namespace
- service domain
- shared application boundary

Responsibility emerges from declared scope.

## Responsibilities

### Application Awareness
- observe workloads and services
- inspect logs and metrics
- understand topology and dependencies

### Incident Analysis
- diagnose failures
- correlate incidents
- coordinate remediation

### Memory and Context
- maintain application knowledge
- record operational context
- contribute cognitive state

### Coordination
- coordinate with Wardens
- coordinate with Emissaries
- participate in Regent coordination

## Constraints

- Stewards do not replace Kubernetes operators
- Stewards do not own reconciliation authority
- Kubernetes remains authoritative for runtime convergence

## Summary

Stewards are declared application-scoped cognitive operators.