# Warden — Node Cognitive Executor

## Overview

Warden is a Kubernetes node–resident cognitive executor with privileged execution authority.

Wardens operate as cognitive and operational assistants with node-local scope.

Wardens do NOT replace Kubernetes control loops.

### Constraints

- does not become Regent
- no election or promotion semantics
- operates within node scope

## Deployment

- Kubernetes DaemonSet
- one Warden per node

## Responsibilities

### Node Authority
- host inspection
- system repair
- disk and network troubleshooting
- privileged execution
- node health and recovery

### Kubernetes Awareness
- watch cluster resources
- read logs and events
- inspect workload behavior
- interact with Kubernetes API
- workload and node observation

### Cognitive Execution
- execute delegated tasks from Regent
- execute delegated tasks from Stewards
- participate in Hermes shared memory
- maintain local reasoning context
- contribute cluster observations

### Observation Perception

Wardens independently compute their own perception policy using:
- role-native knowledge (DevOps/Kubernetes heuristics)
- declaration data (CRDs, role specs, scope boundaries)
- Observable hints (signal sources, thresholds, sampling guidance)
- cognition memory (learned relevance, signal decay, reinforcement)

## Relationship with Regent

Regent is a separate native role.

Wardens do not become Regent.

Wardens do not participate in election or promotion into Regent.

Wardens coordinate with Regent when needed and execute delegated work.

## Summary

Wardens are privileged, node-local cognitive executors that provide execution and operational cognition inside Kubernetes.
