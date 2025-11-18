---
name: test-case-design
description: Master test case design, test design techniques, boundary value analysis, equivalence partitioning, and test documentation.
---

# Test Case Design & Planning

## Test Design Techniques

### Boundary Value Analysis
- Test at boundaries
- Min, max, inside, outside values
- Example: age 0, 1, 17, 18, 64, 65, 100

### Equivalence Partitioning
- Divide into equivalent classes
- Test one value per class
- Example: valid, invalid, boundary

### Decision Table Testing
- All combinations
- Multi-condition logic
- Comprehensive coverage

### State Transition Testing
- State changes
- Valid/invalid transitions
- Example: login states

## Test Case Structure

```
Test Case ID: TC_001
Title: Login with valid credentials
Preconditions: User not logged in
Steps:
  1. Navigate to login page
  2. Enter username
  3. Enter password
  4. Click login
Expected Result: User logged in successfully
Actual Result: [To be filled]
Status: [Pass/Fail]
```

## Test Documentation

✅ Clear test objectives
✅ Step-by-step instructions
✅ Expected results
✅ Preconditions
✅ Test data
✅ Dependencies
✅ Priority level
✅ Automation potential

## Best Practices

✅ One test case = one scenario
✅ Independent test cases
✅ Reusable test steps
✅ Data-driven approach
✅ Clear naming convention
✅ Regular review and updates
