---
name: testing-frameworks-practices
description: Master testing frameworks, test automation, TDD, and quality practices. Learn unit testing, integration testing, E2E testing, and performance testing.
---

# Testing Frameworks & Practices

## Quick Start

### Unit Testing with Jest
```javascript
// sum.js
function sum(a, b) {
  return a + b;
}
module.exports = sum;

// sum.test.js
describe('sum', () => {
  it('should add two numbers', () => {
    expect(sum(2, 3)).toBe(5);
  });

  it('should handle negative numbers', () => {
    expect(sum(-1, 1)).toBe(0);
  });
});
```

### React Component Testing
```javascript
import { render, screen, fireEvent } from '@testing-library/react';
import Counter from './Counter';

test('increments counter on button click', () => {
  render(<Counter />);
  const button = screen.getByRole('button');

  fireEvent.click(button);
  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

### E2E Testing with Cypress
```javascript
describe('User Login', () => {
  it('should login successfully', () => {
    cy.visit('http://localhost:3000');
    cy.get('[data-testid=email]').type('user@example.com');
    cy.get('[data-testid=password]').type('password');
    cy.get('[data-testid=login-btn]').click();
    cy.url().should('include', '/dashboard');
  });
});
```

## Testing Types

### Unit Testing
- Testing individual functions/components
- Fast execution
- Isolated from dependencies
- Mock external dependencies
- High code coverage target (80%+)

#### Tools
- **Jest**: JavaScript testing framework
- **Vitest**: Lightning-fast unit testing
- **Mocha**: Flexible test framework
- **Pytest**: Python testing
- **JUnit**: Java testing

### Integration Testing
- Testing multiple components together
- Realistic interactions
- Database integration
- API mocking
- Slower than unit tests

### End-to-End (E2E) Testing
- Testing user workflows
- Real browser automation
- Full application stack
- Slowest tests
- Critical user paths only

#### Tools
- **Cypress**: Modern, developer-friendly
- **Playwright**: Multi-browser, cross-platform
- **Selenium**: Legacy, industry standard
- **Puppeteer**: Headless browser automation

### API Testing
- Testing HTTP endpoints
- Request/response validation
- Status code checks
- Integration testing

#### Tools
- **Postman**: GUI and automation
- **REST Assured**: Java API testing
- **Supertest**: Node.js HTTP testing
- **Pytest-requests**: Python HTTP testing

### Performance Testing
- Load testing: Many concurrent users
- Stress testing: Push beyond limits
- Spike testing: Sudden load increase
- Soak testing: Long-duration load

#### Tools
- **Apache JMeter**: Load testing
- **k6**: Modern performance testing
- **Locust**: Python load testing
- **Gatling**: Scala-based load testing

## Testing Best Practices

### Arrange-Act-Assert Pattern
```javascript
// Arrange: Set up test data
const user = { name: 'John', age: 30 };

// Act: Perform action
const isAdult = user.age >= 18;

// Assert: Verify result
expect(isAdult).toBe(true);
```

### DRY (Don't Repeat Yourself)
```javascript
describe('UserService', () => {
  let service;

  beforeEach(() => {
    service = new UserService();
  });

  // Tests can now reuse 'service'
});
```

### Test Naming
```javascript
// Good: Clearly describes what is tested
test('should throw error when email is invalid', () => {});

// Bad: Vague
test('email validation', () => {});
```

### Mocking & Stubbing

#### Mocking Functions
```javascript
const mockFn = jest.fn();
mockFn.mockReturnValue(42);
expect(mockFn()).toBe(42);
```

#### Mocking Modules
```javascript
jest.mock('axios');
axios.get.mockResolvedValue({ data: [] });
```

#### Stubbing Time
```javascript
jest.useFakeTimers();
jest.advanceTimersByTime(1000);
jest.runAllTimers();
```

## Test-Driven Development (TDD)

### Red-Green-Refactor Cycle
1. **Red**: Write failing test
2. **Green**: Write minimal code to pass
3. **Refactor**: Improve code quality

### Benefits
- Detailed specifications
- Design thinking upfront
- Regression prevention
- Documentation through tests
- Easier refactoring

## Code Coverage

### Coverage Types
- **Line Coverage**: % of lines executed
- **Branch Coverage**: % of decision branches
- **Function Coverage**: % of functions called
- **Statement Coverage**: % of statements executed

### Coverage Targets
- Overall: 70-80%
- Critical paths: 90%+
- Utility functions: 100%

### Tools
- **Istanbul**: JavaScript coverage
- **Coverage.py**: Python coverage
- **JaCoCo**: Java coverage
- **Codecov**: Coverage tracking

## Testing Strategies

### Test Pyramid
```
        △ E2E Tests (Few)
       ╱ ╲
      ╱   ╲ Integration Tests (Some)
     ╱─────╲
    ╱       ╱ Unit Tests (Many)
   ╱_______╱
```

- Most tests at bottom (unit)
- Fewer integration tests
- Few E2E tests

### Behavior-Driven Development (BDD)
```javascript
describe('Feature: User authentication', () => {
  describe('Scenario: Valid credentials', () => {
    it('should login user', () => {
      // Given: user enters credentials
      // When: user clicks login
      // Then: user sees dashboard
    });
  });
});
```

## Test Automation

### CI/CD Integration
```yaml
# GitHub Actions
- name: Run tests
  run: npm test

- name: Upload coverage
  uses: codecov/codecov-action@v3
```

### Test Execution
- Run tests on every push
- Parallel test execution
- Fail build on test failure
- Coverage reporting
- Test reporting and artifacts

## Advanced Testing

### Contract Testing
- Testing API contracts
- Provider and consumer perspectives
- Pact framework
- Prevents breaking changes

### Mutation Testing
- Mutate code and check if tests catch it
- Identifies weak tests
- Tools: Stryker, PIT

### Chaos Engineering
- Inject failures
- Test system resilience
- Tools: Chaos Toolkit, Gremlin

## Tools Ecosystem

### JavaScript
- **Testing**: Jest, Vitest, Mocha, Jasmine
- **Assertion**: Chai, Should, Expect
- **Mocking**: Sinon, Jest mocks
- **UI Testing**: React Testing Library, Enzyme

### Python
- **Testing**: Pytest, unittest
- **Mocking**: unittest.mock
- **Coverage**: Coverage.py

### Java
- **Testing**: JUnit5, TestNG
- **Mocking**: Mockito, PowerMock
- **API**: REST Assured

## Best Practices

✅ Write tests for critical paths
✅ Keep tests simple and focused
✅ Use meaningful test names
✅ Test behavior, not implementation
✅ Mock external dependencies
✅ Run tests frequently
✅ Maintain test data carefully
✅ Automate test execution
✅ Review test code quality
✅ Track coverage trends

❌ Don't test implementation details
❌ Don't use sleep() for synchronization
❌ Don't skip flaky tests
❌ Don't write too many E2E tests
❌ Don't test everything
❌ Don't ignore test failures
❌ Don't copy-paste test code

## Common Issues & Solutions

### Flaky Tests
- **Problem**: Tests fail intermittently
- **Solutions**: Better synchronization, isolation, deterministic data

### Slow Tests
- **Problem**: Tests take too long
- **Solutions**: Parallel execution, optimize fixtures, use mocks

### Hard to Test Code
- **Problem**: Code isn't testable
- **Solutions**: Refactor, dependency injection, smaller functions

## Related Skills
- Frontend Development
- Backend Development
- System Architecture

## Next Steps
Write comprehensive test suites, aim for high coverage, and implement CI/CD testing pipelines.
