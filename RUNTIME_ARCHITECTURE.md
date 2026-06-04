# Runtime Architecture

## Purpose

This document describes how a Runtime resource is realized as a running cognitive workload.

It defines the relationship between:

- k8s-hermes-collective
- Hermes
- Kubernetes workloads
- Sessions
- Tools
- Channels
- Runtime packages

The goal is to establish a practical implementation model while preserving flexibility for future evolution.

---

# Architectural Principle

Hermes is the cognitive engine.

k8s-hermes-collective is the lifecycle and orchestration system.

Hermes is responsible for cognition.

k8s-hermes-collective is responsible for creating, configuring, maintaining, recovering, and integrating Hermes runtimes within Kubernetes.

Kubernetes remains responsible for workload execution and reconciliation.

The relationship can be viewed as:

Kubernetes
→ executes workloads

k8s-hermes-collective
→ manages cognitive runtimes

Hermes
→ performs cognitive work

---

# Runtime Realization

A Runtime resource does not directly represent a pod.

Instead, the controller resolves a Runtime resource into an execution environment.

Conceptually:

Runtime
→ Controller
→ Runtime Definition
→ Workload
→ Running Cognitive Runtime

The controller owns this transformation.

The Runtime resource remains the authoritative declaration.

---

# Runtime Pod Model

The fundamental execution unit is a runtime pod.

The runtime pod contains a Hermes runtime and any supporting components required by the runtime configuration.

A conceptual layout is:

Pod
├─ Hermes Runtime
├─ Tool Sidecar (optional)
├─ Tool Sidecar (optional)
├─ MCP Sidecar (optional)
└─ Persistence Mounts

The Hermes Runtime container is the only mandatory component.

Additional containers may be added when required by tools, integrations, or operational constraints.

The exact pod composition is derived from Runtime configuration.

---

# Hermes Runtime Container

The Hermes Runtime container hosts the cognitive engine.

Responsibilities include:

- Session usage
- Reasoning
- Tool invocation
- Memory access
- Interaction handling
- Channel consumption
- Channel production

The runtime container should remain generic.

Behavior should be determined primarily through configuration rather than custom images.

The preferred model is:

Hermes Runtime
+ Runtime Configuration
+ Tools
+ Channels
=
Behavior

This allows a single runtime implementation to support many operational use cases.

---

# Hermes Responsibilities

Hermes provides cognitive capabilities.

Expected responsibilities include:

- LLM integration
- Agent execution
- Session management
- Memory interfaces
- Tool invocation
- Reasoning loops
- Interaction loops
- MCP integration

Hermes is treated as an execution engine rather than a platform orchestration layer.

---

# k8s-hermes-collective Responsibilities

k8s-hermes-collective owns runtime lifecycle.

Responsibilities include:

- CRDs
- Controllers
- Runtime reconciliation
- Workload provisioning
- Session attachment
- Persistence coordination
- Tool wiring
- Channel wiring
- Availability management
- Runtime recovery
- Kubernetes integration
- Runtime observability

The platform should avoid reimplementing cognitive concerns already provided by Hermes.

---

# Session Persistence

The initial persistence model should remain simple.

Hermes runtime state is persisted through a durable runtime directory.

Conceptually:

/hermes/.hermes

This directory is backed by persistent storage.

Potential backends include:

- PersistentVolumeClaims
- Ceph
- EFS
- NFS
- Other Kubernetes storage providers

The controller does not need to understand session contents.

Its responsibility is to ensure that a runtime can access the same persisted state after restart or migration.

This preserves continuity while maintaining separation between lifecycle management and cognition.

---

# Tool Architecture

The platform should support multiple tool delivery models.

No single mechanism is expected to satisfy all use cases.

## Local Process Tools

The simplest model.

Tools are available as executable processes within the runtime environment.

Examples:

- kubectl
- terraform
- custom scripts
- operational utilities

Hermes invokes these tools as subprocesses.

This model is expected to provide a strong and practical foundation for early versions.

## MCP Tools

Tools may be provided through MCP servers.

Runtime configuration references MCP endpoints or MCP resources.

The controller resolves configuration and makes the MCP capability available to the runtime.

This model enables:

- Remote capabilities
- Shared integrations
- External systems
- Capability reuse

## Sidecar Tools

Certain capabilities may be packaged as dedicated containers.

Examples include:

- Proprietary SDKs
- Licensed software
- Heavy integrations
- Long-running service adapters

Hermes communicates with these components through well-defined interfaces such as MCP, HTTP, or gRPC.

This allows capabilities to evolve independently from the runtime image.

---

# Channel Architecture

Channels provide communication between runtimes and external systems.

The architecture should separate communication semantics from specific products.

The runtime should think in terms of inputs and outputs rather than Slack, Jira, or other individual systems.

## Input Channels

Input channels introduce information into the runtime.

Examples include:

- Chat systems
- Webhooks
- Event streams
- Ticket systems
- Messaging platforms

Input channels are transformed into runtime events.

## Output Channels

Output channels deliver runtime responses.

Examples include:

- Chat responses
- Alerts
- Ticket updates
- Webhooks
- Structured operational messages

Output channels transport runtime intent to external systems.

## Channel Adapters

Channel-specific logic should be isolated in adapters.

Conceptually:

Runtime
↔ Channel Adapter
↔ External System

This preserves runtime portability and reduces platform coupling.

---

# Controller Launch Model

The controller does not launch agents directly.

Instead, the controller launches execution environments capable of hosting Hermes runtimes.

Controller workflow:

1. Resolve Runtime configuration
2. Resolve referenced profiles and resources
3. Resolve tools and channels
4. Provision storage and secrets
5. Construct workload definition
6. Launch workload
7. Maintain lifecycle and continuity

The runtime process is responsible for cognition once execution begins.

---

# Runtime Packages

Operational patterns should not become native platform types.

Instead, reusable configurations should be represented as runtime packages.

A runtime package describes a reusable operational personality.

Examples:

- Cluster Maintainer
- Node Maintainer
- Product Maintainer
- Incident Investigator
- Support Assistant

A package may define:

- Prompts
- Perception policies
- Tool selections
- Interaction defaults
- Runtime defaults
- Operational guidance

A Runtime resource may reference a package and extend or override selected behavior.

This approach preserves a small platform ontology while enabling rich operational specialization.

---

# Architectural Direction

The preferred direction is to keep the platform focused on runtime lifecycle and integration.

Cognition should remain primarily within Hermes.

Operational specialization should emerge through configuration, packages, tools, channels, and policies rather than through growth in the number of native resource types.

This keeps the platform understandable, extensible, and aligned with Kubernetes design principles.