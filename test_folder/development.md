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

# CodeGroup Component Tests

## Basic CodeGroup Examples

{% codeGroup title="Basic API Example" %}
```javascript
// JavaScript implementation
async function fetchUsers() {
  const response = await fetch('/api/users');
  return response.json();
}
```

```python
# Python implementation
import requests

def fetch_users():
    response = requests.get('/api/users')
    return response.json()
```

```go
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

{% codeGroup %}
```javascript {% title="React Hook" %}
import { useState, useEffect } from 'react';

function useUsers() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('/api/users')
      .then(res => res.json())
      .then(data => {
        setUsers(data);
        setLoading(false);
      });
  }, []);

  return { users, loading };
}
```

```typescript {% title="TypeScript Hook" %}
import { useState, useEffect } from 'react';

interface User {
  id: number;
  name: string;
  email: string;
}

function useUsers(): { users: User[]; loading: boolean } {
  const [users, setUsers] = useState<User[]>([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('/api/users')
      .then(res => res.json())
      .then((data: User[]) => {
        setUsers(data);
        setLoading(false);
      });
  }, []);

  return { users, loading };
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

```rust {% title="Rust + SQLx" showLineNumbers=true highlight="3,7-9,13-15" %}
use sqlx::postgres::PgPool;
use sqlx::Row;
use std::env;

#[derive(Debug)]
struct User {
    id: i32,
    name: String,
    email: String,
}

async fn get_users(pool: &PgPool) -> Result<Vec<User>, sqlx::Error> {
    let rows = sqlx::query("SELECT id, name, email FROM users")
        .fetch_all(pool)
        .await?;
    
    let users = rows.into_iter().map(|row| User {
        id: row.get("id"),
        name: row.get("name"),
        email: row.get("email"),
    }).collect();
    
    Ok(users)
}
```
{% /codeGroup %}

## CodeGroup with Different File Types

{% codeGroup title="Full Stack Configuration" %}
```json {% filename="package.json" %}
{
  "name": "my-fullstack-app",
  "version": "1.0.0",
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "test": "jest"
  },
  "dependencies": {
    "next": "^14.0.0",
    "react": "^18.0.0",
    "react-dom": "^18.0.0"
  }
}
```

```yaml {% filename="docker-compose.yml" %}
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://user:pass@db:5432/app
    depends_on:
      - db
  
  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=app
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

```dockerfile {% filename="Dockerfile" %}
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
```

```bash {% filename="deploy.sh" %}
#!/bin/bash

echo "Building application..."
docker-compose build

echo "Starting services..."
docker-compose up -d

echo "Running database migrations..."
docker-compose exec app npm run migrate

echo "Deployment complete!"
```
{% /codeGroup %}

## CodeGroup with Mixed Languages and Frameworks

{% codeGroup title="Authentication Implementation" %}
```javascript {% title="Express.js Middleware" highlight="4-6,10-12" %}
const jwt = require('jsonwebtoken');

function authenticateToken(req, res, next) {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];
  
  if (!token) {
    return res.sendStatus(401);
  }

  jwt.verify(token, process.env.ACCESS_TOKEN_SECRET, (err, user) => {
    if (err) return res.sendStatus(403);
    req.user = user;
    next();
  });
}

module.exports = authenticateToken;
```

```python {% title="FastAPI Dependency" highlight="5-7,11-13" %}
from fastapi import Depends, HTTPException, status
from fastapi.security import HTTPBearer, HTTPAuthorizationCredentials
import jwt

security = HTTPBearer()

async def get_current_user(credentials: HTTPAuthorizationCredentials = Depends(security)):
    try:
        payload = jwt.decode(
            credentials.credentials, 
            SECRET_KEY, 
            algorithms=[ALGORITHM]
        )
        username: str = payload.get("sub")
        if username is None:
            raise HTTPException(
                status_code=status.HTTP_401_UNAUTHORIZED,
                detail="Could not validate credentials"
            )
        return username
    except jwt.PyJWTError:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Could not validate credentials"
        )
```

```rust {% title="Axum Extractor" highlight="7-9,15-17" %}
use axum::{
    extract::{Request, State},
    http::{header::AUTHORIZATION, StatusCode},
    middleware::Next,
    response::Response,
};
use jsonwebtoken::{decode, DecodingKey, Validation};

pub async fn auth_middleware(
    State(app_state): State<AppState>,
    mut req: Request,
    next: Next,
) -> Result<Response, StatusCode> {
    let auth_header = req
        .headers()
        .get(AUTHORIZATION)
        .and_then(|header| header.to_str().ok())
        .and_then(|header| header.strip_prefix("Bearer "));

    let token = auth_header.ok_or(StatusCode::UNAUTHORIZED)?;
    
    let claims = decode::<Claims>(
        token,
        &DecodingKey::from_secret(app_state.jwt_secret.as_ref()),
        &Validation::default(),
    )
    .map_err(|_| StatusCode::UNAUTHORIZED)?;
    
    req.extensions_mut().insert(claims.claims);
    Ok(next.run(req).await)
}
```
{% /codeGroup %}

## Nested CodeGroups in Other Components

### CodeGroup in Accordion

{% accordion title="API Examples" description="Multiple language implementations" %}
This accordion contains a CodeGroup showing the same API endpoint implemented in different languages:

{% codeGroup title="Create User Endpoint" %}
```javascript {% title="Express.js" showLineNumbers=true %}
app.post('/api/users', async (req, res) => {
  try {
    const { name, email } = req.body;
    
    const user = await User.create({
      name,
      email,
      createdAt: new Date()
    });
    
    res.status(201).json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});
```

```python {% title="FastAPI" showLineNumbers=true %}
@app.post("/api/users", response_model=UserResponse)
async def create_user(user_data: UserCreate):
    try:
        user = User(
            name=user_data.name,
            email=user_data.email,
            created_at=datetime.now()
        )
        
        db.add(user)
        await db.commit()
        await db.refresh(user)
        
        return user
    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))
```
{% /codeGroup %}

{% callout type="info" %}
Both implementations follow RESTful conventions and return appropriate HTTP status codes.
{% /callout %}
{% /accordion %}

### CodeGroup in Column Layout

{% column cols=2 gap="md" %}

{% codeGroup title="Frontend Code" %}
```jsx {% title="React Component" %}
function UserForm() {
  const [user, setUser] = useState({
    name: '',
    email: ''
  });

  const handleSubmit = async (e) => {
    e.preventDefault();
    await createUser(user);
  };

  return (
    <form onSubmit={handleSubmit}>
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
{% /codeGroup %}

{% codeGroup title="Backend Code" %}
```javascript {% title="API Handler" %}
async function createUser(userData) {
  const validation = validateUser(userData);
  if (!validation.isValid) {
    throw new Error(validation.errors.join(', '));
  }

  const user = await db.users.create({
    name: userData.name,
    email: userData.email,
    id: generateId(),
    createdAt: new Date()
  });

  return user;
}

function validateUser(userData) {
  const errors = [];
  
  if (!userData.name) {
    errors.push('Name is required');
  }
  
  if (!userData.email || !isValidEmail(userData.email)) {
    errors.push('Valid email is required');
  }
  
  return {
    isValid: errors.length === 0,
    errors
  };
}
```
{% /codeGroup %}

{% /column %}

## CodeGroup with All Fence Attributes

{% codeGroup title="Advanced Code Examples with All Attributes" %}
```javascript {% title="Authentication Service" filename="auth.service.js" showLineNumbers=true highlight="8-10,15-17" icon="shield" content="JWT Authentication" info="Secure token-based authentication system" %}
class AuthService {
  constructor(secretKey) {
    this.secretKey = secretKey;
    this.tokenExpiry = '24h';
  }

  async generateToken(userId) {
    const payload = {
      userId,
      iat: Math.floor(Date.now() / 1000),
      exp: Math.floor(Date.now() / 1000) + (24 * 60 * 60)
    };
    
    return jwt.sign(payload, this.secretKey);
  }

  async verifyToken(token) {
    try {
      const decoded = jwt.verify(token, this.secretKey);
      return { valid: true, userId: decoded.userId };
    } catch (error) {
      return { valid: false, error: error.message };
    }
  }
}
```

```python {% title="Database Models" filename="models.py" showLineNumbers=true highlight="1-3,12-14,20-22" icon="database" content="SQLAlchemy Models" info="User and session models for the application" %}
from sqlalchemy import Column, Integer, String, DateTime, Boolean
from sqlalchemy.ext.declarative import declarative_base
from datetime import datetime

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    name = Column(String(100), nullable=False)
    email = Column(String(255), unique=True, nullable=False)
    password_hash = Column(String(255), nullable=False)
    is_active = Column(Boolean, default=True)
    created_at = Column(DateTime, default=datetime.utcnow)
    updated_at = Column(DateTime, default=datetime.utcnow, onupdate=datetime.utcnow)

class Session(Base):
    __tablename__ = 'sessions'
    
    id = Column(String(255), primary_key=True)
    user_id = Column(Integer, nullable=False)
    expires_at = Column(DateTime, nullable=False)
    created_at = Column(DateTime, default=datetime.utcnow)
```

```bash {% title="Deployment Script" filename="deploy.sh" icon="rocket" content="Production Deployment" info="Automated deployment script with health checks" %}
#!/bin/bash
set -e

echo "🚀 Starting deployment..."

# Build the application
echo "📦 Building application..."
npm run build

# Run tests
echo "🧪 Running tests..."
npm test

# Deploy to production
echo "🌐 Deploying to production..."
docker build -t myapp:latest .
docker push registry.example.com/myapp:latest

# Update production environment
kubectl set image deployment/myapp myapp=registry.example.com/myapp:latest

# Wait for rollout
kubectl rollout status deployment/myapp

echo "✅ Deployment completed successfully!"
```
{% /codeGroup %}

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

## Card Icon Variations

{% card title="Different Icons" description="Testing various icon options" icon="heart" %}
This card uses a heart icon. Icons should be valid Lucide React icon names.
{% /card %}

{% card title="Settings Card" description="Configuration and settings" icon="settings" %}
Settings-related content with a gear icon.
{% /card %}

{% card title="Database Card" description="Data and storage information" icon="database" %}
Database-related content with an appropriate icon.
{% /card %}

{% card title="Warning Card" description="Important notice or warning" icon="alert-triangle" %}
This card uses a warning icon to draw attention to important information.
{% /card %}

## Horizontal Layout Cards

{% card title="Feature Overview" description="Key platform features" icon="zap" horizontal=true %}
### Lightning Fast Performance
Our platform is optimized for speed with sub-second response times.

### Scalable Architecture
Built to handle millions of users with auto-scaling infrastructure.

### Developer Friendly
Simple APIs and comprehensive documentation for easy integration.
{% /card %}

{% card title="Getting Started" description="Quick setup guide" icon="play" horizontal=true %}
Follow these steps to get started:

1. **Sign up** for an account
2. **Configure** your settings
3. **Deploy** your first application
4. **Monitor** performance metrics

Ready to begin? Click the link to start your journey.
{% /card %}

## Cards with Custom Attributes

{% card title="Custom Card" description="Testing all available attributes" icon="sparkles" showIcon=true horizontal=false href="/custom-page" %}
This card tests multiple attributes:
- **title**: Custom Card
- **description**: Testing all available attributes  
- **icon**: sparkles
- **showIcon**: true (default)
- **horizontal**: false (default)
- **href**: /custom-page

All attributes are working correctly in this example.
{% /card %}

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

## Field with Rich Content

{% field name="profile" type="object" required=true %}
The user's profile information containing personal details.

## Profile Structure

The profile object contains the following nested fields:

- **firstName** (string) - User's first name
- **lastName** (string) - User's last name  
- **bio** (string, optional) - User's biography
- **avatar** (string, optional) - URL to user's profile picture

### Example Profile Object

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "bio": "Software developer passionate about web technologies",
  "avatar": "https://example.com/avatars/johndoe.jpg"
}
```
{% /field %}

{% field name="permissions" type="array" %}
Array of permission strings that define what actions the user can perform.

## Permission Types

The following permission types are available:

1. **read** - Can view resources
2. **write** - Can create and update resources
3. **delete** - Can remove resources
4. **admin** - Full administrative access

{% callout type="warning" %}
Admin permissions should be granted carefully as they provide full system access.
{% /callout %}
{% /field %}

## Field with Code Examples

{% field name="apiKey" type="string" required=true %}
The API key for authenticating requests.

### Usage Example

```javascript
const response = await fetch('/api/users', {
  headers: {
    'Authorization': `Bearer ${apiKey}`,
    'Content-Type': 'application/json'
  }
});
```

### Security Note

{% callout type="danger" %}
Never expose API keys in client-side code or public repositories.
{% /callout %}
{% /field %}

{% field name="metadata" type="object" default="null" %}
Additional metadata associated with the user.

### Metadata Schema

```typescript
interface UserMetadata {
  lastLogin?: string;
  loginCount?: number;
  preferences?: {
    theme: 'light' | 'dark';
    language: string;
    timezone: string;
  };
  tags?: string[];
}
```

### Example Usage

```javascript
// Setting user metadata
const user = {
  id: "123",
  email: "user@example.com",
  metadata: {
    lastLogin: "2023-12-01T10:30:00Z",
    loginCount: 42,
    preferences: {
      theme: "dark",
      language: "en",
      timezone: "UTC"
    },
    tags: ["premium", "early-adopter"]
  }
};
```
{% /field %}

## Complete API Response Example

{% field name="user" type="object" required=true %}
The complete user object returned by the API.

## User Object Structure

{% field name="id" type="string" required=true %}
Unique identifier for the user.
{% /field %}

{% field name="email" type="string" required=true %}
User's email address.
{% /field %}

{% field name="profile" type="object" required=true %}
User profile information.

### Profile Fields

{% field name="firstName" type="string" required=true %}
User's first name.
{% /field %}

{% field name="lastName" type="string" required=true %}
User's last name.
{% /field %}

{% field name="avatar" type="string" %}
URL to the user's profile picture.
{% /field %}

{% /field %}

{% field name="settings" type="object" default="{}" %}
User account settings.

### Available Settings

- **notifications** (boolean) - Enable/disable notifications
- **privacy** (string) - Privacy level: 'public', 'friends', 'private'
- **language** (string) - Preferred language code

```json
{
  "notifications": true,
  "privacy": "friends",
  "language": "en"
}
```
{% /field %}

{% field name="createdAt" type="string" required=true %}
ISO 8601 timestamp of when the user was created.
{% /field %}

{% field name="updatedAt" type="string" required=true %}
ISO 8601 timestamp of when the user was last updated.
{% /field %}

{% /field %}

## Field with Lists

{% field name="roles" type="array" default="['user']" %}
Array of role strings assigned to the user.

### Available Roles

- `user` - Standard user account
- `premium` - Premium subscription user  
- `moderator` - Can moderate content
- `admin` - Full administrative access

### Role Hierarchy

1. **user** - Basic access level
2. **premium** - Includes user permissions plus premium features
3. **moderator** - Includes premium permissions plus moderation tools
4. **admin** - All permissions

{% callout type="info" %}
Users can have multiple roles, and permissions are cumulative.
{% /callout %}
{% /field %}

{% field name="friends" type="array" %}
Array of friend user objects.

### Friend Object Structure

Each friend object contains:

- **id** (string) - Friend's user ID
- **name** (string) - Friend's display name
- **status** (string) - Online status: 'online', 'away', 'offline'
- **mutualFriends** (number) - Count of mutual friends

### Example Response

```json
[
  {
    "id": "user_456", 
    "name": "Jane Smith",
    "status": "online",
    "mutualFriends": 5
  },
  {
    "id": "user_789",
    "name": "Bob Johnson", 
    "status": "away",
    "mutualFriends": 2
  }
]
```
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

{% field name="phone" type="string" %}
User's phone number in international format.

{% expand title="Phone Number Format" %}
Phone numbers should be provided in E.164 format:
- Start with '+' followed by country code
- No spaces, dashes, or parentheses
- Example: +1234567890

```javascript
// Phone validation example
const phoneRegex = /^\+[1-9]\d{1,14}$/;
const isValidPhone = phoneRegex.test(phone);
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

{% field name="bio" type="string" %}
User's biography or description text.

{% expand title="Bio Guidelines" %}
Biography text guidelines:
- Maximum 500 characters
- HTML tags are stripped for security
- Line breaks are preserved
- Markdown formatting is not supported

```javascript
// Bio processing example
function processBio(bio) {
  return bio
    .substring(0, 500)
    .replace(/<[^>]*>/g, '') // Strip HTML
    .trim();
}
```
{% /expand %}
{% /field %}

{% /expand %}
{% /field %}

{% field name="preferences" type="object" %}
User account preferences and settings.

{% expand title="Preferences Structure" %}
User preferences include theme, notifications, and privacy settings.

{% field name="theme" type="string" default="system" %}
UI theme preference for the user interface.

{% expand title="Available Themes" %}
Theme options available to users:
- **system** (default) - Follows system theme
- **light** - Light theme with bright colors
- **dark** - Dark theme with muted colors
- **high-contrast** - High contrast for accessibility

```css
/* Example theme CSS variables */
:root[data-theme="light"] {
  --bg-primary: #ffffff;
  --text-primary: #000000;
}

:root[data-theme="dark"] {
  --bg-primary: #1a1a1a;
  --text-primary: #ffffff;
}
```
{% /expand %}
{% /field %}

{% field name="notifications" type="object" %}
Notification preferences for different types of alerts.

{% expand title="Notification Settings" %}
Controls which notifications the user receives:

{% field name="email" type="boolean" default="true" %}
Whether to send email notifications.
{% /field %}

{% field name="push" type="boolean" default="true" %}
Whether to send push notifications to mobile devices.
{% /field %}

{% field name="sms" type="boolean" default="false" %}
Whether to send SMS notifications for critical alerts.
{% /field %}

{% field name="frequency" type="string" default="immediate" %}
How often to send bundled notifications.

{% expand title="Frequency Options" %}
- **immediate** - Send notifications as they occur
- **hourly** - Bundle notifications every hour
- **daily** - Send daily digest at 9 AM
- **weekly** - Send weekly summary on Mondays
{% /expand %}
{% /field %}

{% /expand %}
{% /field %}

{% field name="privacy" type="object" %}
Privacy settings controlling data visibility.

{% expand title="Privacy Controls" %}
User privacy settings for profile visibility:

{% field name="profileVisibility" type="string" default="public" %}
Who can view the user's profile information.

{% expand title="Visibility Levels" %}
- **public** - Anyone can view the profile
- **friends** - Only confirmed friends can view
- **private** - Only the user can view their profile
- **custom** - Custom visibility rules apply
{% /expand %}
{% /field %}

{% field name="searchable" type="boolean" default="true" %}
Whether the user appears in search results.
{% /field %}

{% field name="showOnlineStatus" type="boolean" default="true" %}
Whether to display online/offline status to other users.
{% /field %}

{% /expand %}
{% /field %}

{% /expand %}
{% /field %}

{% /expand %}

## API Response with Nested Field Documentation

{% expand title="Complete API Response Structure" defaultOpen=true %}
Documentation for the complete user API response including all nested objects.

{% field name="success" type="boolean" required=true %}
Indicates whether the API request was successful.
{% /field %}

{% field name="data" type="object" required=true %}
The main response data containing user information.

{% expand title="User Data Object" %}
Complete user object with all available fields:

{% field name="id" type="string" required=true %}
Unique identifier for the user.
{% /field %}

{% field name="username" type="string" required=true %}
User's chosen username for the platform.

{% expand title="Username Requirements" %}
Username validation rules:
- 3-30 characters long
- Alphanumeric characters, underscores, and hyphens only
- Must start with a letter or number
- Case insensitive but preserved

```javascript
const usernameRegex = /^[a-zA-Z0-9][a-zA-Z0-9_-]{2,29}$/;
const isValidUsername = usernameRegex.test(username);
```
{% /expand %}
{% /field %}

{% field name="metadata" type="object" %}
Additional metadata about the user account.

{% expand title="Metadata Fields" %}
System-generated metadata for analytics and administration:

{% field name="createdAt" type="string" required=true %}
ISO 8601 timestamp when the account was created.
{% /field %}

{% field name="lastLoginAt" type="string" %}
ISO 8601 timestamp of the user's last login.

{% expand title="Login Tracking" %}
Login tracking includes:
- **Timestamp** in UTC format
- **IP Address** (hashed for privacy)
- **User Agent** information
- **Geographic location** (country level)

Privacy note: Detailed login logs are automatically purged after 90 days.
{% /expand %}
{% /field %}

{% field name="accountStatus" type="string" required=true %}
Current status of the user account.

{% expand title="Account Status Types" %}
Possible account status values:
- **active** - Account is fully functional
- **pending** - Email verification required
- **suspended** - Temporarily restricted access
- **banned** - Permanently restricted access
- **deleted** - Account marked for deletion
{% /expand %}
{% /field %}

{% field name="roles" type="array" default="['user']" %}
Array of roles assigned to the user.

{% expand title="Role System" %}
Platform role hierarchy and permissions:

**Standard Roles:**
- `user` - Basic platform access
- `premium` - Premium features access
- `creator` - Content creation privileges
- `moderator` - Community moderation tools
- `admin` - Full administrative access

**Custom Roles:**
Organizations can define custom roles with specific permissions.

```javascript
// Example role checking
function hasPermission(user, permission) {
  return user.roles.some(role => 
    rolePermissions[role]?.includes(permission)
  );
}
```
{% /expand %}
{% /field %}

{% /expand %}
{% /field %}

{% /expand %}
{% /field %}

{% field name="error" type="object" %}
Error information when the request fails (only present when success is false).

{% expand title="Error Object Structure" %}
Detailed error information for debugging and user feedback:

{% field name="code" type="string" required=true %}
Machine-readable error code for programmatic handling.

{% expand title="Common Error Codes" %}
Standard error codes used across the API:
- `VALIDATION_ERROR` - Request data failed validation
- `AUTHENTICATION_REQUIRED` - Valid authentication token required
- `AUTHORIZATION_FAILED` - Insufficient permissions
- `RESOURCE_NOT_FOUND` - Requested resource doesn't exist
- `RATE_LIMIT_EXCEEDED` - Too many requests
- `INTERNAL_ERROR` - Server-side error occurred
{% /expand %}
{% /field %}

{% field name="message" type="string" required=true %}
Human-readable error message safe for display to users.
{% /field %}

{% field name="details" type="array" %}
Array of detailed error information for validation errors.

{% expand title="Error Details Format" %}
Each detail object contains:
- **field** - The field that failed validation
- **code** - Specific validation error code
- **message** - Human-readable error message

```json
{
  "details": [
    {
      "field": "email",
      "code": "INVALID_FORMAT",
      "message": "Email address format is invalid"
    }
  ]
}
```
{% /expand %}
{% /field %}

{% /expand %}
{% /field %}

{% /expand %}

## Field Edge Cases and Complex Types

{% field name="data" type="any" %}
Dynamic data field that can contain any type of value.

### Possible Types

The data field can contain:

- **String values** for text data
- **Number values** for numeric data  
- **Boolean values** for true/false flags
- **Object values** for complex nested data
- **Array values** for lists of items
- **null** when no data is available

### Type Checking

```javascript
// Always check the type before using
if (typeof data === 'string') {
  console.log('Text data:', data);
} else if (typeof data === 'object' && data !== null) {
  console.log('Object data:', data);
} else if (Array.isArray(data)) {
  console.log('Array data:', data);
}
```
{% /field %}

{% field name="legacyField" type="string" deprecated=true default="legacy_value" %}
This field exists for backward compatibility only.

## Migration Guide

{% callout type="warning" %}
This field will be removed in the next major version. Please migrate to using the new field structure.
{% /callout %}

### Migration Steps

1. **Identify usage** of legacyField in your code
2. **Replace** with the new field equivalent
3. **Test** your integration thoroughly
4. **Remove** any references to legacyField

### Code Migration Example

```javascript
// OLD - Don't use
const oldValue = response.legacyField;

// NEW - Use this instead  
const newValue = response.newField || response.metadata?.equivalentValue;
```
{% /field %}

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
The created user object.

### User Object Fields

{% field name="id" type="string" required=true %}
Unique identifier for the created user.
{% /field %}

{% field name="name" type="string" required=true %}
The user's full name as provided in the request.
{% /field %}

{% field name="email" type="string" required=true %}
The user's email address.
{% /field %}

{% field name="role" type="string" required=true %}
The assigned user role.
{% /field %}

{% field name="createdAt" type="string" required=true %}
ISO 8601 timestamp of when the user was created.
{% /field %}

{% field name="isActive" type="boolean" required=true %}
Whether the user account is active (always true for new accounts).
{% /field %}

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

#### Rate Limit Error (429)

```json
{
  "success": false,
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Too many requests. Please try again later.",
    "retryAfter": 60
  }
}
```

{% callout type="warning" %}
Always implement proper error handling in your application to gracefully handle these error responses.
{% /callout %}
{% /tab %}
{% /tabGroup %}

## Nested Tab Examples

{% tabGroup %}
{% tab title="Frontend Implementation" %}
### React Component Example

```jsx
import React, { useState } from 'react';

function UserManager() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(false);

  const createUser = async (userData) => {
    setLoading(true);
    try {
      const response = await fetch('/api/users', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(userData)
      });
      
      if (response.ok) {
        const newUser = await response.json();
        setUsers([...users, newUser.data]);
      }
    } catch (error) {
      console.error('Error creating user:', error);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="user-manager">
      <h2>User Management</h2>
      {/* Component content */}
    </div>
  );
}
```

#### Key Features

{% column cols=2 gap="sm" %}

{% card title="State Management" %}
Uses React hooks for managing component state including user list and loading status.
{% /card %}

{% card title="Error Handling" %}
Implements try-catch blocks to handle API errors gracefully.
{% /card %}

{% /column %}
{% /tab %}

{% tab title="Backend Implementation" %}
### Express.js Route Handler

```javascript
const express = require('express');
const router = express.Router();

router.post('/users', async (req, res) => {
  try {
    const { name, email, role } = req.body;
    
    // Validation
    if (!name || !email) {
      return res.status(400).json({
        success: false,
        error: {
          code: 'VALIDATION_ERROR',
          message: 'Name and email are required'
        }
      });
    }
    
    // Create user
    const user = await User.create({
      name,
      email,
      role: role || 'user',
      isActive: true,
      createdAt: new Date()
    });
    
    res.status(201).json({
      success: true,
      data: user
    });
    
  } catch (error) {
    res.status(500).json({
      success: false,
      error: {
        code: 'INTERNAL_ERROR',
        message: error.message
      }
    });
  }
});

module.exports = router;
```

#### Implementation Notes

{% expand title="Database Integration" %}
This example assumes you're using an ORM like Sequelize or Mongoose. The `User.create()` method would be replaced with your specific database integration.

```javascript
// Sequelize example
const user = await User.create({ name, email, role });

// Mongoose example  
const user = new User({ name, email, role });
await user.save();

// Raw SQL example
const result = await db.query(
  'INSERT INTO users (name, email, role) VALUES (?, ?, ?)',
  [name, email, role]
);
```
{% /expand %}
{% /tab %}

{% tab title="Testing" %}
### Unit Tests

```javascript
const request = require('supertest');
const app = require('../app');

describe('POST /api/users', () => {
  test('should create a new user successfully', async () => {
    const userData = {
      name: 'Test User',
      email: 'test@example.com',
      role: 'user'
    };

    const response = await request(app)
      .post('/api/users')
      .send(userData)
      .expect(201);

    expect(response.body.success).toBe(true);
    expect(response.body.data).toHaveProperty('id');
    expect(response.body.data.name).toBe(userData.name);
  });

  test('should return validation error for missing email', async () => {
    const userData = { name: 'Test User' };

    const response = await request(app)
      .post('/api/users')
      .send(userData)
      .expect(400);

    expect(response.body.success).toBe(false);
    expect(response.body.error.code).toBe('VALIDATION_ERROR');
  });
});
```

### Integration Tests

{% accordion title="API Integration Test" %}
```javascript
describe('User API Integration', () => {
  let authToken;
  let testUserId;

  beforeAll(async () => {
    // Setup authentication
    const authResponse = await request(app)
      .post('/auth/login')
      .send({ email: 'admin@test.com', password: 'password' });
    
    authToken = authResponse.body.token;
  });

  test('complete user lifecycle', async () => {
    // Create user
    const createResponse = await request(app)
      .post('/api/users')
      .set('Authorization', `Bearer ${authToken}`)
      .send({
        name: 'Integration Test User',
        email: 'integration@test.com'
      })
      .expect(201);

    testUserId = createResponse.body.data.id;

    // Fetch user
    const fetchResponse = await request(app)
      .get(`/api/users/${testUserId}`)
      .set('Authorization', `Bearer ${authToken}`)
      .expect(200);

    expect(fetchResponse.body.data.name).toBe('Integration Test User');

    // Update user
    await request(app)
      .put(`/api/users/${testUserId}`)
      .set('Authorization', `Bearer ${authToken}`)
      .send({ name: 'Updated Test User' })
      .expect(200);

    // Delete user
    await request(app)
      .delete(`/api/users/${testUserId}`)
      .set('Authorization', `Bearer ${authToken}`)
      .expect(204);
  });
});
```
{% /accordion %}
{% /tab %}
{% /tabGroup %}

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
{% accordion title="FAQ: Getting Started" description="Basic setup questions" %}
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

{% accordion title="FAQ: Configuration" description="Setup and configuration help" %}
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

{% accordion title="FAQ: Troubleshooting" description="Common issues and solutions" %}
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
{% accordion title="Step 1: Project Setup" description="Initialize your project" defaultOpen=true %}
Start by creating a new project directory and initializing it:

```bash
mkdir my-project
cd my-project
npm init -y
```

This creates the basic project structure you'll need.
{% /accordion %}

{% accordion title="Step 2: Install Dependencies" description="Add required packages" %}
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

{% accordion title="Step 3: Configure Build" description="Set up build process" %}
Create your build configuration:

```json {% filename="webpack.config.js" %}
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

{% accordion title="Step 4: Create Components" description="Build your first components" %}
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

## Configuration Options

{% column cols=2 gap="sm" %}
{% card title="Required Options" %}
- `apiKey`: Your API key
- `baseUrl`: API base URL
{% /card %}

{% card title="Optional Options" %}
- `timeout`: Request timeout (default: 5000ms)
- `retries`: Retry attempts (default: 3)
{% /card %}
{% /column %}
{% /accordion %}

{% accordion title="Examples & Tutorials" description="Step-by-step guides" icon="play" %}
## Basic Usage Tutorial

Follow this tutorial to get started:

{% steps %}
{% step title="Setup" %}
Install and configure the SDK as shown in the SDK Documentation section.
{% /step %}

{% step title="First Request" %}
Make your first API call:

```javascript
const result = await client.api.get('/health');
console.log('API Status:', result.status);
```
{% /step %}

{% step title="Handle Responses" %}
Process the API response data according to your needs.
{% /step %}
{% /steps %}

## Advanced Examples

{% expand title="Error Handling" %}
```javascript {% title="Robust Error Handling" highlight="3-5,8-10" %}
try {
  const data = await client.users.create(userData);
} catch (error) {
  if (error.status === 409) {
    console.log('User already exists');
  } else {
    console.error('Unexpected error:', error.message);
  }
}
```
{% /expand %}
{% /accordion %}
{% /accordionGroup %}

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

{% callout type="tip" %}
Use expand components to keep your documentation clean while providing access to detailed information when needed.
{% /callout %}
{% /expand %}

---

---

# Complex Nested Examples

{% column cols=2 gap="md" %}

{% accordion title="Accordion in Column" description="Testing nested components" %}
This accordion is inside a column layout.

{% callout type="success" %}
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

{% card title="Interactive Card in Column" description="Card with link in column layout" href="/learn-more" icon="arrow-right" %}
This card is in the same column as the accordion above and includes a link.

## Heading in Card
Cards support rich content and can be interactive.

{% expand title="Additional Details" %}
This expand component is nested inside a card to test nested rendering.

{% callout type="info" %}
Expand components work great inside cards for optional details.
{% /callout %}
{% /expand %}

Content after a break inside the card.
{% /card %}

{% /column %}

## All Callout Types in Columns

{% column cols=2 gap="sm" %}

{% callout type="info" %}
Info callout in left column
{% /callout %}

{% callout type="warning" %}
Warning callout in right column
{% /callout %}

{% callout type="error" %}
Error callout in left column
{% /callout %}

{% callout type="success" %}
Success callout in right column
{% /callout %}

{% callout type="tip" %}
Tip callout in left column
{% /callout %}

{% callout type="danger" %}
Danger callout in right column
{% /callout %}

{% /column %}

---

# Final Comprehensive Test

{% column cols=1 %}

{% card title="Everything Combined" description="Testing all features together" horizontal=true href="/complete-guide" icon="book-open" %}

## Card Content with Everything

{% accordion title="Accordion Inside Card" defaultOpen=true %}
This tests accordion inside card functionality with the new horizontal layout.

{% callout type="tip" %}
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
- ✅ **Card tags** (all attributes: title, description, icon, showIcon, horizontal, href)
- ✅ **Column tags** (1, 2, 3 columns with different gaps)
- ✅ **Accordion tags** (all attributes: title, description, defaultOpen, icon, showIcon, className)
- ✅ **AccordionGroup tags** (default behavior, exclusive mode, custom className)
- ✅ **Expand tags** (default closed, default open, custom titles)
- ✅ **Steps tags** (step-by-step instructions container)
- ✅ **Step tags** (individual steps with titles and rich content)
- ✅ **CodeGroup tags** (container for multiple fence blocks, title)
- ✅ **Field tags** (all attributes: name, type, default, required, deprecated, with rich content including paragraphs, headings, code blocks, lists, and nested fields)
- ✅ **Tooltip tags** (tip attribute for contextual help and explanations)
- ✅ **TabGroup tags** (container for tab components with optional className)
- ✅ **Tab tags** (individual tabs with required title and optional className, containing rich content)
- ✅ **Card link functionality** (internal links, external links, CTA text, arrows)
- ✅ **Card layout options** (horizontal vs vertical layouts)
- ✅ **Code fence variations** (different languages, with/without line numbers, icons, content, info attributes)
- ✅ **Line highlighting** (single lines, ranges, mixed patterns)
- ✅ **Steps workflow patterns** (basic steps, advanced with rich content, minimal steps)
- ✅ **Field patterns** (basic fields, default values, deprecated fields, rich content with nested components, API documentation structure)
- ✅ **Tooltip usage patterns** (inline explanations, technical terms, contextual help)
- ✅ **Tab organization patterns** (code examples, API documentation, frontend/backend separation, testing documentation)
- ✅ **Complex nesting** (accordions in cards in columns, codeGroups in accordions, expand in cards, steps with nested components, fields with nested fields, tooltips in content, tabs with all component types)
- ✅ **All attribute combinations** (defaults and custom values)