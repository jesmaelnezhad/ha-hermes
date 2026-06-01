# Emissary Role

## Overview

An Emissary is a declared Hermes role operating outside Kubernetes on Linux, VM, or SSH-accessible systems.

Emissaries extend Hermes cognition and execution beyond the cluster.

## Declaration

Emissaries are intentionally declared after bootstrap.

Typical scope:

- VM
- bare metal host
- SSH-accessible Linux environment
- external infrastructure system

Responsibility emerges from declared scope.

## Responsibilities

### External Awareness
- inspect external systems
- collect operational state
- analyze logs and services

### Execution
- execute system commands
- manage services
- perform diagnostics and recovery

### Coordination
- synchronize findings with Hermes collective
- assist Wardens and Stewards
- participate in operational workflows

## Constraints

- Emissaries are not part of Kubernetes control plane
- Emissaries do not replace reconciliation systems
- Emissaries do not become Regent

## Summary

Emissaries are declared external cognitive operators that extend Hermes beyond Kubernetes.