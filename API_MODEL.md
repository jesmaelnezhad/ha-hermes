# Runtime API Model

## Design Principle

k8s-hermes-collective should expose a small, stable, and Kubernetes-native API.

The platform is a control plane for Hermes runtimes.

Its API should primarily describe:

- What cognitive service should exist
- What capabilities should be available
- How that service should be operated

The platform should avoid reproducing Hermes concepts as Kubernetes resources unless there is clear operational value.

---

# API Topology

The preferred v1 API surface is intentionally small.

## Runtime

The primary resource.

Represents a managed cognitive service.

## Tool

A reusable capability integration.

Provides capabilities that may be consumed by multiple runtimes.

These two resources form the core platform model.

---

# Runtime Resource

Runtime is the primary abstraction of the platform.

A Runtime declares:

> create and operate this Hermes-based cognitive service.

A Runtime is not:

- A pod
- A process
- A profile
- A volume

A Runtime is the desired operational entity that the controller continuously reconciles.

---

# Runtime Spec

A Runtime specification should focus on operational intent.

Illustrative structure:

```yaml
spec:
  runtime:
  persistence:
  continuity:
  availability:
  tools:
  skills:
  channels:
```

Exact schemas may evolve.

The responsibility boundaries should remain stable.

---

# Runtime Configuration

This section controls how Hermes is configured and launched.

Illustrative concerns include:

```yaml
runtime:
  image:
  version:
  configuration:
```

The controller renders configuration artifacts required by Hermes.

The platform should remain focused on Hermes configuration surfaces rather than Hermes internals.

---

# Persistence

Persistence describes runtime durability requirements.

Illustrative structure:

```yaml
persistence:
  enabled:
  storageClass:
  size:
```

The platform preserves runtime state.

Hermes remains responsible for the contents of that state.

---

# Continuity

Continuity describes how runtime state is reused.

Illustrative structure:

```yaml
continuity:
  mode:
  source:
```

Potential modes include:

- Ephemeral
- Persistent
- Existing

This section governs runtime continuity rather than infrastructure persistence.

---

# Availability

Availability describes runtime resilience.

Illustrative structure:

```yaml
availability:
  mode:
  recovery:
```

Examples include:

- Single runtime
- Recoverable runtime
- Service runtime with failover expectations

The platform should preserve the concept of a single cognitive identity even when multiple infrastructure components participate in maintaining availability.

---

# Tools

Runtimes consume reusable Tool resources.

Illustrative structure:

```yaml
tools:
  - github
  - jira
  - cluster-api
```

Tools should be reference-based.

This creates reusable ownership boundaries and avoids repeated capability definitions.

---

# Skills

Skills are delivered to Hermes.

The platform should treat skills primarily as deployable runtime assets.

Illustrative structure:

```yaml
skills:
  - incident-response
  - cluster-analysis
```

The controller is responsible for delivery.

Hermes is responsible for skill behavior.

---

# Channels

Channels describe how information enters and leaves a runtime.

Illustrative structure:

```yaml
channels:
  inputs:
  outputs:
```

Examples include:

- Chat systems
- Webhooks
- Ticket systems
- Event streams
- MCP services

The platform concern is delivery and configuration.

---

# Tool Resource

Tool is the primary reusable resource.

A Tool represents a capability integration.

Illustrative structure:

```yaml
kind: Tool

spec:
  type:
```

Potential implementations include:

- MCP integrations
- External service integrations
- Sidecar-delivered capabilities
- Operational capability providers

The exact implementation should remain hidden behind a stable Tool abstraction.

---

# Status

Status is controller-owned.

Status should communicate:

- Lifecycle state
- Health
- Conditions
- Availability state
- Runtime references
- Continuity information

Status should describe operational reality.

It should not expose runtime cognition.

---

# Configuration Philosophy

The API should remain:

- Runtime-centric
- Operationally focused
- Hermes-aligned
- Declarative
- Small in surface area

The platform should favor reusable resources where ownership boundaries are valuable and embedded configuration where simplicity is more important.