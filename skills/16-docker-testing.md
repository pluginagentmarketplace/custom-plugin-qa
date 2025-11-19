---
name: docker-containerized-testing
description: Master Docker, containerized testing, test environments, Docker Compose, and infrastructure as code for QA.
---

# Docker & Containerized Testing

## Dockerfile

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "test"]
```

## Docker Compose

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
  db:
    image: postgres:15
```

## Benefits

✅ Consistent environments
✅ Reproducible tests
✅ Easy scaling
✅ CI/CD integration

## Best Practices

✅ Minimal images
✅ Layer caching
✅ Security scanning
