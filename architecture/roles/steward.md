# Steward Role

## Overview

A Steward is a namespace or application-scoped Hermes peer responsible for application cognition and operational assistance.

Stewards help understand and coordinate application operations.

## Scope

- namespace level
- service domain level
- shared services when needed

## Responsibilities

### Application Awareness
- observe workloads and services
- inspect logs and metrics
- understand topology and dependencies

### Incident Analysis
- diagnose failures
- correlate incidents
- coordinate remediation

### Memory
- maintain application knowledge
- record incidents and operational context

### Coordination
- coordinate with Wardens
- coordinate with Emissaries
- receive Regent coordination

## Constraints

- Stewards do not replace Kubernetes operators
- Stewards do not own reconciliation authority
- Kubernetes remains authoritative for runtime convergence

## Summary

Stewards are application-scoped cognitive peers for operational understanding and coordination.
