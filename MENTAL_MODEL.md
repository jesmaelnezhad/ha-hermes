# Current Architectural Mental Model

## What k8s-hermes-collective Is

k8s-hermes-collective is a Kubernetes-native system for managing Hermes-based cognitive runtimes through declarative resources.

At its core, the system introduces one or more Kubernetes Custom Resource Definitions (CRDs) and controllers that reconcile those resources into running Hermes-compatible processes.

The purpose of the system is not to implement cognition itself, nor to replace Kubernetes primitives. Instead, it provides a declarative lifecycle and operational model for cognitive runtimes.

A user describes a desired cognitive process declaratively. The controller interprets that declaration, provisions the required runtime environment, maintains lifecycle and continuity, and ensures the desired runtime remains operational.

Hermes serves as enabling runtime technology. k8s-hermes-collective is the orchestration and operational layer around that runtime.

## Core Architectural Shape

The architecture is organized around three layers.

### Kubernetes

Kubernetes remains the authoritative orchestration substrate.

It provides:

- Scheduling
- Reconciliation
- Networking
- Storage primitives
- High availability mechanisms
- Runtime execution infrastructure

k8s-hermes-collective builds on these capabilities rather than replacing or duplicating them.

### k8s-hermes-collective Controller

The controller is the primary system component.

It watches cognitive runtime resources and reconciles them into operational Hermes processes.

Responsibilities include:

- Runtime lifecycle management
- Process bootstrapping
- Configuration resolution
- Session continuity and reuse
- Persistence coordination
- High-availability behavior
- Failure recovery
- Tool and integration wiring
- Input and output channel setup

The controller is responsible for maintaining declared cognitive runtime state.

### Hermes Runtime Process

The runtime process performs cognition.

This process is expected to be Hermes CLI or a Hermes-Agent-derived runtime designed for operational execution.

The runtime may:

- Perform tasks
- Maintain systems
- Assist users
- Observe environments
- Use tools
- Maintain sessions
- Interact through configured channels

k8s-hermes-collective manages the runtime. The runtime performs cognitive work.

## Primary Abstraction

The native abstraction of the system is the cognitive runtime resource.

The exact CRD name remains open.

Possible names include:

- HermesRuntime
- CognitiveRuntime
- Collective
- Other names aligned with project vocabulary

Regardless of naming, the architectural principle is stable:

The system should expose a small number of native primitives.

Behavioral patterns and operational personalities are configurations of those primitives rather than independent platform types.

## Cognitive Runtime Resource

A runtime resource describes enough information for the controller to create and maintain a Hermes-compatible process.

The resource may describe:

### Runtime

How the runtime is launched and operated.

Potential concerns:

- Image
- Runtime implementation
- Command and startup mode
- Resource limits
- Execution environment
- Placement

### Session

Session lifecycle and continuity.

Potential concerns:

- Persistent sessions
- Session reuse
- Existing session references
- Continuity guarantees
- Session ownership

### Perception

Observation and attention behavior.

Potential concerns:

- Existing perception policy reuse
- Bootstrap policies
- Adaptive perception enablement
- Policy references

### Tools

Capability surface available to the runtime.

Potential concerns:

- Tool selection
- Tool configuration
- Permission boundaries
- Runtime capability profiles

### Channels

How the runtime receives and produces information.

Potential concerns:

- User interaction
- Event ingestion
- Messaging systems
- Slack or chat interfaces
- Webhooks
- Ticketing or operational systems
- Structured output destinations

### Availability and Continuity

Operational durability of the runtime.

Potential concerns:

- Replication
- Failover
- Leadership
- Persistence
- Restart behavior
- Recovery policy

These categories are illustrative rather than exhaustive.

The resource should remain flexible enough to support cognitive runtimes with very different operational purposes.

## Use Cases as Configurations

Operational identities such as node maintainers or cluster maintainers are not native architectural types.

They are packaged or reusable configurations built on top of the runtime abstraction.

Examples may include:

- Node maintainer
- Cluster maintainer
- Product maintainer
- Support assistant
- Incident investigator
- Environment-specific operators

These are examples that demonstrate the power of the runtime model rather than architectural primitives themselves.

The architecture should avoid embedding these use cases as first-class ontology unless strong technical constraints justify doing so.

## Design Direction

The system should remain:

- Kubernetes-native
- Declarative
- Minimal in native concepts
- Runtime-oriented
- Flexible in configuration
- Compatible with multiple operational personalities and execution models

The emphasis is on providing a durable and extensible runtime abstraction rather than defining a fixed taxonomy of cognitive roles.