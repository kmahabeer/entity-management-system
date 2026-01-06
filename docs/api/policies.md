---
layout: page
title: Policy Management API
permalink: /api/policies/
---

# Policy Management API

Endpoints for querying applicable policies for entities.

## List Policies

Get all available policies.

**Endpoint:** `GET /policies`

**Response:**

```json
{
  "data": [
    {
      "id": "pol_001",
      "name": "retention_policy",
      "description": "Data retention requirements",
      "rules": [
        {
          "condition": "entity.type == 'document'",
          "action": "retain_for_7_years"
        }
      ]
    }
  ]
}
```

## Get Applicable Policies

Get policies that apply to a specific entity.

**Endpoint:** `GET /policies/applicable`

**Query Parameters:**

- `entity_id` - The entity to check policies for

**Response:**

```json
{
  "data": [
    {
      "policy_id": "pol_001",
      "applies": true,
      "reason": "Entity type matches document retention rule"
    }
  ]
}
```

## Evaluate Policy

Test a policy against entity metadata.

**Endpoint:** `POST /policies/evaluate`

**Request Body:**

```json
{
  "policy_id": "pol_001",
  "entity_metadata": {
    "type": "document",
    "classification": "confidential"
  }
}
```

**Response:**

```json
{
  "data": {
    "policy_id": "pol_001",
    "result": true,
    "matched_rules": ["retention_policy"]
  }
}
