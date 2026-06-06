# V1 Scope

## Purpose

This document defines the first production-capable version of k8s-hermes-collective.

The objective of v1 is to deliver a complete Kubernetes control plane for Hermes runtimes.

V1 should allow teams to declaratively define, operate, persist, recover, expose, observe, and evolve Hermes runtimes using Kubernetes-native workflows.

The objective is not to build an ecosystem of specialized assistants.

The objective is to build the platform on which those assistants can be created.

---

# Success Criteria

A successful v1 should demonstrate the following capabilities.

- Runtime resources can be created and reconciled.
- Hermes runtimes can be launched and managed.
- Runtime state survives infrastructure replacement.
- Existing runtime state can be reused.
- Runtime availability can be maintained through failures.
- Reusable tool integrations can be attached to runtimes.
- MCP-based integrations can be attached to runtimes.
- Runtime channels can be configured.
- Runtime status is observable through Kubernetes.
- Runtime configuration is declarative.
- Runtime lifecycle is controller-managed.
- Specialized solutions can be built without modifying the platform.

If these capabilities are proven, the platform has validated its central architectural thesis.

---

# Non-Goals

The following concerns are intentionally out of scope for v1.

## Collective Systems

Multi-runtime coordination and collective behavior belong to a future phase.

## Package Ecosystems

Catalogs, registries, marketplaces, and distribution systems are not required.

## Advanced Memory Systems

Hermes remains responsible for memory management.

## Distributed Cognition

A Runtime should behave as a single cognitive service.

## Organizational Role Models

Warden, Steward, Product Maintainer, Cluster Maintainer, and similar concepts should not become platform abstractions.

## Multi-Controller Architectures

A single controller implementation is sufficient.

---

# Platform Resources

V1 should remain intentionally small.

The expected native resources are:

- Runtime
- Tool

Additional resources should only be introduced when they provide clear platform value.

---

# Runtime Resource

Runtime is the primary platform abstraction.

A Runtime represents a managed cognitive service.

A Runtime should be capable of expressing:

- Runtime configuration
- Persistence requirements
- Continuity requirements
- Availability requirements
- Tool references
- Skill delivery requirements
- Connectivity requirements
- Channel configuration

The Runtime resource is the primary contract between users and the platform.

---

# Tool Resource

Tools represent reusable capability integrations.

Examples include:

- MCP integrations
- External services
- Operational capabilities
- Sidecar-delivered capabilities

Tools create reusable ownership boundaries and can be shared by multiple runtimes.

---

# Runtime Execution

A Runtime resource should result in an operational Hermes deployment.

The controller should:

1. Resolve Runtime configuration.
2. Resolve Tool references.
3. Render Hermes configuration.
4. Render runtime filesystem layout.
5. Provision required storage.
6. Create workload resources.
7. Expose required connectivity.
8. Maintain lifecycle.
9. Recover from failures.
10. Preserve continuity.

Hermes performs cognitive work.

The controller performs operational work.

---

# Persistence And Continuity

Persistence is a required platform capability.

The controller should provide durable storage and reattach runtime state when workloads are recreated.

A Runtime should be capable of:

- Preserving state
- Reusing existing state
- Recovering after infrastructure replacement
- Maintaining continuity through lifecycle events

The platform should not require knowledge of Hermes internals beyond the interfaces needed to operate Hermes successfully.

---

# Tool Delivery

V1 should support multiple capability delivery mechanisms.

Examples include:

- MCP-based integrations
- Sidecar-delivered capabilities
- External service integrations

The exact delivery mechanisms may evolve.

The platform concern is capability delivery rather than capability implementation.

---

# Channel Delivery

V1 should support runtime channel configuration.

The platform should support the concept of:

- Input channels
- Output channels

The exact adapter set may remain small.

The platform concern is channel delivery and configuration.

---

# Availability

Availability is a required platform capability.

The platform should support:

- Runtime recovery
- Runtime continuity
- Service restoration
- Failover where appropriate

Availability should be achieved using Kubernetes operational patterns rather than shared-active runtime execution.

---

# Status

The controller should expose observable runtime state.

Examples include:

- Lifecycle phase
- Health
- Conditions
- Runtime references
- Continuity information
- Availability information

Users should be able to understand runtime state directly from Kubernetes.

---

# Solution Layer

The platform should enable higher-level solutions.

Examples include:

- Warden
- Steward
- Cluster Maintainer
- Product Maintainer

These solutions are expected to be delivered as configurations, manifests, charts, or other packaging mechanisms built on top of the platform.

They are not platform primitives.

---

# Exit Criteria

V1 can be considered complete when:

- Runtime resources are declarative.
- Tool resources are reusable.
- Hermes runtimes are controller-managed.
- Runtime continuity survives infrastructure replacement.
- Recovery mechanisms function correctly.
- Availability mechanisms function correctly.
- Tool integrations function correctly.
- MCP integrations function correctly.
- Channel delivery functions correctly.
- Runtime status is observable.
- Independent teams can build specialized solutions without modifying the platform.

At that point the platform is complete enough to support future work on collectives, packaging ecosystems, and higher-level runtime compositions.