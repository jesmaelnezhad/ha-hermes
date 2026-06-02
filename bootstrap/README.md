# HA-Hermes Bootstrap

## Overview

This directory defines how to install HA-Hermes into a fresh Kubernetes cluster or extend it to external systems.

## Bootstrap Targets

HA-Hermes distributions install into:

- Kubernetes clusters (primary target)
- Linux VMs
- bare metal systems (via Emissary Distribution)

## Core Installation Flow

### 1. Install Warden Distribution

- Deploy Warden DaemonSet on Kubernetes nodes
- Enable privileged execution
- Enable Kubernetes API access
- Each Warden is independently useful — operates as node-local brain and hands

### 2. Install Regent Distribution

- Deploy Regent as a singleton cluster-scoped distribution
- HA-aware deployment
- Regent starts cluster coordination loop
- Regent must be useful even without Wardens or Stewards present

### 3. Install Steward Distribution

- Deploy Steward per namespace or application domain
- Attach to workload namespaces
- Enable observability hooks
- Highly available deployment model
- Steward must be useful without Regent or Warden

### 4. Optional: Install Emissary Distribution

- Install agent on external systems via SSH or container
- Register with cluster
- Operates independently on non-Kubernetes infrastructure

## Distribution Independence

Each distribution is independently deployable and independently useful:
- Regent alone — valid and operational
- Warden alone — valid and operational
- Steward alone — valid and operational

Integration between distributions is optional. Independence is required.

## Required Kubernetes Primitives

- Deployments
- DaemonSets
- Leases (coordination.k8s.io)
- Persistent Volumes (RWX recommended)
- RBAC roles for Hermes agents

## Cognitive Layer Setup

A shared storage layer must be provisioned:

- `/ha-hermes` volume
- or object storage bucket

Used for:
- tasks
- memory
- sessions
- skills

Every runtime-backed distribution maintains persistent cognition. Loss of pod identity does not imply loss of cognition.

## Post-Bootstrap State

After installation:
- Wardens maintain node health
- Regent coordinates cluster state
- Stewards manage applications
- Emissaries extend system reach
