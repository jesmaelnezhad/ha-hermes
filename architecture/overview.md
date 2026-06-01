# HA-Hermes Architecture Overview

HA-Hermes is a distributed cognitive operator running on top of Kubernetes and surrounding infrastructure.

Kubernetes remains the distributed execution and reconciliation substrate.

HA-Hermes adds cognition, memory, diagnosis, and operational coordination.

## Core Model

Linux plus Hermes CLI:

- Linux provides runtime and execution primitives
- Hermes provides cognition and operational assistance

Kubernetes plus HA-Hermes follows the same model:

- Kubernetes is the distributed substrate
- HA-Hermes is the distributed cognitive operator

## System Planes

### Native Hermes Plane
- Wardens on Kubernetes nodes
- Regent as secure coordination authority
- collective cognition and orchestration

### Application Plane
- declared Stewards per namespace or service domain
- application cognition
- observability and incident reasoning

### External Infrastructure Plane
- declared Emissaries on Linux and external systems
- extends Hermes beyond Kubernetes

## Principles

- Kubernetes reconciliation remains authoritative
- Existing operators and controllers remain enabled
- HA-Hermes coordinates rather than replaces
- Git stores declarative intent
- etcd stores runtime truth
- Hermes stores cognitive state

## Coordination

Regent is a native authority role.

Regent coordinates collective behavior, arbitrates conflicts, and orchestrates secure workflows.

## Goal

Provide a distributed cognitive and operational layer that helps maintain infrastructure and applications through reasoning and coordination.