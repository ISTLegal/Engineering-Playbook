# Pull Request Standards

Minimal guidelines for effective pull requests.

## 📋 PR Structure

### Title Format

```text
#[ISSUE_ID] [Brief Description]
```

**Examples:**

- `#123 Add user authentication`
- `#456 Fix login validation error`
- `#789 Update API docs`

### Description Template

```markdown
## What does this PR do?

Brief description of changes and purpose.

## How to test?

1. Checkout branch: `git checkout feat/user-auth-123`
2. Install deps: `npm install`
3. Run app: `npm run dev`
4. Test scenarios:
   - [ ] User registration works
   - [ ] Login with valid credentials
   - [ ] Login fails with invalid credentials

## Any background context?

- Implements auth system from tech spec
- Database migrations included
- Environment variables need updating

## Related issues?

- Closes #123
- Related to #120
```

## 🎯 Best Practices

### For Authors

- **Self-review** your code first
- **Keep PRs small** and focused
- **Write clear descriptions** with context
- **Test thoroughly** before submitting
- **Respond promptly** to feedback

### For Reviewers

- **Review within 24 hours**
- **Provide specific, helpful feedback**
- **Test the changes** when possible
- **Approve when ready** - don't block unnecessarily

### Review Process

- **8-hour SLA** for initial review
- **All tests must pass** before merge
- **Minimum 1 approval** required
- **Emergency override** available for critical fixes

## 🔧 Quick Checklist

**Before submitting:**

- [ ] All tests pass
- [ ] Code follows style guide
- [ ] Documentation updated
- [ ] No console.logs in production code

**For reviewers:**

- [ ] Code quality looks good
- [ ] Functionality works as expected
- [ ] Security implications considered
- [ ] Performance impact acceptable
