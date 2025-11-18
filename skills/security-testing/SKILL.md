---
name: security-testing
description: Master OWASP Top 10 testing, vulnerability scanning, SQL injection, XSS, authentication testing, compliance.
---

# Security Testing & OWASP

## Quick Start - OWASP Top 10

### 1. Injection
- SQL injection
- NoSQL injection
- Command injection
**Prevention**: Parameterized queries, input validation

### 2. Broken Authentication
- Weak passwords
- Session fixation
- Credential leakage
**Prevention**: MFA, secure session management

### 3. Sensitive Data Exposure
- Unencrypted data
- Weak encryption
- Information disclosure
**Prevention**: Encryption, secure transmission

### 4. XML External Entities (XXE)
- Entity expansion
- External entity reference
**Prevention**: Disable external entities

### 5. Broken Access Control
- Privilege escalation
- Unauthorized access
**Prevention**: RBAC, least privilege

### 6. Security Misconfiguration
- Default credentials
- Unnecessary services
- Debug mode enabled
**Prevention**: Security hardening, configuration review

### 7. Cross-Site Scripting (XSS)
- DOM-based XSS
- Stored XSS
- Reflected XSS
**Prevention**: Input validation, output encoding

### 8. Insecure Deserialization
- Object injection
- Arbitrary code execution
**Prevention**: Type checking, integrity validation

### 9. Using Known Vulnerabilities
- Unpatched components
- Outdated libraries
**Prevention**: Dependency scanning, updates

### 10. Insufficient Logging
- Missing audit trails
- Inadequate monitoring
**Prevention**: Security logging, alerting

## Testing Tools

### OWASP ZAP
- Automated scanning
- Manual testing
- Reporting

### Burp Suite
- Web application scanning
- Vulnerability detection
- Compliance checking

### SonarQube
- Code analysis
- Security issues
- OWASP compliance

## Testing Approach

✅ Threat modeling
✅ Code review
✅ Penetration testing
✅ Automated scanning
✅ Compliance validation
✅ Security regression

## Related Skills
- Security Testing & Compliance
- Test Automation & CI/CD
