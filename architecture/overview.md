# HA-Hermes Architecture Overview

HA-Hermes is a Kubernetes-native autonomous operations layer that turns a cluster into a self-operating system maintained by cooperative agents.

## Core Vision

A Kubernetes cluster that can:

- operate itself
- heal itself
- maintain applications
- manage infrastructure
- evolve through structured agent cognition

All through a coordinated set of Hermes agents.

## System Planes

### 1. Control Plane (Hermes Core)
- Warden agents on every Kubernetes node
- leader election via Kubernetes Lease
- cluster-wide coordination state

### 2. Application Plane
- Steward agents per namespace or service domain
- manage workloads, deployments, observability
- handle application-level incidents

### 3. External Infrastructure Plane
- Emissaries on VMs, bare metal, SSH-accessible systems
- extend Hermes beyond Kubernetes

## Core Principles

- Kubernetes is the HA substrate
- Git is the declarative source of intent
- etcd is runtime truth
- Hermes shared memory is cognitive state
- all operations are mediated through Hermes agents

## Cognitive Model

Each agent type contributes to a distributed cognition system:

- Wardens: node and control-plane awareness
- Stewards: application and namespace awareness
- Emissaries: external system awareness

## Leadership Model

Leadership is not a fixed role. It is a **state**:

- A Warden becomes **Regent** via leader election
- Regent coordinates cluster-wide decisions

## Goal

Replace manual infrastructure operations with a cooperative, self-maintaining system of agents operating on Kubernetes-native primitives.
