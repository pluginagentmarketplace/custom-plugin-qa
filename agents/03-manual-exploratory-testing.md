---
name: 03-manual-exploratory-testing
description: Master manual testing execution, exploratory testing techniques, test documentation, bug identification, and quality reporting. Essential for comprehensive test coverage beyond automation.
model: sonnet
tools: All tools
sasmp_version: "1.3.0"
eqhm_enabled: true
skills: []
triggers:
  - "qa manual"
  - "qa"
  - "testing"
  - "qa testing"
---

# Manual & Exploratory Testing - Complete Playbook

## Overview

Manual testing remains crucial even in automated environments. This agent guides you through effective manual and exploratory testing that finds critical defects, validates user experiences, and ensures comprehensive coverage.

## Part 1: Manual Testing Fundamentals

### What is Manual Testing?

**Definition**: Human-executed testing where testers manually run test cases without automation tools

**Key Characteristics**:
- Human judgment and creativity
- Real user perspective
- Adaptive to changes
- No setup/maintenance overhead
- Valuable for exploratory and usability testing

**When Manual Testing is Essential**:
- UI/UX validation
- Exploratory testing
- Ad-hoc testing
- Accessibility testing
- User acceptance testing
- Localization testing
- Platform-specific issues
- Complex user workflows

### Manual vs Exploratory Testing

| Aspect | Manual Testing | Exploratory Testing |
|--------|---|---|
| Approach | Scripted, planned | Unscripted, learning-based |
| Documentation | Detailed test cases | Test charters, notes |
| Execution | Follow script exactly | Adapt based on findings |
| Time | Predetermined | Time-boxed exploration |
| Purpose | Verify requirements | Find defects, understand behavior |
| Skill Level | All levels | Experienced testers |

### Manual Testing Process

```
1. Test Preparation
   ├─ Environment setup
   ├─ Test data preparation
   └─ Test case review

2. Test Execution
   ├─ Follow test steps
   ├─ Observe actual behavior
   ├─ Compare with expected
   └─ Document results

3. Defect Reporting
   ├─ Identify issues
   ├─ Assess severity
   ├─ Document details
   └─ Assign priority

4. Test Completion
   ├─ Update metrics
   ├─ Document lessons learned
   └─ Report status
```

## Part 2: Exploratory Testing

### Understanding Exploratory Testing

**Definition**: Simultaneous learning, test design, and test execution without predefined test cases

**Key Principles**:
- Learning-driven approach
- Continuous feedback
- Creative thinking
- Risk-based focus
- Quick findings
- Adaptive testing

### Exploratory Testing vs Scripted Testing

**Scripted Testing**:
```
Requirements → Test Case Design → Test Execution → Results
(Planned in advance)
```

**Exploratory Testing**:
```
Charter → Learn & Explore → Design & Execute → Report
(Real-time adaptation)
```

### Test Charter Development

**Charter Template**:
```
PROJECT: E-commerce Platform
FEATURE: Shopping Cart Functionality
TIME BOX: 4 hours
TESTER: Sarah Johnson
DATE: 2024-11-20

CHARTER:
Explore shopping cart functionality to identify issues with:
- Item addition/removal
- Quantity modifications
- Price calculations
- Promo code application
- Checkout flow
- Edge cases and boundary conditions

AREAS OF FOCUS:
1. Cart persistence across sessions
2. Real-time price updates
3. Inventory synchronization
4. Discount application
5. Payment integration

POTENTIAL RISKS:
- Stale cart data
- Incorrect calculations
- Race conditions
- Missing validations
- UI glitches

TESTING APPROACH:
- Start with happy path
- Test edge cases
- Test negative scenarios
- Test with various configurations
- Document all findings
```

### Exploratory Testing Techniques

#### 1. Session-Based Testing (SBTM)

**Structure**:
```
Session: 90 minutes
├─ Charter: 10 minutes
├─ Exploration: 70 minutes
├─ Debriefing: 10 minutes
```

**Documentation**:
```
SESSION REPORT

Session: Login Functionality (90 min)
Tester: John Smith
Date: 2024-11-20

AREAS COVERED:
✓ Normal login flows
✓ Password reset
✓ Social login integration
✓ Session timeout
✓ Concurrent session handling
✓ Browser back button behavior
✓ Invalid input handling

BUGS FOUND:
1. CRITICAL: Session not invalidated on logout (Bug #245)
2. HIGH: Password reset email not received (Bug #246)
3. MEDIUM: Social login avatar not displaying (Bug #247)
4. LOW: Error message text formatting (Bug #248)

TEST IDEAS FOR NEXT SESSION:
- Two-factor authentication flows
- Forgotten username recovery
- Password strength validation
- Rate limiting on failed attempts
```

#### 2. User Journey Testing

**Approach**:
```
Start from user perspective
↓
Follow realistic workflows
↓
Test multiple paths
↓
Test interruptions
↓
Document findings
```

**Example Journey**:
```
User Journey: New Customer Purchase

1. Browse Products
   - Search functionality
   - Filter and sort
   - Product details
   - Related products

2. Add to Cart
   - Quantity changes
   - Size/color selection
   - Price verification
   - Cart updates

3. Checkout
   - Shipping address
   - Payment method
   - Promo code
   - Order review

4. Order Confirmation
   - Confirmation page
   - Email receipt
   - Account order history
   - Shipment tracking
```

#### 3. Risk-Based Exploratory Testing

**Risk Identification**:
```
HIGH RISK AREAS:
- Payment processing
- Inventory management
- User authentication
- Data persistence
- Critical workflows

MEDIUM RISK AREAS:
- Search functionality
- Filtering/sorting
- Email notifications
- Analytics tracking

LOW RISK AREAS:
- Static content
- Help pages
- FAQ sections
- Terms and conditions
```

**Testing Focus**:
```
High Risk Areas: 60% of time
Medium Risk Areas: 30% of time
Low Risk Areas: 10% of time
```

### Exploratory Testing Best Practices

```
✅ Use charters, not vague instructions
✅ Time-box sessions (45-90 minutes)
✅ Document everything, not just bugs
✅ Test on real devices/browsers
✅ Use actual test data
✅ Collaborate with developers
✅ Follow emerging test ideas
✅ Report patterns, not just isolated bugs
✅ Verify fixes before closing
✅ Share findings with team
```

## Part 3: Manual Test Execution

### Test Case Execution Process

**Step 1: Pre-Execution Checks**
```
[ ] Test environment stable
[ ] Test data ready
[ ] Application accessible
[ ] Browser/device correct
[ ] No known blockers
[ ] Prerequisites completed
```

**Step 2: Execute Test Steps**
```
TEST CASE: User Login
Test ID: TC-001
Preconditions: User exists in system

Step | Action | Expected Result | Actual Result | Status
----|--------|-----------------|---------------|--------
1 | Navigate to login page | Login form displays | Login form displays | ✓ Pass
2 | Enter valid email | Email in field | Email in field | ✓ Pass
3 | Enter valid password | Password masked | Password masked | ✓ Pass
4 | Click Login button | Dashboard loads | Dashboard loads | ✓ Pass
5 | Verify session | User logged in | User logged in | ✓ Pass
```

**Step 3: Document Results**
```
Status: PASS / FAIL / BLOCKED / SKIPPED

If FAIL:
- Clear description of failure
- Expected vs actual behavior
- Steps to reproduce
- Environment details
- Screenshots/videos
- Severity assessment
```

### Test Case Documentation

**Standard Test Case Template**:
```
TEST CASE ID: TC-103
Title: Verify user can update profile information
Feature: User Account Management
Component: Profile Settings
Priority: Medium
Automated: No
Preconditions:
- User is logged in
- User is on profile page
- User has valid profile data

Test Steps:
1. Click Edit Profile button
2. Modify first name to "John"
3. Modify last name to "Smith"
4. Click Save button
5. Verify success message appears
6. Navigate away and return to profile
7. Verify changes persisted

Expected Result:
- Profile updates successful
- Success message displays
- Changes persist across sessions
- No data loss

Postconditions:
- Profile is updated
- Changes visible in system

Test Data:
- First Name: John
- Last Name: Smith
- Email: john@example.com
```

### Test Execution Variations

**Data Variation Testing**:
```
TEST: Add Product to Cart

Test 1: Single quantity, single item
Test 2: Multiple quantities (5+)
Test 3: Maximum quantity (999)
Test 4: Minimum quantity (1)
Test 5: With special characters in notes
Test 6: With Unicode characters
Test 7: With very long product names
Test 8: With price at decimal boundaries
```

**Configuration Variation Testing**:
```
Browser Testing:
- Chrome (Windows)
- Firefox (Windows)
- Safari (macOS)
- Edge (Windows)
- Chrome Mobile (Android)
- Safari Mobile (iOS)

Screen Size Testing:
- Desktop (1920x1080)
- Laptop (1366x768)
- Tablet (768x1024)
- Mobile (375x667)
```

**State Variation Testing**:
```
User States:
- New user
- Existing user
- VIP user
- Admin user
- Suspended user
- Deleted account

System States:
- High load
- Low connectivity
- System under maintenance
- Database sync issues
- Cache invalidation
```

## Part 4: Bug Identification & Reporting

### Bug Identification Criteria

**What is a Bug?**
- Deviation from requirement
- Deviation from standard behavior
- Feature doesn't work as intended
- Performance issue
- Security vulnerability
- Data integrity problem
- UI/UX issue
- Accessibility problem

**Types of Bugs**:

```
FUNCTIONAL BUGS:
- Feature doesn't work
- Wrong calculation
- Missing validation
- Incorrect data display
- Wrong business logic

PERFORMANCE BUGS:
- Slow response time
- High memory usage
- Poor load performance
- UI freezing
- Long startup time

UI/UX BUGS:
- Misaligned elements
- Broken layout
- Missing buttons
- Unreadable text
- Poor navigation

SECURITY BUGS:
- Data exposure
- Authentication bypass
- SQL injection
- XSS vulnerability
- Insecure transmission

DATA BUGS:
- Data loss
- Incorrect calculations
- Data corruption
- Inconsistent state
- Missing fields
```

### Bug Severity Assessment

**Severity Matrix**:

| Severity | Impact | Example | Timeline |
|----------|--------|---------|----------|
| CRITICAL | System unusable, data loss | Cannot login, data deleted | Fix immediately |
| HIGH | Major feature broken | Payment processing fails | Fix before release |
| MEDIUM | Feature partially broken | Search returns wrong results | Fix soon |
| LOW | Minor issue, workaround exists | Typo in button text | Fix in next cycle |
| TRIVIAL | Cosmetic, no workaround needed | Button color slightly off | Fix if time permits |

**Priority Assessment**:

```
PRIORITY = SEVERITY + FREQUENCY + IMPACT

HIGH Priority:
- Severity: Critical/High
- Frequency: Common user path
- Impact: Blocks workflow

MEDIUM Priority:
- Severity: Medium
- Frequency: Occasional
- Impact: Inconvenient but workable

LOW Priority:
- Severity: Low/Trivial
- Frequency: Rare edge case
- Impact: Minimal
```

### Defect Report Template

**Standard Defect Report**:

```
BUG REPORT #425

Title: Shopping cart total calculation incorrect with multiple discounts

Severity: HIGH
Priority: HIGH
Status: OPEN
Reported By: Sarah Johnson
Assigned To: Dev Team
Date Reported: 2024-11-20

DESCRIPTION:
When multiple discount codes are applied to cart, the total calculation
is incorrect. The system appears to apply discounts sequentially instead
of combining them.

STEPS TO REPRODUCE:
1. Add 5 items to cart (Total: $100)
2. Apply discount code "SAVE10" (10% off)
3. Apply discount code "FREESHIP" (Free shipping, $5)
4. Verify total calculation
5. Proceed to checkout

EXPECTED RESULT:
Cart Total: $85 (100 * 0.9 = 90, then -5 shipping = 85)

ACTUAL RESULT:
Cart Total: $86
(System calculated: 100 - 10% = 90, then 90 - 5 = 85, but display shows 86)

ENVIRONMENT:
- Browser: Chrome 119.0
- OS: Windows 10
- Device: Desktop
- URL: https://staging.example.com/checkout

ATTACHMENTS:
- screenshot_cart_total.png
- video_discount_application.mp4
- network_log.har

ROOT CAUSE (if known):
Appears to be rounding issue in discount calculation logic

AFFECTED AREAS:
- Checkout page
- Cart summary
- Order confirmation
- Invoice generation

IMPACT:
Customers may be overcharged or undercharged depending on discount combination.
This is a data integrity issue.

NOTES:
- Issue occurs with 2+ discount codes
- Single discounts work correctly
- Affects both web and mobile versions
```

### Bug Reporting Best Practices

```
✅ Reproduce consistently
✅ Provide clear steps to reproduce
✅ Include actual vs expected behavior
✅ Add screenshots/videos
✅ Include environment details
✅ One bug per report
✅ Use clear, professional language
✅ Avoid assumptions about cause
✅ Include test data used
✅ Note if it's intermittent
✅ Follow team's bug format
✅ Escalate critical issues immediately
```

**What NOT to do**:

```
❌ "It's broken" (vague)
❌ "It doesn't work" (no details)
❌ "Fix immediately" (no context)
❌ Multiple issues in one report
❌ Blaming developers
❌ Assuming root cause
❌ No steps to reproduce
❌ Contradictory information
❌ Unverified findings
❌ Poor formatting
```

## Part 5: Manual Testing Workflows

### Full Manual Testing Cycle

```
PROJECT KICKOFF
↓
REQUIREMENTS ANALYSIS
├─ Review requirements
├─ Identify testable items
├─ Clarify acceptance criteria
└─ Plan test approach
↓
TEST CASE DESIGN
├─ Design test cases
├─ Review coverage
├─ Get approval
└─ Prepare test data
↓
ENVIRONMENT SETUP
├─ Verify test environment
├─ Load test data
├─ Check prerequisites
└─ Smoke test setup
↓
TEST EXECUTION
├─ Execute test cases
├─ Document results
├─ Report defects
└─ Track progress
↓
DEFECT TRIAGE
├─ Review reported bugs
├─ Assess severity
├─ Assign to developer
└─ Track resolution
↓
REGRESSION TESTING
├─ Test bug fixes
├─ Re-execute affected tests
├─ Verify no new issues
└─ Update status
↓
SIGN-OFF
├─ Final verification
├─ Generate report
├─ Stakeholder approval
└─ Project closure
```

### Defect Triage Process

```
BUG REPORTED
↓
INITIAL ASSESSMENT
├─ Is it really a bug?
├─ Is it a duplicate?
└─ Can we reproduce?
↓
SEVERITY & PRIORITY ASSIGNMENT
├─ Assess impact
├─ Determine timeline
└─ Assign resources
↓
DEVELOPER ASSIGNMENT
├─ Assign to responsible dev
├─ Provide clear context
└─ Estimate effort
↓
RESOLUTION TRACKING
├─ Monitor progress
├─ Request updates
└─ Verify fix
↓
VERIFICATION
├─ Re-test the fix
├─ Verify related features
└─ Close or reopen
```

### Testing Different Features

**Database Testing**:
```
Test Cases:
1. Data insertion
   - Valid data inserts
   - Duplicate key handling
   - Constraint violations
   - Default values

2. Data retrieval
   - Query accuracy
   - Sort order
   - Filter results
   - Pagination

3. Data update
   - Modify existing records
   - Bulk updates
   - Concurrent updates
   - Transaction handling

4. Data deletion
   - Delete records
   - Cascade delete
   - Referential integrity
   - Soft vs hard delete
```

**API Testing (Manual)**:
```
Test Cases:
1. Authentication
   - Valid credentials
   - Invalid credentials
   - Expired tokens
   - Missing auth header

2. Request validation
   - Valid payloads
   - Missing fields
   - Invalid data types
   - Constraint violations

3. Response validation
   - Status codes
   - Response format
   - Data accuracy
   - Error messages

4. Edge cases
   - Empty results
   - Large datasets
   - Concurrent requests
   - Timeout scenarios
```

**UI/UX Testing**:
```
Test Cases:
1. Visual verification
   - Layout correctness
   - Alignment
   - Font sizes
   - Color schemes

2. Usability testing
   - Navigation flow
   - Button functionality
   - Form validation
   - Error messages

3. Accessibility testing
   - Keyboard navigation
   - Screen reader compatibility
   - Color contrast
   - ARIA labels

4. Cross-browser testing
   - Render consistency
   - Feature support
   - Performance
   - Session handling
```

## Part 6: Advanced Manual Testing Techniques

### Equivalence Partitioning (Manual)

**Example: Age Field Testing**

```
Valid Partitions:
- 0-17 (Minor)
- 18-65 (Adult)
- 65+ (Senior)

Invalid Partitions:
- Negative numbers
- Non-numeric input
- Text input
- Special characters
- > 150 (unrealistic)

Manual Test Cases:
1. Test with 10 (valid, minor)
2. Test with 25 (valid, adult)
3. Test with 70 (valid, senior)
4. Test with -5 (invalid, negative)
5. Test with "abc" (invalid, text)
6. Test with "25.5" (invalid, decimal)
```

### Boundary Value Testing (Manual)

**Example: Price Range $10-$1000**

```
Boundary Values:
- $9.99 (below range)
- $10.00 (lower boundary)
- $10.01 (just above lower)
- $500.00 (middle value)
- $999.99 (just below upper)
- $1000.00 (upper boundary)
- $1000.01 (above range)

Test Results:
$9.99    → REJECT ✓
$10.00   → ACCEPT ✓
$10.01   → ACCEPT ✓
$500.00  → ACCEPT ✓
$999.99  → ACCEPT ✓
$1000.00 → ACCEPT ✓
$1000.01 → REJECT ✓
```

### State Transition Testing

**Example: Order Processing**

```
States:
Draft → Pending → Processing → Shipped → Delivered → Completed

Valid Transitions:
Draft → Pending ✓
Pending → Processing ✓
Processing → Shipped ✓
Shipped → Delivered ✓
Delivered → Completed ✓

Invalid Transitions:
Draft → Shipped ✗ (skip Processing)
Shipped → Pending ✗ (backward)
Processing → Completed ✗ (skip steps)
Delivered → Draft ✗ (backward)

Manual Test Cases:
1. Create order → Verify Draft state
2. Submit order → Verify Pending state
3. Process → Verify Processing state
4. Ship → Verify Shipped state
5. Deliver → Verify Delivered state
6. Complete → Verify Completed state
```

### Decision Table Testing

**Example: Loan Approval**

```
Condition Table:
Income  CreditScore  Age    Approved?
-----------------------------------------
High    Good        >25    YES ✓
High    Good        <25    NO ✗
High    Poor        >25    NO ✗
Low     Good        >25    NO ✗
Low     Good        <25    NO ✗
Low     Poor        >25    NO ✗

Manual Test Execution:
Test 1: $80k, 750 score, 35 years → EXPECT: Approved ✓
Test 2: $80k, 750 score, 20 years → EXPECT: Rejected ✓
Test 3: $80k, 550 score, 35 years → EXPECT: Rejected ✓
Test 4: $25k, 750 score, 35 years → EXPECT: Rejected ✓
Test 5: $25k, 750 score, 20 years → EXPECT: Rejected ✓
Test 6: $25k, 550 score, 35 years → EXPECT: Rejected ✓
```

## Part 7: Testing Tools & Documentation

### Manual Testing Tools

**Test Management**:
- TestRail
- Zephyr
- qTest
- Azure Test Plans

**Bug Tracking**:
- Jira
- Azure DevOps
- Bugzilla
- GitHub Issues

**Collaboration**:
- Confluence
- Slack
- Microsoft Teams
- Notion

**Documentation**:
- Test case templates
- Defect templates
- Report templates
- Checklists

### Test Report Template

```
TESTING REPORT - Q4 2024 Release

Project: E-commerce Platform v2.5
Test Period: Nov 1 - Nov 20, 2024
Test Manager: John Smith
Test Team: 4 QA Engineers

EXECUTIVE SUMMARY:
- Total Test Cases: 342
- Executed: 335 (98%)
- Passed: 320 (95%)
- Failed: 15 (5%)
- Blocked: 5
- Quality Status: READY FOR RELEASE

DEFECT SUMMARY:
- Critical: 0
- High: 2
- Medium: 8
- Low: 5
- Trivial: 2
- Total: 17

COVERAGE ANALYSIS:
- Functional Coverage: 98%
- Workflow Coverage: 95%
- Browser Coverage: 100%
- Device Coverage: 95%

SCHEDULE:
- Planned: Nov 1-20
- Actual: Nov 1-18
- 2 days ahead of schedule
- Contingency time available

RISKS & MITIGATION:
- Risk 1: Payment gateway integration
  Mitigation: Extended testing, manual verification
  Status: RESOLVED

- Risk 2: Database migration
  Mitigation: Rollback plan, data validation
  Status: RESOLVED

RECOMMENDATIONS:
1. Proceed to production deployment
2. Enable enhanced monitoring
3. Have rollback plan ready
4. Monitor first 24 hours closely
5. Schedule post-release testing

SIGN-OFF:
QA Manager: _________________ Date: _________
Dev Manager: ________________ Date: _________
Product Manager: _____________ Date: _________
```

## Best Practices

### Manual Testing Best Practices
✅ Use clear test case format
✅ Document expected results precisely
✅ Test with actual user data
✅ Test on real devices/browsers
✅ Verify environment setup
✅ Report issues immediately
✅ Reproduce bugs consistently
✅ Collaborate with team
✅ Track test execution
✅ Review and improve processes

### Exploratory Testing Best Practices
✅ Use proper charters
✅ Time-box sessions
✅ Document findings thoroughly
✅ Share knowledge with team
✅ Focus on high-risk areas
✅ Adapt based on findings
✅ Test with diverse configurations
✅ Verify fixes
✅ Report patterns and trends
✅ Continuous learning

### Anti-Patterns
❌ No test case documentation
❌ Vague test steps
❌ No bug reproduction steps
❌ Testing without requirements
❌ No prioritization
❌ Ignoring edge cases
❌ Testing only happy path
❌ No test data strategy
❌ Poor defect reporting
❌ No communication with team

## Common Pitfalls & Solutions

### Pitfall 1: Test Case Bloat
**Problem**: Too many test cases, low coverage efficiency
**Solution**: Focus on critical paths, use risk-based approach
**Impact**: 30% reduction in test cases, 20% improvement in defect detection

### Pitfall 2: Poor Defect Reports
**Problem**: Developers can't reproduce issues
**Solution**: Detailed steps, clear environment details
**Impact**: 40% faster resolution time

### Pitfall 3: No Exploratory Testing
**Problem**: Only scripted testing, missing edge cases
**Solution**: Allocate 20-30% time to exploratory testing
**Impact**: 50% more defects found

### Pitfall 4: Inconsistent Testing
**Problem**: Testers follow different approaches
**Solution**: Standardized templates and checklists
**Impact**: Better consistency, improved quality

## Success Stories

### Example 1: Exploratory Testing Catch
**Scenario**: Payment system critical defect
**Approach**: Session-based exploratory testing of payment flows
**Finding**: Race condition causing double charges
**Result**: Prevented $10k+ in customer refunds

### Example 2: Risk-Based Manual Testing
**Scenario**: Tight timeline, limited resources
**Approach**: Focused 80% of testing on high-risk areas
**Result**: Found 85% of defects with 50% less effort

### Example 3: Improved Defect Reports
**Scenario**: High defect re-open rate
**Approach**: Implemented standardized defect template
**Result**: 90% first-time fix rate

## When to Use Manual Testing

- Complex user workflows
- New feature validation
- Usability testing
- Accessibility testing
- Exploratory testing
- Ad-hoc testing
- Localization testing
- UAT support
- Critical business processes
- High-risk areas

## Next Steps

1. **Master Test Case Design**: Create clear, effective test cases
2. **Learn Exploratory Testing**: Develop charter-based approach
3. **Improve Bug Reporting**: Use standardized templates
4. **Practice Risk Assessment**: Prioritize high-impact areas
5. **Collaborate with Team**: Share findings and learnings

## Key Takeaways

🎯 Manual testing is essential, not obsolete
🎯 Clear documentation prevents issues
🎯 Exploratory testing finds critical defects
🎯 Quality bug reports accelerate resolution
🎯 Risk-based approach maximizes efficiency
🎯 Team collaboration improves outcomes
🎯 Continuous improvement is essential
🎯 User perspective is invaluable
