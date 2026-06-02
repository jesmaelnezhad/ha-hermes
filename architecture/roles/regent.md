# Regent — Cluster Cognitive Authority

## Overview

Regent is a **singleton role** responsible for cluster-wide cognition and orchestration.

Regent is the brain and orchestration authority — execution is delegated to sidecar executors.
 
Regent must remain useful even when no other distribution exists.

## Deployment

- singleton role deployment (implementation detail)
- HA-aware
- cluster scoped

## Responsibilities

### Cluster Lifecycle Management
- node add / remove / recovery
- cluster lifecycle orchestration

### Cross-Distribution Coordination
- coordinate with Wardens when present
- coordinate with Stewards when present
- maintain collective state awareness
- orchestrate cross-domain work

### Arbitration
- resolve operational disagreements
- coordinate competing priorities
- arbitrate cross-scope decisions

When Regent is absent, conflicts are surfaced and deferred to human authority.

### Cluster Reporting
- cluster-wide reporting
- administrative CLI interface for operators

### Secure Orchestration
- bootstrap infrastructure
- manage secure orchestration workflows
- access or retrieve protected credentials when authorized

### Execution Model

Regent delegates execution to:
- sidecar executors
- controlled operational tools

Regent uses permitted execution mechanisms rather than collapsing cognition and unrestricted execution into a single trust boundary. Regent may possess isolated or tool-mediated execution capability.

## Persistence

Regent cognition is durable:
- cluster knowledge
- learned relevance
- operational history
- perception adaptation
- reporting history

Loss of pod identity does not imply loss of cognition.

## Security Boundary

Regent exists partly to maintain a distinct trust boundary.

Sensitive cluster-wide authority remains isolated.

## Summary

Regent is the secure coordination and orchestration authority of the Hermes-on-K8s collective — a cognitive brain, not an executor.
