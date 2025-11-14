---
title: Update Document
description: Updates an existing document in your Devscribe workspace
api: PUT /documents
num: 2
---

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | Document identifier (path parameter) |

<CodeGroup>
  <CodeSnippet language="bash" title="cURL">
  {`curl -X PUT "https://api.devscribe.com/v1/documents/doc_01TESTGROUP" \\
  -H "Authorization: Bearer YOUR_API_KEY" \\
  -H "Content-Type: application/json" \\
  -d '{
    "title": "From CodeGroup",
    "tags": ["group", "test"]
  }'`}
  </CodeSnippet>

  <CodeSnippet language="javascript" title="JavaScript">
  {`await fetch("https://api.devscribe.com/v1/documents/doc_01TESTGROUP", {
    method: "PUT",
    headers: {
      Authorization: "Bearer YOUR_API_KEY",
      "Content-Type": "application/json",
    },
    body: JSON.stringify({ title: "From CodeGroup", tags: ["group", "test"] }),
  });`}
  </CodeSnippet>
</CodeGroup>

```bash
curl -X PUT "https://api.devscribe.com/v1/documents/doc_01HZXYABCD" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Authentication",
    "tags": ["auth", "security"]
  }'
```

<CodeGroup>
  <CodeSnippet language="python" title="Python">
  {`import requests

url = "https://api.devscribe.com/v1/documents/doc_01TESTGROUP2"
headers = {
    "Authorization": "Bearer YOUR_API_KEY",
    "Content-Type": "application/json",
}
payload = {"title": "From Second Group", "tags": ["group2", "test"]}
requests.put(url, json=payload, headers=headers)`}
  </CodeSnippet>

  <CodeSnippet language="bash" title="cURL">
  {`curl -X PUT "https://api.devscribe.com/v1/documents/doc_01TESTGROUP2" \\
  -H "Authorization: Bearer YOUR_API_KEY" \\
  -H "Content-Type: application/json" \\
  -d '{
    "title": "From Second Group",
    "tags": ["group2", "test"]
  }'`}
  </CodeSnippet>
</CodeGroup>

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