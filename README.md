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

### Native Roles

#### Warden
- node resident Hermes peer
- privileged execution
- Kubernetes awareness
- node-local substrate cognition

#### Regent
- separate native authority role
- secure orchestration
- coordination and arbitration
- bootstrap and expansion authority

### Declared Roles

#### Steward
- user-declared cognitive operator
- namespace or application cognition
- observability and operational assistance

#### Emissary
- user-declared external peer
- Linux or VM cognition and execution
- extends Hermes beyond Kubernetes

## Principles

- Kubernetes remains authoritative for reconciliation
- HA-Hermes augments rather than replaces operators
- Git stores declarative intent
- etcd stores runtime truth
- Hermes stores cognitive state and memory

## Vision

A distributed cognitive and operational layer for infrastructure and applications.