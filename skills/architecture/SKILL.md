---
name: system-architecture-design
description: Master system design principles, architectural patterns, scalability, design patterns, and enterprise architecture. Build systems that handle millions of users.
---

# System Architecture & Design

## Quick Start

### Load Balancing Architecture
```
                    ┌─────────────────┐
                    │   Load Balancer │
                    │  (Round-Robin)  │
                    └────────┬────────┘
                             │
          ┌──────────────────┼──────────────────┐
          ▼                  ▼                  ▼
      ┌────────┐         ┌────────┐         ┌────────┐
      │ Server │         │ Server │         │ Server │
      │   1    │         │   2    │         │   3    │
      └────┬───┘         └────┬───┘         └────┬───┘
           │                  │                  │
           └──────────────────┼──────────────────┘
                              │
                    ┌─────────▼────────┐
                    │ Database Master  │
                    └─────────┬────────┘
                              │
               ┌──────────────┼──────────────┐
               ▼              ▼              ▼
            ┌─────┐       ┌─────┐       ┌─────┐
            │Read │       │Read │       │Read │
            │Rep1 │       │Rep2 │       │Rep3 │
            └─────┘       └─────┘       └─────┘
```

## Architectural Styles

### Monolithic Architecture
- Single codebase
- Shared database
- Unified deployment
- Advantages: Simple development, debugging
- Disadvantages: Scaling limitations, tight coupling
- Best for: Small to medium teams, startups

### Microservices Architecture
- Independent services
- Separate databases
- Distributed deployment
- Advantages: Independent scaling, technology diversity
- Disadvantages: Operational complexity, distributed transactions
- Best for: Large teams, complex systems

### Serverless Architecture
- Function-as-a-Service (FaaS)
- Event-driven
- Auto-scaling
- Advantages: No server management, pay-per-use
- Disadvantages: Cold starts, vendor lock-in
- Best for: Event-driven workloads, APIs

### Event-Driven Architecture
- Event producers and consumers
- Asynchronous communication
- Event sourcing: Store all changes as events
- CQRS: Separate read and write models
- Advantages: Decoupling, audit trail
- Disadvantages: Complexity, eventual consistency

## Design Patterns

### Creational Patterns
- **Singleton**: Single instance of a class
- **Factory**: Creating objects without specifying classes
- **Builder**: Constructing complex objects step-by-step
- **Prototype**: Cloning objects
- **Abstract Factory**: Family of related objects

### Structural Patterns
- **Adapter**: Making incompatible interfaces work
- **Bridge**: Decoupling abstraction from implementation
- **Composite**: Tree structures
- **Decorator**: Adding behavior dynamically
- **Facade**: Simplified interface to complex subsystem
- **Proxy**: Placeholder for another object

### Behavioral Patterns
- **Observer**: One-to-many dependencies
- **Strategy**: Selecting algorithms at runtime
- **Command**: Encapsulating requests as objects
- **State**: Different behavior based on state
- **Template Method**: Algorithm skeleton
- **Visitor**: Adding operations to objects

## System Design Fundamentals

### Scalability

#### Horizontal Scaling
- Adding more servers
- Load balancing
- Database replication
- Stateless design
- Session management

#### Vertical Scaling
- Bigger server resources
- Limitations (max hardware)
- Simpler initially
- Not future-proof

### Availability

#### Redundancy
- Multiple instances
- Failover mechanisms
- Health checks
- Heartbeat detection

#### SLA: Service Level Agreement
- 99.9% uptime (8.76 hours downtime/year)
- 99.99% uptime (52.56 minutes downtime/year)
- 99.999% uptime (5.26 minutes downtime/year)

### Consistency Models

#### ACID (Traditional Databases)
- **A**tomicity: All or nothing
- **C**onsistency: Valid state transition
- **I**solation: Concurrent safety
- **D**urability: Persisted on failure

#### BASE (Distributed Systems)
- **B**asically Available
- **S**oft state (might change)
- **E**ventually consistent

#### CAP Theorem
- Can't have all three simultaneously:
  - Consistency (C)
  - Availability (A)
  - Partition tolerance (P)

### Caching Strategies

#### Cache-Aside Pattern
```
if key in cache:
  return cache[key]
else:
  value = db.get(key)
  cache.set(key, value)
  return value
```

#### Write-Through Pattern
```
cache.set(key, value)
db.set(key, value)
```

#### Write-Behind Pattern
```
cache.set(key, value)
queue.push({ key, value })
// Background worker updates DB
```

## Database Scaling

### Sharding
```
User ID 1-1000000   → Shard 1
User ID 1000001+    → Shard 2
Geography-based     → Regional shards
```

- Horizontal partitioning
- Shard key selection critical
- Hot spot handling
- Cross-shard queries

### Replication
- Primary-replica setup
- Read replicas for scaling reads
- Write to primary, read from replicas
- Eventual consistency
- Failover handling

### Connection Pooling
- Reuse connections
- Reduce overhead
- Limit concurrent connections
- Better resource utilization

## API Design

### RESTful API Principles
- Resource-based URLs
- HTTP methods (GET, POST, PUT, DELETE)
- Stateless design
- Cacheable responses
- Standard status codes
- Versioning strategies

### Rate Limiting
```
- Token bucket algorithm
- Sliding window
- Rate limit headers
- Throttling strategies
- Per-user limits
- Per-IP limits
```

### Pagination
```
/api/items?page=2&limit=20
/api/items?cursor=abc123&limit=20
/api/items?offset=40&limit=20
```

## Monitoring & Observability

### Key Metrics
- **Latency**: Response time (p50, p95, p99)
- **Throughput**: Requests per second
- **Error Rate**: Failed requests %
- **Resource Utilization**: CPU, memory, disk
- **Business Metrics**: Conversion rate, revenue

### Three Pillars of Observability
- **Logs**: Detailed event records
- **Metrics**: Quantitative measurements
- **Traces**: Request flow through system

### Alerting
- Threshold-based alerts
- Anomaly detection
- On-call rotations
- Escalation policies

## Security Architecture

### Defense in Depth
- Multiple security layers
- API authentication (JWT, OAuth2)
- Rate limiting
- Input validation
- Encryption (TLS, data-at-rest)
- Network segmentation

### Authentication & Authorization
- JWT tokens
- OAuth2 flows
- RBAC (Role-Based Access Control)
- ABAC (Attribute-Based Access Control)
- MFA (Multi-Factor Authentication)

## Common System Design Problems

### E-commerce Platform (1M users)
- Product catalog: Cache + CDN
- Inventory: Real-time, database with versioning
- Orders: Event-driven, idempotency
- Payments: Third-party integration
- Search: Elasticsearch
- Recommendations: ML service

### Social Media Feed (100M users)
- User graph: Graph database
- Feed generation: Pre-computation, caching
- Real-time updates: WebSockets, message queue
- Media storage: Blob storage + CDN
- Analytics: Data warehouse

### Chat Application
- Messages: Persistent queue
- Real-time delivery: WebSockets
- User presence: Cache (Redis)
- Notifications: Push service
- Message history: Database

## Best Practices

✅ Start simple, add complexity when needed
✅ Use load testing to identify bottlenecks
✅ Monitor everything
✅ Plan for scale early
✅ Use CDN for static assets
✅ Cache strategically
✅ Design for failure
✅ Use async processing where possible
✅ Automate deployment and scaling
✅ Plan for disaster recovery

❌ Don't optimize prematurely
❌ Don't skip monitoring
❌ Don't ignore security
❌ Don't trust single points of failure
❌ Don't forget about data migration
❌ Don't design without considering ops
❌ Don't ignore cost implications

## Related Skills
- Microservices Architecture
- Database Design
- DevOps & Infrastructure

## Next Steps
Study system design interview questions, design real-world systems, and understand tradeoffs.
