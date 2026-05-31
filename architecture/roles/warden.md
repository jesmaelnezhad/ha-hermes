# Warden Role

## Overview

A Warden is a Kubernetes-node-resident Hermes agent responsible for node-level control, cluster participation, and privileged execution.

Wardens form the control plane of HA-Hermes.

## Responsibilities

### Node-Level Authority
- manage host state
- perform system repair
- handle disk, network, and runtime issues
- execute privileged operations

### Kubernetes Awareness
- watch pods and nodes
- read logs and events
- debug workloads
- interact with Kubernetes API server

### Hermes Cognition
- participate in shared memory
- maintain local reasoning state
- execute assigned tasks from Regent or Stewards

## Leader Role (Regent State)

A Warden may temporarily become Regent via Kubernetes leader election.

When in Regent state:

- coordinates all Wardens
- resolves conflicts
- assigns cluster-wide tasks
- maintains global operational consistency

## Failure Modes

- node failure triggers failover to another Warden
- loss of leadership triggers automatic re-election

## Execution Model

Wardens operate with two layers:

- Cognitive layer (Hermes reasoning)
- Execution layer (privileged system control)

## Summary

Wardens are the foundational autonomous operators of the cluster, responsible for both infrastructure health and participation in cluster-wide intelligence.
