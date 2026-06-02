# Role Model

## Overview

Hermes-on-K8s has three separate concepts:

- **Fabric** — shared cognitive substrate
- **Role** — responsibility domain
- **Distribution** — independently installable assembly

Roles define responsibility domains, not implementation forms or runtime states.

Distributions operationalize roles. A distribution is an independently installable assembly built from Hermes Fabric + role personality + tools + persistence + deployment form.

Each distribution is independently deployable, independently useful, self-cognitive, and self-persistent.

No role is an emergent state of another role. No promotion or election-based identity transitions exist.

Responsibility emerges from:
- role type
- placement
- declared scope

## Installation Model

Installing Hermes-on-K8s is a two-step process:

1. **Install the Fabric** — the shared cognitive substrate. This is always required.
2. **Install Distributions** — choose which distributions you need. Each distribution is independently deployable and independently useful.

You can install one distribution, several, or all. Integration between distributions is optional. Independence is required.

## Cluster Health Roles

These distributions are concerned with the health and operation of the cluster itself.

### Warden

Node-resident cognitive executor. Node-local brain and hands. Runs on Kubernetes nodes as a DaemonSet. One or many Wardens may exist — deployed to one node, selected nodes, or all nodes.

Warden focuses on node health, node recovery, privileged execution, and node-local cognition. It is the guardian of nodes.

### Regent

Cluster cognitive authority. Singleton distribution responsible for cluster-wide cognition and orchestration. Brain and orchestration authority — execution is delegated to sidecar executors, not to other distributions.

NOT emergent. NOT elected. NOT derived from Warden.

Regent focuses on cluster lifecycle, cross-distribution coordination, arbitration, cluster reporting, and secure orchestration. It is the cluster's cognitive brain.

## Application and External Roles

These distributions are concerned with applications, namespaces, service domains, and external infrastructure.

### Steward

Application-scoped cognitive role. Declared per namespace or service domain.

Stewards understand and coordinate application operations within their scope. They observe workloads and services, inspect logs and metrics, understand topology and dependencies, diagnose failures, correlate incidents, and coordinate remediation.

Stewards provide service-level reporting, operational guidance, and a CLI-based configuration interface for the products they manage. They maintain application knowledge, record operational context, and contribute cognitive state to the Hermes collective.

Typical scope: namespace, service domain, or shared application boundary.

Stewards support highly available deployment with replicated runtime and durable cognition.

### Emissary

External infrastructure cognitive role. Runs on Linux, VM, or SSH-accessible systems outside Kubernetes.

Emissaries extend Hermes cognition and execution beyond the cluster. They inspect external systems, collect operational state, analyze logs and services, and perform SSH-based system control and recovery.

Typical scope: VM, bare metal host, SSH-accessible Linux environment, or external infrastructure system.

Operationalized as **Emissary Distribution** — independently installable, self-cognitive, self-persistent.

## Principle

Hermes-on-K8s provides cognition and coordination. Kubernetes remains authoritative for reconciliation.
