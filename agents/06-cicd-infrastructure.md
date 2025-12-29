---
name: 06-cicd-infrastructure
description: Master CI/CD pipelines, continuous testing, Jenkins, GitHub Actions, Docker, and test infrastructure. Design robust, scalable, fast testing infrastructure.
model: sonnet
tools: All tools
sasmp_version: "1.3.0"
eqhm_enabled: true
---

# CI/CD & Test Infrastructure - Complete Guide

## Overview

CI/CD is critical for modern QA. This agent guides you through designing, implementing, and optimizing continuous testing infrastructure that provides fast feedback and ensures quality at every commit.

## Part 1: CI/CD Pipeline Design

### CI/CD Pipeline Stages

```
CONTINUOUS INTEGRATION:
Code Commit → Code Review → Build → Unit Tests → Code Analysis

CONTINUOUS TESTING:
Integration Tests → API Tests → UI Tests → Performance Tests

CONTINUOUS DEPLOYMENT:
Deploy to Staging → Smoke Tests → Deploy to Production → Monitoring
```

### Pipeline Architecture

```
git push
   ↓
GitHub Webhook
   ↓
CI/CD Server (Jenkins, GitHub Actions)
   ↓
├── Checkout Code
├── Build Application
├── Run Unit Tests
├── Run Integration Tests
├── Run UI Tests
├── Run Performance Tests
├── Generate Reports
├── Archive Artifacts
└── Trigger Deployment (if pass)
```

### Pipeline Stages Explained

**Stage 1: Code Checkout**
```
- Fetch latest code from repository
- Checkout specific branch/commit
- Prepare workspace
```

**Stage 2: Build**
```
- Compile code
- Resolve dependencies
- Create build artifacts
- Run static analysis (SonarQube)
```

**Stage 3: Unit Testing**
```
- Run unit test suite
- Generate coverage reports
- Analyze coverage metrics
- Fail if coverage below threshold
```

**Stage 4: Integration Testing**
```
- Start test database
- Deploy to test environment
- Run integration tests
- Stop test environment
```

**Stage 5: Automated Testing**
```
- Run API tests
- Run UI tests (Selenium, Cypress, Playwright)
- Run performance tests
- Collect results
```

**Stage 6: Quality Gates**
```
- Verify coverage targets
- Check test pass rate
- Verify performance metrics
- Check code quality
```

**Stage 7: Reporting**
```
- Generate test reports
- Create coverage reports
- Build failure notifications
- Archive artifacts
```

## Part 2: GitHub Actions

### GitHub Actions Setup

**Basic Workflow Structure**:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Set up Java
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Run tests
        run: mvn clean test

      - name: Upload coverage
        uses: codecov/codecov-action@v3
```

### GitHub Actions Workflows

**Full E2E Testing Pipeline**:

```yaml
name: E2E Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:14
        env:
          POSTGRES_PASSWORD: postgres
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - uses: actions/checkout@v3

      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm install

      - name: Run unit tests
        run: npm run test:unit

      - name: Run integration tests
        run: npm run test:integration

      - name: Run E2E tests
        run: npm run test:e2e

      - name: Upload test reports
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: test-reports
          path: reports/

      - name: Publish test results
        if: always()
        uses: EnricoMi/publish-unit-test-result-action@v2
        with:
          files: reports/junit.xml

      - name: Create test report comment
        if: always()
        uses: actions/github-script@v6
        with:
          script: |
            const fs = require('fs');
            const report = JSON.parse(fs.readFileSync('reports/summary.json'));
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: `## Test Results\n- Passed: ${report.passed}\n- Failed: ${report.failed}`
            });
```

## Part 3: Jenkins Pipelines

### Jenkins Setup

**Jenkins Pipeline as Code**:

```groovy
pipeline {
  agent any

  options {
    timeout(time: 1, unit: 'HOURS')
    buildDiscarder(logRotator(numToKeepStr: '10'))
    timestamps()
  }

  parameters {
    string(name: 'ENVIRONMENT', defaultValue: 'staging')
    booleanParam(name: 'RUN_PERFORMANCE_TESTS', defaultValue: false)
  }

  triggers {
    githubPush()
    cron('H H * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean compile'
      }
    }

    stage('Unit Tests') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Integration Tests') {
      steps {
        sh 'mvn integration-test'
      }
    }

    stage('E2E Tests') {
      when {
        branch 'main'
      }
      steps {
        sh 'npm run test:e2e'
      }
    }

    stage('Performance Tests') {
      when {
        expression { params.RUN_PERFORMANCE_TESTS == true }
      }
      steps {
        sh 'k6 run tests/performance/load-test.js'
      }
    }

    stage('Quality Analysis') {
      steps {
        sh 'mvn sonar:sonar'
      }
    }

    stage('Reports') {
      always {
        junit 'target/surefire-reports/**/*.xml'
        publishHTML([
          reportDir: 'target/site/jacoco',
          reportFiles: 'index.html',
          reportName: 'Code Coverage'
        ])
        publishHTML([
          reportDir: 'test-results/html',
          reportFiles: 'index.html',
          reportName: 'Test Report'
        ])
      }
    }

    stage('Deploy') {
      when {
        branch 'main'
      }
      steps {
        sh 'deploy.sh ${ENVIRONMENT}'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'test-results/**', allowEmptyArchive: true
      cleanWs()
    }
    failure {
      emailext(
        to: '${DEFAULT_RECIPIENTS}',
        subject: 'Build Failed: ${BUILD_NUMBER}',
        body: 'Build failed. Check Jenkins for details.',
        attachmentsPattern: 'test-results/**'
      )
    }
    success {
      echo 'Build succeeded!'
    }
  }
}
```

## Part 4: Docker for Testing

### Docker Basics for Testing

```dockerfile
# Dockerfile for test environment
FROM openjdk:17-slim

WORKDIR /app

# Install dependencies
RUN apt-get update && apt-get install -y \
    maven \
    chromium-browser \
    && rm -rf /var/lib/apt/lists/*

# Copy application
COPY . .

# Build application
RUN mvn clean package

# Run tests
CMD ["mvn", "test"]
```

### Docker Compose for Testing Infrastructure

```yaml
version: '3.8'

services:
  # Application under test
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      DATABASE_URL: postgresql://postgres:postgres@db:5432/testdb
    depends_on:
      - db
      - redis
    networks:
      - test-network

  # PostgreSQL database
  db:
    image: postgres:14
    environment:
      POSTGRES_DB: testdb
      POSTGRES_PASSWORD: postgres
    volumes:
      - db_data:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    networks:
      - test-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 10s
      timeout: 5s
      retries: 5

  # Redis cache
  redis:
    image: redis:7
    networks:
      - test-network
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5

  # Selenium Hub for browser testing
  selenium-hub:
    image: selenium/hub:4.0
    ports:
      - "4444:4444"
    networks:
      - test-network

  # Chrome node
  chrome:
    image: selenium/node-chrome:4.0
    depends_on:
      - selenium-hub
    environment:
      SE_EVENT_BUS_HOST: selenium-hub
      SE_EVENT_BUS_PUBLISH_PORT: 4442
      SE_EVENT_BUS_SUBSCRIBE_PORT: 4443
    networks:
      - test-network

volumes:
  db_data:

networks:
  test-network:
    driver: bridge
```

## Part 5: Test Parallelization

### Parallel Test Execution

**JUnit 5 Configuration**:

```properties
# junit-platform.properties
junit.jupiter.execution.parallel.enabled=true
junit.jupiter.execution.parallel.mode.default=concurrent
junit.jupiter.execution.parallel.mode.classes.default=concurrent
junit.jupiter.execution.parallel.strategy=dynamic
junit.jupiter.execution.parallel.max.pool.size=8
junit.jupiter.execution.parallel.min.runnable=8
```

**Maven Configuration**:

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <version>3.0.0</version>
  <configuration>
    <parallel>methods</parallel>
    <threadCount>8</threadCount>
  </configuration>
</plugin>
```

**Cypress Parallel Execution**:

```bash
# Using Cypress Cloud
npx cypress run --record --parallel --ci-build-id=$BUILD_ID

# Using Docker
docker-compose -f docker-compose.yml run \
  --rm cypress npx cypress run --parallel --headless
```

## Part 6: Reporting and Artifacts

### Test Report Integration

```groovy
// Jenkins: Publish test results
stage('Reports') {
  steps {
    junit 'target/surefire-reports/**/*.xml'
    publishHTML([
      reportDir: 'coverage',
      reportFiles: 'index.html',
      reportName: 'Code Coverage'
    ])
  }
}
```

### Custom Report Generation

```java
// Java: Generate test report
public class TestReportGenerator {
  public void generateReport(TestResults results) {
    Map<String, Object> reportData = new HashMap<>();
    reportData.put("totalTests", results.getTotal());
    reportData.put("passedTests", results.getPassed());
    reportData.put("failedTests", results.getFailed());
    reportData.put("passRate", results.getPassRate());
    reportData.put("executionTime", results.getExecutionTime());

    generateHTML(reportData);
    generateJSON(reportData);
    sendNotification(reportData);
  }
}
```

## Part 7: Monitoring and Alerting

### Pipeline Metrics

```
- Build duration trend
- Test execution time
- Test pass/fail rate
- Code coverage trend
- Deployment frequency
- Mean time to failure
- Mean time to recovery
```

### Monitoring Setup

```yaml
# Prometheus metrics for CI/CD
apiVersion: v1
kind: ConfigMap
metadata:
  name: prometheus-config
data:
  prometheus.yml: |
    global:
      scrape_interval: 15s
    scrape_configs:
      - job_name: 'jenkins'
        static_configs:
          - targets: ['jenkins:8080']
      - job_name: 'docker'
        static_configs:
          - targets: ['localhost:9323']
```

## Part 8: Best Practices

```
✅ DO:
- Keep pipelines fast (< 10 minutes)
- Fail fast (unit → integration → E2E)
- Parallelize where possible
- Clean up artifacts
- Archive logs for debugging
- Monitor pipeline health
- Version control pipelines
- Document pipeline stages
- Use infrastructure as code
- Regular pipeline reviews

❌ DON'T:
- Long serial test execution
- Ignore test failures
- Leave resources hanging
- Store sensitive data in logs
- Skip quality gates
- Run all tests on every commit
- Manual deployments
- Hard-coded configuration
```

## Part 9: Common Pitfalls & Solutions

### Pitfall 1: Slow Pipelines
**Problem**: Pipeline takes > 30 minutes
**Solution**: Parallelize tests, optimize setup
**Impact**: 10x faster feedback

### Pitfall 2: Flaky Pipeline
**Problem**: Intermittent failures
**Solution**: Fix underlying test flakiness
**Impact**: Reliable CI/CD

### Pitfall 3: Environment Issues
**Problem**: Tests pass locally, fail in CI
**Solution**: Use Docker, match environments
**Impact**: Consistent results

### Pitfall 4: No Visibility
**Problem**: Can't see why build failed
**Solution**: Comprehensive logging, reports
**Impact**: Faster debugging

## Success Stories

### Example 1: Pipeline Optimization
**Problem**: 45-minute pipeline
**Solution**: Parallelized tests, optimized builds
**Result**: 8 minutes

### Example 2: Docker Standardization
**Problem**: "Works on my machine"
**Solution**: Docker for all environments
**Result**: 100% consistency

### Example 3: Automated Reporting
**Problem**: Manual test reporting
**Solution**: Automated report generation
**Result**: Real-time visibility

## When to Use This Agent

- Setting up CI/CD pipelines
- Optimizing pipeline performance
- Docker setup for testing
- Parallel test execution
- Test infrastructure design
- Reporting and monitoring

## Key Takeaways

🎯 Fast feedback is critical
🎯 Fail fast approach saves time
🎯 Parallelization is essential
🎯 Docker standardizes environments
🎯 Infrastructure as code is best practice
🎯 Monitoring drives improvement
🎯 Automation reduces manual work
🎯 Quality gates ensure standards
