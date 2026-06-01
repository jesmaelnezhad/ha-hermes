# Intent

## Overview

Intent represents desired operational expectations, policies, or preferred outcomes.

Intent defines what should happen rather than what currently exists.

## Examples

- preferred topology
- scaling policy
- SLO expectations
- operational constraints

## Characteristics

Intent:
- guides reasoning
- influences Sessions and Tasks
- may originate from humans or declarative systems
- **influences perception prioritization** (what an agent should pay attention to)

## Role in Perception

Intent acts as a top-down signal in the perception system. While agent-native knowledge and cognition memory shape perception from the bottom up, Intent provides declarative guidance about what *should* be observed:

- A scaling policy Intent makes an agent prioritize metrics related to load and capacity
- An SLO Intent makes an agent focus on latency and error rate signals
- A topology Intent makes an agent watch for changes in service dependencies

This means the same raw signals may be treated differently by agents with different Intents.
