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
- Regent as cluster cognitive authority
- collective cognition and orchestration

### Application Plane
- declared Stewards per namespace or service domain
- application cognition
- observability and incident reasoning

### External Infrastructure Plane
- declared Emissaries on Linux and external systems
- extends Hermes beyond Kubernetes

## Distribution Layer

HA-Hermes is distributed as independently installable assemblies:

**Hermes Runtime** — shared cognitive substrate providing:
- cognition store, memory, adaptive perception
- session and task lifecycle
- execution framework
- persistence

**Distributions** — Runtime + role personality + tools + persistence + deployment form:
- Regent Distribution — cluster cognitive authority
- Warden Distribution — node cognitive executor
- Steward Distribution — application cognitive
- Emissary Distribution — external system cognitive

Each distribution is independently deployable, independently useful, self-cognitive, and self-persistent.

## Principles

- Kubernetes reconciliation remains authoritative
- Existing operators and controllers remain enabled
- HA-Hermes coordinates rather than replaces
- Git stores declarative intent
- etcd stores runtime truth
- Hermes stores cognitive state
- Roles define responsibility, not runtime states
- Perception is adaptive and distributed
- Distribution independence — each distribution is valid without others

## Coordination

Regent is the native authority role for cluster-wide coordination, arbitration, and orchestration.

When Regent is absent, conflicts are surfaced and deferred to human authority.

## Goal

Provide a distributed cognitive and operational layer that helps maintain infrastructure and applications through reasoning, coordination, and adaptive perception.
