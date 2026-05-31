# Steward Role

## Overview

A Steward is a Kubernetes namespace or application-level Hermes agent responsible for maintaining workloads, services, and application behavior.

Stewards represent the application plane of HA-Hermes.

## Responsibilities

### Application Management
- manage deployments and services
- handle rollouts and upgrades
- ensure service health
- coordinate scaling decisions

### Observability
- analyze logs and metrics
- detect anomalies in applications
- correlate service-level incidents

### Incident Response
- diagnose application failures
- coordinate fixes with Wardens and Emissaries
- maintain service stability

### Domain Cognition
- maintain application-specific memory
- track service topology
- store operational knowledge per namespace

## Scope

Stewards operate at:

- Kubernetes namespace level
- service domain level
- cluster-shared services when needed

## Interaction Model

Stewards:

- request execution from Wardens for node-level actions
- delegate external tasks to Emissaries
- receive coordination from Regent

## Summary

Stewards are the application intelligence layer of HA-Hermes, responsible for ensuring that services remain healthy, observable, and continuously operable.
