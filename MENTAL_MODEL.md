# Current Architectural Mental Model

## What k8s-hermes-collective Is

k8s-hermes-collective is a Kubernetes-native control plane for Hermes runtimes.

The system introduces Kubernetes resources and controllers that allow Hermes runtimes to be declared, provisioned, operated, recovered, observed, and evolved using Kubernetes patterns.

Hermes remains responsible for cognition, memory management, sessions, skills, tool usage, channel behavior, and agent execution.

k8s-hermes-collective remains responsible for lifecycle management, availability, persistence, integration delivery, workload realization, networking, and observability.

The project should leverage Hermes rather than reimplement it.

---

## Architectural Layers

### Kubernetes

Kubernetes remains the foundational orchestration substrate.

It provides:

- Scheduling
- Storage
- Networking
- Service discovery
- Reconciliation
- Security primitives
- High availability primitives

k8s-hermes-collective builds on these capabilities.

### k8s-hermes-collective

The controller layer is responsible for translating declarative runtime specifications into operational Hermes deployments.

Responsibilities include:

- Runtime lifecycle management
- Runtime reconciliation
- Configuration rendering
- Filesystem layout rendering
- Storage provisioning
- Availability management
- Recovery and failover
- Tool delivery
- Connectivity delivery
- Status reporting

The controller operates Hermes. It does not become Hermes.

### Hermes

Hermes is the cognitive runtime.

Hermes is treated as a complete system that can operate when provided with:

- A home directory
- Configuration
- Tools
- Skills
- Channels
- Runtime resources

Hermes performs cognitive work.

---

## Primary Platform Resource

The primary platform abstraction is Runtime.

A Runtime represents a managed cognitive service.

A Runtime is not merely:

- A pod
- A process
- A profile
- A storage volume

A Runtime is the complete operational entity that combines:

- Identity
- Configuration
- Memory
- Sessions
- Execution
- Lifecycle
- Availability requirements

The controller continuously reconciles this entity into running infrastructure.

---

## Runtime Model

A Runtime describes the desired state of a Hermes-based cognitive service.

Typical concerns include:

### Runtime Configuration

How Hermes should be configured and operated.

### Persistence

What state should survive infrastructure replacement.

### Continuity

How existing sessions and runtime state are reused.

### Availability

How the runtime should recover from failures.

### Tools

Which capabilities should be available to the runtime.

### Skills

Which skill bundles should be delivered to the runtime.

### Channels

How information enters and leaves the runtime.

### Connectivity

How external systems become available to the runtime.

The Runtime resource should remain flexible enough to support interactive assistants, autonomous services, operational agents, maintenance workloads, and future runtime patterns.

---

## Tool Resource

Tools are reusable capability integrations.

A Tool may represent:

- An MCP integration
- A sidecar-delivered capability
- An external service integration
- An operational capability exposed to Hermes

Tools create a reusable ownership boundary.

Runtime operators consume tools.

Tool owners maintain tools.

---

## Runtime Realization

Conceptually the controller performs the following work:

Runtime
→ Resolve tool references
→ Render Hermes configuration
→ Render filesystem layout
→ Provision storage
→ Create Kubernetes workloads
→ Expose required connectivity
→ Maintain runtime lifecycle

The primary outputs of reconciliation are:

- Hermes configuration artifacts
- Runtime filesystem structure
- Kubernetes workload resources
- Connectivity resources

---

## Availability Model

Runtime availability is achieved through recovery and continuity rather than shared-active cognition.

A runtime may expose services, gateways, APIs, or MCP endpoints.

When infrastructure fails, the controller should be able to:

- Recover workloads
- Reattach runtime state
- Restore service availability
- Preserve runtime continuity

Availability is a core platform concern.

---

## Solutions Built On The Platform

Operational personalities are not native platform concepts.

Examples include:

- Warden
- Steward
- Cluster Maintainer
- Product Maintainer
- Support Assistant

These are solutions built on top of the platform.

The platform should provide primitives that allow these solutions to be assembled without modifying the control plane itself.

---

## Design Direction

The system should remain:

- Kubernetes-native
- Hermes-aligned
- Declarative
- Runtime-oriented
- Operationally focused
- Minimal in native abstractions
- Extensible through configuration and integrations

The emphasis is on operating Hermes runtimes well rather than creating a parallel agent framework.