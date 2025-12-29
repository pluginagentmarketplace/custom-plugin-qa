<div align="center">

# QA Development Assistant

### Complete Quality Assurance Mastery for Claude Code

**Master test automation, API testing, performance testing, and CI/CD with 7 specialized agents and 20 production-ready skills**

[![Verified](https://img.shields.io/badge/Verified-Working-success?style=flat-square&logo=checkmarx)](https://github.com/pluginagentmarketplace/custom-plugin-qa)
[![License](https://img.shields.io/badge/License-Custom-yellow?style=flat-square)](LICENSE)
[![Version](https://img.shields.io/badge/Version-2.0.0-blue?style=flat-square)](https://github.com/pluginagentmarketplace/custom-plugin-qa)
[![Status](https://img.shields.io/badge/Status-Production_Ready-brightgreen?style=flat-square)](https://github.com/pluginagentmarketplace/custom-plugin-qa)
[![Agents](https://img.shields.io/badge/Agents-7-orange?style=flat-square)](#agents-overview)
[![Skills](https://img.shields.io/badge/Skills-20-purple?style=flat-square)](#skills-reference)
[![SASMP](https://img.shields.io/badge/SASMP-v1.3.0-blueviolet?style=flat-square)](#)

[![Selenium](https://img.shields.io/badge/Selenium-43B02A?style=for-the-badge&logo=selenium&logoColor=white)](skills/09-selenium-webdriver/)
[![Cypress](https://img.shields.io/badge/Cypress-17202C?style=for-the-badge&logo=cypress&logoColor=white)](skills/10-cypress-playwright/)
[![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge&logo=playwright&logoColor=white)](skills/10-cypress-playwright/)
[![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)](skills/12-rest-api-testing/)

[Quick Start](#quick-start) | [Agents](#agents-overview) | [Skills](#skills-reference) | [Commands](#commands)

</div>

---

## Verified Installation

> **This plugin has been tested and verified working on Claude Code.**
> Last verified: December 2025

---

## Quick Start

### Option 1: Install from GitHub (Recommended)

```bash
# Step 1: Add the marketplace from GitHub
/plugin add marketplace pluginagentmarketplace/custom-plugin-qa

# Step 2: Install the plugin
/plugin install qa-development-assistant@pluginagentmarketplace-qa

# Step 3: Restart Claude Code to load new plugins
```

### Option 2: Clone and Load Locally

```bash
# Clone the repository
git clone https://github.com/pluginagentmarketplace/custom-plugin-qa.git

# Navigate to the directory in Claude Code
cd custom-plugin-qa

# Load the plugin
/plugin load .
```

After loading, restart Claude Code.

### Verify Installation

After restarting Claude Code, verify the plugin is loaded. You should see these agents available:

```
custom-plugin-qa:01-qa-fundamentals
custom-plugin-qa:02-test-strategy-planning
custom-plugin-qa:03-manual-exploratory-testing
custom-plugin-qa:04-test-automation-frameworks
custom-plugin-qa:05-api-performance-testing
custom-plugin-qa:06-cicd-infrastructure
custom-plugin-qa:07-advanced-qa-leadership
```

---

## Available Skills

Once installed, these 20 skills become available:

| Skill | Invoke Command | Golden Format |
|-------|----------------|---------------|
| QA Fundamentals | `Skill("custom-plugin-qa:01-qa-basics")` | qa-basics.yaml |
| SDLC & QA | `Skill("custom-plugin-qa:02-sdlc-qa")` | sdlc-phases.yaml |
| QA Mindset | `Skill("custom-plugin-qa:03-qa-mindset")` | mindset-checklist.yaml |
| Test Planning | `Skill("custom-plugin-qa:04-test-planning")` | test-plan-template.yaml |
| Test Design | `Skill("custom-plugin-qa:05-test-design-techniques")` | design-patterns.yaml |
| Coverage Analysis | `Skill("custom-plugin-qa:06-coverage-analysis")` | coverage-matrix.yaml |
| Manual Testing | `Skill("custom-plugin-qa:07-manual-testing")` | test-case-template.yaml |
| Exploratory Testing | `Skill("custom-plugin-qa:08-exploratory-testing")` | session-charter.yaml |
| Selenium WebDriver | `Skill("custom-plugin-qa:09-selenium-webdriver")` | selenium-config.yaml |
| Cypress & Playwright | `Skill("custom-plugin-qa:10-cypress-playwright")` | cypress-config.yaml |
| Mobile Appium | `Skill("custom-plugin-qa:11-mobile-appium")` | appium-caps.yaml |
| REST API Testing | `Skill("custom-plugin-qa:12-rest-api-testing")` | postman-collection.json |
| GraphQL Testing | `Skill("custom-plugin-qa:13-graphql-testing")` | graphql-queries.yaml |
| Performance Testing | `Skill("custom-plugin-qa:14-performance-load-testing")` | jmeter-test-plan.jmx |
| CI/CD Pipelines | `Skill("custom-plugin-qa:15-cicd-pipelines")` | github-actions.yaml |
| Docker Testing | `Skill("custom-plugin-qa:16-docker-testing")` | docker-compose.yaml |
| Continuous Testing | `Skill("custom-plugin-qa:17-continuous-testing")` | ct-pipeline.yaml |
| Security Testing | `Skill("custom-plugin-qa:18-security-testing")` | owasp-checklist.yaml |
| QA Metrics | `Skill("custom-plugin-qa:19-qa-metrics-reporting")` | metrics-dashboard.yaml |
| QA Leadership | `Skill("custom-plugin-qa:20-qa-leadership")` | team-charter.yaml |

---

## What This Plugin Does

This plugin provides **7 specialized agents** and **20 production-ready skills** for QA mastery:

| Agent | Purpose |
|-------|---------|
| **QA Fundamentals** | Testing types, quality principles, SDLC |
| **Test Strategy** | Test planning, coverage analysis, prioritization |
| **Manual Testing** | Exploratory testing, test cases, bug reporting |
| **Test Automation** | Selenium, Cypress, Playwright, Appium |
| **API & Performance** | REST/GraphQL testing, load testing, JMeter |
| **CI/CD Infrastructure** | Continuous testing, Docker, pipelines |
| **Advanced QA** | Security testing, metrics, team leadership |

---

## Agents Overview

### 7 Implementation Agents

Each agent is designed to **do the work**, not just explain:

| Agent | Capabilities | Example Prompts |
|-------|--------------|-----------------|
| **QA Fundamentals** | Testing basics, quality mindset | `"Explain testing types"`, `"QA in Agile"` |
| **Test Strategy** | Test plans, risk analysis | `"Create test plan"`, `"Prioritize test cases"` |
| **Manual Testing** | Test execution, bug reports | `"Write test cases"`, `"Exploratory testing session"` |
| **Test Automation** | Selenium, Cypress, Playwright | `"Create Cypress tests"`, `"Page Object Model"` |
| **API & Performance** | Postman, JMeter, k6 | `"Test REST API"`, `"Load test with k6"` |
| **CI/CD Infrastructure** | GitHub Actions, Docker | `"Set up test pipeline"`, `"Containerize tests"` |
| **Advanced QA** | OWASP, metrics, leadership | `"Security test plan"`, `"QA metrics dashboard"` |

---

## Commands

4 interactive commands for QA workflows:

| Command | Usage | Description |
|---------|-------|-------------|
| `/qa-path` | `/qa-path` | Choose learning path by skill level |
| `/qa-roadmap` | `/qa-roadmap` | View complete QA career roadmap |
| `/qa-tools` | `/qa-tools` | Explore tools and frameworks |
| `/qa-projects` | `/qa-projects` | Browse 30+ hands-on projects |

---

## Skills Reference

Each skill includes **Golden Format** content:
- `assets/` - YAML templates and configurations
- `scripts/` - Automation and validation scripts
- `references/` - Methodology guides and best practices

### All 20 Skills by Category

| Category | Skills |
|----------|--------|
| **Fundamentals** | qa-basics, sdlc-qa, qa-mindset |
| **Test Strategy** | test-planning, test-design-techniques, coverage-analysis |
| **Manual Testing** | manual-testing, exploratory-testing |
| **Automation** | selenium-webdriver, cypress-playwright, mobile-appium |
| **API Testing** | rest-api-testing, graphql-testing |
| **Performance** | performance-load-testing |
| **CI/CD** | cicd-pipelines, docker-testing, continuous-testing |
| **Advanced** | security-testing, qa-metrics-reporting, qa-leadership |

---

## Usage Examples

### Example 1: Create Cypress E2E Tests

```javascript
// Before: Manual browser testing

// After (with Test Automation agent):
Skill("custom-plugin-qa:10-cypress-playwright")

// Generates:
// - Cypress project setup
// - Page Object Model structure
// - E2E test specs
// - CI/CD integration
```

### Example 2: Set Up API Testing Suite

```javascript
// Before: Manual API testing

// After (with API Testing agent):
Skill("custom-plugin-qa:12-rest-api-testing")

// Provides:
// - Postman collection structure
// - Environment configuration
// - Test scripts for validation
// - Newman CI integration
```

### Example 3: Performance Load Test

```yaml
# Before: No performance testing

# After (with Performance agent):
Skill("custom-plugin-qa:14-performance-load-testing")

# Creates:
# - JMeter test plan
# - k6 load scripts
# - Performance thresholds
# - Results analysis guide
```

---

## Plugin Structure

```
custom-plugin-qa/
├── .claude-plugin/
│   ├── plugin.json           # Plugin manifest
│   └── marketplace.json      # Marketplace config
├── agents/                   # 7 specialized agents
│   ├── 01-qa-fundamentals.md
│   ├── 02-test-strategy-planning.md
│   ├── 03-manual-exploratory-testing.md
│   ├── 04-test-automation-frameworks.md
│   ├── 05-api-performance-testing.md
│   ├── 06-cicd-infrastructure.md
│   └── 07-advanced-qa-leadership.md
├── skills/                   # 20 skills (Golden Format)
│   ├── 01-qa-basics/
│   ├── 09-selenium-webdriver/
│   ├── 10-cypress-playwright/
│   ├── 12-rest-api-testing/
│   └── ... (16 more skills)
├── commands/                 # 4 slash commands
│   ├── qa-learning-path.md
│   ├── qa-roadmap.md
│   ├── qa-tools-frameworks.md
│   └── qa-projects.md
├── hooks/hooks.json
├── README.md
├── CHANGELOG.md
└── LICENSE
```

---

## Technology Coverage

| Category | Technologies |
|----------|--------------|
| **UI Automation** | Selenium WebDriver, Cypress, Playwright |
| **Mobile** | Appium, XCUITest, Espresso |
| **API Testing** | Postman, REST Assured, Supertest |
| **Performance** | JMeter, k6, Gatling, Locust |
| **CI/CD** | Jenkins, GitHub Actions, GitLab CI |
| **Containers** | Docker, Kubernetes, Docker Compose |
| **Security** | OWASP ZAP, Burp Suite, SonarQube |
| **Reporting** | Allure, ExtentReports, TestRail |

---

## Learning Paths

| Path | Duration | Focus |
|------|----------|-------|
| QA Beginner | 4-6 weeks | Fundamentals, manual testing |
| Test Automation | 6-8 weeks | Selenium, Cypress, CI/CD |
| API Specialist | 4-5 weeks | REST, GraphQL, performance |
| QA Lead | 8-10 weeks | Strategy, metrics, leadership |

---

## Security Notice

This plugin is designed for **authorized testing use only**:

**USE FOR:**
- Learning QA practices
- Building test automation
- Performance testing
- Security testing (authorized)

**SECURITY TOPICS:**
- OWASP Top 10 testing
- Penetration testing basics
- Vulnerability scanning
- Security test automation

---

## Metadata

| Field | Value |
|-------|-------|
| **Last Updated** | 2025-12-28 |
| **Maintenance Status** | Active |
| **SASMP Version** | 1.3.0 |
| **Support** | [Issues](../../issues) |

---

## License

Custom License - See [LICENSE](LICENSE) for details.

Copyright (c) 2025 Dr. Umit Kacar & Muhsin Elcicek

---

## Contributing

Contributions are welcome:

1. Fork the repository
2. Create a feature branch
3. Follow the Golden Format for new skills
4. Submit a pull request

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

---

## Contributors

**Authors:**
- **Dr. Umit Kacar** - Senior AI Researcher & Engineer
- **Muhsin Elcicek** - Senior Software Architect

---

<div align="center">

**Master QA with AI assistance!**

[![Made for QA](https://img.shields.io/badge/Made%20for-QA%20Engineers-43B02A?style=for-the-badge&logo=selenium)](https://github.com/pluginagentmarketplace/custom-plugin-qa)

**Built by Dr. Umit Kacar & Muhsin Elcicek**

*Based on [roadmap.sh/qa](https://roadmap.sh/qa)*

</div>
