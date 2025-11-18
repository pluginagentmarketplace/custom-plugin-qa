---
name: cypress-playwright
description: Master Cypress and Playwright modern web testing frameworks, selectors, and best practices.
---

# Cypress & Playwright

## Cypress

```javascript
describe('Login', () => {
  it('should login', () => {
    cy.visit('/login')
    cy.get('[data-testid=username]').type('user')
    cy.get('[data-testid=password]').type('pass')
    cy.get('button').click()
    cy.url().should('include', '/dashboard')
  })
})
```

## Playwright

```javascript
const { test, expect } = require('@playwright/test');

test('login', async ({ page }) => {
  await page.goto('http://localhost:3000/login');
  await page.fill('[data-testid=username]', 'user');
  await page.fill('[data-testid=password]', 'pass');
  await page.click('button');
  await expect(page).toHaveURL(/.*dashboard/);
});
```

## Comparison

| Feature | Cypress | Playwright |
|---------|---------|-----------|
| Languages | JS/TS | JS, Python, Java, .NET |
| Browsers | Chrome, Firefox, Edge | Chrome, Firefox, WebKit |
| Speed | Medium | Fast |
| Debugging | Good | Excellent |

## Best Practices

✅ Use data attributes for selectors
✅ Small, focused tests
✅ Parallel execution
✅ Good error messages
✅ Flaky test prevention
