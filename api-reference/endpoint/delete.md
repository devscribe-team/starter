---
title: Delete Document 
description: Deletes a document from your Devscribe workspace
openapi: DELETE /plants/{id}
---

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | Document identifier (path parameter) |

## Example Request

```bash
curl -X DELETE "https://api.devscribe.com/v1/documents/doc_01HZXYABCD" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## Example Response

```json
{
  "deleted_id": "doc_01HZXYABCD",
  "success": true
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `deleted_id` | string | Identifier of the deleted document |
| `success` | boolean | Whether the deletion was successful | 