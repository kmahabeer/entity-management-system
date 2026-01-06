---
layout: page
title: API Documentation
permalink: /api/
---

# API Documentation

The Entity Management System provides a RESTful API for managing entities, workflows, and policies.

## Base URL

```bash
https://api.ems.example.com/v1
```

## Authentication

API requests require authentication via JWT tokens. Include the token in the Authorization header:

```bash
Authorization: Bearer <jwt-token>
```

## Response Format

All responses are in JSON format. Successful responses include a `data` field, errors include an `error` field.

## Endpoints

### Entities

- [Entity Management](entities) - Register, retrieve, and update entities

### Workflows

- [Workflow Management](workflows) - Issue workflow intents and track status

### Policies

- [Policy Management](policies) - Query applicable policies

## Error Handling

Standard HTTP status codes are used:

- `200` - Success
- `400` - Bad Request
- `401` - Unauthorized
- `404` - Not Found
- `500` - Internal Server Error

Error responses include:

```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "Entity ID is required"
  }
}
```

## Rate Limiting

API requests are rate limited. Exceeding limits returns `429 Too Many Requests`.

## Versioning

The API uses URL versioning. The current version is `v1`.
