---
title: Markdown Guide
icon: book
---

# Syntax Guide

A practical reference to core Markdown syntax for writing docs.

## Basic Formatting

### Text Formatting

- **Bold text** using `**bold text**`
- *Italic text* using `*italic text*`
- `Inline code` using backticks
- ~~Strikethrough~~ using `~~strikethrough~~`

### Headers

{% tabGroup %}
  {% tab title="Preview" %}
  # H1 Header
  ## H2 Header
  ### H3 Header
  #### H4 Header
  ##### H5 Header
  ###### H6 Header
  {% /tab %}

  {% tab title="Syntax" %}
  ```markdown
  # H1 Header
  ## H2 Header
  ### H3 Header
  #### H4 Header
  ##### H5 Header
  ###### H6 Header
  ```
  {% /tab %}
{% /tabGroup %}

## Lists

### Unordered

{% tabGroup %}
  {% tab title="Preview" %}
  - Item 1
  - Item 2
    - Nested item
    - Another nested item
  - Item 3
  {% /tab %}

  {% tab title="Syntax" %}
  ```markdown
  - Item 1
  - Item 2
    - Nested item
    - Another nested item
  - Item 3
  ```
  {% /tab %}
{% /tabGroup %}

### Ordered

{% tabGroup %}
  {% tab title="Preview" %}
  1. First item
  2. Second item
  3. Third item
  {% /tab %}

  {% tab title="Syntax" %}
  ```markdown
  1. First item
  2. Second item
  3. Third item
  ```
  {% /tab %}
{% /tabGroup %}

## Links and Images

### Links

{% tabGroup %}
  {% tab title="Preview" %}
  [Devscribe](https://devscribe.com)  
  [Devscribe with title](https://devscribe.com "Docs Home")
  {% /tab %}

  {% tab title="Syntax" %}
  ```markdown
  [Devscribe](https://devscribe.com)
  [Devscribe with title](https://devscribe.com "Docs Home")
  ```
  {% /tab %}
{% /tabGroup %}

### Images

{% tabGroup %}
  {% tab title="Preview" %}
  ![Devscribe icon](/devscribe-logo.png)

  ![Devscribe logo](/devscribe-logo.png "Devscribe Logo")
  {% /tab %}

  {% tab title="Syntax" %}
  ```markdown
  ![Devscribe icon](/devscribe-logo.png)
  ![Devscribe logo](/devscribe-logo.png "Devscribe Logo")
  ```
  {% /tab %}
{% /tabGroup %}

## Code

### Inline Code
Use single backticks for `inline code`.

### Basic Code Blocks
Use triple backticks with language specification:

{% tabGroup %}
  {% tab title="Preview" %}
  ```ts
  console.log('Hello, world!')
  ```
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  ```ts
  console.log('Hello, world!')
  ```
  ````
  {% /tab %}
{% /tabGroup %}

### Code Blocks with options

{% tabGroup %}
  {% tab title="Preview" %}
  ```ts {% title="Auth Helper" filename="auth.ts" showLineNumbers=true highlight="2,5-7" %}
  export function getToken() {
    return process.env.TOKEN
  }

  export function isLoggedIn() {
    return Boolean(getToken())
  }
  ```
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  ```ts {% title="Auth Helper" filename="auth.ts" showLineNumbers=true highlight="2,5-7" %}
  export function getToken() {
    return process.env.TOKEN
  }

  export function isLoggedIn() {
    return Boolean(getToken())
  }
  ```
  ````
  {% /tab %}
{% /tabGroup %}

---

# Custom Markdoc Components

Custom Markdoc components supported by this repo

Tip: Components can be nested (e.g., a callout inside a card, code fences inside tabs).

## Callouts

Supported types: `info`, `warning`, `error`, `success`, `tip`, `danger`.

{% tabGroup %}
  {% tab title="Preview" className="text-left" %}
{% callout type="info" %}
Informational message about a feature.
{% /callout %}
{% callout type="warning" %}
Heads up about a potentially risky action.
{% /callout %}
{% callout type="error" %}
Something went wrong and needs attention.
{% /callout %}
{% callout type="success" %}
Operation completed successfully.
{% /callout %}
{% callout type="tip" %}
Pro tip to improve your workflow.
{% /callout %}
{% callout type="danger" %}
Destructive action. Proceed with extreme caution.
{% /callout %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% callout type="info" %}
  Informational message about a feature.
  {% /callout %}
  {% callout type="warning" %}
  Heads up about a potentially risky action.
  {% /callout %}
  {% callout type="error" %}
  Something went wrong and needs attention.
  {% /callout %}
  {% callout type="success" %}
  Operation completed successfully.
  {% /callout %}
  {% callout type="tip" %}
  Pro tip to improve your workflow.
  {% /callout %}
  {% callout type="danger" %}
  Destructive action. Proceed with extreme caution.
  {% /callout %}
  ````
  {% /tab %}
{% /tabGroup %}

### Callouts with Rich Content

{% tabGroup %}
  {% tab title="Preview" %}
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
  ### Heading in Callout

  This callout contains a heading and multiple paragraphs.

  This is the second paragraph with **bold text** and *italic text*.
  {% /callout %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
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
  ### Heading in Callout

  This callout contains a heading and multiple paragraphs.

  This is the second paragraph with **bold text** and *italic text*.
  {% /callout %}
  ````
  {% /tab %}
{% /tabGroup %}

## Cards

### Basic Card Examples

{% tabGroup %}
  {% tab title="Preview" %}
  {% card title="Simple Card" description="This is a basic card with title and description" %}
  Basic card content goes here. This card uses the default attributes.
  {% /card %}

  {% card title="Card with Icon" description="This card demonstrates the icon and showIcon attributes" icon="star" %}
  This card includes an icon. The icon name should be from Lucide React.
  {% /card %}

  {% card title="Card without Icon" description="This card has showIcon set to false" icon="user" showIcon=false %}
  Even though an icon is specified, it won't be displayed because showIcon is false.
  {% /card %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% card title="Simple Card" description="This is a basic card with title and description" %}
  Basic card content goes here. This card uses the default attributes.
  {% /card %}


  {% card title="Card with Icon" description="This card demonstrates the icon and showIcon attributes" icon="star" %}
  This card includes an icon. The icon name should be from Lucide React.
  {% /card %}


  {% card title="Card without Icon" description="This card has showIcon set to false" icon="user" showIcon=false %}
  Even though an icon is specified, it won't be displayed because showIcon is false.
  {% /card %}
  ````
  {% /tab %}
{% /tabGroup %}

### Card Layout Options

{% tabGroup %}
  {% tab title="Preview" %}
  {% card title="Horizontal Card" description="This card uses horizontal layout" icon="layout" horizontal=true %}
  This card demonstrates the horizontal layout option where the icon appears on the left and content on the right, similar to a callout.

  You can include rich content in horizontal cards:
  - Lists work great
  - Code blocks too
  - Any nested content
  {% /card %}

  {% card title="Vertical Card" description="This is the default vertical layout" icon="layers" %}
  This card uses the default vertical layout where content flows from top to bottom.

  ### Heading in Card
  Cards support rich content including headings, paragraphs, and other components.
  {% /card %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% card title="Horizontal Card" description="This card uses horizontal layout" icon="layout" horizontal=true %}
  This card demonstrates the horizontal layout option where the icon appears on the left and content on the right, similar to a callout.

  You can include rich content in horizontal cards:
  - Lists work great
  - Code blocks too
  - Any nested content
  {% /card %}


  {% card title="Vertical Card" description="This is the default vertical layout" icon="layers" %}
  This card uses the default vertical layout where content flows from top to bottom.

  ### Heading in Card
  Cards support rich content including headings, paragraphs, and other components.
  {% /card %}
  ````
  {% /tab %}
{% /tabGroup %}

### Clickable Cards

{% tabGroup %}
  {% tab title="Preview" %}
  {% card title="Linked Card" description="This entire card is clickable" icon="external-link" href="https://example.com" %}
  When the href attribute is provided, the entire card becomes clickable and will navigate to the specified URL.

  Click anywhere on this card to test the link functionality.
  {% /card %}

  {% card title="Internal Link Card" description="Card linking to internal page" icon="file-text" href="/introduction" %}
  This card links to an internal page. The href can be any valid URL - external or internal.
  {% /card %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% card title="Linked Card" description="This entire card is clickable" icon="external-link" href="https://example.com" %}
  When the href attribute is provided, the entire card becomes clickable and will navigate to the specified URL.

  Click anywhere on this card to test the link functionality.
  {% /card %}


  {% card title="Internal Link Card" description="Card linking to internal page" icon="file-text" href="/introduction" %}
  This card links to an internal page. The href can be any valid URL - external or internal.
  {% /card %}
  ````
  {% /tab %}
{% /tabGroup %}

### Cards with Rich Content

{% tabGroup %}
  {% tab title="Preview" %}
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
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
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
  ````
  {% /tab %}
{% /tabGroup %}

## CardGroups

### Basic CardGroup Examples

{% tabGroup %}
  {% tab title="Preview" %}
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
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
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
  ````
  {% /tab %}
{% /tabGroup %}

### CardGroup with Different Column Layouts

#### Single Column Layout

{% tabGroup %}
  {% tab title="Preview" %}
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
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
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
  ````
  {% /tab %}
{% /tabGroup %}

#### Three Column Layout

{% tabGroup %}
  {% tab title="Preview" %}
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
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
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
  ````
  {% /tab %}
{% /tabGroup %}

### CardGroup with Mixed Content

{% tabGroup %}
  {% tab title="Preview" %}
  {% cardGroup cols=2 gap="md" %}
  {% card title="API Documentation" description="Complete API reference" icon="book" href="/api-reference/introduction" %}
  ### Getting Started

  Our API provides easy access to all platform features:

  ```bash
  curl -X GET https://api.example.com/v1/users \
    -H "Authorization: Bearer your-token"
  ```

  #### Key Features
  - RESTful design
  - JSON responses
  - Rate limiting
  - Comprehensive documentation
  {% /card %}

  {% card title="SDK Integration" description="Multiple language support" icon="code" %}
  ### Supported Languages

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

  {% card title="Community" description="Join our developer community" icon="users" horizontal=true %}
  Connect with other developers, share experiences, and get help with integration challenges.

  Visit our Discord server or GitHub discussions.
  {% /card %}

  {% card title="Support" description="Get help when you need it" icon="help-circle" horizontal=true %}
  Our support team is available 24/7 to help with any questions or issues you might encounter.

  Email us or open a support ticket.
  {% /card %}
  {% /cardGroup %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% cardGroup cols=2 gap="md" %}
  {% card title="API Documentation" description="Complete API reference" icon="book" href="/api-reference/introduction" %}
  ### Getting Started

  Our API provides easy access to all platform features:

  ```bash
  curl -X GET https://api.example.com/v1/users \
    -H "Authorization: Bearer your-token"
  ```

  #### Key Features
  - RESTful design
  - JSON responses
  - Rate limiting
  - Comprehensive documentation
  {% /card %}

  {% card title="SDK Integration" description="Multiple language support" icon="code" " %}
  ### Supported Languages

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

  {% card title="Community" description="Join our developer community" icon="users" horizontal=true %}
  Connect with other developers, share experiences, and get help with integration challenges.

  Visit our Discord server or GitHub discussions.
  {% /card %}

  {% card title="Support" description="Get help when you need it" icon="help-circle" horizontal=true %}
  Our support team is available 24/7 to help with any questions or issues you might encounter.

  Email us or open a support ticket.
  {% /card %}
  {% /cardGroup %}
  ````
  {% /tab %}
{% /tabGroup %}

## Accordions

{% tabGroup %}
  {% tab title="Preview" %}
  {% accordion title="Basic Accordion" description="This is a basic accordion" %}
  This accordion starts closed by default. It contains paragraph content that should be collapsible.

  - Item 1
  - Item 2
  - Item 3
  {% /accordion %}

  {% accordion title="Open by Default" description="This accordion starts open" defaultOpen=true %}
  This accordion starts in the open state because defaultOpen is set to true.
  {% /accordion %}

  {% accordion title="Accordion with Icon" description="Testing icon attribute" icon="star" showIcon=true %}
  This accordion displays the specified icon because showIcon is explicitly set to true.
  {% /accordion %}
  
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% accordion title="Basic Accordion" description="This is a basic accordion" %}
  This accordion starts closed by default. It contains paragraph content that should be collapsible.

  - Item 1
  - Item 2
  - Item 3
  {% /accordion %}

  {% accordion title="Open by Default" description="This accordion starts open" defaultOpen=true %}
  This accordion starts in the open state because defaultOpen is set to true.
  {% /accordion %}

  {% accordion title="Accordion with Icon" description="Testing icon attribute" icon="star" showIcon=true %}
  This accordion displays the specified icon because showIcon is explicitly set to true.
  {% /accordion %}
  
  ````
  {% /tab %}
{% /tabGroup %}

## Accordion Groups

### Basic Accordion Group

{% tabGroup %}
  {% tab title="Preview" %}
  {% accordionGroup %}
  {% accordion title="FAQ: Getting Started" description="Basic setup questions" icon="help-circle" showIcon=true %}
  Run the following command:

  ```bash
  npm install @my-package/core
  ```
  {% /accordion %}

  {% accordion title="FAQ: Configuration" description="Setup and configuration help" icon="settings" showIcon=true %}
  Create a config file in your project root:

  ```javascript {% filename="config.js" %}
  module.exports = { apiUrl: 'https://api.example.com' };
  ```
  {% /accordion %}
  {% /accordionGroup %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% accordionGroup %}
  {% accordion title="FAQ: Getting Started" description="Basic setup questions" icon="help-circle" showIcon=true %}
  Run the following command:

  ```bash
  npm install @my-package/core
  ```
  {% /accordion %}

  {% accordion title="FAQ: Configuration" description="Setup and configuration help" icon="settings" showIcon=true %}
  Create a config file in your project root:

  ```javascript {% filename="config.js" %}
  module.exports = { apiUrl: 'https://api.example.com' };
  ```
  {% /accordion %}
  {% /accordionGroup %}
  ````
  {% /tab %}
{% /tabGroup %}

### Exclusive Accordion Group

{% tabGroup %}
  {% tab title="Preview" %}
  {% accordionGroup exclusive=true %}
  {% accordion title="Step 1: Project Setup" description="Initialize your project" defaultOpen=true icon="folder-plus" showIcon=true %}
  ```bash
  mkdir my-project && cd my-project && npm init -y
  ```
  {% /accordion %}

  {% accordion title="Step 2: Install Dependencies" description="Add required packages" icon="download" showIcon=true %}
  ```bash
  npm install react react-dom
  ```
  {% /accordion %}
  {% /accordionGroup %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% accordionGroup exclusive=true %}
  {% accordion title="Step 1: Project Setup" description="Initialize your project" defaultOpen=true icon="folder-plus" showIcon=true %}
  ```bash
  mkdir my-project && cd my-project && npm init -y
  ```
  {% /accordion %}

  {% accordion title="Step 2: Install Dependencies" description="Add required packages" icon="download" showIcon=true %}
  ```bash
  npm install react react-dom
  ```
  {% /accordion %}
  {% /accordionGroup %}
  ````
  {% /tab %}
{% /tabGroup %}

## Expand

{% tabGroup %}
  {% tab title="Preview" %}
  {% expand %}
  This expand component uses the default title and starts closed.
  {% /expand %}

  {% expand title="Custom Expand Title" %}
  You can include any content inside, like lists and code blocks.

  ```javascript
  function example() {
    return 'Expand components show/hide optional content';
  }
  ```
  {% /expand %}

  {% expand title="Open by Default" defaultOpen=true %}
  This expand component starts in the open state because defaultOpen is true.
  {% /expand %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% expand %}
  This expand component uses the default title and starts closed.
  {% /expand %}

  {% expand title="Custom Expand Title" %}
  You can include any content inside, like lists and code blocks.

  ```javascript
  function example() {
    return 'Expand components show/hide optional content';
  }
  ```
  {% /expand %}

  {% expand title="Open by Default" defaultOpen=true %}
  This expand component starts in the open state because defaultOpen is true.
  {% /expand %}
  ````
  {% /tab %}
{% /tabGroup %}

## Steps

### Basic Steps

{% tabGroup %}
  {% tab title="Preview" %}
  {% steps %}
  {% step title="Install Dependencies" %}
  ```bash
  npm install @markdoc/markdoc react
  ```
  {% /step %}

  {% step title="Create Configuration" %}
  ```javascript {% filename="markdoc.config.js" %}
  export default { nodes: {}, tags: {} }
  ```
  {% /step %}

  {% step title="Build Your First Document" %}
  ```markdown {% filename="example.md" %}
  # Welcome to Markdoc
  {% callout type="info" %}Hello from Markdoc!{% /callout %}
  ```
  {% /step %}
  {% /steps %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% steps %}
  {% step title="Install Dependencies" %}
  ```bash
  npm install @markdoc/markdoc react
  ```
  {% /step %}

  {% step title="Create Configuration" %}
  ```javascript {% filename="markdoc.config.js" %}
  export default { nodes: {}, tags: {} }
  ```
  {% /step %}

  {% step title="Build Your First Document" %}
  ```markdown {% filename="example.md" %}
  # Welcome to Markdoc
  {% callout type="info" %}Hello from Markdoc!{% /callout %}
  ```
  {% /step %}
  {% /steps %}
  ````
  {% /tab %}
{% /tabGroup %}

### Advanced Steps with Rich Content

{% tabGroup %}
  {% tab title="Preview" %}
  {% steps %}
  {% step title="Database Setup" %}
  Configure your database connection and schema.

  ```sql {% filename="schema.sql" showLineNumbers=true %}
  CREATE TABLE plants (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    tag VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

  {% callout type="warning" %}
  Make sure to backup your database before running schema changes.
  {% /callout %}
  {% /step %}

  {% step title="API Implementation" %}
  Build the API endpoints.

  ```javascript {% filename="api/plants.js" highlight="5-7,12-14" %}
  import express from 'express'
  const router = express.Router()

  router.get('/plants', async (req, res) => {
    const plants = await db.query('SELECT * FROM plants')
    res.json(plants)
  })

  router.post('/plants', async (req, res) => {
    const { name, tag } = req.body
    const result = await db.query('INSERT INTO plants(name, tag) VALUES($1,$2) RETURNING *', [name, tag])
    res.status(201).json(result.rows[0])
  })

  export default router
  ```

  {% callout type="tip" %}
  Return precise status codes and validate inputs.
  {% /callout %}
  
  The endpoints above demonstrate basic read and create operations.
  {% /step %}

  {% step title="Testing & Deployment" %}
  Write tests and deploy your application.

  ```bash {% filename="ci.yml" %}
  npm run test && npm run build && npm run deploy
  ```
  {% /step %}
  {% /steps %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% steps %}
  {% step title="Database Setup" %}
  Configure your database connection and schema.

  ```sql {% filename="schema.sql" showLineNumbers=true %}
  CREATE TABLE plants (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    tag VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

  {% callout type="warning" %}
  Make sure to backup your database before running schema changes.
  {% /callout %}
  {% /step %}

  {% step title="API Implementation" %}
  Build the API endpoints.

  ```javascript {% filename="api/plants.js" highlight="5-7,12-14" %}
  import express from 'express'
  const router = express.Router()

  router.get('/plants', async (req, res) => {
    const plants = await db.query('SELECT * FROM plants')
    res.json(plants)
  })

  router.post('/plants', async (req, res) => {
    const { name, tag } = req.body
    const result = await db.query('INSERT INTO plants(name, tag) VALUES($1,$2) RETURNING *', [name, tag])
    res.status(201).json(result.rows[0])
  })

  export default router
  ```

  {% callout type="tip" %}
  Return precise status codes and validate inputs.
  {% /callout %}
  
  The endpoints above demonstrate basic read and create operations.
  {% /step %}

  {% step title="Testing & Deployment" %}
  Write tests and deploy your application.

  ```bash {% filename="ci.yml" %}
  npm run test && npm run build && npm run deploy
  ```
  {% /step %}
  {% /steps %}
  ````
  {% /tab %}
{% /tabGroup %}

## CodeGroups

{% tabGroup %}
  {% tab title="Preview" %}
  {% codeGroup title="HTTP Clients" %}
  ```bash {% filename="curl.sh" %}
  curl --request POST https://api.example.com/v1/plants \
    --header 'Content-Type: application/json' \
    --header 'Authorization: Bearer <token>' \
    --data '{"name":"Aloe","tag":"succulent"}'
  ```

  ```javascript {% filename="fetch.js" %}
  async function createPlant() {
    const res = await fetch('https://api.example.com/v1/plants', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Authorization: 'Bearer <token>'
      },
      body: JSON.stringify({ name: 'Aloe', tag: 'succulent' })
    })
    return res.json()
  }
  ```

  ```python {% filename="requests_example.py" %}
  import requests

  def create_plant():
      r = requests.post(
          'https://api.example.com/v1/plants',
          headers={'Authorization': 'Bearer <token>'},
          json={'name': 'Aloe', 'tag': 'succulent'}
      )
      return r.json()
  ```
  {% /codeGroup %}

  {% codeGroup title="With Line Numbers + Highlight" %}
  ```ts {% filename="service.ts" showLineNumbers=true highlight="3-5" %}
  export async function listPlants() {
    const res = await fetch('/v1/plants')
    if (!res.ok) throw new Error('Failed to load')
    return res.json()
  }
  ```

  ```go {% filename="main.go" showLineNumbers=true %}
  package main

  import "fmt"

  func main() {
      fmt.Println("Hello CodeGroup")
  }
  ```
  {% /codeGroup %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  {% codeGroup title="HTTP Clients" %}
  ```bash {% filename="curl.sh" %}
  curl --request POST https://api.example.com/v1/plants \
    --header 'Content-Type: application/json' \
    --header 'Authorization: Bearer <token>' \
    --data '{"name":"Aloe","tag":"succulent"}'
  ```

  ```javascript {% filename="fetch.js" %}
  async function createPlant() {
    const res = await fetch('https://api.example.com/v1/plants', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Authorization: 'Bearer <token>'
      },
      body: JSON.stringify({ name: 'Aloe', tag: 'succulent' })
    })
    return res.json()
  }
  ```

  ```python {% filename="requests_example.py" %}
  import requests

  def create_plant():
      r = requests.post(
          'https://api.example.com/v1/plants',
          headers={'Authorization': 'Bearer <token>'},
          json={'name': 'Aloe', 'tag': 'succulent'}
      )
      return r.json()
  ```
  {% /codeGroup %}

  {% codeGroup title="With Line Numbers + Highlight" %}
  ```ts {% filename="service.ts" showLineNumbers=true highlight="3-5" %}
  export async function listPlants() {
    const res = await fetch('/v1/plants')
    if (!res.ok) throw new Error('Failed to load')
    return res.json()
  }
  ```

  ```go {% filename="main.go" showLineNumbers=true %}
  package main

  import "fmt"

  func main() {
      fmt.Println("Hello CodeGroup")
  }
  ```
  {% /codeGroup %}
  ````
  {% /tab %}
{% /tabGroup %}

## Fields

{% tabGroup %}
  {% tab title="Preview" %}
  ### Basic
  {% parameterField name="id" type="string" required=true %}
  The unique identifier.
  {% /parameterField %}

  ### With Default Values
  {% parameterField name="role" type="string" default="user" %}
  The user's role. Defaults to "user".
  {% /parameterField %}

  ### Deprecated
  {% parameterField name="legacyId" type="number" deprecated=true %}
  Legacy identifier. Do not use in new integrations.
  {% /parameterField %}

  ### Within an Expand
  {% expand title="User Fields" %}
  {% parameterField name="email" type="string" required=true %}
  The user's primary email address.
  {% /parameterField %}
  {% parameterField name="name" type="string" %}
  Optional display name.
  {% /parameterField %}
  {% /expand %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  ### Basic
  {% parameterField name="id" type="string" required=true %}
  The unique identifier.
  {% /parameterField %}

  ### With Default Values
  {% parameterField name="role" type="string" default="user" %}
  The user's role. Defaults to "user".
  {% /parameterField %}

  ### Deprecated
  {% parameterField name="legacyId" type="number" deprecated=true %}
  Legacy identifier. Do not use in new integrations.
  {% /parameterField %}

  ### Within an Expand
  {% expand title="User Fields" %}
  {% parameterField name="email" type="string" required=true %}
  The user's primary email address.
  {% /parameterField %}
  {% parameterField name="name" type="string" %}
  Optional display name.
  {% /parameterField %}
  {% /expand %}
  ````
  {% /tab %}
{% /tabGroup %}

## Tooltips

{% tabGroup %}
  {% tab title="Preview" %}
  This is a paragraph with a {% tooltip tip="This is a helpful tooltip message!" %}hover tooltip{% /tooltip %} that provides additional context.

  You can also use tooltips to explain {% tooltip tip="Application Programming Interface - a set of protocols and tools for building software applications" %}technical terms{% /tooltip %} in your documentation.
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  This is a paragraph with a {% tooltip tip="This is a helpful tooltip message!" %}hover tooltip{% /tooltip %} that provides additional context.

  You can also use tooltips to explain {% tooltip tip="Application Programming Interface - a set of protocols and tools for building software applications" %}technical terms{% /tooltip %} in your documentation.
  ````
  {% /tab %}
{% /tabGroup %}

## Tabs

{% tabGroup %}
  {% tab title="Preview" %}
  ### Basic Tabs
  {% tabGroup %}
  {% tab title="JavaScript" %}
  ```javascript
  function greetUser(name) {
    return `Hello, ${name}!`;
  }
  ```
  {% /tab %}
  {% tab title="Python" %}
  ```python
  def greet_user(name):
      return f"Hello, {name}!"
  ```
  {% /tab %}
  {% tab title="TypeScript" %}
  ```typescript
  function greetUser(name: string): string {
    return `Hello, ${name}!`;
  }
  ```
  {% /tab %}
  {% /tabGroup %}

  ### Tab Groups with Rich Content
  {% tabGroup className="api-documentation" %}
  {% tab title="Request" %}
  Make a POST request to create a new resource:

  ```bash
  curl -X POST https://api.example.com/v1/users \
    -H "Content-Type: application/json" \
    -d '{"name":"Jane","email":"jane@example.com"}'
  ```

  #### Request Headers
  - **Content-Type**: `application/json`
  - **Authorization**: `Bearer <token>`

  #### Request Body Fields
  {% parameterField name="name" type="string" required=true %}
  Full name of the new user.
  {% /parameterField %}
  {% parameterField name="email" type="string" required=true %}
  A valid email address for the account.
  {% /parameterField %}
  {% parameterField name="role" type="string" default="user" %}
  Optional role. Defaults to `user`.
  {% /parameterField %}
  {% /tab %}
  {% tab title="Response" %}
  A successful response returns:

  ```json
  {
    "id": "user_123",
    "name": "Jane",
    "email": "jane@example.com"
  }
  ```

  #### Response Fields
  {% responseField name="id" type="string" %}Unique identifier for the user.{% /responseField %}
  {% responseField name="name" type="string" %}User's full name.{% /responseField %}
  {% responseField name="email" type="string" %}User's email address.{% /responseField %}
  {% /tab %}
  {% tab title="Errors" %}
  #### Validation Error (400)
  ```json
  {
    "error": {
      "code": "VALIDATION_ERROR",
      "message": "Invalid input data",
      "details": [{ "field": "email", "message": "Email format is invalid" }]
    }
  }
  ```
  {% callout type="warning" %}
  Always validate input; return field-level errors where possible.
  {% /callout %}
  {% /tab %}
  {% /tabGroup %}
  {% /tab %}

  {% tab title="Syntax" %}
  ````markdown
  ### Basic Tabs
  {% tabGroup %}
  {% tab title="JavaScript" %}
  ```javascript
  function greetUser(name) {
    return `Hello, ${name}!`;
  }
  ```
  {% /tab %}
  {% tab title="Python" %}
  ```python
  def greet_user(name):
      return f"Hello, {name}!"
  ```
  {% /tab %}
  {% tab title="TypeScript" %}
  ```typescript
  function greetUser(name: string): string {
    return `Hello, ${name}!`;
  }
  ```
  {% /tab %}
  {% /tabGroup %}

  ### Tab Groups with Rich Content
  {% tabGroup className="api-documentation" %}
  {% tab title="Request" %}
  Make a POST request to create a new resource:

  ```bash
  curl -X POST https://api.example.com/v1/users \
    -H "Content-Type: application/json" \
    -d '{"name":"Jane","email":"jane@example.com"}'
  ```
  
  #### Request Headers
  - **Content-Type**: `application/json`
  - **Authorization**: `Bearer <token>`

  #### Request Body Fields
  {% parameterField name="name" type="string" required=true %}
  Full name of the new user.
  {% /parameterField %}
  {% parameterField name="email" type="string" required=true %}
  A valid email address for the account.
  {% /parameterField %}
  {% parameterField name="role" type="string" default="user" %}
  Optional role. Defaults to `user`.
  {% /parameterField %}
  {% /tab %}
  {% tab title="Response" %}
  A successful response returns:

  ```json
  {
    "id": "user_123",
    "name": "Jane",
    "email": "jane@example.com"
  }
  ```
  
  #### Response Fields
  {% responseField name="id" type="string" %}Unique identifier for the user.{% /responseField %}
  {% responseField name="name" type="string" %}User's full name.{% /responseField %}
  {% responseField name="email" type="string" %}User's email address.{% /responseField %}
  {% /tab %}
  {% tab title="Errors" %}
  #### Validation Error (400)
  ```json
  {
    "error": {
      "code": "VALIDATION_ERROR",
      "message": "Invalid input data",
      "details": [{ "field": "email", "message": "Email format is invalid" }]
    }
  }
  ```
  {% callout type="warning" %}
  Always validate input; return field-level errors where possible.
  {% /callout %}
  {% /tab %}
  {% /tabGroup %}
  ````
  {% /tab %}
{% /tabGroup %}
