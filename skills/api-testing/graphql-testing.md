---
name: graphql-api-testing
description: Master GraphQL API testing, queries, mutations, subscriptions, and GraphQL-specific validation.
---

# GraphQL API Testing

## GraphQL Basics

```graphql
# Query
query GetUser {
  user(id: "1") {
    id
    name
    email
  }
}

# Mutation
mutation CreateUser {
  createUser(input: {name: "John", email: "john@example.com"}) {
    id
    name
    email
  }
}
```

## GraphQL Testing

✅ Valid queries
✅ Invalid queries
✅ Mutation testing
✅ Subscription testing
✅ Error handling
✅ Authorization
✅ Performance

## Tools

- GraphQL Playground
- Insomnia
- Postman (with GraphQL support)
- Apollo Client Testing

## Best Practices

✅ Test schema validation
✅ Query response format
✅ Error messages
✅ Mutation side-effects
✅ Performance optimization
