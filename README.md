# HA-Hermes

HA-Hermes is a distributed cognitive operator for Kubernetes and surrounding infrastructure.

It operates on top of Kubernetes as an operational and cognitive layer.

## Core Model

Linux plus Hermes CLI:

- Linux provides runtime and execution primitives
- Hermes provides cognition and operational assistance

Kubernetes plus HA-Hermes follows the same model:

- Kubernetes is the distributed substrate
- HA-Hermes is the distributed cognitive operator

## Roles

### Warden
- node resident Hermes peer
- privileged execution
- Kubernetes awareness
- leadership participation

### Regent
- temporary Warden leadership state
- Lease elected
- coordinates Hermes collective

### Steward
- application and namespace cognition
- observability and operational assistance

### Emissary
- external Linux or VM Hermes peer
- extends cognition beyond cluster

## Principles

- Kubernetes remains authoritative for reconciliation
- HA-Hermes augments rather than replaces operators
- Git stores declarative intent
- etcd stores runtime truth
- Hermes stores cognitive memory and tasks

## Vision

A cognitive operational layer for infrastructure and applications.
