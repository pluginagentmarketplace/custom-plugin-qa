---
name: api-testing
description: Master REST API testing, GraphQL testing, request/response validation, API automation.
---

# API Testing & Validation

## Quick Start - Supertest

```javascript
const request = require('supertest');
const app = require('./app');

describe('GET /api/users', () => {
  it('should return all users', async () => {
    const res = await request(app)
      .get('/api/users')
      .expect(200)
      .expect('Content-Type', /json/);

    expect(Array.isArray(res.body)).toBe(true);
  });
});
```

## API Testing Tools

### REST API
- **Postman**: GUI + automation
- **REST Assured**: Java API testing
- **Supertest**: Node.js testing
- **Pytest + requests**: Python testing

### GraphQL
- Apollo Client testing
- GraphQL query validation
- Schema compliance testing

## Testing Aspects

### Request Validation
- Method correctness (GET, POST, etc)
- Headers validation
- Parameter validation
- Request body structure

### Response Validation
- Status codes (200, 201, 400, 404, 500)
- Response schema
- Data types
- Field presence
- Error messages

### Integration
- Database state
- External service calls
- Message queue events
- Cache behavior

## Best Practices

✅ Test critical paths
✅ Validate status codes
✅ Check response schema
✅ Mock external services
✅ Use test data builders
✅ Parallel execution
✅ Document API changes
✅ Monitor API performance

## Related Skills
- Integration & E2E Testing
- Test Automation & CI/CD
