---
layout: page
title: Architecture
permalink: /architecture/
---

# System Architecture

## High-Level Overview

The Entity Management System (EMS) serves as the decision and state layer within a larger Data Management System (DMS). It coordinates entity lifecycles while delegating execution to downstream systems.

## System Components

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

### API / UI Clients

External interfaces that interact with EMS:

- RESTful APIs for programmatic access
- Web UIs for human operators
- Integration points for other DMS services

Responsibilities:

- Initiate entity ingestion
- Query entity status and metadata
- Trigger workflow execution

### Entity Management System (EMS)

The core orchestration service:

**Core Functions:**

- Entity registration and identity assignment
- Metadata normalization and storage
- Policy resolution
- Workflow association
- State tracking and event emission

**Data Storage:**

- Entity registry with canonical identities
- Metadata store for normalized attributes
- State machine for lifecycle tracking
- Event log for audit and monitoring

**Key Constraints:**

- No direct execution of processing tasks
- No storage of large binary files
- Stateless decision-making layer

### Routing / Scheduling Middleware

Handles workflow execution coordination:

**Functions:**

- Workflow DAG expansion
- Task scheduling and resource allocation
- Compute resource selection (CPU/GPU, regions)
- Load balancing and failover

**Integration with EMS:**

- Receives workflow intent from EMS
- Reports execution status back to EMS
- Handles retry logic and error recovery

### Processing Microservices

Specialized execution engines:

**Examples:**

- Media processing services (video, image, audio)
- Text analysis and indexing
- File format conversion
- Quality assurance and validation

**Characteristics:**

- Independent scaling and deployment
- Domain-specific optimizations
- Event-driven communication

## Data Flow

1. **Entity Ingestion**
   - Client submits entity to EMS
   - EMS assigns canonical ID and classifies entity
   - EMS resolves applicable policies and workflow
   - EMS emits workflow intent to middleware

2. **Workflow Execution**
   - Middleware schedules tasks across microservices
   - Microservices process entity and emit status events
   - Middleware aggregates status and reports to EMS

3. **State Tracking**
   - EMS updates entity state based on events
   - Clients can query current state at any time
   - EMS maintains authoritative state history

## Design Principles

### Separation of Concerns

- **EMS**: Decisions and state
- **Middleware**: Coordination and scheduling
- **Microservices**: Execution

### Event-Driven Architecture

- Asynchronous communication between components
- Event sourcing for state reconstruction
- Loose coupling for independent evolution

### Scalability Considerations

- EMS as lightweight decision layer
- Horizontal scaling of processing components
- Caching and optimization for metadata queries

### Reliability

- Idempotent operations
- Eventual consistency for state updates
- Comprehensive logging and monitoring
