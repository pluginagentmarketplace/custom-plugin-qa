---
name: quality-metrics
description: Master quality metrics, KPIs, dashboards, trend analysis, defect metrics, continuous improvement.
---

# Quality Metrics & Reporting

## Key Metrics

### Test Execution Metrics
- **Total test cases**: Overall test count
- **Executed**: Tests actually run
- **Passed**: Successful tests
- **Failed**: Test failures
- **Skipped**: Not executed
- **Blocked**: Dependent on fixes

### Coverage Metrics
- **Line coverage**: % of code lines executed
- **Branch coverage**: % of decision branches tested
- **Function coverage**: % of functions called
- **Statement coverage**: % of statements executed

Target: 80%+ overall, 100% for critical paths

### Defect Metrics
- **Defect density**: Defects per 1000 lines of code
- **Escape rate**: Defects escaping to production
- **Mean time to fix**: Average defect resolution time
- **Severity distribution**: Critical, High, Medium, Low

### Quality Gates
```
Coverage < 80% → FAIL
Test Pass Rate < 95% → FAIL
Critical Issues > 0 → FAIL
Security Vulnerabilities > 0 → FAIL
```

## Dashboards

### Components
- Test execution overview
- Coverage trends
- Defect trends
- Performance metrics
- Automation progress

### Tools
- Jenkins Dashboard
- GitLab Dashboards
- SonarQube
- Grafana
- Custom dashboards

## Trends & Analysis

### Tracking Over Time
- Coverage improvements
- Defect trends
- Test execution speed
- Automation percentage
- Team velocity

### Continuous Improvement
- Identify patterns
- Set goals
- Monitor progress
- Celebrate achievements
- Adjust strategies

## Best Practices

✅ Define clear metrics
✅ Automate metric collection
✅ Track trends
✅ Set realistic targets
✅ Share metrics widely
✅ Use data to guide decisions
✅ Celebrate improvements
✅ Regular metric reviews

## Related Skills
- Quality Metrics & Reporting
- Test Strategy & Planning
