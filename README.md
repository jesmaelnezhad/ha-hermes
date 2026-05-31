# HA-Hermes

HA-Hermes is a Kubernetes-native autonomous operations layer built around a distributed set of cooperative agents called the Hermes Collective.

## Core Idea

The system enables a cluster to self-operate, self-heal, and self-evolve through a hierarchy of agent roles inspired by Hermes-like coordination and boundary-crossing behavior.

## Core Roles

- **Warden**: Node-level agent with privileged execution and local cognition.
- **Steward**: Namespace / application-level operator responsible for workloads and services.
- **Emissary**: External system agent for non-Kubernetes environments (VMs, bare metal, SSH hosts).

## Leadership Model

Leadership is not a separate static role. It is a **state** assumed by one Warden at a time through Kubernetes-native leader election.

This role state is called:

- **Regent (elected Warden state)**

## Principles

- Kubernetes is the primary HA substrate.
- Git stores declarative intent.
- Cluster state is operational truth.
- Hermes shared memory stores cognitive state.
- All human operations are mediated through Hermes.

## Vision

A self-maintaining infrastructure where agents collaboratively operate both infrastructure and applications with minimal human intervention.
