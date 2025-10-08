# Branch Naming Convention

Simple rules for consistent branch names.

## 📋 Format

```
{type}-{description}-{issue-id}
```

**Examples:**

- `feat-user-authentication-123`
- `fix-login-error-456`
- `chore-update-dependencies-789`

## 🏷️ Branch Types

| Type       | Use Case                 | Example                   |
| ---------- | ------------------------ | ------------------------- |
| `feat`     | New features             | `feat-user-dashboard-123` |
| `fix`      | Bug fixes                | `fix-login-error-456`     |
| `chore`    | Maintenance tasks        | `chore-update-deps-789`   |
| `docs`     | Documentation            | `docs-api-guide-101`      |
| `refactor` | Code improvements        | `refactor-db-queries-202` |
| `test`     | Testing related          | `test-user-service-303`   |
| `perf`     | Performance improvements | `perf-db-indexing-404`    |

## 📝 Naming Rules

### ✅ Do's

- **Use kebab-case**: `feat-user-authentication`
- **Be descriptive**: `feat-user-dashboard` not `feat-dashboard`
- **Keep it short**: 2-4 words maximum
- **Include issue ID**: Link to project management
- **Use present tense**: `feat-add-auth` not `feat-added-auth`

### ❌ Don'ts

- **No spaces**: Use hyphens instead
- **No underscores**: Use hyphens for consistency
- **No special characters**: Only letters, numbers, and hyphens
- **Don't be vague**: `feat-stuff` is not helpful
- **Don't skip type**: Always include the branch type

## 🎯 Examples

### Feature Branches

```bash
feat-user-registration-123
feat-payment-processing-124
feat-admin-dashboard-125
```

### Bug Fix Branches

```bash
fix-login-validation-201
fix-mobile-layout-202
fix-database-query-203
```

### Maintenance Branches

```bash
chore-update-react-301
chore-eslint-config-302
docs-api-documentation-401
```

## 🔄 Branch Lifecycle

### Create Branch

```bash
git checkout -b feat-user-auth-123
```

### Rename Branch (if needed)

```bash
git branch -m old-name feat-new-name-123
git push origin -u feat-new-name-123
git push origin --delete old-name
```

### Cleanup

```bash
# Delete local branch after merge
git branch -d feat-user-auth-123

# Delete remote branch
git push origin --delete feat-user-auth-123
```

## 🛠️ Automation

### Pre-commit Hook

```bash
#!/bin/bash
branch_name=$(git rev-parse --abbrev-ref HEAD)

if [[ ! $branch_name =~ ^(feat|fix|chore|docs|refactor|test|perf)-[a-z0-9-]+-[0-9]+$ ]]; then
    echo "❌ Invalid branch name: $branch_name"
    echo "✅ Use format: {type}-{description}-{issue-id}"
    echo "✅ Examples: feat-user-auth-123, fix-login-bug-456"
    exit 1
fi
```

### CI/CD Integration

```yaml
# GitHub Actions
name: CI/CD Pipeline
on:
  push:
    branches: ["feat-*", "fix-*", "chore-*"]
  pull_request:
    branches: ["feat-*", "fix-*", "chore-*"]
```

## 📊 Benefits

- **Clear Context**: Immediately understand branch purpose
- **Easy Navigation**: Quick identification of related work
- **Issue Tracking**: Direct connection to project management
- **Automation**: Enables automated workflows
- **Team Consistency**: Uniform approach across developers
