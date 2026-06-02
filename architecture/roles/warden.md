# Warden — Node Cognitive Executor

## Overview

Warden is a Kubernetes node-resident cognitive executor and the node-local brain and hands.

Wardens operate as cognitive and operational assistants with node-local scope. Each Warden is independently useful — it can operate without Regent, Stewens, or Emissary present.

Wardens do NOT replace Kubernetes control loops.

## Deployment

- Kubernetes DaemonSet
- one Warden per node (or selected nodes)

One or many Wardens may exist. They may be deployed to one node, selected nodes, or all nodes depending on operational needs.

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
- execute node-local cognitive tasks
- participate in Hermes shared memory
- maintain local reasoning context
- contribute cluster observations

### Observation Perception

Wardens independently compute their own perception policy using:
- role-native knowledge (DevOps/Kubernetes heuristics)
- declaration data (CRDs, role specs, scope boundaries)
- Observable guidance (signal sources, thresholds, sampling guidance)
- cognition memory (learned relevance, signal decay, reinforcement)

## Persistence

Warden cognition is durable:
- node memory
- learned relevance
- operational history
- perception adaptation

Loss of pod identity does not imply loss of cognition.

## Constraints

- Wardens do not become Regent
- Wardens operate within node scope
- Wardens are independently useful without other distributions

## Summary

Wardens are privileged, node-local cognitive executors — the brain and hands of each node.
