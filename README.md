# README

The **Entity Management System (EMS)** is a decision and state orchestration service that defines entity identity, resolves applicable workflows, and tracks lifecycle state while delegating all execution, routing, and compute to downstream systems.

## Overview

The Entity Management System (EMS) is an **orchestration service**. It defines, tracks, and coordinates the lifecycle of entities within a larger Data Management System (DMS).

An *entity* is any canonical object the DMS cares about: a file, media asset, document, reference, or derived artifact. EMS exists to make authoritative decisions about entities while delegating all execution to downstream systems. It is the DMS’s **spine**.

EMS decides:

- what something is
- what should happen to it
- what its current state is

## Purpose

### What EMS Is

EMS is responsible for **coordination and state**, not execution.

Specifically, EMS:

- Registers entities and assigns canonical identity
- Classifies entities (image, video, text, etc.)
- Owns and normalizes authoritative metadata
- Resolves policies and workflows
- Enqueues work to downstream systems
- Tracks workflow and entity state over time
- Emits lifecycle events

EMS answers questions such as:

- What is this object?
- What policies apply?
- What workflow should run?
- Has processing completed, failed, or stalled?

EMS is the **source of truth** for entity state.

### What EMS Is Not

EMS is deliberately constrained. It does **not**:

- Process media or run compute-heavy tasks
- Store large binary files
- Render or own user interfaces
- Perform scheduling or compute placement
- Implement search, tagging, or indexing logic

Those responsibilities belong to other services. If EMS begins to absorb them, it has failed its role.

## System Placement

EMS is **not** the entire Data Management System. It is one service within it.

The broader system includes:

- User interfaces
- Storage systems
- Routing and scheduling middleware
- Processing microservices (e.g., Tag Management, Multimedia Processing)
- Search, authentication, infrastructure, and operations

EMS coordinates these components but does not replace them.

If EMS were removed, the system would lose coherence.

If EMS were run alone, nothing would be processed.

EMS sits between clients and execution systems:

```txt
[ UI / Clients ]
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

From the outside, EMS may appear to *be* the system because everything flows through it. Internally, it is a **decision layer**, not a worker.

It centralizes decisions while decentralizing execution. This enables:

- Replaceable UIs
- Independent processors
- Observable workflows
- Policy-driven behavior
- Future service extraction without rewrites

## Goals

The EMS is designed to:

- Provide a single, authoritative source of truth for entity identity and state
- Centralize decision-making while decentralizing execution
- Enable clear separation of concerns across services
- Support policy-driven, observable workflows
- Allow independent evolution of UIs and processing services
- Prevent the emergence of a monolithic or God service

### Non-Goals

EMS is not intended to be:

- A file system
- A processing engine
- A UI backend that “does everything”
- A dumping ground for convenience logic

These shortcuts lead to systems that cannot evolve.

## License

Private, evolving project. Licensing to be determined if components are released publicly.
