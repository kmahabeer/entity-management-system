---
layout: page
title: Entity Management API
permalink: /api/entities/
---

# Entity Management API

Endpoints for registering, retrieving, and managing entities.

## Register Entity

Register a new entity and assign canonical identity.

**Endpoint:** `POST /entities`

**Request Body:**

```json
{
  "type": "file",
  "metadata": {
    "filename": "document.pdf",
    "size": 1024,
    "mime_type": "application/pdf"
  },
  "source": "upload"
}
```

**Response:**

```json
{
  "data": {
    "id": "ent_123456",
    "type": "file",
    "status": "registered",
    "created_at": "2026-01-06T00:00:00Z"
  }
}
```

## Get Entity

Retrieve entity details and current status.

**Endpoint:** `GET /entities/{id}`

**Response:**

```json
{
  "data": {
    "id": "ent_123456",
    "type": "file",
    "status": "processing",
    "metadata": {
      "filename": "document.pdf",
      "size": 1024,
      "mime_type": "application/pdf"
    },
    "workflow_id": "wf_789",
    "created_at": "2026-01-06T00:00:00Z",
    "updated_at": "2026-01-06T00:05:00Z"
  }
}
```

## Update Entity

Update entity metadata.

**Endpoint:** `PUT /entities/{id}`

**Request Body:**

```json
{
  "metadata": {
    "tags": ["important", "review"]
  }
}
```

## Get Entity Status

Get current processing status.

**Endpoint:** `GET /entities/{id}/status`

**Response:**

```json
{
  "data": {
    "entity_id": "ent_123456",
    "status": "completed",
    "workflow_status": "success",
    "last_updated": "2026-01-06T00:10:00Z"
  }
}
```

## List Entities

Query entities with filtering.

**Endpoint:** `GET /entities`

**Query Parameters:**

- `type` - Filter by entity type
- `status` - Filter by status
- `limit` - Maximum results (default: 50)
- `offset` - Pagination offset

**Response:**

```json
{
  "data": [
    {
      "id": "ent_123456",
      "type": "file",
      "status": "completed"
    }
  ],
  "pagination": {
    "total": 100,
    "limit": 50,
    "offset": 0
  }
}
