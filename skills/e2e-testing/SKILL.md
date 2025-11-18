---
name: e2e-testing
description: Master Cypress, Playwright, E2E testing. Write robust user journey tests, handle dynamic content, continuous testing.
---

# E2E Testing Automation

## Quick Start - Cypress

```javascript
describe('User Login', () => {
  it('should login successfully', () => {
    cy.visit('http://localhost:3000');
    cy.get('[data-testid=email]').type('user@example.com');
    cy.get('[data-testid=password]').type('password123');
    cy.get('[data-testid=login-btn]').click();
    cy.url().should('include', '/dashboard');
    cy.get('[data-testid=user-name]').should('be.visible');
  });
});
```

## Frameworks

### Cypress
- Modern, developer-friendly
- Real browser automation
- Time-travel debugging
- Network stubbing
- Screenshots & videos

### Playwright
- Multi-browser support
- Cross-platform
- Better performance
- API for headless testing
- Device emulation

### Selenium
- Industry standard
- All browsers
- Multiple languages
- Legacy systems

## Core Concepts

### Selectors
- CSS selectors
- XPath
- Data attributes (best practice)
- Accessible selectors

### Waits
- Implicit waits
- Explicit waits
- Retry mechanisms
- Network synchronization

### Page Object Model
```javascript
class LoginPage {
  visit() { cy.visit('/login'); }
  fillEmail(email) { cy.get('[data-testid=email]').type(email); }
  submit() { cy.get('[data-testid=submit]').click(); }
}
```

## Best Practices

✅ Test user journeys
✅ Use data attributes
✅ Avoid hardwaits (sleep)
✅ Page Object Model
✅ Parallel execution
✅ Screenshots on failure
✅ Cross-browser testing
✅ Flaky test prevention

## Related Skills
- Integration & E2E Testing
- Test Automation & CI/CD
