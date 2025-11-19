---
name: selenium-webdriver-automation
description: Master Selenium WebDriver, web automation, locator strategies, waits, interactions, and cross-browser testing.
---

# Selenium WebDriver Automation

## Basics

```python
from selenium import webdriver
driver = webdriver.Chrome()
driver.get("https://example.com")
element = driver.find_element("id", "element_id")
element.click()
```

## Locators

- ID
- CSS Selector
- XPath
- Class Name
- Tag Name

## Waits

### Implicit
```python
driver.implicitly_wait(10)
```

### Explicit
```python
WebDriverWait(driver, 10).until(
  EC.presence_of_element_located(("id", "element"))
)
```

## Best Practices

✅ Use explicit waits
✅ Stable locators
✅ Page Object Model
✅ Error handling
