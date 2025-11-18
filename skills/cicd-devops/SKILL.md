---
name: cicd-integration-testing
description: Master CI/CD pipeline design, continuous testing integration, Jenkins, and GitHub Actions.
---

# CI/CD Pipeline Integration

## GitHub Actions Example

```yaml
name: Test Suite
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install
        run: npm install
      - name: Unit Tests
        run: npm test
      - name: E2E Tests
        run: npm run e2e
      - name: Upload Coverage
        uses: codecov/codecov-action@v3
```

## Jenkins Pipeline

```groovy
pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
    stage('E2E') {
      steps {
        sh 'npm run e2e'
      }
    }
    stage('Deploy') {
      steps {
        sh 'npm run deploy'
      }
    }
  }
}
```

## Best Practices

✅ Fast feedback
✅ Parallel execution
✅ Test early
✅ Clear reporting
✅ Fail fast
