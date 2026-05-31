# Cognitive State Model

## Overview

HA-Hermes maintains a distributed cognitive layer that stores memory, tasks, and operational knowledge for agents.

This layer is separate from:

- Git (declarative intent)
- Kubernetes etcd (runtime state)

## Purpose

Cognitive state enables Hermes agents to:

- remember past incidents
- maintain task context
- share operational knowledge
- track investigations

## Storage Model

Cognitive state may be stored using Kubernetes-native or cluster-backed storage:

- Persistent Volumes (RWX preferred)
- object storage
- databases (optional extension)

## Data Categories

### 1. Tasks
- active work items
- assigned responsibilities
- execution progress

### 2. Memory
- historical incidents
- learned patterns
- system knowledge

### 3. Skills
- reusable procedures
- operational playbooks
- automation routines

### 4. Sessions
- active investigations
- debugging state
- reasoning traces

## Access Model

- Wardens read/write system-wide cognitive state
- Stewards maintain application-level cognitive state
- Emissaries sync external state into the system

## Consistency

- eventual consistency is acceptable for most cognitive data
- coordination state remains in Kubernetes (Leases/CRDs)

## Summary

Cognitive state is the shared memory layer that enables HA-Hermes agents to behave as a coordinated system rather than isolated controllers.
