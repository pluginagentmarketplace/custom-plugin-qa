---
name: mobile-appium-automation
description: Master Appium, mobile app testing, iOS/Android automation, and mobile-specific testing strategies.
---

# Mobile Automation with Appium

## Setup

```python
desired_caps = {
  'platformName': 'Android',
  'deviceName': 'Android Emulator',
  'app': '/path/to/app.apk'
}
driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)
```

## Mobile Specific

- Touch gestures
- Device rotation
- Network simulation
- Battery level
- Location testing

## Best Practices

✅ Real device testing
✅ Emulator testing
✅ Gesture testing
✅ Network scenarios
