# Runtime Lifecycle Model

## Purpose

This document defines the lifecycle relationship between a runtime resource, the controller, runtime processes, sessions, and continuity.

The objective is to establish a clear operational model before concrete CRD schemas and implementation details are finalized.

---

# Core Principle

The runtime resource is the durable object.

Pods, processes, leaders, replicas, and executions are implementation details used to realize the desired runtime.

A runtime should maintain continuity across infrastructure events whenever its configuration allows that continuity to be preserved.

The controller is therefore responsible for preserving runtime intent while the runtime process is responsible for cognition and execution.

---

# Runtime Instantiation

A runtime resource represents a desired cognitive runtime.

When a runtime is created, the controller evaluates the specification and materializes the required Kubernetes resources.

The exact workload type is derived from runtime topology.

Examples may include:

- Deployment
- StatefulSet
- DaemonSet
- Job-like execution models

The runtime resource remains the authoritative object.

Workloads exist only to realize that runtime.

The controller owns the mapping between runtime intent and workload implementation.

---

# Runtime Identity

Runtime identity is distinct from process identity.

A runtime may exist for months.

Individual pods may exist for minutes.

A pod restart does not create a new runtime.

A leader transition does not create a new runtime.

A controller restart does not create a new runtime.

The runtime resource defines identity.

All operational artifacts derive from that identity.

---

# Runtime Continuity

Continuity determines whether cognition survives runtime infrastructure changes.

Three conceptual modes currently exist.

## Ephemeral

The runtime begins with no prior continuity.

Restarting the runtime creates a new cognitive instance.

No previous session is reused.

This mode is suitable for:

- One-time tasks
- Experiments
- Temporary assistants

---

## Persistent

The runtime maintains durable continuity.

Restarts preserve runtime history through persisted session state.

The runtime continues from its previously known state whenever recovery is possible.

This mode is suitable for:

- Maintainers
- Long-lived assistants
- Operational ownership scenarios

---

## Referenced

The runtime attaches to an existing continuity source.

The source may have been created by another runtime instance.

This enables:

- Runtime replacement
- Runtime migration
- Shared operational context
- Recovery from infrastructure loss

The exact reference model remains implementation-specific.

---

# Session Binding

Sessions represent cognitive continuity.

A runtime may create, own, or attach to sessions.

The controller does not interpret session contents.

The controller only manages lifecycle relationships.

Conceptually:

Runtime
→ Session
→ Memory

The runtime reasons.

The session preserves continuity.

Memory preserves retained cognition.

These concerns should remain distinct.

---

# Controller Responsibilities

The controller owns lifecycle.

Responsibilities include:

- Configuration resolution
- Runtime provisioning
- Session attachment
- Persistence wiring
- Availability management
- Runtime replacement
- Health observation
- Reconciliation

The controller should not participate in cognition.

It should not:

- Interpret observations
- Execute reasoning
- Make runtime decisions
- Modify cognitive state

The controller maintains runtime existence.

The runtime performs cognitive work.

---

# Runtime Responsibilities

The runtime owns cognition.

Responsibilities include:

- Observation
- Reasoning
- Planning
- Tool usage
- Interaction
- Session evolution
- Memory creation

The runtime should not own infrastructure lifecycle.

Lifecycle remains under controller authority.

---

# Runtime State Machine

A runtime progresses through observable lifecycle phases.

The exact names may evolve.

The conceptual model is:

Pending
→ Bootstrapping
→ Running

Running may transition to:

- Recovering
- Degraded
- Stopped
- Failed

## Pending

The runtime has been declared but infrastructure has not yet been prepared.

## Bootstrapping

Required runtime resources are being created.

Configuration is being resolved.

Session attachment may occur during this phase.

## Running

The runtime is healthy and capable of performing cognitive work.

## Recovering

The runtime is attempting to restore desired continuity after disruption.

## Degraded

The runtime remains operational but continuity, availability, tooling, perception, or integrations are partially impaired.

## Stopped

The runtime has been intentionally halted.

## Failed

The controller cannot currently realize desired runtime behavior.

---

# Availability Model

Availability concerns runtime existence rather than cognition.

A runtime may be configured for:

- Single-instance execution
- High availability
- Distributed placement

The availability model should preserve a simple principle:

A runtime should behave as a single cognitive identity even when multiple infrastructure instances participate in preserving availability.

The user manages one runtime.

The system manages the infrastructure required to keep that runtime available.

---

# Leadership

Certain availability configurations may require leadership.

Leadership exists to coordinate runtime execution.

Leadership does not create multiple independent cognitive actors.

At any point in time, there should be a clear authority responsible for active cognition and execution.

Standby participants exist to preserve continuity and availability.

They do not represent independent runtime identities.

---

# Trigger Models

Trigger models influence runtime lifecycle.

## Reactive

The runtime primarily responds to incoming events or interactions.

Examples include:

- Chat interactions
- Webhooks
- Operational events

Reactive runtimes may eventually support scale-to-zero patterns.

---

## Scheduled

The runtime executes according to defined schedules.

Examples include:

- Daily reviews
- Periodic audits
- Maintenance routines

Scheduled runtimes may spend significant periods inactive.

---

## Continuous

The runtime remains continuously active.

Examples include:

- Cluster maintainers
- Product maintainers
- Environment supervisors

Continuous runtimes are expected to maintain active continuity.

---

# Continuity During Failure

Infrastructure failure should not automatically imply cognitive loss.

When continuity has been configured:

- Sessions should remain recoverable
- Memory should remain accessible
- Leadership should be transferable
- Runtime identity should remain stable

Recovery behavior should be deterministic and observable.

The controller is responsible for restoring runtime operation.

The runtime is responsible for resuming cognitive work.

---

# Architectural Constraint

The lifecycle model should preserve a strict separation between runtime management and cognition.

The controller manages existence.

The runtime manages cognition.

This boundary should remain stable as the platform evolves.