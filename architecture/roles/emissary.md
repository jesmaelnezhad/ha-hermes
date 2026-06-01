# Emissary Role

## Overview

An Emissary is a Hermes peer operating outside Kubernetes on Linux, VM, or SSH-accessible systems.

Emissaries extend Hermes cognition and execution beyond the cluster.

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

- Emissaries do not participate in leader election
- Emissaries are not part of Kubernetes control plane
- Emissaries cannot become Regent

## Summary

Emissaries are external Hermes peers that extend cognitive and operational reach beyond Kubernetes.
