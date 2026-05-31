# Emissary Role

## Overview

An Emissary is a Hermes agent deployed outside the Kubernetes control plane, operating on virtual machines, bare metal systems, or SSH-accessible Linux environments.

Emissaries extend HA-Hermes beyond Kubernetes.

## Responsibilities

### External System Management
- manage non-Kubernetes servers
- execute remote system operations via SSH or local runtime
- perform diagnostics and recovery on external machines

### Execution Capabilities
- run system commands
- manage services (systemd)
- inspect logs and system state
- apply patches or configuration changes

### Reporting
- report system state back to Wardens and Stewards
- participate in incident resolution flows

## Constraints

- Emissaries do not participate in leader election
- Emissaries are not part of control plane quorum
- Emissaries cannot become Regent

## Interaction Model

Emissaries:

- receive tasks from Stewards or Regent
- execute operations on external infrastructure
- synchronize state back into cluster cognition

## Summary

Emissaries are the boundary-extension layer of HA-Hermes, enabling control and observability of infrastructure beyond Kubernetes.
