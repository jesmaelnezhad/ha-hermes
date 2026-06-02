# ADR 0002: Non-Duplication of Reconciliation

## Status
Accepted

## Context

Kubernetes operators and controllers already implement reconciliation loops and healing logic.

Examples include:

- Deployments
- StatefulSets
- HPA
- storage operators
- ingress controllers
- custom operators

Creating parallel Hermes reconciliation systems risks conflict and duplicated authority.

## Decision

hermes-on-k8s SHALL avoid reimplementing reconciliation mechanisms that already exist in Kubernetes.

Instead hermes-on-k8s SHALL:

- observe existing reconciliation
- diagnose failures
- coordinate remediation
- adjust policy and intent when needed
- compose and orchestrate existing controllers

## Consequences

hermes-on-k8s becomes a meta-operational and cognitive layer rather than a competing controller framework.
