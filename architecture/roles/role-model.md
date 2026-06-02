# Role Model

## Overview

Hermes-on-K8s has three separate concepts:

- **Fabric** — shared cognitive substrate
- **Role** — responsibility domain
- **Distribution** — independently installable assembly

Roles define responsibility domains, not implementation forms or runtime states.

Distributions operationalize roles. A distribution is an independently installable assembly built from Hermes Fabric + role personality + tools + persistence + deployment form.

Each distribution is independently deployable, independently useful, self-cognitive, and self-persistent.

No role is an emergent state of another role. No promotion or election-based identity transitions exist.

Responsibility emerges from:
- role type
- placement
- declared scope

## Native Roles

Native roles are installed as part of Hermes-on-K8s bootstrap. !!comment for hermes: this is wrong. bootstrap in fabric installs whatever is needed as fabric, then installing any distribution installs what is needed additionally. So Warden is not installed until Warden distribution is installed.!!

### Warden

Node-resident cognitive executor. Node-local brain and hands. Runs on every Kubernetes node as a DaemonSet.

### Regent

Cluster cognitive authority. Singleton role responsible for cluster-wide cognition and orchestration. Brain and orchestration authority — execution is delegated to Wardens, Emissaries, and sidecars. !!comment for hermes: wrong. only execution may be delegated to sidecar but never to wardens or etc. because regent is independent of other distributions!!

NOT emergent. NOT elected. NOT derived from Warden.

## Declared Roles

Declared roles are created intentionally after bootstrap via CRDs and configuration. !!comment for hermes: this is old way. now it's like you install the fabric, then you can install any distribution you want. So now all regent and warden and steward are all delarative, while regent and warden are about health of the cluster and stward and emissary are about products/namespaces/applications/external vms/ etc. -- I think you might want to rewrite this file completely!!

### Steward

Application or namespace cognitive role. Observation scope is defined via CRDs, Observable configuration, system knowledge constraints, and cognition history adaptation. !!comment for hermes: one problem is there is relatively too much talk about perception and observation. not saying that is not important but for example here I expect much more explaantion about the nature and usage of steward!!

### Emissary

External infrastructure cognitive role. Runs on Linux, VM, or SSH-accessible systems outside Kubernetes. Operationalized as Emissary Distribution — independently installable, self-cognitive, self-persistent.

## Principle

Kubernetes remains authoritative for reconciliation. !!comment for hermes: why is particularly important here? we know this.!!

Hermes-on-K8s provides cognition and coordination.
