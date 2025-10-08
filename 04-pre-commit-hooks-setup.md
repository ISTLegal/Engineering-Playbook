# Pre-commit Hooks Setup Guide

This guide shows how to set up pre-commit hooks for code quality and consistency across different project types using [pre-commit](https://pre-commit.com/), a framework for managing and maintaining multi-language pre-commit hooks.

## ⚠️ Prerequisites

### Python Required for All Project Types

**Important**: Even for Node.js, Java, and Flutter projects, you need **Python** installed on developer machines to use pre-commit.

```bash
# Check if Python is installed
python --version  # Should be >= 3.9.0
pip --version     # Should be >= 21.0.0

# Install Python if needed:
# - Download from https://python.org/
# - Use package managers: brew install python, apt install python3, etc.
# - Use version managers: pyenv, conda, virtualenv
```

### Why Python is Required

- **pre-commit**: Multi-language hooks framework (Python tool)
- **Universal tooling**: Works consistently across all project types
- **Rich ecosystem**: Extensive library of pre-built hooks
- **CI/CD integration**: Easy to integrate with build pipelines

### Alternative Approaches (Without Python)

If Python installation is not feasible, consider:

- **Husky**: Node.js-based hooks (requires Node.js)
- **Lefthook**: Rust-based alternative (no Python required)
- **Manual git hooks**: Shell scripts (platform-specific)
- **IDE plugins**: Built-in formatting and validation

## 📋 Pre-commit Overview

### Core Philosophy

1. **Prevent bad code** from entering the repository
2. **Enforce consistent** code formatting and style
3. **Automate quality checks** before commits
4. **Support multiple project types** with appropriate tooling
5. **Fast feedback loop** for developers

### How It Works

- **Pre-commit hooks** run automatically before each commit
- **Staged files only** are processed (fast execution)
- **Automatic fixes** when possible (formatting, imports)
- **Commit blocked** if issues cannot be auto-fixed
- **Consistent experience** across all developer machines

## 🚀 Quick Setup by Project Type

### Node.js/Vue.js Projects

#### 1. Install pre-commit

```bash
pip install pre-commit
```

#### 2. Create Configuration

Create `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
      - id: check-merge-conflict

  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
        language_version: python3

  - repo: https://github.com/pre-commit/mirrors-eslint
    rev: v8.44.0
    hooks:
      - id: eslint
        files: \.(js|ts|vue)$
        additional_dependencies:
          - eslint@8.44.0
          - @typescript-eslint/eslint-plugin@5.59.0
          - @typescript-eslint/parser@5.59.0

  - repo: https://github.com/pre-commit/mirrors-prettier
    rev: v3.0.0
    hooks:
      - id: prettier
        files: \.(js|ts|vue|json|md|yml|yaml)$
```

#### 3. Install Hooks

```bash
pre-commit install
```

### Java Projects

#### 1. Install pre-commit

```bash
pip install pre-commit
```

#### 2. Create Configuration

Create `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
      - id: check-merge-conflict

  - repo: https://github.com/diffplug/spotless
    rev: 6.22.0
    hooks:
      - id: spotless
        name: Spotless
        entry: ./gradlew spotlessApply
        language: system
        files: \.java$
        pass_filenames: false
        always_run: true

  - repo: local
    hooks:
      - id: checkstyle
        name: Checkstyle
        entry: ./gradlew checkstyleMain
        language: system
        files: \.java$
        pass_filenames: false
        always_run: true
```

#### 3. Install Hooks

```bash
pre-commit install
```

### Flutter Projects

#### 1. Install pre-commit

```bash
pip install pre-commit
```

#### 2. Create Configuration

Create `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
      - id: check-merge-conflict

  - repo: local
    hooks:
      - id: dart-format
        name: Dart Format
        entry: dart format
        language: system
        files: \.dart$
        args: [--set-exit-if-changed]

      - id: flutter-analyze
        name: Flutter Analyze
        entry: flutter analyze
        language: system
        files: \.dart$
        pass_filenames: false
        always_run: true
```

#### 3. Install Hooks

```bash
pre-commit install
```

## 📁 Configuration Examples

### Universal Configuration

```yaml
# .pre-commit-config.yaml
repos:
  # Universal hooks for all projects
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-json
      - id: check-added-large-files
      - id: check-merge-conflict
      - id: check-case-conflict
      - id: check-ast
      - id: debug-statements
      - id: detect-private-key
```

### Node.js/Vue.js Specific

```yaml
repos:
  # ESLint for JavaScript/TypeScript
  - repo: https://github.com/pre-commit/mirrors-eslint
    rev: v8.44.0
    hooks:
      - id: eslint
        files: \.(js|ts|vue)$
        additional_dependencies:
          - eslint@8.44.0
          - @typescript-eslint/eslint-plugin@5.59.0
          - @typescript-eslint/parser@5.59.0
          - eslint-plugin-vue@9.12.0

  # Prettier for formatting
  - repo: https://github.com/pre-commit/mirrors-prettier
    rev: v3.0.0
    hooks:
      - id: prettier
        files: \.(js|ts|vue|json|md|yml|yaml)$

  # Black for Python (if using Python scripts)
  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
        files: \.py$
```

### Java Specific

```yaml
repos:
  # Spotless for code formatting
  - repo: https://github.com/diffplug/spotless
    rev: 6.22.0
    hooks:
      - id: spotless
        name: Spotless
        entry: ./gradlew spotlessApply
        language: system
        files: \.java$
        pass_filenames: false
        always_run: true

  # Local Gradle tasks
  - repo: local
    hooks:
      - id: checkstyle
        name: Checkstyle
        entry: ./gradlew checkstyleMain
        language: system
        files: \.java$
        pass_filenames: false
        always_run: true

      - id: test
        name: Run Tests
        entry: ./gradlew test
        language: system
        files: \.java$
        pass_filenames: false
        always_run: true
```

### Flutter Specific

```yaml
repos:
  # Dart formatting
  - repo: local
    hooks:
      - id: dart-format
        name: Dart Format
        entry: dart format
        language: system
        files: \.dart$
        args: [--set-exit-if-changed]

      - id: flutter-analyze
        name: Flutter Analyze
        entry: flutter analyze
        language: system
        files: \.dart$
        pass_filenames: false
        always_run: true

      - id: flutter-test
        name: Flutter Test
        entry: flutter test
        language: system
        files: \.dart$
        pass_filenames: false
        always_run: true
```

## 🔧 Advanced Configuration

### Custom Hooks

```yaml
repos:
  - repo: local
    hooks:
      - id: custom-security-check
        name: Security Check
        entry: ./scripts/security-check.sh
        language: script
        files: \.(js|ts|java|dart)$

      - id: custom-lint
        name: Custom Lint
        entry: ./scripts/custom-lint.sh
        language: script
        files: \.(js|ts|vue)$
        args: [--fix]
```

### Conditional Hooks

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
        exclude: ^(.*\.md)$ # Skip markdown files

      - id: check-yaml
        exclude: ^(.*\.yml)$ # Skip .yml files

  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
        files: \.py$
        exclude: ^(migrations/.*)$ # Skip migration files
```

### Performance Optimization

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
        # Only run on changed files
        files: \.(js|ts|vue|java|dart|py)$
        # Skip binary files
        exclude: \.(png|jpg|jpeg|gif|ico|svg)$
```

## 🔍 Quick Commands

### Manual Testing

```bash
# Test all hooks on all files
pre-commit run --all-files

# Test specific hook
pre-commit run eslint

# Test hooks on staged files only
pre-commit run

# Update hook versions
pre-commit autoupdate
```

### Bypass Hooks (Emergency Only)

```bash
# Skip pre-commit hooks
git commit --no-verify -m "emergency fix"
```

**⚠️ Warning**: Only use `--no-verify` in emergencies. Always fix issues properly.

## ⚠️ Troubleshooting

### Hook Not Running

```bash
# Reinstall hooks
pre-commit uninstall
pre-commit install

# Check hook permissions
ls -la .git/hooks/pre-commit

# Verify pre-commit is installed
pre-commit --version
```

### Hook Fails

```bash
# Error example
pre-commit....................................................................Failed
- hook id: eslint
- exit code: 1
- files were modified by this hook
```

**Solutions**:

1. Fix linting errors manually: `npm run lint`
2. Fix formatting: `npm run format`
3. Stage fixed files: `git add .`
4. Retry commit

### Python Command Not Found

```bash
# Install Python via package manager
# macOS
brew install python

# Ubuntu/Debian
sudo apt update && sudo apt install python3 python3-pip

# Windows
# Download from https://python.org/ or use chocolatey
choco install python
```

### Permission Errors

```bash
# Fix pip permissions (Linux/macOS)
mkdir ~/.pip-global
pip config set global.prefix '~/.pip-global'
echo 'export PATH=~/.pip-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

## 🔄 Customization

### Adding Custom Hooks

```yaml
repos:
  - repo: local
    hooks:
      - id: my-custom-hook
        name: My Custom Hook
        entry: ./scripts/my-hook.sh
        language: script
        files: \.(js|ts|vue|java|dart)$
        args: [--verbose]
```

### Environment Variables

```yaml
repos:
  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
        env:
          - BLACK_LINE_LENGTH: 88
          - BLACK_SKIP_STRING_NORMALIZATION: true
```

### Multiple Language Support

```yaml
repos:
  # JavaScript/TypeScript
  - repo: https://github.com/pre-commit/mirrors-eslint
    rev: v8.44.0
    hooks:
      - id: eslint
        files: \.(js|ts|vue)$

  # Python
  - repo: https://github.com/psf/black
    rev: 23.3.0
    hooks:
      - id: black
        files: \.py$

  # Java
  - repo: local
    hooks:
      - id: spotless
        entry: ./gradlew spotlessApply
        language: system
        files: \.java$

  # Dart/Flutter
  - repo: local
    hooks:
      - id: dart-format
        entry: dart format
        language: system
        files: \.dart$
```

## 📚 Resources by Technology

### Universal

- [Pre-commit Documentation](https://pre-commit.com/)
- [Pre-commit Hooks](https://github.com/pre-commit/pre-commit-hooks)
- [Hook Examples](https://github.com/pre-commit/pre-commit.com)

### Node.js/Vue.js

- [ESLint Pre-commit](https://github.com/pre-commit/mirrors-eslint)
- [Prettier Pre-commit](https://github.com/pre-commit/mirrors-prettier)
- [Vue.js Style Guide](https://vuejs.org/style-guide/)

### Java

- [Spotless Pre-commit](https://github.com/diffplug/spotless)
- [Google Java Format](https://github.com/google/google-java-format)
- [Gradle Documentation](https://docs.gradle.org/)

### Flutter

- [Dart Style Guide](https://dart.dev/guides/language/effective-dart/style)
- [Flutter Lints](https://pub.dev/packages/flutter_lints)
- [Analysis Options](https://dart.dev/guides/language/analysis-options)

## 🎯 Best Practices

### Commit Guidelines

1. **Fix Issues Before Committing**: Don't bypass hooks unnecessarily
2. **Stage Only What You Want**: Use `git add` selectively
3. **Test Locally**: Run hooks manually before committing
4. **Review Changes**: Use `git diff` before committing

### Code Quality

1. **Consistent Formatting**: Let hooks handle formatting automatically
2. **Early Detection**: Catch issues before they reach the repository
3. **Team Consistency**: All developers use the same quality checks
4. **Fast Feedback**: Quick iteration on code quality

### Project-Specific Practices

#### Node.js/Vue.js

- Run `npm run lint` and `npm run format` locally
- Use TypeScript strict mode when possible
- Follow Vue.js component naming conventions

#### Java

- Run `./gradlew spotlessApply` before committing
- Follow Google Java Style Guide
- Use meaningful variable and method names

#### Flutter

- Run `dart format` and `flutter analyze` regularly
- Follow Dart naming conventions
- Use const constructors where possible

### Troubleshooting Tips

1. **Permission Issues**: Ensure Python and pip are properly installed
2. **Version Conflicts**: Use virtual environments for Python dependencies
3. **Path Issues**: Ensure tools are in PATH or use full paths in hooks
4. **Emergency Bypasses**: Only use `--no-verify` in genuine emergencies
5. **Cross-platform**: Use forward slashes in hook scripts for Windows compatibility

---

_This pre-commit setup ensures code quality and consistency across different IST-AiDev project types while maintaining technology-specific best practices. Note that this is a living document, anyone can raise a PR for any necessary changes to it._
