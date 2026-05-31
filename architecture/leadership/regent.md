# Regent

## Overview

Regent is a temporary leadership state held by one Warden through Kubernetes leader election.

It is not a separate agent type.

## Responsibilities

- coordinate Wardens
- assign cluster-wide tasks
- resolve conflicts
- maintain global view of cluster state

## Lifecycle

- elected via Kubernetes Lease
- only one Regent exists at a time
- replaced automatically on failure

## Summary

Regent is the active leadership state of the Warden collective.
