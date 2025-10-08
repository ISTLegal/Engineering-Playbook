# Testing Standards

Minimal guidelines for effective software testing practices.

## 🎯 Purpose

Testing ensures:

- **Code Quality** - Catch bugs before production
- **Confidence** - Safe refactoring and changes
- **Documentation** - Tests as living examples
- **Reliability** - Consistent application behavior

## 📋 Testing Pyramid

```
       /\
      /E2E\         Few - Slow - Expensive
     /------\
    /  INT   \      Some - Medium - Moderate
   /----------\
  /    UNIT    \    Many - Fast - Cheap
 /--------------\
```

### Test Distribution

- **70%** Unit Tests - Individual functions/methods
- **20%** Integration Tests - Component interactions
- **10%** E2E Tests - Complete user workflows

## 🧪 Test Types

### Unit Tests

Test individual components in isolation.

**When to write:**
- Pure functions
- Business logic
- Utility functions
- Class methods

**Example (Jest):**

```javascript
// userService.test.js
describe('UserService', () => {
  describe('validateEmail', () => {
    it('should return true for valid email', () => {
      const result = validateEmail('user@example.com');
      expect(result).toBe(true);
    });

    it('should return false for invalid email', () => {
      const result = validateEmail('invalid-email');
      expect(result).toBe(false);
    });

    it('should handle null gracefully', () => {
      const result = validateEmail(null);
      expect(result).toBe(false);
    });
  });
});
```

### Integration Tests

Test how components work together.

**When to write:**
- API endpoints
- Database operations
- Service interactions
- Third-party integrations

**Example (Jest + Supertest):**

```javascript
// userApi.test.js
describe('User API', () => {
  describe('POST /api/users', () => {
    it('should create a new user', async () => {
      const response = await request(app)
        .post('/api/users')
        .send({
          email: 'test@example.com',
          password: 'SecurePass123!'
        });

      expect(response.status).toBe(201);
      expect(response.body).toHaveProperty('id');
      expect(response.body.email).toBe('test@example.com');
    });

    it('should reject duplicate email', async () => {
      // Create first user
      await createUser({ email: 'test@example.com' });

      // Try to create duplicate
      const response = await request(app)
        .post('/api/users')
        .send({ email: 'test@example.com', password: 'Pass123!' });

      expect(response.status).toBe(409);
      expect(response.body.error).toContain('already exists');
    });
  });
});
```

### End-to-End Tests

Test complete user workflows.

**When to write:**
- Critical user journeys
- Authentication flows
- Payment processes
- Key business features

**Example (Cypress):**

```javascript
// login.cy.js
describe('User Login', () => {
  it('should login successfully with valid credentials', () => {
    cy.visit('/login');

    cy.get('[data-testid="email-input"]')
      .type('user@example.com');

    cy.get('[data-testid="password-input"]')
      .type('SecurePass123!');

    cy.get('[data-testid="login-button"]').click();

    cy.url().should('include', '/dashboard');
    cy.get('[data-testid="welcome-message"]')
      .should('contain', 'Welcome back');
  });

  it('should show error for invalid credentials', () => {
    cy.visit('/login');

    cy.get('[data-testid="email-input"]')
      .type('user@example.com');

    cy.get('[data-testid="password-input"]')
      .type('WrongPassword');

    cy.get('[data-testid="login-button"]').click();

    cy.get('[data-testid="error-message"]')
      .should('contain', 'Invalid credentials');
  });
});
```

## 📊 Test Coverage

### Minimum Requirements

- **Overall Coverage**: 80% minimum
- **Critical Paths**: 100% coverage
- **New Features**: 90% coverage minimum

### Coverage Commands

```bash
# JavaScript/Node.js
npm run test:coverage

# Java
./gradlew test jacocoTestReport

# Flutter
flutter test --coverage

# Python
pytest --cov=src tests/
```

### What to Cover

✅ **Must Cover:**
- Business logic
- Authentication/Authorization
- Payment processing
- Data validation
- Error handling

❌ **Skip Coverage:**
- Generated code
- Configuration files
- Simple getters/setters
- Third-party code

## 🎯 Best Practices

### Test Structure (AAA Pattern)

```javascript
it('should calculate total price with tax', () => {
  // Arrange - Setup test data
  const items = [
    { price: 10, quantity: 2 },
    { price: 5, quantity: 1 }
  ];
  const taxRate = 0.1;

  // Act - Execute the functionality
  const total = calculateTotal(items, taxRate);

  // Assert - Verify the result
  expect(total).toBe(27.5); // (10*2 + 5*1) * 1.1
});
```

### Naming Conventions

```javascript
// Good - Descriptive and clear
it('should reject login when password is too short', () => {});
it('should calculate discount for premium members', () => {});
it('should send email notification after successful payment', () => {});

// Bad - Vague and unclear
it('should work', () => {});
it('test1', () => {});
it('checks the function', () => {});
```

### Test Independence

```javascript
// Good - Each test is independent
describe('UserService', () => {
  beforeEach(() => {
    // Fresh setup for each test
    user = createTestUser();
  });

  it('should update user email', () => {
    updateEmail(user, 'new@example.com');
    expect(user.email).toBe('new@example.com');
  });

  it('should update user password', () => {
    updatePassword(user, 'NewPass123!');
    expect(user.password).not.toBe('OldPass123!');
  });
});

// Bad - Tests depend on each other
describe('UserService', () => {
  let user;

  it('should create user', () => {
    user = createUser(); // Other tests depend on this
  });

  it('should update user', () => {
    updateEmail(user, 'new@example.com'); // Depends on previous test
  });
});
```

### Mocking and Stubbing

```javascript
// Good - Mock external dependencies
describe('EmailService', () => {
  it('should send welcome email to new user', async () => {
    // Mock SMTP client
    const mockSmtp = {
      send: jest.fn().mockResolvedValue({ success: true })
    };

    const emailService = new EmailService(mockSmtp);
    const result = await emailService.sendWelcome('user@example.com');

    expect(mockSmtp.send).toHaveBeenCalledWith({
      to: 'user@example.com',
      subject: 'Welcome!',
      template: 'welcome'
    });
    expect(result.success).toBe(true);
  });
});
```

## 🔧 Testing Tools

### JavaScript/TypeScript

- **Jest** - Unit and integration testing
- **Vitest** - Fast unit testing (Vite projects)
- **Cypress** - E2E testing
- **Playwright** - Cross-browser E2E testing
- **Testing Library** - React/Vue component testing

### Java

- **JUnit 5** - Unit testing
- **Mockito** - Mocking framework
- **Spring Test** - Integration testing
- **TestContainers** - Database testing
- **REST Assured** - API testing

### Flutter/Dart

- **flutter_test** - Unit and widget testing
- **mockito** - Mocking
- **integration_test** - Integration testing

### Python

- **pytest** - Testing framework
- **unittest** - Built-in testing
- **mock** - Mocking library
- **selenium** - Browser automation

## 🚀 CI/CD Integration

### GitHub Actions Example

```yaml
name: Test Suite
on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: "18"
          cache: "npm"

      - name: Install dependencies
        run: npm ci

      - name: Run unit tests
        run: npm run test:unit

      - name: Run integration tests
        run: npm run test:integration

      - name: Generate coverage report
        run: npm run test:coverage

      - name: Upload coverage to Codecov
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info
          fail_ci_if_error: true
```

## 📝 Test Documentation

### Test Descriptions

```javascript
// Good - Clear business context
describe('Shopping Cart', () => {
  describe('when adding items', () => {
    it('should increase total price by item cost', () => {});
    it('should update item quantity if already in cart', () => {});
    it('should reject items with zero or negative price', () => {});
  });

  describe('when applying discount codes', () => {
    it('should reduce total by discount percentage', () => {});
    it('should reject expired discount codes', () => {});
    it('should only allow one discount code per cart', () => {});
  });
});
```

### Test Data Factories

```javascript
// testHelpers.js
export const createTestUser = (overrides = {}) => ({
  id: '123',
  email: 'test@example.com',
  name: 'Test User',
  role: 'user',
  createdAt: new Date(),
  ...overrides
});

export const createTestProduct = (overrides = {}) => ({
  id: '456',
  name: 'Test Product',
  price: 29.99,
  stock: 100,
  ...overrides
});

// Usage in tests
it('should calculate discount for premium users', () => {
  const premiumUser = createTestUser({ role: 'premium' });
  const product = createTestProduct({ price: 100 });

  const discount = calculateDiscount(premiumUser, product);
  expect(discount).toBe(20); // 20% for premium
});
```

## ⚠️ Common Pitfalls

### Don't Test Implementation Details

```javascript
// Bad - Tests implementation
it('should call calculateTax method', () => {
  const spy = jest.spyOn(service, 'calculateTax');
  service.processOrder(order);
  expect(spy).toHaveBeenCalled();
});

// Good - Tests behavior
it('should include tax in order total', () => {
  const order = { subtotal: 100, taxRate: 0.1 };
  const result = service.processOrder(order);
  expect(result.total).toBe(110);
});
```

### Avoid Brittle Tests

```javascript
// Bad - Breaks with minor UI changes
cy.get('div > form > div:nth-child(2) > input').type('email');

// Good - Uses semantic selectors
cy.get('[data-testid="email-input"]').type('email');
cy.get('[aria-label="Email address"]').type('email');
```

### Don't Ignore Flaky Tests

```javascript
// Bad - Hiding the problem
it.skip('sometimes fails - will fix later', () => {});

// Good - Make tests deterministic
it('should handle async operations correctly', async () => {
  await waitFor(() => {
    expect(screen.getByText('Loaded')).toBeInTheDocument();
  });
});
```

## 📋 Test Checklist

**Before committing:**

- [ ] All tests pass locally
- [ ] New code has corresponding tests
- [ ] Test names are descriptive
- [ ] Tests are independent
- [ ] No skipped tests without tracking issue
- [ ] Coverage meets minimum requirements
- [ ] No hardcoded test data (use factories)
- [ ] External dependencies are mocked

**For code review:**

- [ ] Tests verify behavior, not implementation
- [ ] Edge cases are covered
- [ ] Error scenarios are tested
- [ ] Tests are maintainable and readable
- [ ] No unnecessary assertions
- [ ] Test data is meaningful

## 📚 Resources

### General Testing

- [Testing Best Practices](https://testingjavascript.com/)
- [Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)
- [TDD Guide](https://www.testdriven.io/)

### JavaScript/TypeScript

- [Jest Documentation](https://jestjs.io/)
- [Cypress Documentation](https://docs.cypress.io/)
- [Testing Library](https://testing-library.com/)

### Java

- [JUnit 5 Documentation](https://junit.org/junit5/)
- [Mockito](https://site.mockito.org/)
- [Spring Testing](https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html)

### Flutter

- [Flutter Testing Guide](https://flutter.dev/docs/testing)
- [Effective Dart: Testing](https://dart.dev/guides/language/effective-dart/testing)

---

**Note**: These are minimal standards. Adjust based on project needs and team capacity. The goal is sustainable testing, not perfect coverage.
