# Runtime Lifecycle Model

## Purpose

This document defines the lifecycle relationship between Runtime resources, controllers, Kubernetes workloads, and Hermes runtimes.

The objective is to establish a stable operational model for runtime management.

---

# Core Principle

A Runtime is the durable managed entity.

Pods, containers, services, storage volumes, and leaders are implementation artifacts used to realize that Runtime.

The controller preserves Runtime existence.

Hermes performs cognitive work.

---

# Runtime Lifecycle

A Runtime represents desired operational state.

When a Runtime is created, the controller:

- Resolves Runtime configuration
- Resolves Tool references
- Renders Hermes configuration
- Constructs runtime filesystem layouts
- Provisions storage
- Creates workload resources
- Establishes connectivity
- Maintains lifecycle

The Runtime resource remains authoritative throughout its lifetime.

---

# Runtime Identity

Runtime identity is independent from infrastructure identity.

A Runtime may survive:

- Pod replacement
- Container replacement
- Node replacement
- Controller restart

The Runtime remains the same managed cognitive service.

Infrastructure artifacts are replaceable.

Runtime identity is not.

---

# Runtime Continuity

Continuity determines how runtime state survives lifecycle events.

## Ephemeral

Runtime state is not reused.

Infrastructure replacement creates a fresh runtime instance.

Suitable for:

- One-time tasks
- Temporary workloads
- Experimental runtimes

---

## Persistent

Runtime state survives infrastructure replacement.

The controller restores access to persisted runtime state.

Suitable for:

- Long-lived assistants
- Operational maintainers
- Service runtimes

---

## Existing

A Runtime attaches to previously established runtime state.

Suitable for:

- Migration
- Recovery
- Runtime replacement
- Continuity transfer

The controller manages attachment.

Hermes manages the resulting cognitive continuity.

---

# Controller Responsibilities

The controller owns operational lifecycle.

Responsibilities include:

- Runtime reconciliation
- Tool resolution
- Configuration rendering
- Filesystem rendering
- Workload provisioning
- Persistence provisioning
- Connectivity provisioning
- Recovery
- Health observation
- Availability management

The controller should not participate in cognition.

---

# Hermes Responsibilities

Hermes owns cognitive execution.

Responsibilities include:

- Reasoning
- Tool usage
- Session management
- Memory management
- Skill execution
- Channel interaction
- Agent behavior

Hermes should not be responsible for infrastructure lifecycle.

---

# Runtime States

A Runtime progresses through observable operational states.

Conceptually:

Pending
→ Provisioning
→ Starting
→ Running

Running may transition to:

- Recovering
- Degraded
- Stopped
- Failed

## Pending

The Runtime has been declared.

No infrastructure has yet been realized.

## Provisioning

Storage, configuration, tools, secrets, and connectivity are being prepared.

## Starting

Workloads are launching and attaching required runtime resources.

## Running

The Runtime is healthy and available.

## Recovering

The controller is restoring desired Runtime state.

## Degraded

The Runtime remains available but some capabilities are impaired.

## Stopped

The Runtime has been intentionally halted.

## Failed

The controller cannot currently realize the Runtime.

---

# Availability Model

Availability concerns Runtime existence and service continuity.

A Runtime should behave as a single cognitive identity.

Availability mechanisms exist to preserve that identity.

Examples include:

- Workload recreation
- Runtime recovery
- Service restoration
- Leadership transfer

Availability should not create multiple independent cognitive actors.

---

# Leadership

Some Runtime configurations may require leadership.

Leadership coordinates active execution.

At any point in time there should be a clearly defined active execution authority.

Standby infrastructure may exist to support recovery and availability.

The Runtime remains a single managed entity.

---

# Service Runtimes

Certain runtimes operate as continuously available services.

Examples include:

- MCP servers
- Operational assistants
- Persistent organizational runtimes

The platform should support recovery patterns that preserve service availability and runtime continuity.

---

# Failure Recovery

Infrastructure failure should not automatically imply Runtime loss.

When continuity is configured:

- Runtime state should remain accessible
- Runtime identity should remain stable
- Service availability should be restorable
- Runtime execution should be recoverable

The controller restores operation.

Hermes resumes cognitive work.

---

# Architectural Constraint

A strict boundary should be maintained.

The controller manages:

- Existence
- Infrastructure
- Lifecycle
- Availability
- Persistence

Hermes manages:

- Cognition
- Memory
- Sessions
- Skills
- Behavior

This boundary should remain stable as the platform evolves.