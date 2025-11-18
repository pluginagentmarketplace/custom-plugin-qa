---
name: security-authentication
description: Master application security, authentication, authorization, data protection, and compliance. Build secure systems resistant to common attacks.
---

# Security & Authentication

## Quick Start

### Secure Password Storage
```javascript
const bcrypt = require('bcrypt');

// Hashing
const hashedPassword = await bcrypt.hash(password, 10);

// Verification
const isMatch = await bcrypt.compare(password, hashedPassword);
```

### JWT Authentication
```javascript
const jwt = require('jsonwebtoken');

// Generate token
const token = jwt.sign(
  { userId: 123 },
  process.env.JWT_SECRET,
  { expiresIn: '1h' }
);

// Verify token
const decoded = jwt.verify(token, process.env.JWT_SECRET);
```

### Basic Helmet Setup
```javascript
const helmet = require('helmet');
const express = require('express');
const app = express();

app.use(helmet()); // Sets security headers
```

## OWASP Top 10

### 1. Injection

#### SQL Injection
```javascript
// BAD - Vulnerable
query = "SELECT * FROM users WHERE id = " + userId;

// GOOD - Parameterized
query = "SELECT * FROM users WHERE id = ?";
db.query(query, [userId]);
```

#### Prevention
- Parameterized queries
- Prepared statements
- Input validation
- Escape special characters
- ORMs with built-in protection

### 2. Broken Authentication

#### Weak Passwords
```
❌ "password" (common, easy)
❌ "123456" (sequential)
✅ "P@ssw0rd!xY9zQ" (strong, unique)
```

#### Password Policy Requirements
- Minimum 12 characters
- Mix of uppercase, lowercase, numbers, symbols
- Dictionary checks
- History to prevent reuse
- Expiration (debate: maybe not needed)

#### Multi-Factor Authentication (MFA)
```javascript
// SMS-based MFA
async function sendOTP(phone) {
  const code = generateRandomCode(6);
  await sms.send(phone, `Your code: ${code}`);
  return storeOTP(phone, code, expiresIn: 5);
}

async function verifyOTP(phone, code) {
  return validateOTP(phone, code);
}
```

#### Session Management
- Secure session tokens
- HttpOnly cookies
- Secure flag for HTTPS
- Proper logout
- Session timeout
- Concurrent session limits

### 3. Sensitive Data Exposure

#### Data Encryption
```javascript
const crypto = require('crypto');

// Encrypt data
function encrypt(data, key) {
  const iv = crypto.randomBytes(16);
  const cipher = crypto.createCipheriv('aes-256-cbc', key, iv);
  return iv.toString('hex') + ':' + cipher.update(data, 'utf8', 'hex') + cipher.final('hex');
}

// Decrypt data
function decrypt(encrypted, key) {
  const [iv, data] = encrypted.split(':');
  const decipher = crypto.createDecipheriv('aes-256-cbc', key, Buffer.from(iv, 'hex'));
  return decipher.update(data, 'hex', 'utf8') + decipher.final('utf8');
}
```

#### HTTPS/TLS
- Always use HTTPS in production
- Valid SSL certificates
- Strong cipher suites
- HSTS headers
- Certificate pinning for mobile

#### PII Data Protection
- Encryption at rest
- Encryption in transit
- Minimal collection
- Retention limits
- Secure deletion

### 4. XML External Entities (XXE)

```javascript
// BAD - Vulnerable
const libxmljs = require('libxmljs');
const doc = libxmljs.parseXml(userInput);

// GOOD - Disable external entities
const result = libxmljs.parseXml(userInput, {
  noent: false,
  nocdata: true,
  nocdata: true
});
```

### 5. Broken Access Control

#### Role-Based Access Control (RBAC)
```javascript
const roles = {
  admin: ['read', 'write', 'delete'],
  user: ['read'],
  guest: ['read']
};

function authorize(user, action) {
  return roles[user.role].includes(action);
}
```

#### Attribute-Based Access Control (ABAC)
```javascript
function canAccess(user, resource, action) {
  return (
    user.department === resource.department &&
    user.role === 'admin' &&
    resource.status === 'active'
  );
}
```

#### API Authorization
```javascript
app.get('/api/users/:id', authenticate, authorize('admin'), (req, res) => {
  // Only authenticated admins can access
});
```

### 6. Security Misconfiguration

#### Secure Defaults
```javascript
// Error handling - don't expose internals
app.use((err, req, res, next) => {
  console.error(err); // Log internally
  res.status(500).json({ error: 'Internal Server Error' }); // Generic message
});

// Remove unnecessary headers
app.disable('x-powered-by');

// Use security headers
app.use(helmet());
```

#### Disable Unnecessary Services
- Only enable required services
- Remove test endpoints in production
- Disable debug mode
- Hide version information

### 7. Cross-Site Scripting (XSS)

#### Prevention Methods

**Stored XSS Prevention:**
```javascript
// Sanitize input
const sanitize = (input) => {
  return input.replace(/</g, '&lt;').replace(/>/g, '&gt;');
};

// Store sanitized data
const sanitizedInput = sanitize(userInput);
db.save(sanitizedInput);
```

**Reflected XSS Prevention:**
```javascript
// Escape output
const escaped = escapeHtml(userInput);
res.send(`<p>${escaped}</p>`);
```

**DOM-based XSS Prevention:**
```javascript
// Good: Use textContent instead of innerHTML
element.textContent = userInput; // Safe

// Bad: innerHTML can execute scripts
element.innerHTML = userInput; // Vulnerable
```

#### Content Security Policy (CSP)
```javascript
app.use((req, res, next) => {
  res.setHeader(
    'Content-Security-Policy',
    "default-src 'self'; script-src 'self' 'unsafe-inline'"
  );
  next();
});
```

### 8. Insecure Deserialization

```javascript
// Bad - Unsafe deserialization
const data = JSON.parse(userInput); // Object injection risk

// Good - Validate structure
const schema = {
  name: { type: 'string', maxLength: 100 },
  age: { type: 'number', min: 0, max: 150 }
};
const data = validateAndParse(userInput, schema);
```

### 9. Using Components with Known Vulnerabilities

#### Dependency Management
```bash
# Check for vulnerabilities
npm audit

# Update to patch versions
npm update

# Review advisories
npm audit report
```

#### Tools
- npm audit
- SNYK
- Dependabot
- Black Duck
- WhiteSource

### 10. Insufficient Logging & Monitoring

#### Security Logging
```javascript
function logSecurityEvent(event, user, details) {
  const log = {
    timestamp: new Date(),
    event,
    userId: user.id,
    ip: req.ip,
    userAgent: req.headers['user-agent'],
    details
  };
  logger.warn(log);
}

// Log failed login attempts
logSecurityEvent('login_failed', user, { reason: 'invalid_password' });

// Log unauthorized access attempts
logSecurityEvent('unauthorized_access', user, { resource: '/admin' });
```

## Authentication Methods

### Session-Based
- Traditional approach
- Server maintains session store
- Cookies store session ID
- Suitable for web apps

### Token-Based (JWT)
- Stateless approach
- Token contains claims
- No server-side session store
- Suitable for APIs and SPAs

### OAuth2
- Third-party authorization
- User delegates access
- Token-based
- Suitable for social login

### OpenID Connect
- Built on OAuth2
- Authentication layer
- User information
- Suitable for SSO

## Secure Development Practices

### Code Review
- Security-focused reviews
- Peer review process
- Automated scanning (SAST)
- Manual code inspection

### Security Testing
- Penetration testing
- Vulnerability scanning (DAST)
- Security audits
- Threat modeling

### Secrets Management
```javascript
// Use environment variables
const apiKey = process.env.API_KEY;

// Use vault systems
const vault = require('node-vault');
const secret = await vault.read('secret/api-key');
```

### Secure Libraries
- Use well-maintained libraries
- Check security track record
- Monitor for advisories
- Regular updates

## Compliance & Standards

### GDPR (EU)
- Consent for data collection
- Right to access
- Right to deletion
- Data protection impact assessment

### CCPA (California)
- Consumer data rights
- Opt-out mechanisms
- Data inventory
- Privacy policy requirements

### PCI-DSS (Payment Processing)
- Secure network architecture
- Protect cardholder data
- Regular security testing
- Access control policies

### HIPAA (Healthcare)
- Protect patient health information
- Access controls
- Audit controls
- Integrity controls

## Best Practices

✅ Use HTTPS everywhere
✅ Hash passwords with bcrypt/Argon2
✅ Implement rate limiting
✅ Validate all inputs
✅ Use parameterized queries
✅ Implement proper logging
✅ Keep dependencies updated
✅ Use security headers
✅ Implement MFA
✅ Regular security audits

❌ Don't hardcode secrets
❌ Don't trust client-side validation
❌ Don't expose error details
❌ Don't use weak encryption
❌ Don't store passwords in plain text
❌ Don't ignore security updates
❌ Don't disable security features
❌ Don't log sensitive data

## Security Headers

### Essential Headers
```javascript
app.use((req, res, next) => {
  res.setHeader('X-Content-Type-Options', 'nosniff');
  res.setHeader('X-Frame-Options', 'DENY');
  res.setHeader('X-XSS-Protection', '1; mode=block');
  res.setHeader('Strict-Transport-Security', 'max-age=31536000');
  res.setHeader('Referrer-Policy', 'no-referrer');
  next();
});
```

## Incident Response

### Steps
1. **Detection**: Identify security incident
2. **Investigation**: Gather information
3. **Containment**: Stop the incident
4. **Eradication**: Remove the threat
5. **Recovery**: Restore systems
6. **Post-Incident**: Review and improve

## Related Skills
- System Architecture
- DevOps & Infrastructure
- Backend Development

## Next Steps
Implement security best practices, conduct security audits, and stay updated on vulnerabilities.
