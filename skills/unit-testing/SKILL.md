---
name: unit-testing-frameworks
description: Master Jest, Vitest, Pytest. Write effective unit tests, use mocking, achieve code coverage, implement TDD.
---

# Unit Testing Frameworks

## Quick Start - Jest

```javascript
describe('Calculator', () => {
  it('should add two numbers', () => {
    const result = add(2, 3);
    expect(result).toBe(5);
  });

  it('should handle negative numbers', () => {
    expect(add(-1, 1)).toBe(0);
  });
});
```

## Core Concepts

### Jest Basics
- Test suites with `describe()`
- Test cases with `it()` or `test()`
- Assertions with `expect()`
- Setup/teardown: `beforeEach()`, `afterEach()`
- Mocking: `jest.fn()`, `jest.mock()`

### Vitest
- Faster, Vite-native
- Same API as Jest
- Zero-config setup
- Better TypeScript support

### Pytest (Python)
- Fixtures for test data
- Parametrized tests
- Markers for test organization
- Plugins for extensions

## Testing Patterns

### Mocking
```javascript
const mockFunction = jest.fn();
mockFunction.mockReturnValue(42);
mockFunction.mockResolvedValue(data);
```

### Spy
```javascript
const spy = jest.spyOn(object, 'method');
expect(spy).toHaveBeenCalled();
```

### Code Coverage
- Line coverage
- Branch coverage
- Function coverage
- Statement coverage

Target: 80%+ overall, 100% for critical paths

## Best Practices

✅ Keep tests small and focused
✅ Use descriptive test names
✅ Arrange-Act-Assert pattern
✅ Mock external dependencies
✅ Don't test implementation details
✅ Keep tests fast
✅ Use test fixtures
✅ Automate test execution

## Related Skills
- Test Automation & CI/CD
- Quality Metrics & Reporting
