

# What @playwright/test Provides

- Test runner — run tests with npx playwright test

- Assertions — built-in assertion library like expect

- Test hooks — beforeAll, beforeEach, afterEach, afterAll

- Parallel test execution

- Retries & timeouts per test

- Reporter support — HTML, JSON, list, etc.

- Browser projects — run tests in Chromium, Firefox, WebKit

# How It Looks in Code
```js
// Import test runner and assertion library
const { test, expect } = require('@playwright/test');

// Define a test
test('Google search', async ({ page }) => {
  await page.goto('https://www.google.com');
  await page.fill('input[name="q"]', 'Playwright');
  await page.press('input[name="q"]', 'Enter');

  // Assert that results appear
  await expect(page.locator('#search')).toContainText('Playwright');
});
```

### Explanation:

- test → defines a test case

- expect → assertions to validate conditions

- { page } → test fixture provided by Playwright to interact with a browser page

# Why Use @playwright/test Instead of Plain Playwright
| Feature | @playwright/test | Plain Playwright |
|--------|------------------|------------------|
| **Test runner** | ✅ Built-in | ❌ No |
| **Assertions** | ✅ Built-in | ❌ Requires third-party (Jest, Chai) |
| **Hooks** | ✅ Yes (`beforeAll`, `afterEach`) | ❌ Manual setup |
| **Parallel execution** | ✅ Yes | ❌ Extra configuration needed |
| **Reporting** | ✅ Built-in | ❌ Requires external libraries |
