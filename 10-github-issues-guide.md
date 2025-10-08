# GitHub Issues Guide

Minimal guidelines for creating effective GitHub issues.

## 📋 Issue Types & Templates

### 🚀 Feature Request

```markdown
## What feature do you want?

Brief description of the new feature.

## Why is this needed?

Explain the problem this solves or value it provides.

## Acceptance Criteria

- [ ] User can do X
- [ ] System responds with Y
- [ ] Error handling for Z

## Additional Context

Any relevant background, mockups, or examples.
```

**Example:**

```markdown
## What feature do you want?

Add user authentication with email/password login.

## Why is this needed?

Users need to securely access their accounts and data.

## Acceptance Criteria

- [ ] User can register with email/password
- [ ] User can login with valid credentials
- [ ] User gets error for invalid credentials
- [ ] Password is securely hashed
- [ ] Session persists across browser refreshes

## Additional Context

This is part of the MVP requirements. Should integrate with existing user management system.
```

**More Examples:**

```markdown
## What feature do you want?

Add dark mode toggle to the application.

## Why is this needed?

Users have requested dark mode support for better accessibility and user preference.

## Acceptance Criteria

- [ ] Toggle switch in user settings
- [ ] Theme persists across browser sessions
- [ ] All components support dark theme
- [ ] Smooth transition between themes
- [ ] System preference detection

## Additional Context

Design mockups available in Figma. Should use CSS custom properties for theming.
```

```markdown
## What feature do you want?

Add real-time notifications for new messages.

## Why is this needed?

Users need immediate feedback when they receive new messages to improve engagement.

## Acceptance Criteria

- [ ] WebSocket connection established on page load
- [ ] Notifications appear in top-right corner
- [ ] Clicking notification opens relevant message
- [ ] Notifications auto-dismiss after 5 seconds
- [ ] Sound notification option available

## Additional Context

Using Socket.io for real-time communication. Should work across all browsers.
```

### 🐛 Bug Report

```markdown
## What's the bug?

Brief description of the issue.

## Steps to Reproduce

1. Go to...
2. Click on...
3. See error...

## Expected vs Actual

**Expected:** Should work like this
**Actual:** Instead it does this

## Environment

- Browser: Chrome 91
- OS: Windows 10
- App version: 1.2.3

## Screenshots/Logs

[Attach relevant files]
```

**Example:**

```markdown
## What's the bug?

Login button doesn't work on mobile devices.

## Steps to Reproduce

1. Open app on mobile browser
2. Enter valid credentials
3. Tap "Login" button
4. Nothing happens

## Expected vs Actual

**Expected:** User should be logged in and redirected to dashboard
**Actual:** Button tap is ignored, no response

## Environment

- Browser: Safari Mobile 14
- OS: iOS 14.5
- App version: 1.2.3
```

**More Examples:**

```markdown
## What's the bug?

Dashboard charts not loading on Firefox.

## Steps to Reproduce

1. Open Firefox browser
2. Navigate to dashboard
3. Charts section shows loading spinner indefinitely

## Expected vs Actual

**Expected:** Charts should display with data
**Actual:** Loading spinner never resolves

## Environment

- Browser: Firefox 91.0
- OS: Windows 10
- App version: 1.2.3
- Console errors: "Chart.js failed to load"
```

```markdown
## What's the bug?

API returns 500 error when creating user with special characters in name.

## Steps to Reproduce

1. Go to user registration form
2. Enter name: "José María"
3. Submit form
4. Server returns 500 error

## Expected vs Actual

**Expected:** User should be created successfully
**Actual:** Server error with special characters

## Environment

- Browser: Chrome 91
- OS: macOS 11.5
- App version: 1.2.3
- Server logs: "UnicodeEncodeError: 'ascii' codec can't encode character"
```

### 🔧 Chore/Task

```markdown
## What needs to be done?

Brief description of the task.

## Tasks

- [ ] Task 1
- [ ] Task 2
- [ ] Task 3

## Definition of Done

- [ ] All tasks completed
- [ ] Tests written
- [ ] Documentation updated
```

**Example:**

```markdown
## What needs to be done?

Update project dependencies to latest versions.

## Tasks

- [ ] Update React to v18
- [ ] Update Node.js to v18
- [ ] Update all npm packages
- [ ] Fix breaking changes
- [ ] Update documentation

## Definition of Done

- [ ] All dependencies updated
- [ ] No breaking changes
- [ ] All tests pass
- [ ] README updated with new requirements
```

**More Examples:**

```markdown
## What needs to be done?

Set up automated security scanning in CI/CD pipeline.

## Tasks

- [ ] Configure Snyk for dependency scanning
- [ ] Set up OWASP ZAP for dynamic scanning
- [ ] Add security scan to GitHub Actions
- [ ] Configure alerting for security issues
- [ ] Document security scan results

## Definition of Done

- [ ] Security scans run on every PR
- [ ] Alerts configured for high-severity issues
- [ ] Documentation updated with security process
- [ ] Team trained on security scan results
```

```markdown
## What needs to be done?

Migrate from MongoDB to PostgreSQL.

## Tasks

- [ ] Design PostgreSQL schema
- [ ] Create data migration scripts
- [ ] Update application code for PostgreSQL
- [ ] Test data migration with production data
- [ ] Deploy and verify migration

## Definition of Done

- [ ] All data migrated successfully
- [ ] Application works with PostgreSQL
- [ ] Performance meets requirements
- [ ] Rollback plan documented
- [ ] Team trained on new database
```

## 🏷️ Labels & Organization

### Essential Labels

- `bug` - Something is broken
- `enhancement` - New feature or improvement
- `chore` - Maintenance task
- `documentation` - Documentation updates
- `good first issue` - Good for newcomers
- `help wanted` - Needs community help

### Priority Labels

- `priority: high` - Critical issues
- `priority: medium` - Important but not urgent
- `priority: low` - Nice to have

### Status Labels

- `status: needs triage` - Needs review
- `status: in progress` - Being worked on
- `status: blocked` - Waiting on something
- `status: ready for review` - Needs review

## 📝 Best Practices

### Writing Issues

- **Be specific** - Clear, actionable descriptions
- **Include context** - Why is this needed?
- **Add examples** - Show what you mean
- **Use checklists** - Break down complex tasks
- **Link related issues** - Connect related work

### Managing Issues

- **Assign owners** - Someone responsible for each issue
- **Set milestones** - Group related issues
- **Close when done** - Don't leave issues hanging
- **Use templates** - Consistent format
- **Regular triage** - Review and organize regularly

## 🔄 Issue Lifecycle

1. **Created** → Needs triage
2. **Triaged** → Assigned and prioritized
3. **In Progress** → Being worked on
4. **Review** → Ready for review/testing
5. **Done** → Completed and verified
6. **Closed** → Issue resolved
