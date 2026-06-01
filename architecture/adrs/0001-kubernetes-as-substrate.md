# ADR 0001: Kubernetes as Substrate

## Status
Accepted

## Context

Early HA-Hermes architecture language suggested that HA-Hermes might become a distributed operating system.

Further analysis clarified that Kubernetes already provides the distributed execution and reconciliation substrate.

Kubernetes already provides:

- reconciliation
- scheduling
- runtime state
- watch/event mechanisms
- operator and controller ecosystem

Duplicating these mechanisms would create conflict and controller overlap.

## Decision

HA-Hermes SHALL operate as a distributed cognitive operator layered on top of Kubernetes.

HA-Hermes SHALL:

- observe
- reason
- coordinate
- remember
- automate

HA-Hermes SHALL NOT attempt to replace Kubernetes-native reconciliation.

## Consequences

- Kubernetes controllers remain authoritative
- Existing operators remain enabled
- HA-Hermes acts as a meta-operational layer
- Warden, Steward and Emissary coordinate operations using native Kubernetes primitives
