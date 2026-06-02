# ADR 0004: Leverage Existing Infrastructure — Prefer Integration Over Reimplementation

## Status

Accepted.

## Context

Hermes-on-k8s requires several infrastructure capabilities to operate: persistent storage, highly available state, databases for the evolving perception layer, distributed file systems, messaging, and more. Many of these capabilities already exist in the user's environment.

ADR 0002 established the principle of not duplicating Kubernetes-native reconciliation. This ADR extends that same philosophy to **all infrastructure concerns**: Hermes-on-k8s should not force users to install redundant infrastructure components when they already have them.

Without this principle, every Hermes installation would need to bring its own storage, databases, and messaging systems — even if the user already runs CephFS, PostgreSQL, Kafka, or similar. This increases operational cost, adds failure modes, and makes adoption unnecessarily expensive.

## Decision

Hermes-on-k8s SHALL **provide the option to integrate with existing infrastructure** rather than always bundling its own. Users who already run infrastructure components (storage, databases, messaging, etc.) should be able to connect their own installations. Users who need self-contained systems should also be supported.

When Hermes-on-k8s requires an infrastructure capability, it SHALL:

1. **Define a clear interface** for that capability within the Hermes Fabric
2. **Provide adapters** for common existing systems
3. **Allow users to connect their own installations** behind the interface

When the user does not have an existing system, Hermes-on-k8s MAY provide a lightweight default, but this MUST NOT be the only option.

### Examples

| Capability | Interface | Common Adapters |
|---|---|---|
| Persistent storage | PVC / POSIX / object storage API | CephFS, NFS, MinIO, S3, local PV |
| Cognitive state / memory | Key-value / document API | etcd, PostgreSQL, Redis, SQLite |
| Distributed file system | RWX volume | CephFS, NFS, GlusterFS |
| Messaging / events | Pub-sub channel | NATS, Kafka, Redis Streams |
| Observability signals | OTLP / Prometheus | Prometheus, OpenTelemetry, Elasticsearch |

### Fabric Installation Principle

The Hermes Fabric installation MUST be as lightweight as possible. It MUST NOT force-install heavy infrastructure solely for its own use. Every bundled default MUST be optional and replaceable.

## Alternatives Considered

| Alternative                                    | Why Rejected                                                                                                              |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Bundle everything (self-contained install)** | Contradicts ADR 0002 philosophy; forces redundant infrastructure; expensive for users who already have storage, DBs, etc. |
| **Require specific infrastructure**            | Locks users into one vendor/stack; reduces adoption; contradicts existing-system integration principle                    |
| **No defaults at all**                         | Too high a barrier for new users; reasonable defaults with opt-out are acceptable                                         |

## Consequences

### Benefits
- Lower installation cost — users leverage what they already run
- Smaller operational footprint — no redundant storage, databases, or messaging
- Easier enterprise adoption — compliance and policy often mandate specific storage/DB backends
- Consistent with ADR 0002 (don't duplicate Kubernetes reconciliation) — same principle, broader scope
- Fabric stays lightweight — distributions only bring what they need

### Trade-offs
- Interface design requires upfront discipline — poorly defined adapters create coupling
- Testing matrix grows — each supported adapter needs validation
- Documentation must clearly explain both default and custom paths
- Some adapters may have feature gaps — not all backends support every capability equally

## Relationship to Other ADRs

- **ADR 0002** — Extends the "don't duplicate" principle from Kubernetes reconciliation to all infrastructure
- **ADR 0003** — Infrastructure adapter interfaces belong in Hermes Fabric; distributions reference them but don't reimplement them

## Notes

- This ADR establishes the principle. Concrete adapter interfaces and supported backends will be defined in follow-up design documents per capability.
- The "interface + adapter" pattern applies equally inside and outside Kubernetes (e.g., Emissary connecting to an existing PostgreSQL instance for perception state).
