# Markdoc Configuration Test Document

This document tests all the custom Markdoc nodes and tags defined in the markdoc configuration.

# Code Components Tests

## CodeSnippet Tests (Self-Closing)

{% codeSnippet code="console.log('Hello, World!');" language="javascript" /%}

{% codeSnippet code="const greeting: string = 'Hello, TypeScript!';\nconsole.log(greeting);" language="typescript" title="TypeScript Example" /%}

{% codeSnippet code="def hello_world():\n    print('Hello, Python!')\n\nhello_world()" language="python" filename="hello.py" showLineNumbers=true /%}

{% codeSnippet code="<div className='container'>\n  <h1>Hello React!</h1>\n  <p>This is a JSX example</p>\n</div>" language="jsx" title="React Component" filename="HelloComponent.jsx" showLineNumbers=true copyable=true /%}

{% codeSnippet code="# Hello Bash\necho 'Setting up environment...'\nnpm install\nnpm run build" language="bash" title="Build Script" copyable=false /%}

{% codeSnippet code="{\n  \"name\": \"my-project\",\n  \"version\": \"1.0.0\",\n  \"scripts\": {\n    \"dev\": \"next dev\",\n    \"build\": \"next build\"\n  }\n}" language="json" filename="package.json" title="Package Configuration" showLineNumbers=true /%}

---

# Card Component Tests

## Basic Cards
{% column %}

{% card title="Basic Card" description="Default card with text icon" %}
This card uses all default attributes and should display properly.
{% /card %}

{% card title="Card with Image" description="Testing image attribute" image="/path/to/image.jpg" imageAlt="Custom alt text" %}
This card includes an image with custom alt text.
{% /card %}

{% /column %}

## Link Cards
{% column cols=2 gap="md" %}

{% card title="Internal Link Card" description="Card that links internally" href="/internal-page" %}
This card links to an internal page with default CTA text.
{% /card %}

{% card title="External Link Card" description="Card that links externally" href="https://example.com" external=true ctaText="Visit Site" %}
This card links to an external site with custom CTA text.
{% /card %}

{% card title="Card with Arrow" description="Shows arrow indicator" href="/somewhere" showArrow=true %}
This card displays an arrow indicator.
{% /card %}

{% card title="External with Arrow" description="External link with arrow" href="https://github.com" external=true showArrow=true ctaText="View on GitHub" %}
External link with both arrow and custom CTA.
{% /card %}

{% /column %}

## Horizontal Layout Cards
{% card title="Horizontal Card Layout" description="This card uses horizontal layout" horizontal=true %}
This card demonstrates the horizontal layout option where content flows horizontally instead of vertically.
{% /card %}

{% card title="Horizontal with Link" description="Horizontal card that's also a link" horizontal=true href="/horizontal-page" ctaText="Explore More" showArrow=true %}
This horizontal card also functions as a clickable link with arrow indicator.
{% /card %}

## Complex Card Variations
{% column cols=3 gap="sm" %}

{% card title="Full Featured Card" description="Card with all attributes" image="/hero.jpg" imageAlt="Hero image" icon="star" href="https://example.com" external=true ctaText="Learn More" showArrow=true %}
This card uses every available attribute to test full functionality.
{% /card %}

{% card title="Horizontal External" description="Horizontal external link" horizontal=true href="https://docs.example.com" external=true ctaText="Read Docs" %}
Horizontal card linking to external documentation.
{% /card %}

{% card title="Image with Internal Link" description="Image card with internal navigation" image="/thumbnail.png" href="/details" showArrow=true %}
Card with image that links internally and shows an arrow.
{% /card %}

{% /column %}

---

# Callouts
Preset definitions for callouts include: info, warning, error, success, tip, AND danger

{% callout title="Information Callout" type="info" %}
This is an info callout with blue styling
{% /callout %}

{% callout title="Warning Callout" type="warning" %}
This is a warning callout with yellow/orange styling
{% /callout %}

{% callout title="Error Callout" type="error" %}
This is an error callout with red styling
{% /callout %}

{% callout title="Success Callout" type="success" %}
This is a success callout with green styling
{% /callout %}

{% callout title="Tip Callout" type="tip" %}
This is a tip callout with helpful information
{% /callout %}

{% callout title="Danger Callout" type="danger" %}
This is a danger callout for critical warnings
{% /callout %}

{% callout title="Default Callout" %}
This callout has no type specified, should use default styling
{% /callout %}

---

## CodeGroup Tests

{% codeGroup %}
{% codeSnippet code="console.log('First snippet in group');" language="javascript" title="JavaScript Example" /%}
{% codeSnippet code="print('Second snippet in group')" language="python" title="Python Example" /%}
{% codeSnippet code="echo 'Third snippet in group'" language="bash" title="Bash Example" /%}
{% /codeGroup %}

{% codeGroup title="API Setup Examples" %}
{% codeSnippet code="// Express.js setup\nconst express = require('express');\nconst app = express();\n\napp.get('/api/users', (req, res) => {\n  res.json({ users: [] });\n});\n\napp.listen(3000);" language="javascript" filename="server.js" /%}
{% codeSnippet code="# FastAPI setup\nfrom fastapi import FastAPI\n\napp = FastAPI()\n\n@app.get('/api/users')\ndef get_users():\n    return {'users': []}\n\nif __name__ == '__main__':\n    import uvicorn\n    uvicorn.run(app, host='0.0.0.0', port=8000)" language="python" filename="main.py" /%}
{% codeSnippet code="// Next.js API route\nexport default function handler(req, res) {\n  if (req.method === 'GET') {\n    res.status(200).json({ users: [] });\n  } else {\n    res.setHeader('Allow', ['GET']);\n    res.status(405).end('Method Not Allowed');\n  }\n}" language="javascript" filename="pages/api/users.js" /%}
{% /codeGroup %}

{% codeGroup title="Database Schemas" showLineNumbers=true %}
{% codeSnippet code="-- PostgreSQL Schema\nCREATE TABLE users (\n  id SERIAL PRIMARY KEY,\n  email VARCHAR(255) UNIQUE NOT NULL,\n  name VARCHAR(100) NOT NULL,\n  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP\n);\n\nCREATE TABLE posts (\n  id SERIAL PRIMARY KEY,\n  title VARCHAR(200) NOT NULL,\n  content TEXT,\n  user_id INTEGER REFERENCES users(id),\n  published BOOLEAN DEFAULT false,\n  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP\n);" language="sql" filename="schema.sql" /%}
{% codeSnippet code="// Prisma Schema\nmodel User {\n  id        Int      @id @default(autoincrement())\n  email     String   @unique\n  name      String\n  posts     Post[]\n  createdAt DateTime @default(now())\n\n  @@map(\"users\")\n}\n\nmodel Post {\n  id        Int      @id @default(autoincrement())\n  title     String\n  content   String?\n  published Boolean  @default(false)\n  author    User     @relation(fields: [authorId], references: [id])\n  authorId  Int\n  createdAt DateTime @default(now())\n\n  @@map(\"posts\")\n}" language="prisma" filename="schema.prisma" /%}
{% codeSnippet code="// MongoDB Schema (Mongoose)\nconst mongoose = require('mongoose');\n\nconst userSchema = new mongoose.Schema({\n  email: {\n    type: String,\n    required: true,\n    unique: true\n  },\n  name: {\n    type: String,\n    required: true\n  },\n  createdAt: {\n    type: Date,\n    default: Date.now\n  }\n});\n\nconst postSchema = new mongoose.Schema({\n  title: {\n    type: String,\n    required: true\n  },\n  content: String,\n  published: {\n    type: Boolean,\n    default: false\n  },\n  author: {\n    type: mongoose.Schema.Types.ObjectId,\n    ref: 'User',\n    required: true\n  },\n  createdAt: {\n    type: Date,\n    default: Date.now\n  }\n});\n\nmodule.exports = {\n  User: mongoose.model('User', userSchema),\n  Post: mongoose.model('Post', postSchema)\n};" language="javascript" filename="models.js" /%}
{% /codeGroup %}

{% codeGroup title="Testing Examples" %}
{% codeSnippet code="// Jest test\nconst { add } = require('./math');\n\ndescribe('Math functions', () => {\n  test('should add two numbers correctly', () => {\n    expect(add(2, 3)).toBe(5);\n    expect(add(-1, 1)).toBe(0);\n    expect(add(0, 0)).toBe(0);\n  });\n\n  test('should handle decimal numbers', () => {\n    expect(add(0.1, 0.2)).toBeCloseTo(0.3);\n  });\n});" language="javascript" filename="math.test.js" copyable=true /%}
{% codeSnippet code="# pytest test\nimport pytest\nfrom math_utils import add\n\nclass TestMathFunctions:\n    def test_add_positive_numbers(self):\n        assert add(2, 3) == 5\n        \n    def test_add_negative_numbers(self):\n        assert add(-1, 1) == 0\n        \n    def test_add_zero(self):\n        assert add(0, 0) == 0\n        \n    def test_add_decimals(self):\n        result = add(0.1, 0.2)\n        assert abs(result - 0.3) < 1e-10" language="python" filename="test_math.py" /%}
{% /codeGroup %}

---

# Accordion Components

{% accordion title="Basic Accordion" description="This is a basic accordion" %}
This accordion starts closed by default. It contains paragraph content that should be collapsible.

You can put any content inside accordions including lists:
- Item 1
- Item 2
- Item 3
{% /accordion %}

{% accordion title="Open by Default" description="This accordion starts open" defaultOpen=true %}
This accordion starts in the open state because defaultOpen is set to true.

## Heading inside accordion
Accordions can contain headings and other rich content.

```javascript
// Even code blocks work
const example = "code in accordion";
```
{% /accordion %}

{% accordion title="Accordion with Icon" description="Testing icon attribute" icon="star" %}
This accordion has an icon specified. The icon handling might need to be implemented similar to cards.
{% /accordion %}

{% accordion title="Minimal Accordion" %}
This accordion only has a title, using defaults for other attributes.
{% /accordion %}

---

# Break Components

This is content before a default break.

{% break %}

This content comes after a level 3 break (default).

{% break level=1 %}

This content comes after a level 1 break (should be minimal spacing).

{% break level=5 %}

This content comes after a level 5 break (should be maximum spacing).

---

# Complex Nested Examples

{% column cols=2 gap="md" %}

{% accordion title="Accordion in Column" description="Testing nested components" %}
This accordion is inside a column layout.

{% callout title="Nested Callout" type="success" %}
This callout is nested inside an accordion which is inside a column.
{% /callout %}

{% codeGroup title="Code Group in Accordion" %}
{% codeSnippet code="// First nested snippet\nfunction example1() {\n  return 'Code in accordion in column!';\n}" language="javascript" title="JavaScript" /%}
{% codeSnippet code="# Second nested snippet\ndef example2():\n    return 'Python in accordion too!'" language="python" title="Python" /%}
{% /codeGroup %}

More content in the accordion.
{% /accordion %}

{% card title="Interactive Card in Column" description="Card with link in column layout" href="/learn-more" showArrow=true ctaText="Discover" %}
This card is in the same column as the accordion above and includes a link.

## Heading in Card
Cards support rich content and can be interactive.

{% break level=2 %}

Content after a break inside the card.
{% /card %}

{% /column %}

{% break level=4 %}

## All Callout Types in Columns

{% column cols=2 gap="sm" %}

{% callout title="Info in Column" type="info" %}
Info callout in left column
{% /callout %}

{% callout title="Warning in Column" type="warning" %}
Warning callout in right column
{% /callout %}

{% callout title="Error in Column" type="error" %}
Error callout in left column
{% /callout %}

{% callout title="Success in Column" type="success" %}
Success callout in right column
{% /callout %}

{% callout title="Tip in Column" type="tip" %}
Tip callout in left column
{% /callout %}

{% callout title="Danger in Column" type="danger" %}
Danger callout in right column
{% /callout %}

{% /column %}

---

# Final Comprehensive Test

{% column cols=1 %}

{% card title="Everything Combined" description="Testing all features together" horizontal=true href="/complete-guide" external=false ctaText="View Full Guide" showArrow=true %}

## Card Content with Everything

{% accordion title="Accordion Inside Card" defaultOpen=true %}
This tests accordion inside card functionality with the new horizontal layout.

{% callout title="Triple Nested!" type="tip" %}
Callout inside accordion inside card inside column! This card also has href, ctaText, showArrow, and horizontal attributes.
{% /callout %}
{% /accordion %}

{% break level=3 %}

More card content after the accordion and break.

{% /card %}

{% /column %}

## Test Summary

This document tests:
- ✅ **Paragraph nodes** (custom Paragraph component)
- ✅ **Heading nodes** (all levels with Heading component)  
- ✅ **Callout tags** (all 6 types: info, warning, error, success, tip, danger)
- ✅ **Card tags** (all attributes: title, description, image, imageAlt, icon, href, ctaText, showArrow, external, horizontal)
- ✅ **Break tags** (levels 1, 3, 5)
- ✅ **Column tags** (1, 2, 3 columns with different gaps)
- ✅ **Accordion tags** (default closed, default open, with icons)
- ✅ **CodeSnippet tags** (all attributes: code, language, filename, title, showLineNumbers, copyable)
- ✅ **CodeGroup tags** (container for multiple codeSnippets, title, showLineNumbers)
- ✅ **Card link functionality** (internal links, external links, CTA text, arrows)
- ✅ **Card layout options** (horizontal vs vertical layouts)
- ✅ **Code component variations** (different languages, with/without line numbers, copy functionality)
- ✅ **Code organization patterns** (groups vs individual snippets)
- ✅ **Complex nesting** (accordions in cards in columns, codeGroups in accordions)
- ✅ **All attribute combinations** (defaults and custom values)