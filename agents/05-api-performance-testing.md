---
description: Master REST/GraphQL API testing, API automation, performance testing, load testing, and performance optimization. Ensure backend reliability, scalability, and speed.
capabilities:
  - REST API testing with Postman/REST Assured
  - GraphQL API testing and validation
  - API automation and CI/CD integration
  - Performance testing fundamentals
  - Load testing (JMeter, k6, Gatling)
  - Stress & spike testing
  - Bottleneck identification and optimization
  - Performance metrics analysis
  - Monitoring and alerting setup
  - Performance baseline establishment
---

# API & Performance Testing - Complete Guide

## Overview

API and performance testing are critical for modern applications. This agent guides you through comprehensive API validation, automation, and performance testing that ensures reliability and speed.

## Part 1: REST API Testing

### REST API Fundamentals

**HTTP Methods**:
```
GET     - Retrieve resource (safe, idempotent)
POST    - Create resource (not idempotent)
PUT     - Replace entire resource (idempotent)
PATCH   - Partial update (idempotent)
DELETE  - Remove resource (idempotent)
HEAD    - Like GET, no response body
OPTIONS - Describe communication options
```

**HTTP Status Codes**:
```
1xx - Information
2xx - Success
  200 OK
  201 Created
  204 No Content

3xx - Redirection
  301 Moved Permanently
  304 Not Modified
  307 Temporary Redirect

4xx - Client Error
  400 Bad Request
  401 Unauthorized
  403 Forbidden
  404 Not Found
  409 Conflict
  422 Unprocessable Entity

5xx - Server Error
  500 Internal Server Error
  502 Bad Gateway
  503 Service Unavailable
```

### API Testing with REST Assured (Java)

```java
// Basic GET request
@Test
public void testGetUser() {
  given()
    .baseUri("https://api.example.com")
    .basePath("/api/users")
    .when()
      .get("/{id}")
      .pathParam("id", 1)
    .then()
      .statusCode(200)
      .body("id", equalTo(1))
      .body("name", notNullValue());
}

// POST with request body
@Test
public void testCreateUser() {
  String requestBody = """
    {
      "name": "John",
      "email": "john@example.com",
      "age": 30
    }
  """;

  given()
    .contentType(ContentType.JSON)
    .body(requestBody)
    .when()
      .post("/users")
    .then()
      .statusCode(201)
      .body("id", notNullValue());
}

// Authentication
@Test
public void testWithAuthentication() {
  given()
    .auth()
      .basic("username", "password")
    .when()
      .get("/protected")
    .then()
      .statusCode(200);
}

// Complex assertions
@Test
public void testComplexResponse() {
  given()
    .when()
      .get("/users")
    .then()
      .statusCode(200)
      .body("data", hasSize(greaterThan(0)))
      .body("data[0].email", matchesPattern("[a-z0-9._%+-]+@[a-z0-9.-]+\\.[a-z]{2,}"))
      .body("pagination.total", greaterThan(100))
      .time(lessThan(2000L), TimeUnit.MILLISECONDS);
}
```

### Postman API Testing

```json
// Postman Pre-request Script
const baseUrl = pm.environment.get("baseUrl");
const authToken = pm.variables.get("authToken");

pm.request.headers.add({
  "Authorization": `Bearer ${authToken}`,
  "Content-Type": "application/json"
});

// Postman Test Script
pm.test("Status code is 200", () => {
  pm.response.to.have.status(200);
});

pm.test("Response time is less than 2 seconds", () => {
  pm.expect(pm.response.responseTime).to.be.below(2000);
});

pm.test("Response body structure is valid", () => {
  const jsonData = pm.response.json();
  pm.expect(jsonData).to.have.property("id");
  pm.expect(jsonData).to.have.property("email");
});

// Extract value for next request
const responseData = pm.response.json();
pm.environment.set("userId", responseData.id);
```

### API Test Design Patterns

```
POSITIVE TESTS (Happy Path):
- Valid request → Valid response
- Correct status code
- Expected data in response
- Proper response format

NEGATIVE TESTS (Error Handling):
- Missing required fields → 400
- Invalid data type → 400
- Unauthorized access → 401
- Forbidden action → 403
- Resource not found → 404
- Duplicate resource → 409
- Invalid input → 422

EDGE CASES:
- Empty request body
- Very large payloads
- Special characters
- Unicode characters
- Null values
- Boundary values
```

## Part 2: GraphQL API Testing

### GraphQL Fundamentals

```graphql
// Query example
query GetUser {
  user(id: 1) {
    id
    name
    email
    posts {
      id
      title
    }
  }
}

// Mutation example
mutation CreateUser {
  createUser(input: {
    name: "John"
    email: "john@example.com"
  }) {
    id
    name
    email
  }
}
```

### GraphQL Testing with REST Assured

```java
@Test
public void testGraphQLQuery() {
  String graphQLQuery = """
    query {
      user(id: 1) {
        id
        name
        email
      }
    }
  """;

  given()
    .contentType(ContentType.JSON)
    .body(Map.of("query", graphQLQuery))
    .when()
      .post("/graphql")
    .then()
      .statusCode(200)
      .body("data.user.id", notNullValue())
      .body("data.user.name", equalTo("John"))
      .body("errors", empty());
}
```

## Part 3: API Automation

### API Test Framework Architecture

```
tests/
├── api/
│   ├── endpoints/
│   │   ├── UserEndpoint.java
│   │   ├── ProductEndpoint.java
│   │   └── OrderEndpoint.java
│   ├── models/
│   │   ├── User.java
│   │   ├── Product.java
│   │   └── Order.java
│   ├── tests/
│   │   ├── UserAPITest.java
│   │   ├── ProductAPITest.java
│   │   └── OrderAPITest.java
│   └── utils/
│       ├── APIClient.java
│       └── TestDataFactory.java
```

### API Client Implementation

```java
public class APIClient {
  private static final String BASE_URL = "https://api.example.com";
  private static final int TIMEOUT = 10;
  private String authToken;

  public APIClient withAuth(String token) {
    this.authToken = token;
    return this;
  }

  public Response get(String endpoint) {
    return given()
      .baseUri(BASE_URL)
      .auth()
        .oauth2(authToken)
      .when()
        .get(endpoint)
      .then()
        .extract()
        .response();
  }

  public Response post(String endpoint, Object body) {
    return given()
      .baseUri(BASE_URL)
      .contentType(ContentType.JSON)
      .auth()
        .oauth2(authToken)
      .body(body)
      .when()
        .post(endpoint)
      .then()
        .extract()
        .response();
  }
}

// Usage
@Test
public void testUserAPI() {
  APIClient client = new APIClient().withAuth("token123");

  User user = new User("John", "john@example.com");
  Response createResponse = client.post("/users", user);

  assertThat(createResponse.getStatusCode()).isEqualTo(201);

  String userId = createResponse.jsonPath().getString("id");
  Response getResponse = client.get("/users/" + userId);

  assertThat(getResponse.getStatusCode()).isEqualTo(200);
}
```

## Part 4: Performance Testing

### Performance Testing Types

```
LOAD TESTING:
- Normal user load
- Baseline performance
- Identify bottlenecks
- Measure response times
- Verify throughput

STRESS TESTING:
- Exceed normal capacity
- Find breaking point
- Identify failure modes
- Test recovery

SPIKE TESTING:
- Sudden traffic increase
- System response
- Resource management
- Recovery time

SOAK TESTING:
- Sustained load
- Memory leaks
- Stability over time
- Resource degradation
```

### JMeter Performance Testing

```
// Test Plan Structure
Test Plan
├── Thread Group (Users: 100, Ramp-up: 60s, Loop: 10)
├── HTTP Request Sampler
│   └── GET /api/users
├── HTTP Request Sampler
│   └── POST /api/users
├── Response Assertions
│   └── Status code = 200
├── View Results Tree (Listener)
├── Summary Report (Listener)
└── Aggregate Graph (Listener)
```

### k6 Performance Testing

```javascript
import http from 'k6/http';
import { check, group, sleep } from 'k6';
import { Rate, Trend } from 'k6/metrics';

// Custom metrics
export const errorRate = new Rate('errors');
export const responseTime = new Trend('response_time');

// Test configuration
export const options = {
  vus: 100,              // Virtual users
  duration: '5m',        // Test duration
  thresholds: {
    http_req_duration: ['p(95)<500', 'p(99)<1000'],
    errors: ['rate<0.1'],
  },
  stages: [
    { duration: '1m', target: 50 },   // Ramp-up
    { duration: '3m', target: 100 },  // Sustain
    { duration: '1m', target: 0 },    // Ramp-down
  ],
};

export default function () {
  group('Load Testing', () => {
    // Test 1: GET request
    const getResponse = http.get('https://api.example.com/users');
    check(getResponse, {
      'status is 200': (r) => r.status === 200,
      'response time < 500ms': (r) => r.timings.duration < 500,
    });
    errorRate.add(getResponse.status !== 200);
    responseTime.add(getResponse.timings.duration);

    // Test 2: POST request
    const postResponse = http.post('https://api.example.com/users', {
      name: 'Test User',
      email: 'test@example.com',
    });
    check(postResponse, {
      'status is 201': (r) => r.status === 201,
    });

    sleep(1);
  });
}
```

## Part 5: Performance Metrics & Analysis

### Key Performance Indicators

```
RESPONSE TIME:
- Min: Minimum response time
- Max: Maximum response time
- Avg: Average response time
- P50 (Median): 50th percentile
- P95: 95th percentile (most users experience)
- P99: 99th percentile (worst case)

THROUGHPUT:
- Requests per second (RPS)
- Transactions per second (TPS)
- Bytes per second

RESOURCE UTILIZATION:
- CPU usage
- Memory usage
- Disk I/O
- Network bandwidth

ERROR RATES:
- HTTP errors (4xx, 5xx)
- Timeouts
- Connection errors
- Assertion failures
```

### Performance Benchmarks

```
ACCEPTABLE THRESHOLDS:
Web API Response Time:
- P50: < 200ms
- P95: < 500ms
- P99: < 1000ms

Throughput:
- Min: 100 RPS
- Target: 500+ RPS

Error Rate:
- Target: < 0.1%

Connection Time:
- Target: < 50ms
```

## Part 6: Performance Optimization

### Common Bottlenecks

```
DATABASE OPTIMIZATION:
- Add indexes
- Optimize queries
- Connection pooling
- Caching

API OPTIMIZATION:
- Pagination for large datasets
- Compression (gzip)
- Caching headers
- Reduce payload size
- Lazy loading
- Batch operations

INFRASTRUCTURE:
- Load balancing
- Horizontal scaling
- CDN for static content
- Database replication
```

## Part 7: Performance Best Practices

```
✅ DO:
- Define performance requirements upfront
- Establish baseline metrics
- Test with realistic data volume
- Test with realistic user load
- Monitor system resources
- Identify bottlenecks early
- Create performance regression tests
- Document performance targets
- Review performance trends
- Regular performance testing

❌ DON'T:
- Test with tiny datasets
- Use synthetic data
- Test on development machines
- Ignore performance metrics
- Skip performance testing
- Test only happy path
- Use single-threaded testing
- Ignore third-party services
```

## Part 8: Common Pitfalls & Solutions

### Pitfall 1: Unrealistic Test Scenarios
**Problem**: Tests don't reflect real usage
**Solution**: Use real data, realistic load patterns
**Impact**: Accurate performance insights

### Pitfall 2: Ignoring Think Time
**Problem**: Unrealistic rapid requests
**Solution**: Add realistic delays between requests
**Impact**: More realistic results

### Pitfall 3: Test Environment Differences
**Problem**: Performance varies from production
**Solution**: Match production environment closely
**Impact**: Reliable predictions

### Pitfall 4: No Baseline Metrics
**Problem**: Can't measure improvement
**Solution**: Establish baseline before optimization
**Impact**: Clear measurement of impact

## Success Stories

### Example 1: Database Query Optimization
**Problem**: API response time 3000ms
**Approach**: Added index to slow query
**Result**: 90% improvement (300ms)

### Example 2: Load Testing Discovery
**Problem**: System crashes under load
**Approach**: Load test identified memory leak
**Result**: Fixed before production

### Example 3: Performance Regression
**Problem**: Performance degraded silently
**Approach**: Automated performance regression tests
**Result**: Caught issues immediately

## When to Use This Agent

- API testing needed
- Performance validation required
- Load testing planning
- Bottleneck analysis needed
- Performance optimization
- Backend testing

## Key Takeaways

🎯 API testing is essential for backend reliability
🎯 Automate API tests in CI/CD pipeline
🎯 Performance testing prevents production issues
🎯 Establish baselines before optimization
🎯 Monitor real-time performance metrics
🎯 Use realistic test data and scenarios
🎯 Performance is non-functional requirement
🎯 Continuous monitoring is critical
