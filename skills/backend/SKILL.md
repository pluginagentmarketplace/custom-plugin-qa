---
name: nodejs-express-mastery
description: Master Node.js, Express.js, and backend development. Learn API design, middleware, authentication, async patterns, and building scalable server applications.
---

# Node.js & Express.js Mastery

## Quick Start

Create a basic Express server:

```javascript
const express = require('express');
const app = express();

app.use(express.json());

app.get('/api/users', async (req, res) => {
  try {
    const users = await User.find();
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

## Node.js Fundamentals

### Event-Driven Architecture
- EventEmitter: Core of Node.js
- Streams: Memory-efficient data processing
- Callbacks and error handling
- Promises and async/await
- Event loop understanding

### Module System
- CommonJS vs ES Modules
- require() and import
- Module caching
- Circular dependencies
- npm and package management

### File System & Paths
- Reading and writing files
- Directory operations
- Path manipulation
- Stream processing large files
- File watching

### Asynchronous Patterns
- Callbacks (callback hell)
- Promises and then/catch
- Async/await best practices
- Promise.all and Promise.race
- Error handling in async code
- Concurrency control

## Express.js Framework

### Core Concepts
- Routing and HTTP methods
- Middleware pipeline
- Request/Response objects
- Error handling middleware
- Built-in middleware
- Third-party middleware

### Routing
- Basic routes
- Route parameters and queries
- Regular expressions in routes
- Route chaining
- Modular route files
- Router objects

### Middleware Patterns
```javascript
// Custom middleware
app.use((req, res, next) => {
  req.startTime = Date.now();
  next();
});

// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.message);
  res.status(err.status || 500).json({ error: err.message });
});
```

### Authentication & Authorization
- Session management
- JWT tokens
- OAuth2 implementation
- Role-based access control
- Middleware for auth checks
- Token refresh strategies

### Data Validation
- Input validation libraries (joi, yup)
- Request body validation
- Query parameter validation
- Custom validators
- Error messages
- Validation middleware

### RESTful API Design
- Resource-based URLs
- HTTP methods correctly used
- Status codes (200, 201, 400, 404, 500)
- Request/Response formats
- Pagination strategies
- API versioning

## Database Integration

### ORM/ODM
- Mongoose (MongoDB)
- Sequelize (SQL databases)
- TypeORM
- Prisma
- Query building
- Migrations

### Database Patterns
- Connection pooling
- Transaction handling
- N+1 query prevention
- Eager loading
- Lazy loading
- Caching strategies

## Advanced Topics

### Middleware Ecosystem
- CORS handling
- Request logging (Morgan)
- Rate limiting
- Compression
- Security headers
- Body parsing

### Testing Express APIs
```javascript
const request = require('supertest');
const app = require('./app');

describe('GET /api/users', () => {
  it('should return all users', async () => {
    const res = await request(app).get('/api/users');
    expect(res.status).toBe(200);
    expect(Array.isArray(res.body)).toBe(true);
  });
});
```

### Performance Optimization
- Response compression
- Caching strategies
- Connection pooling
- Query optimization
- Pagination
- Lazy loading

### Security Best Practices
- Input validation
- SQL injection prevention
- XSS protection
- CSRF tokens
- Rate limiting
- Authentication/Authorization
- HTTPS/TLS
- Environment variables

### Error Handling Strategy
- Try-catch blocks
- Error middleware
- Custom error classes
- Error logging
- User-friendly messages
- Stack traces in development

## GraphQL with Node.js

### Apollo Server
- Schema definition
- Resolvers
- Query and Mutation
- Subscriptions
- Middleware
- Authentication

### Query Optimization
- Data loaders
- N+1 prevention
- Caching
- Query complexity analysis

## Real-Time Applications

### WebSockets with Socket.io
- Connection management
- Broadcasting events
- Rooms and namespaces
- Binary data
- Acknowledgments
- Reconnection handling

## Deployment & DevOps

### Process Management
- PM2: Production process manager
- Forever: Node.js monitoring
- StrongLoop Process Manager
- Docker containerization

### Environment Configuration
- .env files
- Environment-specific configs
- Secrets management
- Feature flags

## Best Practices

✅ Use async/await for clarity
✅ Handle errors properly
✅ Validate all inputs
✅ Use middleware for cross-cutting concerns
✅ Structure code into modules
✅ Use environment variables
✅ Implement proper logging
✅ Write comprehensive tests
✅ Use rate limiting
✅ Secure sensitive data

❌ Don't ignore errors
❌ Don't hardcode secrets
❌ Don't trust user input
❌ Don't create synchronous blocking operations
❌ Don't write endpoints without authentication
❌ Don't skip validation
❌ Don't use deprecated packages

## Related Skills
- System Architecture
- Database Design
- Testing Frameworks
- Security

## Next Steps
Build production-ready APIs, master async patterns, and deploy to cloud platforms.
