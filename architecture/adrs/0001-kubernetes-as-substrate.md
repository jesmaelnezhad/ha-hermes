# ADR 0001: Kubernetes as Substrate

## Status
Accepted

## Context

Kubernetes already provides the distributed execution and reconciliation substrate.

Kubernetes already provides:

- reconciliation
- scheduling
- runtime state
- watch/event mechanisms
- operator and controller ecosystem

Duplicating these mechanisms would create conflict and controller overlap.

## Decision

hermes-on-k8s SHALL operate as a distributed cognitive operator layered on top of Kubernetes.

hermes-on-k8s SHALL:

- observe
- reason
- coordinate
- remember
- automate

hermes-on-k8s SHALL NOT attempt to replace Kubernetes-native reconciliation.

## Consequences

- Kubernetes controllers remain authoritative
- Existing operators remain enabled
- hermes-on-k8s acts as a meta-operational layer
- Warden, Steward and Emissary coordinate operations using native Kubernetes primitives
