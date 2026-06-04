# V1 Scope

## Purpose

This document defines the first production-capable version of k8s-hermes-collective.

The objective of v1 is to deliver the complete Runtime platform.

The objective is not to build a large ecosystem of specialized agents, packages, collectives, or organizational patterns. Those should be able to emerge on top of the platform without requiring changes to the platform itself.

V1 should establish a Kubernetes-native foundation for operating Hermes runtimes with persistence, continuity, availability, tooling, connectivity, and observability.

---

# Success Criteria

A successful v1 should demonstrate the following capabilities.

- A Runtime resource can be created and reconciled.
- A Hermes runtime can be launched and managed.
- Runtime continuity can survive pod replacement.
- Existing sessions can be reused.
- Runtime availability can be maintained through failure scenarios.
- Tools can be attached and used.
- MCP-based integrations can be attached and used.
- Input and output channels can be configured.
- Runtime status is observable through Kubernetes.
- Runtime configuration is declarative.
- Runtime lifecycle is controller-managed.
- The platform can support multiple operational personalities without code changes.

If these capabilities are proven, the project will have validated its central architectural thesis.

---

# Non-Goals

The following concerns are intentionally out of scope for v1.

## Collective Systems

V1 focuses on individual Runtime resources.

Multi-runtime collectives and collaboration models belong to a future phase.

## Advanced Package Ecosystems

Package catalogs, marketplaces, registries, and distribution systems are not required.

## Advanced Memory Systems

Persisted Hermes state is sufficient.

Dedicated memory architectures, retrieval systems, and shared cognition models should be deferred.

## Distributed Cognition

A Runtime should behave as a single cognitive actor.

Distributed reasoning systems are not required.

## Organizational Role Models

Cluster maintainers, product maintainers, support assistants, and similar concepts should not become native platform abstractions.

## Multi-Controller Architectures

A single controller implementation is sufficient.

---

# Runtime Resource

V1 should contain a single primary CRD.

Runtime is the native abstraction of the platform.

The Runtime resource must be capable of expressing:

- Runtime configuration
- Session configuration
- Persistence requirements
- Availability requirements
- Tool configuration
- MCP configuration
- Channel configuration
- Package composition

The Runtime resource is the platform contract.

---

# Runtime Packages

Runtime packages should exist as a platform capability in v1.

The purpose of v1 packages is composition rather than ecosystem development.

A Runtime should be able to reference a package and override selected behavior.

Conceptually:

Runtime
+ Package
+ Overrides
=
Resolved Runtime

Package catalogs, registries, discovery systems, and marketplaces are not required.

The extension point should exist even if the surrounding ecosystem does not.

---

# Runtime Execution

A Runtime resource should result in a running Hermes runtime.

The controller should:

1. Resolve Runtime configuration.
2. Resolve package configuration.
3. Resolve tools and integrations.
4. Provision required storage.
5. Construct workload definitions.
6. Launch runtime workloads.
7. Maintain lifecycle.
8. Recover from failures.
9. Preserve continuity.

The runtime should perform cognitive work once launched.

---

# Persistence And Continuity

Persistence is a required v1 capability.

The preferred approach is persistent storage of the Hermes runtime directory.

Conceptually:

/hermes/.hermes

The controller should provide durable storage and reattach that storage when workloads are recreated.

Session reuse is a first-class capability.

A Runtime should be capable of:

- Creating sessions
- Reusing sessions
- Recovering sessions
- Continuing operation after infrastructure replacement

---

# Tool Model

V1 should support multiple capability delivery mechanisms.

Required capabilities include:

- Local process tools
- MCP-based tools

Sidecar-delivered capabilities may be supported where operational requirements justify them.

Tool integration is a platform concern and should be available from the beginning.

---

# Channel Model

V1 should include a channel framework.

The platform should support the concept of:

- Input channels
- Output channels

The exact set of adapters may remain small.

The abstraction itself is a core platform capability.

---

# Availability

Availability is a required v1 capability.

The platform should support runtime continuity during infrastructure failures.

The exact implementation remains open, but the platform should include:

- Runtime recovery
- Continuity preservation
- Leadership where required
- Failover mechanisms where required

Availability is part of the Runtime platform rather than a future enhancement.

---

# Status

The controller should expose observable runtime state.

Examples include:

- Lifecycle phase
- Health
- Conditions
- Runtime references
- Continuity information
- Session information

Users should be able to understand runtime lifecycle directly from Kubernetes.

---

# Exit Criteria

V1 can be considered complete when:

- Runtime resources are declarative.
- Hermes runtimes are controller-managed.
- Persistent runtimes survive infrastructure replacement.
- Session reuse works reliably.
- Availability and recovery mechanisms function correctly.
- Tool execution works reliably.
- MCP integrations work reliably.
- Channel abstractions function correctly.
- Runtime status is observable.
- Runtime packages can be composed into Runtime definitions.
- Independent teams can build specialized assistants without modifying the platform.

At that point, the Runtime platform is complete enough to support future work on packages, collectives, and richer cognitive ecosystems.