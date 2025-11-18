---
name: test-automation-cicd
description: Master CI/CD integration, GitHub Actions, GitLab CI, Jenkins. Build continuous testing pipelines.
---

# Test Automation & CI/CD

## Quick Start - GitHub Actions

```yaml
name: Test Suite
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm test -- --coverage
      - run: npm run e2e
```

## CI/CD Platforms

### GitHub Actions
- Integrated with GitHub
- Matrix builds
- Secrets management
- Reusable workflows

### GitLab CI
- GitLab-native
- Runners (Docker, Kubernetes)
- Artifact management
- Environment-specific jobs

### Jenkins
- Self-hosted
- Extensive plugins
- Pipeline as Code
- Distributed builds

## Pipeline Stages

### 1. Trigger
- Commit push
- Pull request
- Scheduled runs
- Manual trigger

### 2. Build
- Code compilation
- Dependency resolution
- Artifact creation

### 3. Test
- Unit tests
- Integration tests
- Code quality checks
- Security scanning

### 4. Deploy
- Staging deployment
- Production deployment
- Smoke tests
- Rollback capability

## Best Practices

✅ Fast feedback loop
✅ Parallel execution
✅ Clear failure messages
✅ Artifact management
✅ Environment separation
✅ Deployment automation
✅ Monitoring integration
✅ Documentation

## Test Execution

```
Unit Tests (fast)
↓
Integration Tests
↓
E2E Tests
↓
Performance Tests
↓
Security Tests
```

## Related Skills
- Test Automation & CI/CD
- Quality Metrics & Reporting
