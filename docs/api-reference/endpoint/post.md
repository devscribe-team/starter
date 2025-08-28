---
title: Create Document
theme: dark
description: Creates a new document in your Devscribe workspace
openapi: POST https://api.devscribe.com/v1/documents
---

## Body Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `title` | string | Title of the document |
| `content` | string | Markdown content of the document |
| `tags` | array[string] | Optional tags for organization |
| `project_id` | string | Project to associate the document with |

## Example Request

```bash
curl -X POST "https://api.devscribe.com/v1/documents" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Changelog",
    "content": "# Changelog\n\n- Initial release",
    "tags": ["release", "changelog"],
    "project_id": "site-docs"
  }'
```

## Example Response

```json
{
  "data": {
    "id": "doc_01HZXYJKL",
    "title": "Changelog",
    "slug": "changelog",
    "project_id": "site-docs",
    "tags": ["release", "changelog"],
    "created_at": "2024-01-15T10:30:00Z",
    "updated_at": "2024-01-15T10:30:00Z"
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