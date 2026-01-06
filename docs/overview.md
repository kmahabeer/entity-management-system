---
layout: page
title: Overview
permalink: /overview/
---

# Overview

## What is an Entity?

An ***entity*** is any canonical object the DMS cares about: a file, digital asset, URL, document, reference, derived artifact, etc. EMS exists to make authoritative decisions about entities while delegating all execution to downstream systems. It is the DMS's **spine**.

## Purpose

EMS exists to impose coherence on a distributed system. It provides a single, authoritative layer that:

- assigns identity
- resolves intent
- tracks state

Without EMS, the system degrades into loosely connected processors with no shared understanding of *what* is being processed or *why*.

## Responsibilities

EMS is responsible for **coordination and state**, not execution.

Specifically, EMS:

- Registers entities and assigns canonical identity
- Classifies entities (image, video, text, etc.)
- Owns and normalizes authoritative metadata
- Resolves applicable policies
- Resolves which workflow applies to an entity
- Issues workflow intent to downstream systems
- Tracks entity and workflow state over time
- Emits lifecycle and state-change events

EMS answers questions such as:

- What is this object?
- What policies apply?
- What workflow should run?
- What is the current state of this entity?
- Has processing completed, failed, or stalled?

EMS is the **source of truth** for entity state.

## What EMS Is Not

EMS is deliberately constrained. It does **not**:

- Process media or run compute-heavy tasks
- Store large binary files
- Expand workflow DAGs
- Perform routing or scheduling
- Select CPU/GPU tiers, regions, or placement
- Implement search, tagging, or indexing logic
- Render or own user interfaces

Those responsibilities belong to other services. If EMS begins to absorb them, it has failed its role.

## EMS and the Overall System

EMS is **not** the entire Data Management System, rather it is one service, the **decision layer**, *within* it. Its boundaries are intentional.

EMS sits between clients and execution systems:

```txt
[ API / UI Clients ]
          |
          v
[ Entity Management System (EMS) ]
          |
          v
[ Routing / Scheduling Middleware ]
          |
          v
[ Processing Microservices ]
```

From the outside, EMS may appear to *be* the system because everything flows through it. Internally, it is a **decision and state layer**, not a worker.

### EMS → Routing / Scheduling Middleware

EMS delegates tasks via **workflows**. The routing/scheduling middleware decides *how* and *where* the workflow runs.

- EMS determines *which* workflow applies
- EMS does **not** expand DAGs
- EMS does **not** schedule tasks
- EMS does **not** select compute resources

### EMS → API / UI Clients

EMS exposes authoritative state:

- entity identity and metadata
- workflow association
- lifecycle and status

Clients may initiate ingest or query status, but EMS remains the canonical source of truth.

### EMS ← Status Events

EMS consumes high-level status updates from downstream systems in order to:

- update entity and workflow state
- maintain a coherent lifecycle history

EMS does not interpret task-level results; it tracks aggregate state.

## Goals

The EMS is designed to:

- Provide a single, authoritative source of truth for entity identity and state
- Centralize decision-making while decentralizing execution
- Enforce clear separation of concerns across services
- Enable policy-driven, observable workflows
- Support replaceable UIs and independent processors
- Prevent the emergence of a monolithic or God service

## Non-Goals

EMS is not intended to be:

- A file system
- A processing engine
- A workflow executor
- A routing or scheduling engine
- A UI backend that "does everything"
- A dumping ground for convenience logic

These shortcuts lead to systems that cannot evolve.
