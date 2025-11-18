---
name: rest-api-testing
description: Master REST API testing, HTTP methods, response validation, and API test automation.
---

# REST API Testing

## REST API Basics

```bash
# GET request
curl -X GET https://api.example.com/users

# POST request
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -d '{"name":"John"}'

# PUT request
curl -X PUT https://api.example.com/users/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"Jane"}'
```

## API Testing Checklist

✅ HTTP status codes (200, 201, 400, 404, 500)
✅ Response structure
✅ Data types
✅ Field presence
✅ Error messages
✅ Headers
✅ Authentication
✅ Authorization

## API Test Tools

- Postman
- REST Assured (Java)
- Requests (Python)
- Supertest (Node.js)
- Thunder Client (VS Code)

## Best Practices

✅ Test all endpoints
✅ Validate responses
✅ Error handling
✅ Authentication testing
✅ Data validation
✅ Performance checks
