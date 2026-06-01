# Warden Role

## Overview

A Warden is a Kubernetes-node-resident Hermes peer responsible for privileged execution, node awareness, and participation in the Hermes collective.

Wardens do not replace Kubernetes control loops.

They operate as cognitive and operational assistants with node-local authority.

## Deployment

- Kubernetes DaemonSet
- one Warden per node
- participates in Lease-based leadership election

## Responsibilities

### Node Authority
- host inspection
- system repair
- disk and network troubleshooting
- privileged execution

### Kubernetes Awareness
- watch cluster resources
- read logs and events
- inspect workload behavior
- interact with Kubernetes API

### Cognitive Participation
- participate in Hermes shared memory
- maintain local reasoning context
- execute delegated work
- contribute cluster observations

## Regent State

A Warden may temporarily become Regent.

Regent is:

- leadership state
- not a separate role
- elected via Kubernetes Lease

## Important Constraints

Wardens:

- do not replace Kubernetes controllers
- do not own reconciliation authority
- augment cluster operations through reasoning and coordination

## Summary

Wardens are privileged, node-local Hermes peers that provide execution and operational cognition inside Kubernetes.
