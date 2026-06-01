# Role Model

## Overview

HA-Hermes roles define **responsibility domains**, not implementation forms or runtime states.

No role is an emergent state of another role.
No promotion or election-based identity transitions exist.

Responsibility emerges from:

- role type
- placement
- declared scope

## Native Roles

Native roles are installed as part of HA-Hermes bootstrap.

### Warden

Node-resident cognitive executor. Runs on every Kubernetes node as a DaemonSet.

### Regent

Cluster cognitive authority. Singleton role responsible for cluster-wide cognition and orchestration. NOT emergent, NOT elected, NOT derived from Warden.

## Declared Roles

Declared roles are created intentionally after bootstrap via CRDs and configuration.

### Steward

Application or namespace cognitive role. Observation scope is defined via CRDs, Observable configuration, system knowledge constraints, and cognition history adaptation — not dynamically chosen freely.

### Emissary

External infrastructure cognitive role. Runs on Linux, VM, or SSH-accessible systems outside Kubernetes.

## Principle

Kubernetes remains authoritative for reconciliation.

HA-Hermes provides cognition and coordination.
