---
name: sql-nosql-databases
description: Master SQL databases (PostgreSQL, MySQL), NoSQL solutions (MongoDB), data modeling, query optimization, indexing, and scaling strategies.
---

# SQL & NoSQL Databases

## Quick Start

### SQL Query Basics
```sql
-- Create table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Query with JOIN
SELECT u.id, u.email, COUNT(o.id) as order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id
ORDER BY order_count DESC;

-- Create index
CREATE INDEX idx_users_email ON users(email);
```

### MongoDB Basics
```javascript
// Insert document
db.users.insertOne({
  email: 'user@example.com',
  profile: { name: 'John' },
  createdAt: new Date()
});

// Query with aggregation
db.users.aggregate([
  { $match: { status: 'active' } },
  { $group: { _id: '$category', count: { $sum: 1 } } },
  { $sort: { count: -1 } }
]);
```

## SQL Databases

### PostgreSQL Deep Dive
- Advanced data types (JSON, Arrays, UUID)
- Window functions
- Common Table Expressions (CTE)
- Recursive queries
- Full-text search
- PostGIS for geospatial data

### MySQL & MariaDB
- InnoDB vs MyISAM storage engines
- Query optimization
- Replication and clustering
- Partitioning
- Security and privileges

### Schema Design

#### Normalization
- First Normal Form (1NF)
- Second Normal Form (2NF)
- Third Normal Form (3NF)
- Boyce-Codd Normal Form (BCNF)
- Denormalization trade-offs

#### Keys & Relationships
- Primary keys
- Foreign keys
- Unique constraints
- Check constraints
- One-to-many relationships
- Many-to-many relationships
- Self-referencing relationships

#### Indexing Strategies
- B-tree indexes
- Hash indexes
- Full-text indexes
- Partial indexes
- Multi-column indexes
- Index selectivity
- When to index vs denormalize

### Query Optimization

#### EXPLAIN ANALYSIS
```sql
EXPLAIN ANALYZE
SELECT * FROM orders
WHERE customer_id = 123
  AND order_date > '2024-01-01';
```

#### Optimization Techniques
- Index selection
- Join ordering
- Query rewriting
- Caching strategies
- Materialized views
- Query statistics

### Transactions & ACID
- Isolation levels (READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE)
- Locking mechanisms
- Deadlock handling
- Rollback strategies
- Transaction logging

## NoSQL Databases

### MongoDB

#### Data Modeling
- Document structure
- Embedded documents
- References between collections
- Denormalization strategies
- Array fields
- Schema validation

#### CRUD Operations
```javascript
// Create
db.products.insertMany([{...}, {...}]);

// Read
db.products.find({ price: { $gt: 100 } });

// Update
db.products.updateOne(
  { _id: id },
  { $set: { price: newPrice } }
);

// Delete
db.products.deleteOne({ _id: id });
```

#### Aggregation Pipeline
- $match: Filtering
- $group: Aggregation
- $project: Reshaping
- $sort: Ordering
- $limit: Pagination
- $lookup: Joins
- $unwind: Array expansion

#### Indexing
- Single field indexes
- Compound indexes
- Text indexes
- Geospatial indexes
- TTL indexes (auto-expiry)

#### Transactions
- ACID transactions (4.0+)
- Multi-document transactions
- Rollback mechanisms

### Other NoSQL Solutions
- **Cassandra**: Distributed, high availability
- **DynamoDB**: AWS managed, scalable
- **Firebase**: Real-time, serverless
- **Redis**: In-memory, cache, sessions

## Caching Strategies

### Redis
```javascript
// Basic operations
client.set('key', 'value', 'EX', 3600);
const value = client.get('key');

// Caching patterns
const data = await cache.get('users:123');
if (!data) {
  const data = await db.users.findById(123);
  await cache.set('users:123', JSON.stringify(data), 3600);
}
```

### Cache Invalidation
- Time-based expiration
- Event-based invalidation
- LRU (Least Recently Used) eviction
- Versioning strategies
- Cache-aside pattern
- Write-through pattern
- Write-behind pattern

## Data Scaling

### Sharding
- Hash-based sharding
- Range-based sharding
- Geographic sharding
- Shard key selection
- Hot spot handling

### Replication
- Primary-replica replication
- Multi-replica setups
- Read replicas for scaling
- Consistency considerations
- Failover handling

### Backup & Recovery
- Point-in-time recovery
- Backup strategies
- Disaster recovery planning
- RTO & RPO
- Archive strategies

## Query Patterns

### Pagination
```sql
-- SQL
SELECT * FROM users
LIMIT 10 OFFSET 20;

-- MongoDB
db.users.find().skip(20).limit(10);
```

### Full-Text Search
```sql
SELECT * FROM articles
WHERE to_tsvector('english', content) @@
      to_tsquery('english', 'database & performance');
```

### Aggregations
```sql
SELECT
  DATE_TRUNC('month', created_at) as month,
  COUNT(*) as total,
  AVG(amount) as avg_amount
FROM transactions
GROUP BY month
ORDER BY month DESC;
```

## Performance Monitoring

### Query Performance
- Query execution time
- Index usage
- Sequential scans
- Query plans
- Slow query logging

### Metrics
- Queries per second (QPS)
- Latency percentiles (p50, p95, p99)
- Cache hit ratio
- Connection pool utilization
- Disk I/O

## Best Practices

✅ Design schemas carefully
✅ Use appropriate indexes
✅ Normalize when appropriate
✅ Monitor query performance
✅ Implement caching
✅ Use connection pooling
✅ Regular backups
✅ Plan for scaling
✅ Use transactions for consistency
✅ Validate data integrity

❌ Don't over-normalize
❌ Don't create too many indexes
❌ Don't ignore query plans
❌ Don't hardcode connection strings
❌ Don't skip backups
❌ Don't trust user input
❌ Don't use SELECT *

## Related Skills
- System Architecture
- Backend Development
- DevOps & Infrastructure

## Next Steps
Master query optimization, implement caching strategies, and design scalable databases.
