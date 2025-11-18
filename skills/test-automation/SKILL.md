---
name: selenium-webdriver
description: Master Selenium WebDriver, browser automation, locators, waits, and automation framework design.
---

# Selenium & WebDriver Automation

## Selenium Basics

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://example.com")
element = driver.find_element(By.ID, "element-id")
element.click()
driver.quit()
```

## Locator Strategies
- ID: `find_element(By.ID, "id")`
- CSS Selector: `find_element(By.CSS_SELECTOR, "selector")`
- XPath: `find_element(By.XPATH, "xpath")`
- Class: `find_element(By.CLASS_NAME, "class")`

## Waits

### Implicit Wait
```python
driver.implicitly_wait(10)
```

### Explicit Wait
```python
from selenium.webdriver.support.ui import WebDriverWait
wait = WebDriverWait(driver, 10)
element = wait.until(EC.presence_of_element_located((By.ID, "id")))
```

## Best Practices

✅ Use explicit waits
✅ Unique, stable locators
✅ Page Object Model
✅ Error handling
✅ Screenshots on failure
✅ Parallel execution
✅ Maintenance focus
