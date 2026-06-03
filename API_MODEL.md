# Runtime API Model

## Design Principle

k8s-hermes-collective should expose a small and composable API surface.

The system centers around a primary runtime resource that declares desired cognitive runtime behavior and lifecycle.

Supporting resources may exist where reuse, independent evolution, or policy sharing provide architectural value.

The objective is to preserve a simple user experience while avoiding oversized and tightly coupled resource definitions.

The architecture therefore follows:

- One primary runtime resource
- Optional supporting resources
- Embedded-first configuration with optional references

This provides an approachable default model while allowing composition and reuse where appropriate.

---

# API Topology

The API surface is organized around a single primary runtime resource.

Supporting resources exist to provide reusable configuration and policy.

## Primary Resource

The runtime resource is the native abstraction of the platform.

The exact resource name remains open.

Possible names include:

- Runtime
- HermesRuntime
- CognitiveRuntime
- Collective

For architectural discussion, this document uses:

`Runtime`

as a neutral placeholder.

The runtime resource declares:

> instantiate and maintain this cognitive runtime

The runtime is the only required cognitive resource.

---

## Supporting Resources

Certain concerns are naturally reusable and should not necessarily be embedded repeatedly across runtime definitions.

Potential supporting resources include:

| Resource | Purpose |
|---|---|
| PerceptionPolicy | Attention and observation behavior |
| ToolProfile | Capability bundles |
| MemoryProfile | Memory and retention strategy |
| InteractionProfile | Input, output, and trigger behavior |
| RuntimeTemplate | Reusable runtime patterns |

These resources are optional.

A runtime may:

- Embed configuration directly
- Reference reusable resources
- Mix both approaches

This flexibility supports both simple and advanced deployment models.

---

# Runtime Resource

The runtime resource defines desired runtime behavior.

Conceptually:

Identity
+ Environment
+ Cognition
+ Capabilities
+ Interaction
=
Runtime Specification

---

# Spec

The runtime specification represents declarative intent.

High-level structure:

```yaml
spec:
  identity
  environment
  cognition
  capabilities
  interaction
```

---

# Identity

Identity describes semantic context.

This layer is distinct from Kubernetes metadata.

It describes what the runtime is intended to be and why it exists.

Illustrative structure:

```yaml
identity:
  purpose:
  persona:
  owner:
  labels:
  description:
```

Identity may describe:

- Purpose
- Behavioral identity
- Ownership
- Domain context
- Descriptive semantics

Examples:

- Cluster maintainer
- Incident investigator
- Product assistant

Identity provides runtime context without embedding operational behavior.

---

# Environment

Environment describes operational embodiment.

This layer answers:

> how should this runtime exist?

Illustrative structure:

```yaml
environment:
  runtime:
  placement:
  availability:
  resources:
  storage:
```

This section is infrastructure-oriented and cognition-agnostic.

## Runtime

Defines execution engine configuration.

Illustrative structure:

```yaml
runtime:
  implementation:
  image:
  version:
  args:
```

This allows runtime evolution while preserving API stability.

The implementation may include Hermes CLI, Hermes-agent-derived runtimes, or future compatible engines.

## Placement

Defines scheduling and topology.

Illustrative structure:

```yaml
placement:
  mode:
  nodeSelector:
  affinity:
  tolerations:
```

Potential placement modes include:

- Deployment-style
- Daemon-style
- Singleton

Placement governs runtime topology rather than cognition.

## Availability

Defines runtime durability.

Illustrative structure:

```yaml
availability:
  replicas:
  leaderElection:
  restartPolicy:
```

Availability describes how runtime existence is preserved.

## Resources

Defines conventional compute constraints.

Illustrative structure:

```yaml
resources:
  requests:
  limits:
```

## Storage

Defines operational persistence.

Illustrative structure:

```yaml
storage:
  workspace:
  persistence:
```

Storage concerns operational continuity rather than cognitive memory.

---

# Cognition

Cognition defines how the runtime thinks and preserves continuity.

Illustrative structure:

```yaml
cognition:
  session:
  perception:
  memory:
  reasoning:
```

This layer forms the cognitive center of the runtime.

## Session

Session defines continuity.

Illustrative structure:

```yaml
session:
  mode:
  reuse:
  retention:
```

Potential modes include:

- Ephemeral
- Persistent
- Referenced

Referenced sessions enable continuity through explicit session reuse.

Illustrative reuse model:

```yaml
reuse:
  sessionRef:
```

Session concerns continuity of runtime identity and operation.

## Perception

Perception controls what enters cognition.

Illustrative structure:

```yaml
perception:
  policyRef:
  adaptive:
```

Perception is expected to be policy-driven.

Reusable policies enable:

- Shared behavior
- Experimentation
- Consistent operational interpretation
- Reuse across runtimes

## Memory

Memory concerns retained cognition.

Illustrative structure:

```yaml
memory:
  profileRef:
  scope:
```

Potential scopes include:

- Runtime-local
- Namespace
- Shared

Memory is optional.

Not all runtimes require retained cognition.

## Reasoning

Reasoning defines behavioral posture.

Illustrative structure:

```yaml
reasoning:
  autonomy:
  safety:
  planning:
```

Reasoning influences runtime behavior.

Examples:

- Advisory
- Supervised
- Autonomous

Reasoning governs cognitive behavior rather than authority.

---

# Capabilities

Capabilities define action surface.

Illustrative structure:

```yaml
capabilities:
  tools:
  permissions:
  policies:
```

Capabilities answer:

> what may this runtime do?

## Tools

Tools define available capabilities.

Illustrative structure:

```yaml
tools:
  refs:
```

Tool profiles support reuse and small runtime specifications.

## Permissions

Permissions define authority.

Capability and authority are intentionally separate.

A runtime may possess a tool while remaining restricted in how that tool may be used.

Illustrative structure:

```yaml
permissions:
  profiles:
```

Permissions may later integrate with runtime policy, execution boundaries, and Kubernetes authorization models.

## Policies

Policies define execution guardrails.

Illustrative structure:

```yaml
policies:
  approval:
  escalation:
  restrictions:
```

Policies govern execution behavior rather than capability availability.

---

# Interaction

Interaction defines communication and activation behavior.

Illustrative structure:

```yaml
interaction:
  triggers:
  inputs:
  outputs:
```

Interaction is broader than transport or messaging.

It describes how cognition enters and leaves the runtime.

## Triggers

Triggers define runtime activation behavior.

Illustrative structure:

```yaml
triggers:
  mode:
```

Potential modes include:

- Reactive
- Scheduled
- Continuous

Trigger behavior significantly influences runtime lifecycle.

## Inputs

Inputs define ingress.

Illustrative structure:

```yaml
inputs:
  refs:
```

Potential examples include:

- Chat systems
- Webhooks
- Event streams
- Tickets
- Operational systems

## Outputs

Outputs define egress.

Illustrative structure:

```yaml
outputs:
  refs:
```

Potential examples include:

- Chat
- Alerts
- Ticket updates
- Webhooks
- Structured operational responses

---

# Status

Status is controller-owned.

It describes observed runtime reality.

Illustrative structure:

```yaml
status:
  lifecycle:
  runtime:
  continuity:
```

Status answers:

> what is happening now?

It does not expose cognition contents.

## Lifecycle

Operational state.

Illustrative structure:

```yaml
lifecycle:
  phase:
  ready:
  conditions:
```

This follows conventional Kubernetes patterns.

## Runtime

Observed runtime state.

Illustrative structure:

```yaml
runtime:
  podRefs:
  leader:
  version:
```

This reflects observed operational reality.

## Continuity

Continuity describes runtime-level cognitive state without exposing cognition itself.

Illustrative structure:

```yaml
continuity:
  sessionId:
  memoryRef:
  lastActivity:
```

This preserves separation between runtime lifecycle and runtime knowledge.

---

# Configuration Philosophy

The platform follows an embedded-first configuration model with optional references.

Simple runtimes should be easy to author directly.

Reusable policy and profile resources should remain available where shared configuration provides value.

The preferred progression is:

1. Embedded configuration by default
2. Reusable references where composition becomes useful
3. Mixed models where operational flexibility requires both

This approach balances usability and long-term composability.