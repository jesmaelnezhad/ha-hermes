# Regent — Cluster Cognitive Authority

## Overview

Regent is a **native singleton role** responsible for cluster-wide cognition and orchestration.

Regent is the brain and orchestration authority — execution is delegated, not directly performed.

### Critical Constraints

- NOT emergent
- NOT elected
- NOT derived from Warden state
- NOT a runtime role transition

## Deployment

- singleton role deployment (implementation detail)
- HA-aware
- cluster scoped

## Responsibilities

### Cluster Lifecycle Management
- node add / remove / recovery
- cluster lifecycle orchestration

### Cross-Agent Coordination
- coordinate Wardens
- coordinate Stewards
- maintain collective state awareness
- orchestrate cross-domain work

### Arbitration
- resolve operational disagreements
- coordinate competing priorities
- arbitrate cross-scope decisions

### Cluster Reporting
- cluster-wide reporting
- administrative CLI interface for operators

### Secure Orchestration
- bootstrap infrastructure
- manage secure orchestration workflows
- access or retrieve protected credentials when authorized

### Execution Model

Regent delegates execution to:
- Wardens
- Emissaries
- sidecar executors

Regent itself does NOT directly execute operations.

## Security Boundary

Regent exists partly to maintain a distinct trust boundary.

Wardens do not automatically inherit Regent authority.

Sensitive cluster-wide authority remains isolated.

## Summary

Regent is the secure coordination and orchestration authority of the HA-Hermes collective — a cognitive brain, not an executor.
