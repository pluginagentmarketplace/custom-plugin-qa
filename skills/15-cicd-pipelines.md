---
name: cicd-pipeline-implementation
description: Master CI/CD pipeline design, test integration, GitHub Actions, Jenkins, and continuous testing automation.
---

# CI/CD Pipeline Implementation

## GitHub Actions

```yaml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm install
      - run: npm test
      - run: npm run e2e
```

## Jenkins

```groovy
pipeline {
  agent any
  stages {
    stage('Test') {
      steps { sh 'npm test' }
    }
    stage('E2E') {
      steps { sh 'npm run e2e' }
    }
  }
}
```

## Best Practices

✅ Fast feedback
✅ Parallel execution
✅ Clear reporting
✅ Failure handling
