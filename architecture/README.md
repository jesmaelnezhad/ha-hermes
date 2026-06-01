# Architecture Index

This directory contains the architectural definition of HA-Hermes.

## Foundational Model

HA-Hermes is a distributed cognitive operator layered on top of Kubernetes and surrounding infrastructure.

Kubernetes remains the execution and reconciliation substrate.

HA-Hermes provides:

- cognition
- memory
- diagnosis
- coordination
- operational assistance

## Contents

### Overview
- overview.md

### Roles
- roles/warden.md
- roles/steward.md
- roles/emissary.md

### Leadership
- leadership/regent.md

### State
- state/cognition.md

### ADRs
- adrs/0001-kubernetes-as-substrate.md
- adrs/0002-non-duplication-of-reconciliation.md
