# Data Fetching in Next.js

## Overview

This document covers different approaches to fetching data in Next.js applications and best practices for implementing them.

## Data Fetching Approaches

### API Layer

- Acts as an intermediary between application code and database
- Use cases:
  - When working with third-party services that provide an API
  - When fetching data from the client to avoid exposing database secrets
- Can be implemented using Next.js Route Handlers

### Database Queries

- Direct database interaction for full-stack applications
- Implementation options:
  - SQL queries
  - Object-Relational Mapping (ORM)
- Use cases:
  - When creating API endpoints
  - When using React Server Components (server-side data fetching)

### React Server Components

- Default in Next.js applications
- Benefits:
  - Native support for Promises
  - Simplified async/await syntax without useEffect or useState
  - Server-side execution for expensive operations
  - Direct database querying without API layer
  - Reduced client-side JavaScript

## SQL Implementation

### Benefits

- Industry standard for relational databases
- Provides fundamental database understanding
- Versatile data fetching and manipulation
- Protection against SQL injections (when using Vercel Postgres SDK)

### Usage with Vercel Postgres

```typescript
import { sql } from "@vercel/postgres";

// Example query
const data = await sql`SELECT * FROM table`;
```

## Performance Considerations

### Request Waterfalls

- Definition: Sequential network requests where each request depends on previous ones
- Impact: Can affect application performance
- Valid use cases:
  - When conditional data fetching is required
  - When subsequent requests depend on previous data

### Parallel Data Fetching

- Implementation using Promise.all() or Promise.allSettled()

```typescript
const [data1, data2, data3] = await Promise.all([
  fetchData1(),
  fetchData2(),
  fetchData3(),
]);
```

- Benefits:
  - Improved performance through concurrent requests
  - Native JavaScript pattern
- Considerations:
  - Overall response time depends on slowest request
  - Error handling needs careful consideration

## Best Practices

1. Use Server Components when possible for data fetching
2. Implement parallel data fetching to avoid waterfalls
3. Write specific SQL queries instead of fetching entire datasets
4. Keep database queries in a separate data layer
5. Protect sensitive information by keeping database operations server-side

## Related Concepts

- Static Rendering (default in Next.js)
- Dynamic Rendering
- API Route Handlers
- Database connection management
