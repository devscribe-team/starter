# Markdoc Configuration Test Document

This document tests all the custom Markdoc nodes and tags defined in the final markdoc configuration.

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

```jsx {% title="React Component" filename="Component.jsx" showLineNumbers=true highlight="2,5-7" %}
import React from 'react';
const Greeting = ({ name }) => {
  return (
    <div className="greeting">
      <h1>Hello, {name}!</h1>
      <p>Welcome to our application!</p>
    </div>
  );
};
export default Greeting;
```

---

# Callout Component Tests

## All Callout Types

{% callout type="info" %}
This is an info callout. Use this for general information or helpful tips.
{% /callout %}

{% callout type="warning" %}
This is a warning callout. Use this to alert users about potential issues or important considerations.
{% /callout %}

{% callout type="error" %}
This is an error callout. Use this for error messages or critical issues that need immediate attention.
{% /callout %}

{% callout type="success" %}
This is a success callout. Use this for positive feedback or successful operations.
{% /callout %}

{% callout type="tip" %}
This is a tip callout. Use this for helpful suggestions or best practices.
{% /callout %}

{% callout type="danger" %}
This is a danger callout. Use this for serious warnings about destructive actions.
{% /callout %}

## Callouts with Rich Content

{% callout type="info" %}
You can include code blocks in callouts:

```javascript
console.log('Hello from inside a callout!');
```

And lists too:
- Item 1
- Item 2
- Item 3
{% /callout %}

{% callout type="warning" %}
## Heading in Callout

This callout contains a heading and multiple paragraphs.

This is the second paragraph with **bold text** and *italic text*.
{% /callout %}

---

# Card Component Tests

## Basic Card Examples

{% card title="Simple Card" description="This is a basic card with title and description" %}
Basic card content goes here. This card uses the default attributes.
{% /card %}

{% card title="Card with Icon" description="This card demonstrates the icon and showIcon attributes" icon="star" %}
This card includes an icon. The icon name should be from Lucide React.
{% /card %}

{% card title="Card without Icon" description="This card has showIcon set to false" icon="user" showIcon=false %}
Even though an icon is specified, it won't be displayed because showIcon is false.
{% /card %}

## Card Layout Options

{% card title="Horizontal Card" description="This card uses horizontal layout" icon="layout" horizontal=true %}
This card demonstrates the horizontal layout option where the icon appears on the left and content on the right, similar to a callout.

You can include rich content in horizontal cards:
- Lists work great
- Code blocks too
- Any nested content
{% /card %}

{% card title="Vertical Card" description="This is the default vertical layout" icon="layers" %}
This card uses the default vertical layout where content flows from top to bottom.

## Heading in Card
Cards support rich content including headings, paragraphs, and other components.
{% /card %}

## Clickable Cards

{% card title="Linked Card" description="This entire card is clickable" icon="external-link" href="https://example.com" %}
When the href attribute is provided, the entire card becomes clickable and will navigate to the specified URL.

Click anywhere on this card to test the link functionality.
{% /card %}

{% card title="Internal Link Card" description="Card linking to internal page" icon="file-text" href="/documentation" %}
This card links to an internal page. The href can be any valid URL - external or internal.
{% /card %}

## Cards with Rich Content

{% card title="Card with Code" description="Demonstrating code blocks in cards" icon="code" %}
Cards can contain code examples:

```javascript
function greetUser(name) {
  return `Hello, ${name}! Welcome to our app.`;
}

const message = greetUser('Alice');
console.log(message);
```

The code formatting is preserved inside the card component.
{% /card %}

{% card title="Card with Lists" description="Cards supporting various content types" icon="list" %}
Cards work well with different content types:

### Ordered Lists
1. First item
2. Second item
3. Third item

### Unordered Lists
- Bullet point one
- Bullet point two
- Bullet point three

### Mixed Content
You can combine text, lists, and other elements seamlessly.
{% /card %}

---

# CardGroup Component Tests

## Basic CardGroup Examples

{% cardGroup cols=2 gap="md" %}
{% card title="Feature 1" description="Core functionality" icon="zap" %}
Fast and reliable performance with optimized algorithms.
{% /card %}

{% card title="Feature 2" description="Easy integration" icon="plug" %}
Simple APIs that integrate with your existing workflow.
{% /card %}

{% card title="Feature 3" description="Secure by default" icon="shield" %}
Built-in security features to protect your data.
{% /card %}

{% card title="Feature 4" description="Scalable architecture" icon="trending-up" %}
Scales automatically to handle increased demand.
{% /card %}
{% /cardGroup %}

## CardGroup with Different Column Layouts

### Single Column Layout

{% cardGroup cols=1 gap="lg" %}
{% card title="Full Width Card" description="This card spans the full width" icon="maximize" %}
In a single column layout, cards take up the full available width, making them perfect for detailed content.

```javascript
// Example: Full-width content
const fullWidthComponent = () => {
  return <div className="full-width">Content here</div>;
};
```
{% /card %}

{% card title="Another Full Width Card" description="Second card in single column" icon="square" %}
This layout is ideal for:
- Detailed explanations
- Code examples that need space
- Step-by-step instructions
{% /card %}
{% /cardGroup %}

### Three Column Layout

{% cardGroup cols=3 gap="sm" %}
{% card title="Quick Tip 1" description="Compact design" icon="lightbulb" %}
Use small gaps for compact layouts.
{% /card %}

{% card title="Quick Tip 2" description="Performance" icon="gauge" %}
Optimize your components for speed.
{% /card %}

{% card title="Quick Tip 3" description="Accessibility" icon="accessibility" %}
Always consider accessibility in design.
{% /card %}

{% card title="Quick Tip 4" description="User Experience" icon="users" %}
Focus on user-centered design principles.
{% /card %}

{% card title="Quick Tip 5" description="Mobile First" icon="smartphone" %}
Design for mobile devices first.
{% /card %}

{% card title="Quick Tip 6" description="Testing" icon="check-circle" %}
Test your components thoroughly.
{% /card %}
{% /cardGroup %}

### Four Column Layout

{% cardGroup cols=4 gap="lg" %}
{% card title="Tool 1" icon="hammer" %}
Development tools
{% /card %}

{% card title="Tool 2" icon="wrench" %}
Configuration utilities
{% /card %}

{% card title="Tool 3" icon="cog" %}
System settings
{% /card %}

{% card title="Tool 4" icon="monitor" %}
Monitoring dashboard
{% /card %}
{% /cardGroup %}

## CardGroup Gap Variations

### Small Gap
{% cardGroup cols=3 gap="sm" %}
{% card title="Tight Layout" description="Small gaps" icon="minimize" %}
Compact spacing between cards.
{% /card %}

{% card title="Close Together" description="Minimal space" icon="compress" %}
Cards are closely positioned.
{% /card %}

{% card title="Dense Grid" description="More content" icon="grid" %}
Fits more cards in the view.
{% /card %}
{% /cardGroup %}

### Large Gap
{% cardGroup cols=2 gap="lg" %}
{% card title="Spacious Layout" description="Large gaps" icon="maximize" %}
Generous spacing between cards for a clean, airy feel.
{% /card %}

{% card title="Breathing Room" description="Comfortable spacing" icon="space" %}
Provides visual separation and reduces clutter.
{% /card %}
{% /cardGroup %}

## CardGroup with Mixed Content

{% cardGroup cols=2 gap="md" %}
{% card title="API Documentation" description="Complete API reference" icon="book" href="/api-docs" %}
## Getting Started

Our API provides easy access to all platform features:

```bash
curl -X GET https://api.example.com/v1/users \
  -H "Authorization: Bearer your-token"
```

### Key Features
- RESTful design
- JSON responses
- Rate limiting
- Comprehensive documentation
{% /card %}

{% card title="SDK Integration" description="Multiple language support" icon="code" href="/sdk" %}
## Supported Languages

We provide SDKs for popular programming languages:

- **JavaScript/TypeScript** - npm package
- **Python** - pip package  
- **Go** - Go modules
- **PHP** - Composer package

```javascript
import { APIClient } from '@our-platform/sdk';
const client = new APIClient('your-api-key');
```
{% /card %}

{% card title="Community" description="Join our developer community" icon="users" href="/community" horizontal=true %}
Connect with other developers, share experiences, and get help with integration challenges.

Visit our Discord server or GitHub discussions.
{% /card %}

{% card title="Support" description="Get help when you need it" icon="help-circle" href="/support" horizontal=true %}
Our support team is available 24/7 to help with any questions or issues you might encounter.

Email us or open a support ticket.
{% /card %}
{% /cardGroup %}

---

# Accordion Component Tests

## Individual Accordions

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
This accordion has an icon specified and uses the default showIcon=true.
{% /accordion %}

{% accordion title="Accordion without Icon" description="Testing showIcon attribute" icon="star" showIcon=false %}
This accordion has an icon specified but showIcon is set to false, so no icon will be displayed.
{% /accordion %}

{% accordion title="Custom Class Accordion" description="Testing className attribute" icon="settings" className="custom-accordion-style" %}
This accordion includes a custom className for styling purposes.
{% /accordion %}

{% accordion title="Minimal Accordion" %}
This accordion only has a title, using defaults for other attributes.
{% /accordion %}

## Accordion Groups

### Basic Accordion Group (Default Behavior)

{% accordionGroup %}
{% accordion title="FAQ: Getting Started" description="Basic setup questions" icon="help-circle" %}
**Q: How do I install the package?**

Run the following command:
```bash
npm install @my-package/core
```

**Q: What are the system requirements?**

- Node.js 16 or higher
- NPM 7 or higher
- Modern browser support
{% /accordion %}

{% accordion title="FAQ: Configuration" description="Setup and configuration help" icon="settings" %}
**Q: How do I configure the application?**

Create a config file in your project root:
```javascript {% filename="config.js" %}
module.exports = {
  apiUrl: 'https://api.example.com',
  timeout: 5000,
  retries: 3
};
```

**Q: Can I use environment variables?**

Yes! The application automatically loads `.env` files.
{% /accordion %}

{% accordion title="FAQ: Troubleshooting" description="Common issues and solutions" icon="alert-triangle" %}
**Q: The application won't start**

Check these common issues:
1. Verify Node.js version
2. Clear node_modules and reinstall
3. Check for port conflicts

**Q: API requests are failing**

{% callout type="warning" %}
Make sure your API endpoint is accessible and CORS is configured properly.
{% /callout %}
{% /accordion %}
{% /accordionGroup %}

### Exclusive Accordion Group

{% accordionGroup exclusive=true %}
{% accordion title="Step 1: Project Setup" description="Initialize your project" defaultOpen=true icon="folder-plus" %}
Start by creating a new project directory and initializing it:

```bash
mkdir my-project
cd my-project
npm init -y
```

This creates the basic project structure you'll need.
{% /accordion %}

{% accordion title="Step 2: Install Dependencies" description="Add required packages" icon="download" %}
Install the necessary dependencies for your project:

```bash {% title="Install Core Dependencies" %}
npm install react react-dom
npm install -D @types/react @types/react-dom
npm install -D typescript webpack webpack-cli
```

{% callout type="info" %}
This setup assumes you're building a React application with TypeScript.
{% /callout %}
{% /accordion %}

{% accordion title="Step 3: Configure Build" description="Set up build process" icon="gear" %}
Create your build configuration:

```json {% filename="tsconfig.json" showLineNumbers=true %}
{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "es6"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  }
}
```
{% /accordion %}

{% accordion title="Step 4: Create Components" description="Build your first components" icon="component" %}
Create your main application component:

```jsx {% filename="src/App.jsx" showLineNumbers=true %}
import React from 'react';

function App() {
  return (
    <div className="app">
      <header>
        <h1>My Application</h1>
      </header>
      <main>
        <p>Welcome to your new application!</p>
      </main>
    </div>
  );
}

export default App;
```
{% /accordion %}
{% /accordionGroup %}

### Accordion Group with Custom Styling

{% accordionGroup className="documentation-accordions" %}
{% accordion title="API Reference" description="Complete API documentation" icon="code" %}
## Authentication

All API requests require authentication using Bearer tokens:

```javascript {% title="API Authentication" highlight="3" %}
const response = await fetch('/api/data', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer your-token-here',
    'Content-Type': 'application/json'
  }
});
```

## Endpoints

### GET /api/users
Returns a list of all users in the system.

### POST /api/users
Creates a new user account.
{% /accordion %}

{% accordion title="SDK Documentation" description="Client library usage" icon="book" %}
## Installation

```bash
npm install @myapp/sdk
```

## Quick Start

```javascript {% filename="example.js" showLineNumbers=true %}
import { MyAppSDK } from '@myapp/sdk';

const client = new MyAppSDK({
  apiKey: 'your-api-key',
  baseUrl: 'https://api.myapp.com'
});

// Fetch user data
const users = await client.users.list();
console.log(users);
```
{% /accordion %}

{% accordion title="Examples & Tutorials" description="Step-by-step guides" icon="play" %}
## Basic Usage Tutorial

Follow this tutorial to get started with the platform.

### Example Code

```javascript
const result = await client.api.get('/health');
console.log('API Status:', result.status);
```
{% /accordion %}
{% /accordionGroup %}

---

# Expand Component Tests

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

{% callout type="tip" %}
Use expand components to keep your documentation clean while providing access to detailed information when needed.
{% /callout %}
{% /expand %}

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

{% cardGroup cols=2 gap="sm" %}
{% card title="GET /users" description="Retrieve all users" icon="users" %}
Returns a list of all users in the system.
{% /card %}

{% card title="POST /users" description="Create new user" icon="user-plus" %}
Creates a new user with email and name.
{% /card %}
{% /cardGroup %}
{% /step %}

{% step title="Testing & Deployment" %}
Write tests and deploy your application.

{% accordion title="Unit Tests" defaultOpen=true icon="test-tube" %}
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

---

# CodeGroup Component Tests

## Basic CodeGroup Examples

{% codeGroup title="Basic API Example" %}
```javascript {% filename="fetchUsers.js" %}
// JavaScript implementation
async function fetchUsers() {
  const response = await fetch('/api/users');
  return response.json();
}
```

```python {% filename="fetch_users.py" %}
# Python implementation
import requests

def fetch_users():
    response = requests.get('/api/users')
    return response.json()
```

```go {% filename="main.go" %}
// Go implementation
package main

import (
    "encoding/json"
    "net/http"
)

func fetchUsers() ([]User, error) {
    resp, err := http.Get("/api/users")
    if err != nil {
        return nil, err
    }
    defer resp.Body.Close()
    
    var users []User
    err = json.NewDecoder(resp.Body).Decode(&users)
    return users, err
}
```
{% /codeGroup %}

## CodeGroup with Line Numbers and Highlighting

{% codeGroup title="Database Connection Patterns" %}
```javascript {% title="Node.js + PostgreSQL" showLineNumbers=true highlight="5-7,12-14" %}
const { Pool } = require('pg');

const pool = new Pool({
  user: 'dbuser',
  host: 'database.server.com',
  database: 'mydb',
  password: 'secretpassword',
  port: 3211,
});

async function queryUsers() {
  const client = await pool.connect();
  try {
    const result = await client.query('SELECT * FROM users');
    return result.rows;
  } finally {
    client.release();
  }
}
```

```python {% title="Python + SQLAlchemy" showLineNumbers=true highlight="1-3,8-10,15-17" %}
from sqlalchemy import create_engine, text
from sqlalchemy.orm import sessionmaker
import os

DATABASE_URL = os.getenv('DATABASE_URL')
engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(bind=engine)

def get_users():
    session = SessionLocal()
    try:
        result = session.execute(text('SELECT * FROM users'))
        return result.fetchall()
    finally:
        session.close()
```
{% /codeGroup %}

---

# Field Component Tests

## Basic Field Examples

{% field name="id" type="string" required=true %}
The unique identifier for the user resource.
{% /field %}

{% field name="email" type="string" required=true %}
The user's email address. Must be a valid email format.
{% /field %}

{% field name="name" type="string" %}
The user's full name. This field is optional.
{% /field %}

{% field name="age" type="number" default="18" %}
The user's age in years. Defaults to 18 if not provided.
{% /field %}

{% field name="isActive" type="boolean" default="true" %}
Whether the user account is currently active.
{% /field %}

## Field with Default Values

{% field name="createdAt" type="string" default="new Date().toISOString()" %}
The timestamp when the user was created. Automatically set to current time if not provided.
{% /field %}

{% field name="role" type="string" default="user" %}
The user's role in the system. Can be 'user', 'admin', or 'moderator'.
{% /field %}

{% field name="preferences" type="object" default="{}" %}
User preferences object containing theme, language, and notification settings.
{% /field %}

## Field with Deprecated Fields

{% field name="username" type="string" deprecated=true %}
The user's username. This field is deprecated and will be removed in v2.0. Use 'email' instead.
{% /field %}

{% field name="legacyId" type="number" deprecated=true required=false %}
Legacy identifier from the old system. This field is deprecated and should not be used in new implementations.
{% /field %}

## Field with Expand Components

{% expand title="User Profile Fields" %}
Complete documentation for user profile-related fields.

{% field name="userId" type="string" required=true %}
The unique identifier for the user account.
{% /field %}

{% field name="profile" type="object" required=true %}
User profile information containing personal and contact details.

{% expand title="Profile Object Structure" %}
The profile object contains the following nested properties:

{% field name="firstName" type="string" required=true %}
User's first name as entered during registration.
{% /field %}

{% field name="lastName" type="string" required=true %}
User's last name as entered during registration.
{% /field %}

{% field name="email" type="string" required=true %}
Primary email address for the user account. Must be unique across the system.

{% expand title="Email Validation Rules" %}
Email validation follows these rules:
- Must contain a valid email format (user@domain.com)
- Domain must have valid DNS records
- Cannot be from disposable email providers
- Maximum length of 255 characters

```javascript
// Example email validation
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
const isValid = emailRegex.test(email) && email.length <= 255;
```
{% /expand %}
{% /field %}

{% field name="avatar" type="string" %}
URL to the user's profile picture.

{% expand title="Avatar Requirements" %}
Profile pictures must meet these requirements:
- **Format**: JPEG, PNG, or WebP
- **Size**: Maximum 5MB
- **Dimensions**: Minimum 100x100px, recommended 400x400px
- **Aspect Ratio**: Square (1:1) preferred

### Upload Process
1. Client uploads image to `/api/upload/avatar`
2. Server validates format and size
3. Image is resized and optimized
4. CDN URL is returned for the avatar field
{% /expand %}
{% /field %}

{% /expand %}
{% /field %}

{% /expand %}

---

# Tooltip Component Tests

## Basic Tooltip Examples

This is a paragraph with a {% tooltip tip="This is a helpful tooltip message!" %}hover tooltip{% /tooltip %} that provides additional context.

You can also use tooltips to explain {% tooltip tip="Application Programming Interface - a set of protocols and tools for building software applications" %}technical terms{% /tooltip %} in your documentation.

## Tooltips with Rich Content

Here's a {% tooltip tip="A JavaScript library for building user interfaces, developed by Facebook (now Meta)" %}React{% /tooltip %} component example.

This {% tooltip tip="A superset of JavaScript that adds static type definitions, helping catch errors during development" %}TypeScript{% /tooltip %} interface shows the structure.

## Complex Tooltip Examples

The {% tooltip tip="A design pattern that allows an object to notify multiple dependent objects about state changes" %}Observer pattern{% /tooltip %} is commonly used in {% tooltip tip="Event-driven programming paradigm where the flow of the program is determined by events such as user actions, sensor outputs, or messages from other programs" %}event-driven architectures{% /tooltip %}.

When working with {% tooltip tip="Asynchronous JavaScript and XML - a technique for creating fast and dynamic web pages by exchanging data with a server behind the scenes" %}AJAX{% /tooltip %} requests, you should handle {% tooltip tip="JavaScript promises provide a way to handle asynchronous operations and their eventual completion or failure" %}promises{% /tooltip %} properly.

---

# TabGroup and Tab Component Tests

## Basic Tab Examples

{% tabGroup %}
{% tab title="JavaScript" %}
```javascript
function greetUser(name) {
  return `Hello, ${name}! Welcome to our application.`;
}

const message = greetUser('Alice');
console.log(message);
```

This JavaScript example shows a simple greeting function that takes a name parameter and returns a personalized message.
{% /tab %}

{% tab title="Python" %}
```python
def greet_user(name):
    return f"Hello, {name}! Welcome to our application."

message = greet_user('Alice')
print(message)
```

The Python version uses f-strings for string formatting, which is the modern way to format strings in Python 3.6+.
{% /tab %}

{% tab title="TypeScript" %}
```typescript
function greetUser(name: string): string {
  return `Hello, ${name}! Welcome to our application.`;
}

const message: string = greetUser('Alice');
console.log(message);
```

TypeScript adds type annotations to provide better IDE support and catch errors at compile time.
{% /tab %}
{% /tabGroup %}

## Tab Groups with Rich Content

{% tabGroup className="api-documentation" %}
{% tab title="Request" %}
### API Request Example

Make a POST request to create a new user:

```bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-token" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user"
  }'
```

#### Request Headers

- **Content-Type**: `application/json`
- **Authorization**: `Bearer {your_access_token}`

#### Request Body

The request body should contain the following fields:

- **name** (string, required) - The full name of the user to create
- **email** (string, required) - A valid email address for the user account  
- **role** (string, optional) - The role to assign to the user. Can be 'user', 'admin', or 'moderator'. Defaults to 'user'
{% /tab %}

{% tab title="Response" %}
### API Response Example

Successful user creation returns:

```json
{
  "success": true,
  "data": {
    "id": "user_123456",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "user",
    "createdAt": "2023-12-01T10:30:00Z",
    "isActive": true
  }
}
```

#### Response Fields

{% field name="success" type="boolean" required=true %}
Indicates whether the request was successful.
{% /field %}

{% field name="data" type="object" required=true %}
The created user object containing all user information.
{% /field %}
{% /tab %}

{% tab title="Error Handling" %}
### Error Response Examples

#### Validation Error (400)

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": [
      {
        "field": "email",
        "message": "Email format is invalid"
      }
    ]
  }
}
```

#### Authentication Error (401)

```json
{
  "success": false,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Invalid or missing authentication token"
  }
}
```

{% callout type="warning" %}
Always implement proper error handling in your application to gracefully handle these error responses.
{% /callout %}
{% /tab %}
{% /tabGroup %}

---

# Complex Nested Examples

## Cards in CardGroups with Rich Content

{% cardGroup cols=2 gap="md" %}

{% card title="Frontend Implementation" description="React component examples" icon="code" %}
### Component Structure

```jsx
import React, { useState } from 'react';

function UserForm() {
  const [user, setUser] = useState({
    name: '',
    email: ''
  });

  return (
    <form>
      <input
        value={user.name}
        onChange={(e) => setUser({...user, name: e.target.value})}
        placeholder="Name"
      />
      <input
        type="email"
        value={user.email}
        onChange={(e) => setUser({...user, email: e.target.value})}
        placeholder="Email"
      />
      <button type="submit">Create User</button>
    </form>
  );
}
```

{% accordion title="Component Props" icon="settings" %}
The UserForm component accepts the following props:

{% field name="onSubmit" type="function" required=true %}
Callback function called when the form is submitted.
{% /field %}

{% field name="initialValues" type="object" %}
Initial values for the form fields.
{% /field %}
{% /accordion %}
{% /card %}

{% card title="Backend Integration" description="API connection details" icon="server" %}
### API Connection

```javascript
async function createUser(userData) {
  const response = await fetch('/api/users', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(userData)
  });

  if (!response.ok) {
    throw new Error('Failed to create user');
  }

  return response.json();
}
```

{% expand title="Error Handling Strategy" %}
Implement comprehensive error handling:

1. **Network errors** - Handle connection issues
2. **Validation errors** - Display field-specific messages
3. **Server errors** - Show user-friendly error messages
4. **Timeout errors** - Retry with backoff strategy

```javascript
const handleError = (error) => {
  if (error.name === 'ValidationError') {
    showFieldErrors(error.details);
  } else {
    showGenericError('Something went wrong. Please try again.');
  }
};
```
{% /expand %}
{% /card %}

{% card title="Testing Strategy" description="Comprehensive test coverage" icon="test-tube" horizontal=true %}
Our testing approach covers all aspects of the application:

- **Unit tests** for individual components
- **Integration tests** for API endpoints
- **End-to-end tests** for user workflows
- **Performance tests** for load handling

{% callout type="tip" %}
Use Jest for unit testing and Cypress for end-to-end testing.
{% /callout %}
{% /card %}

{% card title="Deployment" description="Production deployment guide" icon="rocket" horizontal=true %}
Deploy your application using modern DevOps practices:

{% steps %}
{% step title="Build" %}
Create production build with optimizations.
{% /step %}

{% step title="Test" %}
Run all test suites before deployment.
{% /step %}

{% step title="Deploy" %}
Use CI/CD pipeline for automated deployment.
{% /step %}
{% /steps %}
{% /card %}

{% /cardGroup %}

## All Components Together

{% cardGroup cols=1 gap="lg" %}

{% card title="Complete Integration Example" description="Demonstrating all components working together" icon="puzzle" %}

## Project Overview

This example shows how all Markdoc components can work together to create comprehensive documentation.

{% tabGroup %}
{% tab title="Getting Started" %}
### Quick Start Guide

{% steps %}
{% step title="Prerequisites" %}
Make sure you have the required tools installed:

{% field name="node" type="string" required=true %}
Node.js version 16 or higher for running JavaScript.
{% /field %}

{% field name="npm" type="string" required=true %}
NPM version 7 or higher for package management.
{% /field %}
{% /step %}

{% step title="Installation" %}
Install the project dependencies:

```bash
npm install @markdoc/markdoc
npm install react react-dom
```

{% callout type="info" %}
This will install all the necessary packages for Markdoc integration.
{% /callout %}
{% /step %}
{% /steps %}
{% /tab %}

{% tab title="Configuration" %}
### Setup Instructions

{% accordion title="Basic Configuration" defaultOpen=true icon="gear" %}
Create your markdoc.config.js file:

```javascript {% filename="markdoc.config.js" showLineNumbers=true %}
export const markdocTags = {
  callout: {
    render: 'Callout',
    attributes: {
      type: { type: String, matches: ["info", "warning", "error"] }
    }
  },
  card: {
    render: 'Card',
    attributes: {
      title: { type: String },
      description: { type: String }
    }
  }
};
```
{% /accordion %}

{% accordion title="Advanced Options" icon="cog" %}
For advanced use cases, you can customize:

{% expand title="Custom Renderers" %}
Create custom React components for rendering:

```jsx
function CustomCallout({ type, children }) {
  return (
    <div className={`callout callout-${type}`}>
      {children}
    </div>
  );
}
```
{% /expand %}

{% expand title="Schema Validation" %}
Add schema validation for better error handling:

- Validate attribute types
- Check required attributes
- Provide helpful error messages
{% /expand %}
{% /accordion %}
{% /accordionGroup %}
{% /tab %}

{% tab title="Examples" %}
### Component Examples

{% cardGroup cols=2 gap="sm" %}
{% card title="Callouts" icon="info" %}
Use callouts for important information.

{% callout type="tip" %}
This is an example callout inside a card inside a tab!
{% /callout %}
{% /card %}

{% card title="Code Blocks" icon="code" %}
Syntax highlighting works great:

```javascript
const example = "nested code";
```
{% /card %}

{% card title="Fields" icon="database" %}
Document your API fields:

{% field name="example" type="string" %}
This field demonstrates nesting.
{% /field %}
{% /card %}

{% card title="Tooltips" icon="help-circle" %}
Add {% tooltip tip="This tooltip is inside a card!" %}helpful tooltips{% /tooltip %} anywhere.
{% /card %}
{% /cardGroup %}
{% /tab %}
{% /tabGroup %}

{% /card %}

{% /cardGroup %}

---

## Test Summary

This document comprehensively tests:

- ✅ **Fence nodes** (code fences render as CodeSnippet with syntax highlighting, line numbers, and highlighting)
- ✅ **Callout tags** (all 6 types: info, warning, error, success, tip, danger)
- ✅ **Card tags** (all attributes: title, description, icon, showIcon, horizontal, href)
- ✅ **CardGroup tags** (all attributes: cols, gap - supporting 1-4 columns and sm/md/lg gaps)
- ✅ **Accordion tags** (all attributes: title, description, defaultOpen, icon, showIcon, className)
- ✅ **AccordionGroup tags** (exclusive mode, custom className)
- ✅ **Expand tags** (title, defaultOpen attributes)
- ✅ **Steps tags** (step-by-step instructions container)
- ✅ **Step tags** (individual steps with titles and rich content)
- ✅ **CodeGroup tags** (container for multiple fence blocks with titles)
- ✅ **Field tags** (all attributes: name, type, default, required, deprecated, with rich content)
- ✅ **Tooltip tags** (tip attribute for contextual help)
- ✅ **TabGroup tags** (container for tab components with optional className)
- ✅ **Tab tags** (individual tabs with required title and optional className)

### Key Features Tested:
- ✅ **Rich content support** - All components support nested content including paragraphs, headings, code blocks, lists
- ✅ **Component nesting** - Complex combinations like cards in cardGroups, fields in expands, accordions in steps
- ✅ **Icon integration** - Cards and accordions with Lucide React icons and showIcon control
- ✅ **Layout options** - CardGroup grid layouts, horizontal cards, accordion groups
- ✅ **Interactive elements** - Clickable cards, collapsible accordions/expands, tabbed content
- ✅ **Accessibility** - Proper semantic structure and keyboard navigation support
- ✅ **All attribute combinations** - Testing default values, custom values, and edge cases 