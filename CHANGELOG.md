# Changelog

All notable changes to the QA Development Assistant plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2.0.0] - 2025-12-28

### Added
- marketplace.json for plugin marketplace compatibility
- SASMP v1.3.0 compliance for all agents
- Template v2.1.0 README format (18 required sections)
- Verified Installation notice
- Available Skills table with `Skill("...")` invoke syntax
- Usage Examples section
- Plugin Structure directory tree
- Technology Coverage table

### Changed
- plugin.json restructured to new format (paths, author object, repository string)
- README updated to template v2.1.0
- Quick Start commands fixed (`/plugin add marketplace` format)
- Version bump from 1.0.0 to 2.0.0
- hooks.json standardized to `{"hooks": {}}`

### Fixed
- E307: plugin.json repository format (object to string)
- E303: marketplace.name differs from plugin.name

---

## [1.0.0] - 2024-11-18

### Initial Release

**7 QA Specialist Agents**
- QA Fundamentals & Mindset
- Test Strategy & Planning
- Manual & Exploratory Testing
- Test Automation Frameworks
- API & Performance Testing
- CI/CD & Test Infrastructure
- Advanced QA & Leadership

**20 Comprehensive Skills**
- QA Fundamentals, SDLC, Mindset
- Test Planning, Design, Coverage
- Manual & Exploratory Testing
- Selenium, Cypress, Playwright, Appium
- REST/GraphQL API Testing
- Performance & Load Testing
- CI/CD, Docker, Continuous Testing
- Security Testing, QA Metrics, Leadership

**4 Main Commands**
- /qa-path, /qa-roadmap, /qa-tools, /qa-projects

**Status**: Production Ready

---

## Contributors

- **Dr. Umit Kacar** - Senior AI Researcher & Engineer
- **Muhsin Elcicek** - Senior Software Architect

---

*Last Updated: 2025-12-28*
