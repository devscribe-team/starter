# Markdoc Configuration Test Document

This document tests all the custom Markdoc nodes and tags defined in the markdoc configuration.

# Code Fence Tests (fence nodes render as CodeSnippet)

## Basic Code Fence Examples

```javascript
console.log('Hello, World!');
```

```typescript {% title="TypeScript Example" %}
const greeting: string = 'Hello, TypeScript!';
console.log(greeting);
```

```python {% filename="hello.py" showLineNumbers=true %}
def hello_world():
    print('Hello, Python!')

hello_world()
```

```jsx {% title="React Component" filename="HelloComponent.jsx" showLineNumbers=true %}
<div className='container'>
  <h1>Hello React!</h1>
  <p>This is a JSX example</p>
</div>
```

```bash {% title="Build Script" icon="terminal" %}
# Hello Bash
echo 'Setting up environment...'
npm install
npm run build
```

```json {% filename="package.json" title="Package Configuration" showLineNumbers=true %}
{
  "name": "my-project",
  "version": "1.0.0",
  "scripts": {
    "dev": "next dev",
    "build": "next build"
  }
}
```

## Code Fences with New Attributes

```javascript {% title="Code with Icon" icon="code" info="This shows the new icon attribute" %}
function greet(name) {
  return `Hello, ${name}!`;
}
```

```python {% content="Database Connection" info="Example showing content and info attributes" %}
import psycopg2

def connect_to_db():
    conn = psycopg2.connect(
        host="localhost",
        database="myapp",
        user="user",
        password="password"
    )
    return conn
```

## Line Highlighting Examples

```javascript {% title="Highlight Single Lines" showLineNumbers=true highlight="3,8,15" %}
function createUser(userData) {
  // Validate input data
  if (!userData.email) {
    throw new Error('Email is required');
  }
  
  // Create user object
  const user = {
    id: generateId(),
    email: userData.email,
    name: userData.name || 'Anonymous',
    createdAt: new Date()
  };
  
  // Save to database
  return database.save(user);
}
```

```jsx {% title="Highlight Line Ranges" showLineNumbers=true highlight="1-2,9-19,31-35" filename="UserProfile.jsx" %}
import React, { useState, useEffect } from 'react';
import { fetchUserData } from '../api/users';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function loadUser() {
      try {
        setLoading(true);
        const userData = await fetchUserData(userId);
        setUser(userData);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    if (userId) {
      loadUser();
    }
  }, [userId]);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  if (!user) return <div>User not found</div>;

  return (
    <div className="user-profile">
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
}
```

```python {% title="Mixed Highlighting" showLineNumbers=true highlight="8,10-15,23,28" filename="database.py" %}
class DatabaseConnection:
    def __init__(self, host, port, database):
        self.host = host
        self.port = port
        self.database = database
        self.connection = None
    
    def connect(self):
        """Establish database connection"""
        try:
            self.connection = psycopg2.connect(
                host=self.host,
                port=self.port,
                database=self.database
            )
            print(f"Connected to {self.database}")
        except Exception as e:
            print(f"Connection failed: {e}")
            raise
    
    def execute_query(self, query, params=None):
        """Execute a database query"""
        if not self.connection:
            raise Exception("Not connected to database")
        
        cursor = self.connection.cursor()
        try:
            cursor.execute(query, params)
            return cursor.fetchall()
        except Exception as e:
            self.connection.rollback()
            raise
        finally:
            cursor.close()
```

---

# Steps Component Tests

## Basic Steps Example

{% steps %}
{% step title="Install Dependencies" %}
First, install the required packages for your project.

```bash
npm install @markdoc/markdoc react
```

This will add Markdoc and React to your project dependencies.
{% /step %}

{% step title="Create Configuration" %}
Set up your Markdoc configuration file.

```javascript {% filename="markdoc.config.js" %}
import { Config } from '@markdoc/markdoc';

const config = {
  nodes: {},
  tags: {}
};

export default config;
```

The configuration defines how your content will be rendered.
{% /step %}

{% step title="Build Your First Document" %}
Create a Markdoc file with some content.

```markdown {% filename="example.md" %}
# Welcome to Markdoc

This is your first Markdoc document!

{% callout type="info" %}
Markdoc combines the simplicity of Markdown with the power of React.
{% /callout %}
```
{% /step %}
{% /steps %}

## Advanced Steps with Rich Content

{% steps %}
{% step title="Database Setup" %}
Configure your database connection and schema.

```sql {% filename="schema.sql" showLineNumbers=true %}
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  name VARCHAR(100) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_users_email ON users(email);
```

{% callout type="warning" %}
Make sure to backup your database before running schema changes.
{% /callout %}
{% /step %}

{% step title="API Implementation" %}
Build the API endpoints for user management.

```javascript {% filename="api/users.js" highlight="5-7,12-14" %}
const express = require('express');
const router = express.Router();

router.get('/users', async (req, res) => {
  try {
    const users = await db.query('SELECT * FROM users');
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: 'Database error' });
  }
});

router.post('/users', async (req, res) => {
  const { email, name } = req.body;
  
  try {
    const result = await db.query(
      'INSERT INTO users (email, name) VALUES ($1, $2) RETURNING *',
      [email, name]
    );
    res.status(201).json(result.rows[0]);
  } catch (error) {
    res.status(400).json({ error: 'Invalid data' });
  }
});

module.exports = router;
```

{% column cols=2 gap="sm" %}
{% card title="GET /users" description="Retrieve all users" %}
Returns a list of all users in the system.
{% /card %}

{% card title="POST /users" description="Create new user" %}
Creates a new user with email and name.
{% /card %}
{% /column %}
{% /step %}

{% step title="Testing & Deployment" %}
Write tests and deploy your application.

{% accordion title="Unit Tests" defaultOpen=true %}
```javascript {% filename="tests/users.test.js" %}
const request = require('supertest');
const app = require('../app');

describe('Users API', () => {
  test('GET /users returns user list', async () => {
    const response = await request(app)
      .get('/api/users')
      .expect(200);
    
    expect(Array.isArray(response.body)).toBe(true);
  });
});
```
{% /accordion %}

{% expand title="Deployment Configuration" %}
```yaml {% filename="docker-compose.yml" %}
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://user:pass@db:5432/myapp
  
  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=myapp
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
```
{% /expand %}
{% /step %}
{% /steps %}

## Steps with Minimal Content

{% steps %}
{% step title="Quick Start" %}
Get up and running in seconds.
{% /step %}

{% step title="Configure" %}
Set up your preferences and options.
{% /step %}

{% step title="Deploy" %}
Launch your application to production.
{% /step %}
{% /steps %}

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

# Expand Components

{% expand %}
This expand component uses the default title and starts closed. Expand components are similar to accordions but have a simpler interface focused just on showing/hiding content.
{% /expand %}

{% expand title="Custom Expand Title" %}
This expand component has a custom title and demonstrates the basic expand/collapse functionality.

You can include any content inside:
- Lists
- Code blocks  
- Other components

## Headings work too
More content to show the expand functionality.
{% /expand %}

{% expand title="Open by Default" defaultOpen=true %}
This expand component starts in the open state because defaultOpen is set to true.

```javascript
// Code blocks work in expand components
function example() {
  return 'Expand components are great for optional content';
}
```

This is useful for content that should be visible by default but can still be collapsed.
{% /expand %}

{% expand title="Documentation Section" %}
Expand components are perfect for:

1. **FAQ sections** - Questions with expandable answers
2. **Code examples** - Show/hide detailed implementation  
3. **Additional information** - Optional details that don't clutter the main content
4. **Troubleshooting steps** - Expandable help sections

{% callout title="Pro Tip" type="tip" %}
Use expand components to keep your documentation clean while providing access to detailed information when needed.
{% /callout %}
{% /expand %}

---

---

# Complex Nested Examples

{% column cols=2 gap="md" %}

{% accordion title="Accordion in Column" description="Testing nested components" %}
This accordion is inside a column layout.

{% callout title="Nested Callout" type="success" %}
This callout is nested inside an accordion which is inside a column.
{% /callout %}

{% codeGroup title="Code Group in Accordion" %}
```javascript {% title="JavaScript" highlight="2,4" %}
function example1() {
  console.log('Starting function');
  const result = 'Code in accordion in column!';
  console.log('Function complete');
  return result;
}
```
```python {% title="Python" highlight="1,3,5" %}
def example2():
    print('Starting function')
    result = 'Python in accordion too!'
    print('Function complete')
    return result
```
{% /codeGroup %}

More content in the accordion.
{% /accordion %}

{% card title="Interactive Card in Column" description="Card with link in column layout" href="/learn-more" showArrow=true ctaText="Discover" %}
This card is in the same column as the accordion above and includes a link.

## Heading in Card
Cards support rich content and can be interactive.

{% expand title="Additional Details" %}
This expand component is nested inside a card to test nested rendering.

{% callout title="Nested in Card" type="info" %}
Expand components work great inside cards for optional details.
{% /callout %}
{% /expand %}

Content after a break inside the card.
{% /card %}

{% /column %}

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

More card content after the accordion and break.

{% /card %}

{% /column %}

## Test Summary

This document tests:
- ✅ **Paragraph nodes** (custom Paragraph component)
- ✅ **Heading nodes** (all levels with Heading component)
- ✅ **Fence nodes** (code fences render as CodeSnippet with new attributes: language, filename, title, showLineNumbers, highlight, icon, content, info)
- ✅ **Callout tags** (all 6 types: info, warning, error, success, tip, danger)
- ✅ **Card tags** (all attributes: title, description, image, imageAlt, icon, href, ctaText, showArrow, external, horizontal)

- ✅ **Column tags** (1, 2, 3 columns with different gaps)
- ✅ **Accordion tags** (default closed, default open, with icons)
- ✅ **Expand tags** (default closed, default open, custom titles)
- ✅ **Steps tags** (step-by-step instructions container)
- ✅ **Step tags** (individual steps with titles and rich content)
- ✅ **CodeGroup tags** (container for multiple fence blocks, title)
- ✅ **Card link functionality** (internal links, external links, CTA text, arrows)
- ✅ **Card layout options** (horizontal vs vertical layouts)
- ✅ **Code fence variations** (different languages, with/without line numbers, icons, content, info attributes)
- ✅ **Line highlighting** (single lines, ranges, mixed patterns)
- ✅ **Steps workflow patterns** (basic steps, advanced with rich content, minimal steps)
- ✅ **Complex nesting** (accordions in cards in columns, codeGroups in accordions, expand in cards, steps with nested components)
- ✅ **All attribute combinations** (defaults and custom values)