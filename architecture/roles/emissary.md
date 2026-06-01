# Emissary — External System Cognitive Role

## Overview

Emissary is a declarative external-infrastructure cognitive agent.

Emissaries extend Hermes cognition and execution beyond the cluster to non-Kubernetes systems.

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
- SSH-based system control

### Execution
- execute system commands
- manage services
- perform diagnostics and recovery
- VM/bare-metal operations
- non-Kubernetes operational execution

### External Integration
- external system integration
- synchronize findings with Hermes collective

### Coordination
- assist Wardens and Stewards
- participate in operational workflows

## Observation Perception

Emissaries independently compute their own perception policy using:
- role-native knowledge (system administration heuristics)
- declaration data (CRDs, role specs, scope boundaries)
- Observable hints (signal sources, thresholds, environment constraints)
- cognition memory (learned relevance, signal decay, reinforcement)

## Scope Difference from Steward

- Steward: Kubernetes / namespace domain
- Emissary: external systems / machines

## Constraints

- Emissaries are not part of Kubernetes control plane
- Emissaries do not replace reconciliation systems
- Emissaries do not become Regent

## Summary

Emissaries are declared external cognitive operators that extend Hermes beyond Kubernetes.
