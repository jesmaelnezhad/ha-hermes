# Hermes Feedback — Architectural Review

> Role: Software Architect & Developer
> Date: 2026-05-31
> Repo: ha-hermes (master)

---

## What I Like

**1. Layered cognition model is sound.**
The three-plane separation (Native Hermes / Application / External Infrastructure) maps well to real operational concerns. Wardens for nodes, Stewards for apps, Emissary for outside-cluster. This mirrors how platform teams actually think.

**2. "Kubernetes stays authoritative" is the right call.**
ADR 0001 and 0002 both enforce this clearly. No reconciliation overlap, no competing controllers. HA-Hermes as a *cognitive* layer on top of Kubernetes' execution layer is architecturally clean. This is the single most important design decision and it's correct.

**3. Git/etcd/Hermes three-store model.**
Git = declarative intent, etcd = runtime truth, Hermes = cognitive state. This is a clean separation of concerns that prevents the common trap of mixing configuration, state, and memory.

**4. Role simplicity.**
Four roles (Warden, Regent, Steward, Emissary) is a manageable number. Each has a clear scope boundary. Native vs declared is a good distinction — it separates system-critical from user-intentional.

**5. Cognitive artifacts are well-defined.**
Observation → Session → Task → Execution → Memory, with Skill and Intent as cross-cutting influences. This is a solid cognitive loop that maps to how AI agents actually work.

**6. Emissary as the Linux/VM edge agent.**
Extending Hermes beyond Kubernetes via SSH-accessible agents is pragmatic. It acknowledges that real infrastructure isn't just K8s.

---

## What I Dislike / Concerns

**1. ~~Regent model is contradictory.~~ RESOLVED.**
Initially, regent.md said Regent was a "separate role" while warden.md said "A Warden may temporarily become Regent" via Lease election — a direct contradiction. This has been resolved across two commits:
- `regent.md` updated to: "Regent is not derived from runtime election or emergence" and "Regent is a predefined native role instance"
- `warden.md` updated to: "Regent is a separate native role. Wardens do not become Regent. Wardens do not participate in election or promotion into Regent."
Both files are now consistent. Regent is a separate native role, not an elected Warden state.

**2. Shared memory / cognitive state storage is undefined.**
The cognition model is conceptually solid but the persistence layer is TBD ("Possible approaches include: RWX storage, object storage, database-backed cognition"). This is the hardest problem in the whole system — distributed cognitive state across agents — and it's left as an exercise. Without this, the cognitive artifacts (Session, Memory, Skill, Intent) are just documentation, not implementation. I'd建议 stubbing at least a CRD or schema for these early.

**3. No clear inter-agent communication model.**
How do Wardens talk to Stewards? How does Regent coordinate Wardens? Is this via K8s API, a message bus, gRPC, shared storage? The architecture is silent on this. For a *distributed* cognitive operator, the communication substrate is as important as Kubernetes is for the execution substrate. It shouldn't be an afterthought.

**4. "Hermes CLI" as the cognitive runtime is underspecified.**
The core model says "Hermes provides cognition" but doesn't say which Hermes — is this the Nous Hermes CLI tool (hermes-agent)? A custom Hermes build? If it's the off-the-shelf Hermes CLI, the architecture needs to address:
- How Hermes sessions map to K8s workloads
- How Hermes memory/skills are shared across agents
- How Hermes tool calling interacts with the K8s API vs privileged node commands

**5. Bootstrap "no manual operations required" is aspirational, not realistic.**
The bootstrap README says: "After bootstrap, no manual cluster operations are required outside Hermes itself." This is a nice goal but it glosses over: who bootstraps the bootstrap? How does HA-Hermes handle its own upgrades? What happens when Hermes itself has a bug that prevents it from self-managing? There should be an "escape hatch" or break-glass procedure documented.

**6. Missing: security model details.**
Regent has "access or retrieve protected credentials when authorized" — authorized by what? How are secrets stored and accessed? What's the trust model between roles? RBAC is mentioned briefly but not specified. For a system with privileged execution on every node, security needs to be a first-class document, not a stub.

**7. Missing: multi-cluster / federation.**
No mention of multi-cluster scenarios. Even if v1 is single-cluster, the architecture should at least acknowledge whether multi-cluster is a future direction or explicitly out of scope.

**8. Skill artifact is underspecified.**
Skills are defined as "reusable operational capability" with examples like "node recovery, kafka troubleshooting, certificate renewal." But there's no format, no storage, no versioning mechanism described. Given that Hermes Agent already has a skill system (SKILL.md), there should be at least a reference to how K8s-hosted skills map to the existing skill format.

---

## What's Missing (Gaps to Address)

1. **Concrete CRD or API schema** for cognitive artifacts (at minimum: Session, Task, Memory, Skill, Intent)
2. **Inter-agent communication protocol** — how roles communicate and coordinate
3. **Identity and RBAC** per role — what each role can do, how it authenticates
4. **Failure modes** — what happens when Regent goes down, when a Warden is partitioned, when cognitive state is lost
5. **Upgrade strategy** — how HA-Hermes updates itself
6. **Observability of HA-Hermes itself** — who watches the watchers
7. **Concrete Hermes runtime spec** — exact version, configuration model, how it's containerized
8. **Networking** — how agent-to-agent traffic is routed, secured, and isolated

---

## Overall Assessment

The architectural thinking is solid. The big ideas are right:
- Cognition layer on top of a proven execution layer (Kubernetes)
- Don't duplicate what K8s already does
- Clear role separation with defined scopes
- Store intent, truth, and cognition in separate places

The main gap is that the docs read like an **early design document** (which they are) but they're missing the **concrete implementation bridges** that turn concepts into a working system. The next phase should pick 2-3 of the biggest gaps — I'd recommend: (1) define the cognitive state persistence layer, (2) specify the inter-agent communication mechanism, and (3) stub CRD schemas for cognitive artifacts.

The declared-agents.md file that was just removed was presumably for custom user-defined agent types? I'd suggest either replacing it with something more specific or ensuring the role-model.md covers extensibility.

---

*This feedback is based on reading all files in the repository as of the latest pull (commit d3c3d08). Regent contradiction was resolved in commits 4834e11 and d3c3d08.*
