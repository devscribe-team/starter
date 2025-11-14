---
title: openapi.json Guide
description: How to wire your OpenAPI spec into the docs
icon: file-text
---

## What is it?

`openapi.json` is an optional OpenAPI 3.x spec the site reads to auto‑generate rich API docs for an endpoint page. When present and referenced by a page’s frontmatter, it powers:

- Method badge and route display
- Request auth, path/query params, and request body fields
- Response schemas per status, plus example payloads
- A cURL request prefilled from your spec (server URL, params, auth, body)

Location: `src/app/(pages)/openapi.json`

Version: OpenAPI 3.x (typical fields — `info`, `servers`, `paths`, `components.securitySchemes`, etc.)

## Enabling it on a page

In your endpoint markdown (e.g., `api-reference/endpoint/put.mdx`), add frontmatter like:

```md
---
title: Update Document
description: Updates an existing document
openapi: "PUT /documents"  # METHOD + route must match your spec
---
```

How matching works:

- The system reads `src/app/(pages)/openapi.json` at build time.
- It matches the page’s `openapi` frontmatter to `paths["/documents"].put` in the spec.

If there’s no match or the spec is missing, the page gracefully falls back and logs a warning to the server console.

## What the UI pulls from your spec

- Servers: Uses `servers[0].url` to build the cURL `--url` (e.g., `https://api.example.com`).
- Security: From operation `security` or global `security`. Supports common patterns:
  - HTTP bearer (`Authorization: Bearer <token>`) when `type: http`, `scheme: bearer`
  - API key in `header`, `query`, or `cookie` (e.g., `X-API-Key: <apiKey>`)
  - For other schemes (oauth2/openId), cURL falls back to a bearer header placeholder.
- Parameters: Path/query/header params rendered with names, types, and `required` flags. Path params are substituted in cURL as placeholders like `<id>`.
- Request body: Reads `requestBody.content[<contentType>].schema` and shows a field list plus a generated example based on JSON Schema (handles `$ref`, `allOf`, objects/arrays).
- Responses: For each `responses[status].content`, renders a field list (object/array) and an example payload.

Supported request content types with special handling:

- `application/json`: Adds `--header 'Content-Type: application/json'` and a JSON body example.
- `application/x-www-form-urlencoded`: Encodes each property with `--data-urlencode`.
- `multipart/form-data`: Adds `--header 'Content-Type: multipart/form-data'` and `-F 'field=<value>'` entries.

## Fallbacks and alternatives

You don’t have to use `openapi.json`. You have two alternatives:

1. Lightweight API mode using `api` frontmatter

    ```md
    ---
    title: Update Document
    description: Updates an existing document
    api: "PUT /documents"
    ---
    ```

    - Shows a minimal method+route header and a cURL with basic placeholders.
    - Does not parse parameters, bodies, or responses from a spec.

2. Plain page (no `openapi` or `api` in frontmatter)

    - Renders your markdown as written. Ideal for conceptual docs or tutorials.

## Tips for a good spec

- Include a `servers` array with your production base URL for correct cURL output.
- Define `components.securitySchemes` clearly. The UI auto‑detects bearer/apiKey details.
- Use `$ref` and `allOf` to compose schemas; the renderer resolves these for field lists and examples.
- Provide response schemas for your typical success and error codes (e.g., `200`, `400`, `401`).

## Example: minimal `openapi.json`

```json
{
  "openapi": "3.0.3",
  "info": { "title": "My API", "version": "1.0.0" },
  "servers": [{ "url": "https://api.example.com/v1" }],
  "paths": {
    "/documents": {
      "put": {
        "description": "Update a document",
        "security": [{ "bearerAuth": [] }],
        "parameters": [
          { "name": "id", "in": "path", "required": true, "schema": { "type": "string" } },
          { "name": "draft", "in": "query", "schema": { "type": "boolean" } }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "title": { "type": "string" },
                  "tags": { "type": "array", "items": { "type": "string" } }
                },
                "required": ["title"]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": { "type": "string" },
                    "title": { "type": "string" }
                  },
                  "required": ["id", "title"]
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "securitySchemes": {
      "bearerAuth": { "type": "http", "scheme": "bearer", "bearerFormat": "JWT" }
    }
  }
}
```

## Where the data flows

- The page reads frontmatter `openapi` (or `api`).
- If `openapi` is present, it loads `src/app/(pages)/openapi.json` and matches the method+route.
- It renders endpoint details, parameters, request body fields, responses, auth, and example cURL.
- If `api` is present instead, it renders a smaller API header and cURL only.

## Code examples in the sidebar

- For pages using `openapi:`
  - The sidebar is generated from the spec: cURL request and response example blocks per status code.
  - Any code fences or code groups in your markdown remain in the main content.
  - The `num` frontmatter is ignored for `openapi` pages.

- For pages using `api:` (lightweight mode)
  - You can control how many code items (code groups and/or code fences) are moved to the right sidebar using `num`.
  - The first N code items by source order go to the sidebar; the rest remain in the main content.
  - Code groups (`<CodeGroup>...</CodeGroup>`) count as one item.

```md
---
api: "PUT /documents"
num: 2
---
```

## When to choose which

- Use `openapi.json` when you want accurate, always‑up‑to‑date request/response and parameter rendering from a single source of truth.
- Use `api:` when you just need a quick method+route+cURL without maintaining a full spec.
- Use neither for conceptual docs that don’t describe a single HTTP endpoint.


