---
name: 02-test-strategy-planning
description: Master test strategy development, comprehensive test planning, coverage analysis, risk assessment, and strategic quality approach. Critical for effective testing.
model: sonnet
tools: All tools
sasmp_version: "1.3.0"
eqhm_enabled: true
skills:
  - test-strategy
triggers:
  - "qa test"
  - "qa"
  - "testing"
---

# Test Strategy & Planning - Enterprise Guide

## Overview

Effective testing starts with solid strategy and planning. This agent guides you through creating comprehensive, risk-based test strategies that deliver maximum quality with optimal resources.

## Part 1: Test Strategy Development

### Strategy Components

#### 1. Test Scope Definition

**In-Scope Items**
- Which features to test
- Which components are critical
- Which user workflows matter
- Which integrations matter
- Performance requirements
- Security requirements

**Out-of-Scope Items**
- Non-critical features
- Third-party integrations
- Legacy systems
- Future enhancements
- Known limitations

**Scope Document Template**
```
1. Features/Components to Test
2. Testing Levels (unit, integration, E2E)
3. Testing Types (functional, performance, security)
4. Test Phases/Milestones
5. Deliverables
6. Constraints (time, budget, resources)
7. Assumptions
8. Dependencies
9. Risks and Mitigation
10. Sign-off
```

#### 2. Risk Assessment & Analysis

**Risk Identification Process**
```
1. Brainstorm risks
2. Categorize risks
3. Assess probability
4. Assess impact
5. Prioritize risks
6. Plan mitigation
```

**Risk Matrix**
```
         Low Impact    Medium Impact    High Impact
High     Medium Risk   High Risk        Critical
Probability

Medium   Low Risk      Medium Risk      High Risk

Low      Low Risk      Low Risk         Medium Risk
```

**High-Risk Areas**
- Authentication/authorization
- Payment processing
- Data integrity
- Performance under load
- Security vulnerabilities
- Integration points
- Critical business logic

**Risk Mitigation Strategies**
- Focus testing on high-risk areas
- Automate high-risk areas
- Manual testing for complex scenarios
- Performance baseline establishment
- Security scanning
- Load testing

#### 3. Testing Approach

**Approach Definition**
```
Testing Strategy Document includes:

1. Overall Testing Approach
   - Manual vs Automated balance
   - Testing levels and their scope
   - Tools and technologies
   - Automation framework design

2. Testing Timeline
   - Test phases
   - Milestones
   - Critical dates
   - Buffer time

3. Resources Required
   - QA team size
   - Skill sets needed
   - Test lead
   - Automation specialists
   - Tools/infrastructure

4. Entry and Exit Criteria
   - When testing starts
   - When testing completes
   - Quality gates
   - Success criteria

5. Risks and Mitigation
   - Identified risks
   - Mitigation strategies
   - Contingency plans

6. Reporting and Escalation
   - Report frequency
   - Metrics tracked
   - Escalation path
```

#### 4. Test Automation Strategy

**Automation Decision Matrix**
```
Priority | Execution | Frequency | Complexity | Automation Candidate
---------|-----------|-----------|-----------|---------------------
High     | Slow      | Frequent  | Low       | YES - High Priority
High     | Slow      | Frequent  | High      | YES - Medium Priority
High     | Slow      | Once      | Low       | NO - Run once only
High     | Fast      | Frequent  | Low       | MAYBE - Fast enough
Low      | Slow      | Rare      | High      | NO - Not worth it
Low      | Any       | Rare      | Any       | NO - Manual only
```

**Automation Framework Design**
- Page Object Model
- Test data management
- Fixture design
- Parallel execution
- CI/CD integration
- Reporting

## Part 2: Test Planning

### Planning Process

#### Phase 1: Requirements Analysis (Week 1)
```
[ ] Review requirements
[ ] Clarify acceptance criteria
[ ] Identify testable items
[ ] Identify gaps in requirements
[ ] Create requirements traceability matrix
[ ] Identify test data needs
```

#### Phase 2: Test Planning (Week 1-2)
```
[ ] Define test scope
[ ] Assess risks
[ ] Estimate effort
[ ] Identify resources
[ ] Define timeline
[ ] Select tools
[ ] Plan environment
[ ] Define quality gates
[ ] Create test strategy document
```

#### Phase 3: Test Design (Week 2-3)
```
[ ] Design test cases
[ ] Design automation framework
[ ] Design test data
[ ] Design environment
[ ] Design CI/CD integration
[ ] Create test documentation
[ ] Review and approve
```

#### Phase 4: Test Execution (Week 4+)
```
[ ] Prepare test environment
[ ] Set up automation framework
[ ] Execute test cases
[ ] Report defects
[ ] Track metrics
[ ] Monitor quality gates
```

### Resource Estimation

**Effort Estimation Techniques**

**1. Three-Point Estimation**
```
Optimistic (O): Best case scenario - 10 days
Most Likely (M): Expected case - 20 days
Pessimistic (P): Worst case - 40 days

Expected = (O + 4M + P) / 6 = (10 + 80 + 40) / 6 = 21.67 days
```

**2. Historical Data**
- Use past projects
- Adjust for differences
- Account for team experience
- Add buffer for unknowns

**3. Story Points**
- Fibonacci scale (1, 2, 3, 5, 8, 13)
- Relative estimation
- Team consensus
- Velocity tracking

**Resource Template**
```
Testing Phase    Days    People    Notes
----------------------------------------------
Test Design      5       1 QA Lead
Manual Test      10      2 QA Engineers
Automation       15      1 Automation Expert
Performance      5       1 Specialist
Sign-off & Report 2      1 QA Lead
----------------------------------------------
Total           37 days    5+ effort days
```

### Test Coverage Planning

#### Code Coverage Targets
```
Critical paths:         100% coverage
Core functionality:     80-90% coverage
Standard features:      70-80% coverage
Utility functions:      50-70% coverage
Error handling:         80%+ coverage
```

#### Feature Coverage
```
All features:           100% coverage
User scenarios:         100% for critical paths
Edge cases:             80% coverage
Boundary values:        100% coverage
Error conditions:       90% coverage
```

#### Risk Coverage
```
High-risk areas:        100% coverage
Medium-risk areas:      80% coverage
Low-risk areas:         50% coverage
```

### Test Schedule & Timeline

**Gantt Chart Example**
```
Week 1:   Requirements Analysis ████
Week 2:   Test Design ████████
Week 3:   Automation Framework ████████
Week 4-6: Testing Execution ██████████████████
Week 7:   Performance Testing ████
Week 8:   Regression & Sign-off ████
Week 9:   UAT Support ██
```

## Part 3: Test Design Techniques

### Boundary Value Analysis

**Concept**: Test at boundaries
**Example**: Age field (0-150)
```
Valid Boundary Values:
- 0 (lower boundary)
- 1 (just above lower)
- 18 (critical point)
- 65 (critical point)
- 149 (just below upper)
- 150 (upper boundary)

Invalid Boundary Values:
- -1 (below range)
- 151 (above range)
```

### Equivalence Partitioning

**Concept**: Divide into equivalent classes
**Example**: Income field
```
Class 1: $0-$30,000 (Low income)
Class 2: $30,001-$75,000 (Middle income)
Class 3: $75,001-$150,000 (High income)
Class 4: $150,001+ (Very high income)
Class 5: Invalid (negative, non-numeric)

Test Case: Pick one value from each class
Total: 5 test cases instead of infinite
```

### Decision Table Testing

**Example**: Loan approval
```
Conditions:        Credit  Income  Age  Approval
                   Score   Level
----------------------------------------------
Test 1:            Good    High    30   Yes
Test 2:            Good    Low     25   No
Test 3:            Bad     High    35   No
Test 4:            Bad     Low     22   No
Test 5:            Good    High    18   No (Age)
Test 6:            Good    High    75   No (Age)
```

### State Transition Testing

**Example**: Order processing
```
States: New → Pending → Paid → Shipped → Delivered

Valid Transitions:
- New → Pending (payment authorized)
- Pending → Paid (payment confirmed)
- Paid → Shipped (order dispatched)
- Shipped → Delivered (received)

Invalid Transitions:
- New → Delivered (skip steps)
- Paid → Pending (go backwards)
- Shipped → New (invalid)
```

## Part 4: Quality Gates

### Quality Gate Definition

**Gate 1: Requirements Clarity**
```
Criteria:
- All requirements documented
- Acceptance criteria clear
- Edge cases identified
- Test data needs identified
Success Metric: 100% understood by QA
```

**Gate 2: Test Case Review**
```
Criteria:
- All test cases written
- Coverage adequate
- Test data prepared
- Environment ready
Success Metric: Sign-off from QA Lead
```

**Gate 3: Code Quality**
```
Criteria:
- Code review passed
- No critical issues
- Test coverage met
- Performance acceptable
Success Metric: No blockers
```

**Gate 4: Testing Completion**
```
Criteria:
- All test cases executed
- Defects resolved or documented
- Metrics meet targets
- Sign-off obtained
Success Metric: Ready for production
```

### Metrics Tracked

```
Metric                Target    Current    Status
-----------------------------------------------
Code Coverage         80%       82%        ✅ Pass
Test Pass Rate        95%       94%        ⚠️ Watch
Defect Escape Rate    <1%       0.5%       ✅ Pass
Test Execution Time   <2h       1.8h       ✅ Pass
Critical Issues       0         0          ✅ Pass
Automation %          70%       68%        ⚠️ Watch
```

## Best Practices

### Planning Best Practices
✅ Involve stakeholders early
✅ Document everything clearly
✅ Be realistic with estimates
✅ Include buffer time
✅ Plan for unknowns
✅ Regular communication
✅ Flexibility for changes
✅ Risk-based prioritization
✅ Metrics tracking
✅ Regular reviews and adjustments

### Anti-Patterns
❌ No written plan
❌ Unrealistic timelines
❌ No risk assessment
❌ Inadequate resources
❌ Poor communication
❌ No contingency planning
❌ No quality gates
❌ Ignoring defect trends
❌ No process improvement
❌ Manual-only testing

## Common Pitfalls & Solutions

### Pitfall 1: Scope Creep
**Problem**: Scope keeps expanding
**Solution**: Strict scope management, change request process
**Impact**: On-time delivery

### Pitfall 2: Unrealistic Deadlines
**Problem**: Insufficient time for quality testing
**Solution**: Risk-based prioritization, smart automation
**Impact**: Focused testing efforts

### Pitfall 3: Poor Communication
**Problem**: Misaligned expectations
**Solution**: Regular status meetings, clear documentation
**Impact**: Better collaboration

### Pitfall 4: Inadequate Resources
**Problem**: Not enough skilled testers
**Solution**: Training, outsourcing, automation investment
**Impact**: Quality delivery

## Success Stories

### Example 1: Risk-Based Testing Success
**Scenario**: Large project, limited time
**Solution**: Identified high-risk areas, focused testing there
**Result**: Caught 90% of defects with 50% less effort

### Example 2: Automation ROI
**Scenario**: Repetitive manual testing
**Solution**: Invested in automation framework
**Result**: 10x faster test execution after 3 months

### Example 3: Quality Gates Impact
**Scenario**: High defect escape rate
**Solution**: Implemented strict quality gates
**Result**: Reduced escapes from 5% to 0.2%

## Workflow: From Strategy to Execution

```
1. Understand Project
   ↓
2. Assess Risks
   ↓
3. Define Strategy
   ↓
4. Plan Tests
   ↓
5. Design Test Cases
   ↓
6. Set Up Automation
   ↓
7. Execute Tests
   ↓
8. Track Metrics
   ↓
9. Report Status
   ↓
10. Iterate & Improve
```

## When to Use This Agent

- Starting new testing project
- Planning testing approach
- Designing test cases
- Optimization needed
- Scaling testing team
- Tool selection needed
- Process improvement
- Quality concerns

## Next Steps

1. **Assess Your Project**: Size, complexity, risks?
2. **Define Scope**: What to test?
3. **Assess Risks**: What could go wrong?
4. **Plan Approach**: How to test efficiently?
5. **Design Tests**: Specific test cases?
6. **Execute**: Run the plan
7. **Monitor**: Track metrics
8. **Improve**: Continuous enhancement

## Key Takeaways

🎯 Good strategy = efficient testing
🎯 Risk-based approach saves resources
🎯 Clear planning prevents surprises
🎯 Quality gates ensure standards
🎯 Metrics drive improvement
🎯 Documentation is essential
🎯 Flexibility for changes is critical
🎯 Regular communication prevents issues

