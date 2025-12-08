# 📘 Playwright { page } vs { browser } — How Browser Selection Works

This guide explains:

What { page } means

What { browser } means

How Playwright decides which browser to use

How configuration affects test execution

```configs.js
## ✅ 1. Using { page } (Most Common)
test('@Web UI Controls', async ({ page }) => {
  await page.goto("https://rahulshettyacademy.com/loginpagePractise/");
});
```

✔ How it works

Playwright automatically creates:

a browser (from config)

a browser context

a page

You don’t manage the browser manually.

✔ Default Browser

If you do NOT configure anything, Playwright uses:

Chromium (default)

## 📌 2. Using { browser } (Manual Control)

``` test.js
test('@Web Browser Context-Validating Error login', async ({ browser }) => {
  const context = await browser.newContext();
  const page = await context.newPage();
});
```
✔ How it works

Here you are responsible for:

creating the context

creating the page

applying custom settings

✔ When to use

Multi-user scenarios

Custom viewport, geolocation, permissions

Reusing login state

Recording video per test

Multi-tab testing

## 🆚 3. Difference Between { page } and { browser }
Feature	{ page }	{ browser }
Browser comes from config	✅ Yes	❌ No (you create manually)
Context is auto-created	✅	❌
Best for	Simple UI tests	Advanced/customized tests
Multi-browser testing	Automatic via config	Must handle manually
Custom context options	Limited	Full control
Simpler to write	✔✔✔	✔
🚀 4. Which Browser Does { page } Use?
✔ It uses whatever is defined in your playwright.config.js.

Example default config:
``` configs.js
// playwright.config.js
module.exports = {
  projects: [
    {
      name: 'chromium',
      use: { browserName: 'chromium' }
    }
  ]
};
```
👉 Result

All { page } tests run in Chromium.

📌 5. Running Tests in Multiple Browsers
``` configs.js
projects: [
  { name: 'chromium', use: { browserName: 'chromium' } },
  { name: 'firefox', use: { browserName: 'firefox' } },
  { name: 'webkit', use: { browserName: 'webkit' } }
]
```

Running:

npx playwright test

👉 { page } tests will run in all three browsers automatically.
🔧 6. Browser Selection Summary
✔ { page }

Browser is selected from config

Usually Chromium unless changed

Automatic, beginner-friendly

✔ { browser }

You control context/page creation

Use only when needed

Allows full customization

⭐ Final Summary

{ page } uses the default browser defined in Playwright config.
If no project is configured, it uses Chromium.
{ browser } gives you manual control for custom scenarios.
