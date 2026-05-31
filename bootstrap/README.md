# HA-Hermes Bootstrap

## Overview

This directory defines how to install HA-Hermes into a fresh Kubernetes cluster or extend it to external systems.

## Bootstrap Targets

HA-Hermes can bootstrap into:

- Kubernetes clusters (primary target)
- Linux VMs
- bare metal systems (via Emissary)

## Core Installation Flow

### 1. Install Wardens (Control Plane)

- Deploy Warden DaemonSet on all Kubernetes nodes
- Enable privileged execution
- Enable Kubernetes API access
- Enable leader election (Lease-based)

### 2. Initialize Regent Election

- Kubernetes Lease object created
- One Warden becomes Regent
- Regent starts cluster coordination loop

### 3. Install Steward Layer

- Deploy Steward per namespace or application domain
- Attach to workload namespaces
- Enable observability hooks

### 4. Optional: Emissary Deployment

- Install agent on external systems via SSH or container
- Register with cluster via Warden API

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

## Post-Bootstrap State

After installation:

- Wardens maintain cluster health
- Regent coordinates system state
- Stewards manage applications
- Emissaries extend system reach

## Goal

After bootstrap, no manual cluster operations are required outside Hermes itself.
