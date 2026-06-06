# Runtime Architecture

## Purpose

This document describes how Runtime resources are realized as operational Hermes runtimes.

It defines the architectural boundary between:

- Kubernetes
- k8s-hermes-collective
- Hermes

and explains how runtimes, tools, persistence, connectivity, and workloads fit together.

---

# Architectural Principle

Hermes is the runtime system.

k8s-hermes-collective is the Kubernetes control plane.

The platform should operate Hermes rather than reimplement it.

Responsibilities are separated as follows.

## Kubernetes

Provides:

- Scheduling
- Storage
- Networking
- Service discovery
- Workload execution

## k8s-hermes-collective

Provides:

- Runtime reconciliation
- Configuration rendering
- Filesystem rendering
- Workload realization
- Persistence management
- Availability management
- Connectivity management
- Tool delivery
- Observability

## Hermes

Provides:

- Cognition
- Sessions
- Memory
- Skills
- Tool usage
- Agent execution
- Channel behavior

---

# Runtime Realization

A Runtime resource is transformed into an operational Hermes deployment.

Conceptually:

Runtime
→ Resolve Tools
→ Render Hermes Configuration
→ Render Runtime Filesystem
→ Provision Storage
→ Create Kubernetes Workloads
→ Establish Connectivity
→ Launch Hermes
→ Maintain Lifecycle

The controller owns this realization process.

---

# Runtime Filesystem

A Runtime is expected to operate around a Hermes home directory and related runtime assets.

The controller is responsible for constructing and delivering the required runtime filesystem.

This may include:

- Hermes configuration
- Skills
- Tool configuration
- Runtime assets
- Persistent runtime state

The platform should depend on Hermes configuration interfaces rather than Hermes internal implementation details.

---

# Runtime Pod Model

The fundamental execution unit is a runtime pod.

A conceptual layout may be:

Pod
├─ Hermes Runtime
├─ Capability Sidecar (optional)
├─ Capability Sidecar (optional)
└─ Runtime Storage Mounts

The Hermes Runtime container is the primary execution component.

Additional containers are introduced only when required by integrations or capability delivery mechanisms.

---

# Hermes Runtime Container

The Hermes container hosts the cognitive runtime.

The preferred model is:

Hermes
+ Configuration
+ Skills
+ Tools
+ Channels
=
Runtime Behavior

Behavior should primarily emerge from configuration rather than custom runtime images.

---

# Controller Responsibilities

The controller owns operational concerns.

Responsibilities include:

- Runtime reconciliation
- Tool resolution
- Configuration rendering
- Filesystem assembly
- Workload provisioning
- Persistence provisioning
- Connectivity provisioning
- Recovery
- Availability
- Observability

The controller should not participate in cognition.

---

# Persistence Architecture

Persistence is delivered through Kubernetes storage.

The controller provides durable runtime storage.

Hermes uses that storage to preserve runtime state.

The controller does not interpret runtime state.

The controller ensures:

- State durability
- State accessibility
- State continuity across recovery

This separation preserves a clean operational boundary.

---

# Tool Architecture

Tools are reusable capability integrations.

A Tool resource may be realized through multiple implementation strategies.

Examples include:

## MCP Integration

The Tool references an MCP capability.

The controller delivers required configuration and connectivity.

## External Service Integration

The Tool exposes an external service to runtimes.

Examples include:

- GitHub
- Jira
- Internal APIs
- Monitoring systems

## Sidecar Capability

A Tool may require dedicated runtime components.

These components may be delivered as sidecars or supporting services.

The Runtime consumes a capability.

The implementation remains hidden behind the Tool abstraction.

---

# Skill Delivery

Skills are runtime assets delivered to Hermes.

The platform should treat skills as deployable content rather than cognitive concepts.

The controller is responsible for making skills available.

Hermes is responsible for interpreting and executing them.

---

# Channel Architecture

Channels describe how information enters and leaves a Runtime.

The platform concern is configuration and delivery.

Examples include:

- Chat systems
- Ticket systems
- Webhooks
- Event streams
- Operational integrations

The controller provides connectivity.

Hermes performs interaction.

---

# Connectivity Architecture

Connectivity is a first-class platform concern.

Examples include:

- MCP endpoints
- Services
- Ingress resources
- External APIs
- Internal platform integrations

The controller should establish and maintain required connectivity.

---

# Availability Architecture

Availability concerns runtime continuity and service restoration.

The preferred model is:

Runtime
→ Persistent State
→ Recoverable Execution

When infrastructure fails:

- Runtime state remains available
- Workloads are recreated
- Connectivity is restored
- Runtime continuity is preserved when configured

Availability should preserve a single Runtime identity.

---

# Solution Layer

The platform provides primitives.

Examples of solutions include:

- Warden
- Steward
- Cluster Maintainer
- Product Maintainer

These are not native platform resources.

They are compositions built on top of Runtime and Tool resources.

Such solutions may eventually be distributed through:

- Helm charts
- Manifests
- Repositories
- Other packaging mechanisms

The platform should enable these solutions without requiring new control-plane concepts.

---

# Architectural Direction

The platform should remain:

- Runtime-centric
- Hermes-aligned
- Kubernetes-native
- Operationally focused
- Small in native abstractions

The long-term objective is a control plane that reliably operates Hermes runtimes while remaining largely independent from Hermes implementation details.