# Regent

## Overview

Regent is a native HA-Hermes role responsible for collective coordination, arbitration, and secure orchestration.

Regent is a separate role from Warden.

It is not a Warden leadership state.

## Deployment

- singleton cluster role
- likely Deployment or StatefulSet
- HA-aware
- cluster scoped

## Responsibilities

### Collective Coordination
- coordinate Wardens
- coordinate Stewards
- maintain collective state awareness
- orchestrate cross-domain work

### Arbitration
- resolve operational disagreements
- coordinate competing priorities
- arbitrate cross-scope decisions

### Secure Orchestration
- bootstrap infrastructure
- coordinate node addition
- manage secure orchestration workflows
- access or retrieve protected credentials when authorized

## Security Boundary

Regent exists partly to maintain a distinct trust boundary.

Wardens do not automatically inherit Regent authority.

Sensitive cluster-wide authority remains isolated.

## Summary

Regent is the secure coordination and orchestration authority of the HA-Hermes collective.