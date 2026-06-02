# Role Model

## Overview

HA-Hermes has three separate concepts:

- **Runtime** — shared cognitive substrate
- **Role** — responsibility domain
- **Distribution** — independently installable assembly

Roles define responsibility domains, not implementation forms or runtime states.

Distributions operationalize roles. A distribution is an independently installable assembly built from Hermes Runtime + role personality + tools + persistence + deployment form.

Each distribution is independently deployable, independently useful, self-cognitive, and self-persistent.

No role is an emergent state of another role. No promotion or election-based identity transitions exist.

Responsibility emerges from:
- role type
- placement
- declared scope

## Native Roles

Native roles are installed as part of HA-Hermes bootstrap.

### Warden

Node-resident cognitive executor. Node-local brain and hands. Runs on every Kubernetes node as a DaemonSet.

### Regent

Cluster cognitive authority. Singleton role responsible for cluster-wide cognition and orchestration. Brain and orchestration authority — execution is delegated to Wardens, Emissaries, and sidecars.

NOT emergent. NOT elected. NOT derived from Warden.

## Declared Roles

Declared roles are created intentionally after bootstrap via CRDs and configuration.

### Steward

Application or namespace cognitive role. Observation scope is defined via CRDs, Observable configuration, system knowledge constraints, and cognition history adaptation.

### Emissary

External infrastructure cognitive role. Runs on Linux, VM, or SSH-accessible systems outside Kubernetes.

## Principle

Kubernetes remains authoritative for reconciliation.

HA-Hermes provides cognition and coordination.
