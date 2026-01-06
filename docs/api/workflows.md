---
layout: page
title: Workflow Management API
permalink: /api/workflows/
---

# Workflow Management API

Endpoints for issuing workflow intents and tracking workflow status.

## Issue Workflow Intent

Trigger workflow execution for an entity.

**Endpoint:** `POST /workflows`

**Request Body:**

```json
{
  "entity_id": "ent_123456",
  "workflow_type": "document_processing",
  "priority": "normal"
}
```

**Response:**

```json
{
  "data": {
    "id": "wf_789",
    "entity_id": "ent_123456",
    "status": "queued",
    "created_at": "2026-01-06T00:00:00Z"
  }
}
```

## Get Workflow Status

Retrieve workflow execution status.

**Endpoint:** `GET /workflows/{id}`

**Response:**

```json
{
  "data": {
    "id": "wf_789",
    "entity_id": "ent_123456",
    "status": "running",
    "progress": 0.75,
    "tasks_completed": 3,
    "total_tasks": 4,
    "started_at": "2026-01-06T00:01:00Z",
    "estimated_completion": "2026-01-06T00:15:00Z"
  }
}
```

## List Workflows

Query workflows with filtering.

**Endpoint:** `GET /workflows`

**Query Parameters:**

- `entity_id` - Filter by entity
- `status` - Filter by status (queued, running, completed, failed)
- `limit` - Maximum results
- `offset` - Pagination offset

## Cancel Workflow

Cancel a running workflow.

**Endpoint:** `DELETE /workflows/{id}`

**Response:**

```json
{
  "data": {
    "id": "wf_789",
    "status": "cancelled"
  }
}
```

## Workflow Types

Supported workflow types:

- `document_processing` - Text extraction, indexing
- `media_analysis` - Video/image analysis
- `quality_check` - Validation and QA
- `archival` - Long-term storage preparation
