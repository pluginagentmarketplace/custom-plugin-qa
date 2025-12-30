---
name: qa-roadmap
description: Complete QA Engineer Learning Roadmap with milestones and success criteria
allowed-tools: Read
version: "2.1.0"
exit_codes:
  0: success
  1: invalid_input
  2: resource_not_found
---

# QA Engineer Complete Roadmap

Your production-grade path from beginner to expert QA Engineer.

## Usage

```
/qa-roadmap              # Show full roadmap
/qa-roadmap --level=beginner   # Filter by level
/qa-roadmap --phase=3    # Jump to specific phase
```

## Phase 1: Foundations (Weeks 1-4)

### Learning Objectives
- Understand QA fundamentals and principles
- Master testing types and methodologies
- Develop QA mindset and critical thinking
- Learn SDLC and QA's role in each phase

### Topics Covered
| Topic | Agent | Duration | Priority |
|-------|-------|----------|----------|
| QA Fundamentals | 01-qa-fundamentals | Week 1 | Critical |
| Testing Types | 01-qa-fundamentals | Week 1 | Critical |
| SDLC & QA Role | 01-qa-fundamentals | Week 2 | High |
| QA Mindset | 01-qa-fundamentals | Week 2 | High |
| Test Documentation | 02-test-strategy | Week 3-4 | Medium |

### Success Criteria
- [ ] Can explain QA vs QC difference
- [ ] Understands all testing levels (unit, integration, E2E)
- [ ] Can identify risks in requirements
- [ ] Writes clear bug reports
- [ ] Creates basic test cases

### Exit Gate: Foundation Certified
```yaml
requirements:
  - Complete all foundation topics
  - Pass foundation assessment (>80%)
  - Create 10 valid test cases
  - Report 5 bugs with proper documentation
```

---

## Phase 2: Test Design (Weeks 5-7)

### Learning Objectives
- Master test design techniques
- Create comprehensive test strategies
- Understand coverage analysis
- Implement risk-based testing

### Topics Covered
| Topic | Agent | Duration | Priority |
|-------|-------|----------|----------|
| Test Planning | 02-test-strategy | Week 5 | Critical |
| Test Design Techniques | 02-test-strategy | Week 5-6 | Critical |
| Coverage Analysis | 02-test-strategy | Week 6 | High |
| Risk Assessment | 02-test-strategy | Week 7 | High |

### Success Criteria
- [ ] Creates test strategy documents
- [ ] Applies boundary value analysis
- [ ] Uses equivalence partitioning
- [ ] Calculates test coverage
- [ ] Prioritizes tests by risk

### Exit Gate: Test Designer Certified
```yaml
requirements:
  - Create complete test strategy document
  - Design test cases using all techniques
  - Achieve 80% requirements coverage
  - Risk assessment for 1 feature
```

---

## Phase 3: Manual & Exploratory Testing (Weeks 8-9)

### Learning Objectives
- Master manual testing execution
- Develop exploratory testing skills
- Learn session-based testing
- Improve bug hunting techniques

### Topics Covered
| Topic | Agent | Duration | Priority |
|-------|-------|----------|----------|
| Manual Testing | 03-manual-exploratory | Week 8 | Critical |
| Exploratory Testing | 03-manual-exploratory | Week 8-9 | Critical |
| Session-Based Testing | 03-manual-exploratory | Week 9 | High |
| Bug Hunting | 03-manual-exploratory | Week 9 | High |

### Success Criteria
- [ ] Executes test cases systematically
- [ ] Conducts effective exploratory sessions
- [ ] Documents exploration charters
- [ ] Finds edge cases consistently
- [ ] Reports bugs with reproduction steps

### Exit Gate: Manual Testing Expert
```yaml
requirements:
  - Execute 50+ test cases
  - Complete 5 exploratory sessions
  - Find 20+ valid bugs
  - Create session reports
```

---

## Phase 4: Test Automation (Weeks 10-15)

### Learning Objectives
- Master test automation frameworks
- Learn Selenium, Cypress, Playwright
- Implement Page Object Model
- Build maintainable test suites

### Topics Covered
| Topic | Agent | Duration | Priority |
|-------|-------|----------|----------|
| Selenium WebDriver | 04-automation | Week 10-11 | Critical |
| Cypress | 04-automation | Week 12 | Critical |
| Playwright | 04-automation | Week 13 | High |
| Mobile (Appium) | 04-automation | Week 14 | Medium |
| Framework Design | 04-automation | Week 15 | Critical |

### Success Criteria
- [ ] Writes reliable automated tests
- [ ] Implements Page Object Model
- [ ] Handles waits properly
- [ ] Creates data-driven tests
- [ ] Builds reusable utilities

### Exit Gate: Automation Engineer
```yaml
requirements:
  - Build automation framework from scratch
  - Create 50+ automated tests
  - Achieve 80% pass rate
  - CI/CD integration working
```

---

## Phase 5: API & Performance Testing (Weeks 16-19)

### Learning Objectives
- Master REST and GraphQL API testing
- Learn performance testing fundamentals
- Use k6, JMeter for load testing
- Analyze performance metrics

### Topics Covered
| Topic | Agent | Duration | Priority |
|-------|-------|----------|----------|
| REST API Testing | 05-api-performance | Week 16 | Critical |
| GraphQL Testing | 05-api-performance | Week 17 | High |
| Performance Basics | 05-api-performance | Week 18 | Critical |
| Load Testing | 05-api-performance | Week 18-19 | Critical |
| Performance Analysis | 05-api-performance | Week 19 | High |

### Success Criteria
- [ ] Creates API test suites
- [ ] Validates response schemas
- [ ] Designs load test scenarios
- [ ] Analyzes performance metrics
- [ ] Identifies bottlenecks

### Exit Gate: API & Performance Specialist
```yaml
requirements:
  - Build API test framework
  - Create performance test suite
  - Run load test with 100+ VUs
  - Generate performance report
```

---

## Phase 6: CI/CD & Infrastructure (Weeks 20-22)

### Learning Objectives
- Master CI/CD pipelines
- Learn Docker for testing
- Implement continuous testing
- Build test infrastructure

### Topics Covered
| Topic | Agent | Duration | Priority |
|-------|-------|----------|----------|
| CI/CD Pipelines | 06-cicd | Week 20 | Critical |
| GitHub Actions | 06-cicd | Week 20 | Critical |
| Docker Testing | 06-cicd | Week 21 | High |
| Continuous Testing | 06-cicd | Week 21-22 | Critical |
| Infrastructure | 06-cicd | Week 22 | High |

### Success Criteria
- [ ] Sets up CI/CD pipeline
- [ ] Integrates tests in pipeline
- [ ] Uses Docker for testing
- [ ] Implements quality gates
- [ ] Monitors test results

### Exit Gate: DevOps QA Engineer
```yaml
requirements:
  - Working CI/CD pipeline
  - Tests running in containers
  - Quality gates configured
  - Automated reporting
```

---

## Phase 7: Advanced Topics (Weeks 23-26)

### Learning Objectives
- Master security testing
- Implement QA metrics
- Develop leadership skills
- Drive quality culture

### Topics Covered
| Topic | Agent | Duration | Priority |
|-------|-------|----------|----------|
| Security Testing | 07-advanced-leadership | Week 23 | Critical |
| OWASP Top 10 | 07-advanced-leadership | Week 23 | Critical |
| QA Metrics | 07-advanced-leadership | Week 24 | High |
| Team Leadership | 07-advanced-leadership | Week 25 | High |
| Quality Culture | 07-advanced-leadership | Week 26 | High |

### Success Criteria
- [ ] Performs security assessments
- [ ] Defines and tracks KPIs
- [ ] Leads QA initiatives
- [ ] Improves team processes
- [ ] Drives quality culture

### Exit Gate: QA Leader
```yaml
requirements:
  - Complete security assessment
  - Implement metrics dashboard
  - Create team training plan
  - Process improvement initiative
```

---

## Roadmap Summary

```
Week 1-4:   [████████] Foundations
Week 5-7:   [██████] Test Design
Week 8-9:   [████] Manual Testing
Week 10-15: [████████████] Automation
Week 16-19: [████████] API & Performance
Week 20-22: [██████] CI/CD
Week 23-26: [████████] Advanced

Total: 26 weeks (6 months)
```

## Quick Commands

| Command | Description |
|---------|-------------|
| `/qa-path` | Interactive path selection |
| `/qa-tools` | Tool recommendations |
| `/qa-projects` | Practice projects |

## Troubleshooting

### Issue: Stuck on a Topic
```yaml
diagnosis:
  1. Review prerequisites
  2. Check recommended resources
  3. Practice with simpler examples
  4. Seek mentor guidance

solutions:
  - Break into smaller steps
  - Use additional resources
  - Practice more
  - Ask for help
```

### Issue: Skill Gap
```yaml
diagnosis:
  1. Identify specific gap
  2. Review earlier phases
  3. Focus practice

solutions:
  - Revisit foundation topics
  - Extra practice projects
  - Pair with experienced QA
```

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 2.1.0 | 2025-01 | Production-grade with troubleshooting |
| 2.0.0 | 2024-12 | SASMP v1.3.0 compliance |
| 1.0.0 | 2024-11 | Initial release |
