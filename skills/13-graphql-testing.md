---
name: graphql-api-testing-queries
description: Master GraphQL API testing, queries, mutations, subscriptions, and GraphQL-specific validation strategies.
---

# GraphQL API Testing

## GraphQL Queries

```graphql
query GetUser {
  user(id: "1") {
    id
    name
    email
  }
}
```

## Mutations

```graphql
mutation CreateUser {
  createUser(input: {name: "John"}) {
    id
    name
  }
}
```

## Validation

✅ Schema validation
✅ Query response
✅ Mutation effects
✅ Error handling
✅ Performance

## Tools

- Apollo Client
- Insomnia
- Postman
