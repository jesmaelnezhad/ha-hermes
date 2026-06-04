# V1 Scope

## Purpose

This document defines the first buildable version of k8s-hermes-collective.

The objective of v1 is not to realize the full architectural vision.

The objective is to validate the core premise:

A Kubernetes resource can declaratively describe a cognitive runtime and a controller can reliably realize, maintain, and recover that runtime using Hermes.

Every feature included in v1 should contribute directly to validating that premise.

---

# Success Criteria

A successful v1 should demonstrate the following capabilities.

- A Runtime resource can be created.
- The controller can reconcile the Runtime.
- A Hermes runtime can be launched.
- Runtime state can survive pod replacement.
- Tools can be made available to the runtime.
- Runtime status is observable through Kubernetes.
- Runtime configuration is declarative.
- Runtime lifecycle is controller-managed.

If these capabilities are proven, the project will have validated its core architecture.

---

# Non-Goals

The following concerns are intentionally out of scope for v1.

## Advanced Memory Systems

Persisted Hermes state is sufficient.

Dedicated memory architectures, retrieval systems, and shared cognition models should be deferred.

## Distributed Cognition

A Runtime should behave as a single cognitive actor.

Distributed reasoning systems are not required.

## Advanced Package Ecosystems

Runtime packages may be discussed architecturally but should not be required for v1.

## Complex Perception Systems

Perception should remain simple.

A runtime can begin with static configuration and evolve later.

## Rich Channel Ecosystems

Only a minimal communication model is required.

## Runtime Marketplaces

Package distribution, catalogs, and registries should be deferred.

## Multi-Controller Architectures

A single controller implementation is sufficient.

---

# Runtime Resource

V1 should contain a single primary CRD.

Conceptually:

Runtime

The Runtime resource is the native abstraction of the platform.

Supporting CRDs should be avoided unless they are required to prove core functionality.

The platform should remain intentionally small.

---

# Runtime Specification

The first Runtime specification should be intentionally conservative.

Illustrative shape:

```yaml
spec:
  image:

  session:
    persistent:

  tools:

  prompt:

  channels:
```

This is not necessarily the final API.

It represents the level of complexity appropriate for validating the architecture.

---

# Runtime Execution

A Runtime resource should result in a running Hermes runtime.

The controller should:

1. Resolve Runtime configuration.
2. Provision required storage.
3. Construct workload definitions.
4. Launch runtime workloads.
5. Maintain lifecycle.
6. Recover from failures.

The runtime should perform cognitive work once launched.

---

# Persistence

Persistence is a required v1 capability.

The preferred approach is persistent storage of the Hermes runtime directory.

Conceptually:

/hermes/.hermes

The controller should provide durable storage and reattach that storage when workloads are recreated.

The controller does not need to interpret persisted contents.

The goal is continuity rather than cognitive awareness of persistence.

---

# Tool Model

V1 should support local process tools.

Examples:

- kubectl
- shell utilities
- custom scripts

Hermes should be able to invoke these tools directly.

This model provides a large amount of practical capability with minimal architectural complexity.

MCP-based tools and sidecar-delivered tools may be introduced later.

They should not be required to validate the platform.

---

# Channel Model

V1 should support a minimal interaction model.

The exact implementation remains open.

Potential approaches include:

- Standard input and output
- Kubernetes resources
- Webhooks

The objective is to demonstrate runtime interaction rather than establish a comprehensive communication framework.

---

# Availability

V1 should prioritize correctness over sophistication.

Single-instance runtime execution is sufficient.

Leader election, active standby configurations, and advanced failover models should be deferred until runtime continuity has been validated.

---

# Status

The controller should expose observable runtime state.

Examples include:

```yaml
status:
  phase:
  ready:
  podRef:
  session:
```

Users should be able to understand runtime lifecycle directly from Kubernetes.

---

# Example Runtime

An illustrative v1 Runtime might resemble:

```yaml
apiVersion: collective.io/v1alpha1
kind: Runtime
metadata:
  name: cluster-assistant

spec:
  image: ghcr.io/hermes/runtime

  session:
    persistent: true

  tools:
    - kubectl

  prompt: |
    You are a Kubernetes operational assistant.

  channels:
    - stdio
```

The controller should be capable of realizing this resource into a functioning Hermes runtime.

---

# Exit Criteria

V1 can be considered complete when:

- Runtime resources are declarative.
- Hermes runtimes are controller-managed.
- Session continuity survives pod replacement.
- Runtime status is observable.
- Tool execution works reliably.
- The architecture can be demonstrated through at least one practical operational assistant.

At that point, the project will have validated its central architectural thesis and can evolve toward richer runtime, package, channel, perception, and memory models.