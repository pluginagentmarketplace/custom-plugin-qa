---
name: mobile-automation
description: Master mobile app testing with Appium, iOS/Android automation, and mobile best practices.
---

# Mobile Testing & Appium

## Appium Setup

```python
from appium import webdriver

desired_caps = {
    'platformName': 'Android',
    'deviceName': 'Android Emulator',
    'appPackage': 'com.example.app',
    'appActivity': '.MainActivity'
}

driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)
element = driver.find_element('id', 'com.example.app:id/button')
element.click()
```

## Mobile Locators
- ID: `find_element('id', 'resource-id')`
- Accessibility ID: `find_element('accessibility id', 'id')`
- XPath: `find_element('xpath', 'expression')`
- Class Name: `find_element('class name', 'name')`

## Mobile Testing Types
- Touch gestures
- Device rotation
- Network conditions
- Battery level
- Location

## Best Practices

✅ Real device testing
✅ Emulator testing
✅ Touch-specific tests
✅ Network simulation
✅ Mobile gestures
✅ App lifecycle
✅ Performance monitoring
