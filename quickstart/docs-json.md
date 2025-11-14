---
title: docs.json Guide
description: How to configure navigation, tabs, groups, and pages with docs.json
icon: navigation
---

## What is it?

`docs.json` is the single source of truth for your documentation navigation. It defines tabs, groups, and the ordered list of pages that appear in the sidebar, and it powers previous/next navigation.

- Location: `src/app/(pages)/docs.json`
- Used by: navigation, left sidebar, previous/next links, and page metadata helpers

## File structure

```json
{
  "name": "your-site-name",
  "favicon": "/favicon.svg",
  "navigation": {
    "tabs": [
      {
        "tab": "Guides",
        "groups": [
          {
            "group": "Get Started",
            "pages": [
              "introduction",
              "quickstart/guide"
            ]
          }
        ]
      },
      {
        "tab": "API Reference",
        "groups": [
          {
            "group": "Endpoints",
            "pages": [
              "api-reference/endpoint/get",
              "api-reference/endpoint/post"
            ]
          }
        ]
      }
    ],
    "global": {
      "anchors": [
        { "anchor": "Community", "href": "https://example.com/community", "icon": "slack" }
      ]
    }
  }
}
```

### Top‑level fields

- `name`: Site identifier used in a few places (branding/logging).
- `favicon`: Path to the favicon under `public/`.
- `navigation.tabs[]`: Primary navigation areas in the left sidebar.
- `navigation.global.anchors[]`: Optional external links rendered globally (e.g., footer or header menus), each with `anchor`, `href`, and `icon`.

### Tabs and groups

- `tab`: The visible tab label in the sidebar (for example, "Guides", "API Reference").
- `groups[]`: Buckets within a tab. Each group has a `group` label and a `pages` array.

### Pages

- Each entry is a page path (without `.mdx`) relative to `src/app/(pages)`.
- The order of this array determines:
  - Left sidebar ordering
  - Previous/Next navigation (computed from this order)
- The file must exist as `src/app/(pages)/<page>.mdx`.
- Titles come from the page frontmatter (`title:`). If omitted, a title is derived from the filename.

## Adding a new page to `docs.json`

1. Create a markdown file under `src/app/(pages)` (e.g., `src/app/(pages)/quickstart/my-page.mdx`).
2. Add frontmatter at the top:

```md
---
title: My Awesome Page
description: Short description shown below the title
---
```

3. Add the page path (without `.mdx`) to the appropriate `pages` array in `docs.json`:

```json
{
  "tab": "Guides",
  "groups": [
    {
      "group": "Quickstart",
      "pages": [
        "quickstart/guide",
        "quickstart/my-page"
      ]
    }
  ]
}
```

## API endpoint pages (optional)

If a page represents an API endpoint, include one of the following in the frontmatter:

- `openapi: "GET /documents"` (preferred)
- `api: "GET /documents"`

This enables API‑aware UI (method badge, try‑it button, request/response details) and determines HTTP method visualization throughout the navigation. The method color mapping is handled internally.

## Icons (optional)

You can set a page icon via page frontmatter:

```md
---
title: My Page
icon: code
---
```

Icon names map to built‑in icons. See `src/lib/sidebar-utils.ts` for the available keys (e.g., `code`, `book`, `file-text`, `slack`, etc.).

## Global anchors (optional)

Add external links under `navigation.global.anchors`:

```json
{
  "navigation": {
    "global": {
      "anchors": [
        { "anchor": "Community", "href": "https://example.com/community", "icon": "slack" },
        { "anchor": "Status", "href": "https://status.example.com", "icon": "shield" }
      ]
    }
  }
}
```

## Common pitfalls

- The `pages` path must match the markdown path without the `.mdx` extension.
- Ordering in `pages` controls Previous/Next; if navigation feels wrong, check order.
- Titles missing in frontmatter will be auto‑generated from filenames (may not look polished).
- Invalid `icon` names won’t render; use keys defined in `src/lib/sidebar-utils.ts`.
- If you add a page but don’t see it, ensure both the file exists and `docs.json` is updated.

## Full example

```json
{
  "name": "devscribe",
  "favicon": "/favicon.svg",
  "navigation": {
    "tabs": [
      {
        "tab": "Guides",
        "groups": [
          {
            "group": "Get Started",
            "pages": ["introduction"]
          },
          {
            "group": "Quickstart",
            "pages": [
              "quickstart/guide",
              "quickstart/docs-json"
            ]
          }
        ]
      },
      {
        "tab": "API Reference",
        "groups": [
          {
            "group": "Endpoints",
            "pages": [
              "api-reference/endpoint/get",
              "api-reference/endpoint/post",
              "api-reference/endpoint/delete",
              "api-reference/endpoint/put"
            ]
          }
        ]
      }
    ],
    "global": {
      "anchors": [
        { "anchor": "Community", "href": "https://mintlify.com/community", "icon": "slack" }
      ]
    }
  }
}
```

You’re set—edit `docs.json` to reorganize your docs without touching page code. Changes take effect on the next build/dev reload.


