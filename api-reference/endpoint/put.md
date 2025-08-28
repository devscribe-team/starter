---
title: Update Document
theme: dark
description: Updates an existing document in your Devscribe workspace
openapi: PUT https://api.devscribe.com/v1/documents/{id}
---

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | Document identifier (path parameter) |

## Example Request

```bash
curl -X PUT "https://api.devscribe.com/v1/documents/doc_01HZXYABCD" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Authentication",
    "tags": ["auth", "security"]
  }'
```

## Example Response

```json
{
  "data": {
    "id": "doc_01HZXYABCD",
    "title": "Authentication",
    "slug": "authentication",
    "project_id": "site-docs",
    "tags": ["auth", "security"],
    "created_at": "2024-01-15T10:30:00Z",
    "updated_at": "2024-02-01T09:00:00Z"
  },
  "success": true
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique document identifier |
| `title` | string | Document title |
| `slug` | string | URL-friendly identifier |
| `project_id` | string | Project the document belongs to |
| `tags` | array[string] | Tags associated with the document |
| `created_at` | string | ISO 8601 timestamp of creation |
| `updated_at` | string | ISO 8601 timestamp of last update | 