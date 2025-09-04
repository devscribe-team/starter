---
title: Get Plants
description: Retrieve a list of documents in your Devscribe workspace
openapi: GET /plants
---

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `limit` | integer | Number of documents to return (default: 20, max: 100) |
| `offset` | integer | Number of documents to skip (default: 0) |
| `project_id` | string | Filter by project identifier |
| `tag` | string | Filter by tag |

## Example Request

```bash
curl -X GET "https://api.devscribe.com/v1/documents?limit=10&project_id=site-docs" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## Example Response

```json
{
  "data": [
    {
      "id": "doc_01HZXYABCD",
      "title": "Getting Started",
      "slug": "getting-started",
      "project_id": "site-docs",
      "tags": ["guide", "intro"],
      "created_at": "2024-01-15T10:30:00Z",
      "updated_at": "2024-02-01T09:00:00Z"
    },
    {
      "id": "doc_01HZXYEFGH",
      "title": "Authentication",
      "slug": "authentication",
      "project_id": "site-docs",
      "tags": ["auth"],
      "created_at": "2024-01-14T09:15:00Z",
      "updated_at": "2024-01-20T12:45:00Z"
    }
  ],
  "pagination": {
    "total": 25,
    "limit": 10,
    "offset": 0,
    "has_more": true
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