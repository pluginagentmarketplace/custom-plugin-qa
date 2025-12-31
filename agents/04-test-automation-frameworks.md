---
name: 04-test-automation-frameworks
description: Master test automation frameworks, Selenium, Cypress, Playwright, Appium, and automation architecture. Design scalable, maintainable, reliable test automation solutions.
model: sonnet
tools: All tools
sasmp_version: "1.3.0"
eqhm_enabled: true
skills:
  - automation
  - test-strategy
triggers:
  - "qa test"
  - "qa"
  - "testing"
---

# Test Automation Frameworks - Complete Mastery Guide

## Overview

Test automation is critical for modern QA. This agent guides you through industry-leading frameworks, architectures, and best practices for building reliable, maintainable, scalable automation.

## Part 1: Selenium WebDriver Deep Dive

### Selenium Architecture

```
Browser (Chrome, Firefox, Safari, Edge)
        ↑
        ↓
WebDriver Protocol (Wire format)
        ↑
        ↓
WebDriver Client Library (Java, Python, JS)
        ↑
        ↓
Test Code
```

### Selenium Element Locators

**Locator Strategies** (Priority Order):

```
1. ID (Most reliable, unique)
   WebElement element = driver.findElement(By.id("user-email"));

2. Name (Reliable if unique)
   WebElement element = driver.findElement(By.name("password"));

3. CSS Selector (Recommended balance)
   WebElement element = driver.findElement(By.cssSelector("button.login-btn"));

4. XPath (Most flexible, can be fragile)
   WebElement element = driver.findElement(By.xpath("//button[@class='login-btn']"));

5. Link Text (For links only)
   WebElement element = driver.findElement(By.linkText("Sign In"));

6. Class Name (Avoid if unstable)
   WebElement element = driver.findElement(By.className("submit-btn"));

7. Tag Name (Avoid, not specific)
   WebElement element = driver.findElement(By.tagName("button"));
```

**CSS Selector Best Practices**:

```
✅ GOOD:
- button.login-btn
- input[type="email"]
- div.form-container > button
- #user-email
- [data-test-id="login-button"]

❌ BAD (Fragile):
- div > div > div > button (too many levels)
- button:nth-child(5) (brittle to HTML changes)
- .btn-sm.btn-primary.pt-2 (too many classes)
```

### Selenium Waits (Critical!)

```
WAIT TYPES:

1. Implicit Wait (Global, not recommended)
   driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);

2. Explicit Wait (Recommended)
   WebDriverWait wait = new WebDriverWait(driver, 10);
   element = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("element")));

3. Fluent Wait (Most flexible)
   Wait<WebDriver> wait = new FluentWait<>(driver)
     .withTimeout(30, TimeUnit.SECONDS)
     .pollingEvery(5, TimeUnit.SECONDS)
     .ignoring(NoSuchElementException.class);

WAIT CONDITIONS:
- presenceOfElementLocated: Element exists in DOM
- visibilityOfElementLocated: Element visible on page
- elementToBeClickable: Element clickable
- invisibilityOfElement: Element not visible
- textToBePresentInElement: Text appears
- urlContains: URL contains text
- titleIs: Page title matches
```

**Wait Best Practices**:

```
✅ DO:
- Use explicit waits
- Set appropriate timeouts (8-15 seconds)
- Wait for specific conditions
- Wait for clickability before clicking
- Wait for visibility before reading text

❌ DON'T:
- Use implicit waits
- Use Thread.sleep()
- Set very long timeouts
- Wait for too generic conditions
- Use multiple waits for same element
```

### Selenium Advanced Interactions

```
Mouse Actions:
- Click: element.click();
- Double-click: actions.doubleClick(element).perform();
- Right-click: actions.contextClick(element).perform();
- Hover: actions.moveToElement(element).perform();
- Drag-drop: actions.dragAndDrop(source, target).perform();

Keyboard Actions:
- Type text: element.sendKeys("text");
- Press key: actions.sendKeys(Keys.ENTER).perform();
- Key combination: actions.keyDown(Keys.CONTROL).sendKeys("a").keyUp(Keys.CONTROL).perform();
- Clear field: element.clear();

Window Management:
- Switch window: driver.switchTo().window("window handle");
- Switch frame: driver.switchTo().frame("frame id");
- Switch alert: driver.switchTo().alert();
- Full screenshot: File screenshot = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
```

### Selenium Cross-Browser Testing

**Browser-Specific Capabilities**:

```
Chrome:
- Options options = new ChromeOptions();
- options.addArguments("--disable-blink-features=AutomationControlled");
- options.setExperimentalOption("excludeSwitches", asList("enable-automation"));
- options.setExperimentalOption("useAutomationExtension", false);

Firefox:
- FirefoxOptions options = new FirefoxOptions();
- options.setLogLevel(FirefoxDriverLogLevel.DEBUG);

Safari:
- SafariOptions options = new SafariOptions();
- options.setAutomaticInspection(true);

Edge:
- EdgeOptions options = new EdgeOptions();
- options.addArguments("--disable-blink-features=AutomationControlled");

Remote (Grid):
- RemoteWebDriver driver = new RemoteWebDriver(new URL("http://localhost:4444"), capabilities);
```

## Part 2: Cypress Framework

### Cypress vs Selenium

| Feature | Cypress | Selenium |
|---------|---------|----------|
| Architecture | Browser-native | WebDriver protocol |
| Execution | Fast, in-browser | Slower, protocol overhead |
| Debugging | Time-travel debugging | Screenshots/logs |
| Languages | JavaScript | Multiple |
| Mobile | Limited | Full support (Appium) |
| APIs | Direct command chaining | More verbose |
| Learning | Easier for JS developers | Steeper learning curve |

### Cypress Setup & Configuration

```
// cypress.config.js
export default defineConfig({
  e2e: {
    baseUrl: 'http://localhost:3000',
    viewportWidth: 1280,
    viewportHeight: 720,
    requestTimeout: 5000,
    responseTimeout: 5000,
    defaultCommandTimeout: 5000,
    execTimeout: 60000,
    pageLoadTimeout: 30000,
    setupNodeEvents(on, config) {
      // Event handlers
    }
  }
});
```

### Cypress Commands & Syntax

```
// Visiting
cy.visit('/login');

// Querying
cy.get('#username').should('be.visible');
cy.contains('button', 'Login').click();
cy.get('[data-test-id="submit"]').click();

// Typing & Clearing
cy.get('input[type="email"]').type('user@example.com');
cy.get('input[type="password"]').clear().type('password');

// Assertions
cy.get('h1').should('contain.text', 'Dashboard');
cy.get('input').should('have.value', 'test@example.com');
cy.get('[role="alert"]').should('have.class', 'error');

// Intercepts (Mock API)
cy.intercept('GET', '/api/users', { fixture: 'users.json' }).as('getUsers');
cy.intercept('POST', '/api/login', { status: 200, body: { token: 'abc123' } }).as('login');
cy.wait('@login');

// Fixtures & Test Data
cy.fixture('users').then(users => {
  cy.get('#user').select(users[0].name);
});
```

### Cypress Page Object Model

```
// pages/LoginPage.js
export class LoginPage {
  getEmailInput() {
    return cy.get('input[type="email"]');
  }

  getPasswordInput() {
    return cy.get('input[type="password"]');
  }

  getLoginButton() {
    return cy.get('button:contains("Login")');
  }

  login(email, password) {
    this.getEmailInput().type(email);
    this.getPasswordInput().type(password);
    this.getLoginButton().click();
  }

  verifyLoginSuccess() {
    cy.get('h1').should('contain.text', 'Dashboard');
  }
}

// cypress/e2e/login.cy.js
import { LoginPage } from '../pages/LoginPage';

describe('Login Tests', () => {
  const loginPage = new LoginPage();

  beforeEach(() => {
    cy.visit('/login');
  });

  it('should login successfully', () => {
    loginPage.login('user@example.com', 'password');
    loginPage.verifyLoginSuccess();
  });
});
```

## Part 3: Playwright Multi-Browser Testing

### Playwright vs Cypress

**Advantages**:
- Multi-browser (Chrome, Firefox, Safari)
- Multiple languages (JS, Python, Java, .NET)
- Better for mobile testing
- More flexible reporting

**Setup**:

```
npm install -D @playwright/test

// playwright.config.ts
export default defineConfig({
  testDir: './tests',
  fullyParallel: true,
  forbidOnly: !!process.env.CI,
  retries: process.env.CI ? 2 : 0,
  workers: process.env.CI ? 1 : undefined,
  timeout: 30 * 1000,
  expect: { timeout: 5000 },
  use: { baseURL: 'http://localhost:3000' },
  projects: [
    { name: 'chromium', use: { ...devices['Desktop Chrome'] } },
    { name: 'firefox', use: { ...devices['Desktop Firefox'] } },
    { name: 'webkit', use: { ...devices['Desktop Safari'] } },
    { name: 'Mobile Chrome', use: { ...devices['Pixel 5'] } },
  ],
});
```

### Playwright API

```
// Navigating
await page.goto('http://example.com');

// Locating
await page.click('button:has-text("Login")');
await page.fill('input[type="email"]', 'user@example.com');
await page.keyboard.type('password');

// Waiting
await page.waitForSelector('#submit-button');
await page.waitForNavigation();
await page.waitForURL('**/dashboard');

// Taking actions
await page.screenshot({ path: 'screenshot.png' });
const pdf = await page.pdf({ path: 'page.pdf' });

// Intercepting
await page.route('**/api/**', route => {
  if (route.request().method() === 'GET') {
    route.abort();
  } else {
    route.continue();
  }
});

// Handling popups
page.once('popup', popup => {
  popup.close();
});
```

### Playwright Test Structure

```
// tests/login.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Login Tests', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('/login');
  });

  test('successful login', async ({ page }) => {
    await page.fill('input[type="email"]', 'user@example.com');
    await page.fill('input[type="password"]', 'password');
    await page.click('button:has-text("Login")');

    await expect(page).toHaveURL('**/dashboard');
    await expect(page.locator('h1')).toContainText('Dashboard');
  });

  test('invalid credentials', async ({ page }) => {
    await page.fill('input[type="email"]', 'user@example.com');
    await page.fill('input[type="password"]', 'wrong');
    await page.click('button:has-text("Login")');

    await expect(page.locator('[role="alert"]')).toContainText('Invalid credentials');
  });
});
```

## Part 4: Appium Mobile Automation

### Appium Architecture

```
Appium Server (Node.js HTTP Server)
       ↑
       ↓
Appium Client (Java/Python/JS)
       ↑
       ↓
Mobile Device (iOS/Android)
       ↑
       ↓
Native/Web/Hybrid App
```

### Appium Setup

```
// Appium server
npm install -g appium
appium

// Appium client (Java)
WebDriverManager.chromedriver().setup();

DesiredCapabilities capabilities = new DesiredCapabilities();
capabilities.setCapability("platformName", "Android");
capabilities.setCapability("deviceName", "emulator-5554");
capabilities.setCapability("app", "/path/to/app.apk");
capabilities.setCapability("automationName", "UiAutomator2");

AppiumDriver driver = new AndroidDriver(
    new URL("http://127.0.0.1:4723"),
    capabilities
);
```

### Appium Locators (Android)

```
// ID
driver.findElement(By.id("com.example:id/button"));

// Accessibility ID
driver.findElement(AppiumBy.accessibilityId("submitButton"));

// XPath
driver.findElement(By.xpath("//android.widget.Button[@text='Login']"));

// Class Name
driver.findElement(By.className("android.widget.Button"));

// Content Description
driver.findElement(AppiumBy.accessibilityId("login_button"));
```

### Mobile Testing Best Practices

```
✅ DO:
- Test on real devices when possible
- Use explicit waits
- Test network conditions
- Test device orientations
- Test touch gestures
- Handle app lifecycle
- Test with real data

❌ DON'T:
- Rely only on emulators
- Use implicit waits
- Ignore battery/connectivity
- Test only portrait orientation
- Use brittle XPath
- Ignore permissions
```

## Part 5: Automation Architecture

### Page Object Model (POM)

```
// Base Page Class
public abstract class BasePage {
  protected WebDriver driver;
  protected WebDriverWait wait;

  public BasePage(WebDriver driver) {
    this.driver = driver;
    this.wait = new WebDriverWait(driver, Duration.ofSeconds(10));
  }

  protected WebElement find(By locator) {
    return wait.until(ExpectedConditions.presenceOfElementLocated(locator));
  }

  protected void click(By locator) {
    wait.until(ExpectedConditions.elementToBeClickable(locator)).click();
  }

  protected void type(By locator, String text) {
    WebElement element = find(locator);
    element.clear();
    element.sendKeys(text);
  }

  protected String getText(By locator) {
    return find(locator).getText();
  }
}

// Login Page
public class LoginPage extends BasePage {
  private By emailField = By.id("email");
  private By passwordField = By.id("password");
  private By loginButton = By.xpath("//button[@class='btn-login']");
  private By errorMessage = By.xpath("//div[@class='error-message']");

  public LoginPage(WebDriver driver) {
    super(driver);
  }

  public void login(String email, String password) {
    type(emailField, email);
    type(passwordField, password);
    click(loginButton);
  }

  public boolean isErrorDisplayed() {
    try {
      return find(errorMessage).isDisplayed();
    } catch (NoSuchElementException e) {
      return false;
    }
  }

  public String getErrorMessage() {
    return getText(errorMessage);
  }
}

// Test Class
public class LoginTest {
  private WebDriver driver;
  private LoginPage loginPage;

  @BeforeEach
  public void setUp() {
    driver = new ChromeDriver();
    loginPage = new LoginPage(driver);
  }

  @Test
  public void testLoginSuccess() {
    driver.get("http://localhost:3000/login");
    loginPage.login("user@example.com", "password");
    // Verify success
  }

  @Test
  public void testLoginError() {
    driver.get("http://localhost:3000/login");
    loginPage.login("user@example.com", "wrongpassword");
    assertTrue(loginPage.isErrorDisplayed());
    assertEquals("Invalid credentials", loginPage.getErrorMessage());
  }

  @AfterEach
  public void tearDown() {
    driver.quit();
  }
}
```

### Test Data Management

```
// Test Data Factory
public class TestDataFactory {
  public static User createValidUser() {
    return new User("user@example.com", "password", "John", "Doe");
  }

  public static User createAdminUser() {
    User user = createValidUser();
    user.setRole("ADMIN");
    return user;
  }

  public static User createInvalidUser() {
    return new User("", "", "", "");
  }
}

// CSV Data Provider
@ParameterizedTest
@CsvSource({
  "user1@example.com,password1,true",
  "user2@example.com,password2,true",
  "invalid@example.com,wrong,false"
})
public void testLoginWithData(String email, String password, boolean shouldSucceed) {
  loginPage.login(email, password);
  // Assertions
}

// External File Data
@ParameterizedTest
@CsvFileSource(resources = "/test_data.csv")
public void testWithExternalData(String email, String password) {
  // Test code
}
```

## Part 6: Framework Best Practices

### Flaky Test Prevention

**Common Causes & Solutions**:

```
1. TIMING ISSUES
   Problem: Element not ready when accessed
   Solution: Use explicit waits for all interactions

2. STALE ELEMENTS
   Problem: Element reference becomes invalid
   Solution: Re-find element for each action

3. RACE CONDITIONS
   Problem: Test timing depends on system speed
   Solution: Use explicit waits, not Thread.sleep()

4. DATA INCONSISTENCY
   Problem: Test data varies between runs
   Solution: Use proper test data setup/cleanup

5. ENVIRONMENT ISSUES
   Problem: Test passes locally, fails in CI
   Solution: Use same environment, handle dependencies
```

**Flaky Test Checklist**:

```
✅ No Thread.sleep() calls
✅ All waits are explicit, not implicit
✅ Proper test data setup/teardown
✅ No hardcoded wait times
✅ Proper error handling
✅ Tests isolated and independent
✅ Proper synchronization
✅ No random data in assertions
✅ Proper resource cleanup
✅ Environment-independent tests
```

### Reliable Locators

```
LOCATOR STABILITY RATING:

ID                    ★★★★★ (Most stable)
name                  ★★★★☆
data-testid           ★★★★☆
CSS class (specific)  ★★★☆☆
XPath (specific)      ★★★☆☆
CSS class (generic)   ★★☆☆☆
XPath (generic)       ★☆☆☆☆ (Least stable)

BEST PRACTICES:
- Use ID when available
- Use data-testid if developers support it
- Use CSS selectors over XPath
- Avoid complex XPath expressions
- Avoid multiple class selectors
- Use specific attributes (type, role, etc.)
- Avoid index-based selectors
```

### Parallel Execution

```
// TestNG parallel execution
@Test(threadPoolSize = 3, invocationCount = 9, timeOut = 10000)
public void testParallel() {
  // Test code
}

// JUnit 5 parallel execution
junit.jupiter.execution.parallel.enabled = true
junit.jupiter.execution.parallel.mode.default = concurrent
junit.jupiter.execution.parallel.mode.classes.default = concurrent

// Cypress parallel
npx cypress run --spec "cypress/e2e/**/*.cy.js" --parallel --record

// Playwright parallel
npx playwright test --workers=4
```

## Part 7: CI/CD Integration

### GitHub Actions

```yaml
name: E2E Tests
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm run test:e2e

      - name: Upload results
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: test-results
          path: cypress/videos
```

### Jenkins Pipeline

```groovy
pipeline {
  agent any

  stages {
    stage('Setup') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh 'npm run test:e2e'
      }
    }

    stage('Report') {
      steps {
        junit 'test-results/junit.xml'
        publishHTML([
          reportDir: 'test-results/html',
          reportFiles: 'index.html',
          reportName: 'E2E Test Report'
        ])
      }
    }
  }
}
```

## Part 8: Common Pitfalls & Solutions

### Pitfall 1: Over-Automation
**Problem**: Automating everything including UI details
**Solution**: Focus on critical paths, business logic
**Impact**: Reduced maintenance, better ROI

### Pitfall 2: Flaky Tests
**Problem**: Tests fail intermittently
**Solution**: Proper waits, data isolation
**Impact**: Team trust, faster feedback

### Pitfall 3: Poor Locators
**Problem**: Tests break with UI changes
**Solution**: Use stable, specific locators
**Impact**: Less maintenance

### Pitfall 4: No Data Management
**Problem**: Tests fail due to data issues
**Solution**: Proper setup/cleanup, fixtures
**Impact**: Reliable tests

### Pitfall 5: No Reporting
**Problem**: Can't diagnose failures
**Solution**: Screenshots, videos, logs
**Impact**: Faster debugging

## Success Stories

### Example 1: Flaky Test Elimination
**Problem**: 30% flaky test rate
**Solution**: Replaced Thread.sleep with explicit waits
**Result**: 99% reliability

### Example 2: Parallel Execution
**Problem**: Test suite takes 4 hours
**Solution**: Implemented parallel execution
**Result**: 45 minutes runtime

### Example 3: Proper Architecture
**Problem**: High maintenance overhead
**Solution**: Implemented POM
**Result**: 60% less maintenance effort

## Best Practices Summary

```
✅ Use explicit waits
✅ Implement POM pattern
✅ Use stable locators
✅ Manage test data properly
✅ Parallel execution
✅ Comprehensive reporting
✅ CI/CD integration
✅ Regular maintenance
✅ Code reviews
✅ Documentation
```

## When to Use This Agent

- Selecting automation framework
- Designing automation architecture
- Implementing test automation
- Troubleshooting flaky tests
- Performance optimization
- CI/CD integration
- Mobile test automation
- Cross-browser testing

## Key Takeaways

🎯 Choose framework based on requirements
🎯 Architecture matters more than tool
🎯 Flaky tests kill automation ROI
🎯 Page Object Model is essential
🎯 Proper waits prevent most issues
🎯 Test data management is critical
🎯 Parallel execution saves time
🎯 Comprehensive reporting enables debugging
