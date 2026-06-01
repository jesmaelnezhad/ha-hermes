# Role Model

## Overview

HA-Hermes roles are divided into native and declared roles.

Responsibility emerges from:

- role type
- placement
- declared scope

It is not a separate ownership artifact.

## Native Roles

Native roles are installed as part of HA-Hermes bootstrap.

### Warden

Node-resident privileged Hermes peer.

### Regent

Secure coordination and orchestration authority.

## Declared Roles

Declared roles are created intentionally after bootstrap.

### Steward

Application or namespace cognition.

### Emissary

External infrastructure cognition.

## Principle

Kubernetes remains authoritative for reconciliation.

HA-Hermes provides cognition and coordination.