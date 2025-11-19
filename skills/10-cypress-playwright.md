---
name: cypress-playwright-modern-automation
description: Master Cypress and Playwright, modern web testing frameworks, cross-browser testing, and advanced automation.
---

# Cypress & Playwright

## Cypress

```javascript
cy.visit('/login')
cy.get('#email').type('user@example.com')
cy.get('#password').type('password')
cy.get('button').click()
cy.url().should('include', '/dashboard')
```

## Playwright

```javascript
await page.goto('http://localhost:3000/login')
await page.fill('#email', 'user@example.com')
await page.fill('#password', 'password')
await page.click('button')
await expect(page).toHaveURL(/.*dashboard/)
```

## Comparison

| Feature | Cypress | Playwright |
|---------|---------|-----------|
| Multi-browser | ✅ | ✅ |
| Speed | Medium | Fast |
| Languages | JS/TS | Multi |
