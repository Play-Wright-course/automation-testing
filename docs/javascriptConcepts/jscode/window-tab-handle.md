# Handling Multiple Tabs and Windows in Playwright (JavaScript)

This document explains **7 real-world scenarios** for handling multiple tabs and windows in **Playwright with JavaScript**.
Each scenario includes:
- Practical use case
- Complete code snippet
- Line-by-line explanation

---

## Prerequisites

Install Playwright:

```bash
npm init -y
npm install playwright
```

Import Playwright:

```js
javascript
Copy code
const { chromium } = require('@playwright/test');
```

## Scenario 1: Handle New Tab Opened by Clicking a Link
### Use Case
#### User clicks a link (target="_blank") and a new tab opens.
```js
Code
javascript
Copy code
// Launch browser
const browser = await chromium.launch();

// Create isolated browser context
const context = await browser.newContext();

// Open a new tab
const page = await context.newPage();

// Navigate to application
await page.goto('https://example.com');

// Capture the new tab opened on click
const [newPage] = await Promise.all([
  context.waitForEvent('page'),  // Waits for new tab
  page.click('a[target="_blank"]') // Action that opens new tab
]);

// Wait until new tab loads completely
await newPage.waitForLoadState();

// Print title of new tab
console.log(await newPage.title());

// Close browser
await browser.close();
```

####  Explanation
- `chromium.launch()` → Starts browser

- `browser.newContext()` → Creates fresh session

- `context.waitForEvent('page')` → Detects new tab

- `Promise.all()` → Avoids race condition

- `newPage` → Reference to new tab


## Scenario 2: Switch Between Multiple Open Tabs
### Use Case
#### Application opens multiple tabs and user needs to switch between them.

``` js
Code
javascript
Copy code
// Get all open tabs
const pages = context.pages();

// Switch to second tab
await pages[1].bringToFront();
console.log(await pages[1].url());

// Switch back to first tab
await pages[0].bringToFront();
```

#### Explanation
- `context.pages()` → Returns array of all tabs

- `bringToFront()` → Brings tab into focus

- `Index` represents tab order

## Scenario 3: Handle Popup Window (window.open)
### Use Case
#### Clicking a button opens a popup window.

```js
Code
javascript
Copy code
const [popup] = await Promise.all([
  page.waitForEvent('popup'), // Waits for popup window
  page.click('#printInvoice') // Action triggering popup
]);

// Wait for popup to load
await popup.waitForLoadState();

// Print popup title
console.log(await popup.title());
```
### Explanation
- `page.waitForEvent('popup')` → Captures popup window

- Popup is linked to parent page automatically

- Treated same as a normal page

## Scenario 4: Close Child Tab and Return to Parent Tab
### Use Case
#### Child tab opens → perform action → close it → return to parent.

```js
Code
javascript
Copy code
// Store parent tab reference
const parentPage = page;

// Open child tab
const [childPage] = await Promise.all([
  context.waitForEvent('page'),
  page.click('#openChildTab')
]);

// Wait for child tab to load
await childPage.waitForLoadState();

// Close child tab
await childPage.close();

// Bring parent tab back to focus
await parentPage.bringToFront();
```

### Explanation
- `Parent page` reference is stored

- `Child page` is captured and closed

- Control is returned to parent tab

## Scenario 5: Switch to a Tab Based on Title
### Use Case
#### Multiple tabs are open → switch to required one using title.
``` js
Code
javascript
Copy code
for (const p of context.pages()) {
  const title = await p.title();

  if (title.includes('Dashboard')) {
    await p.bringToFront();
    break;
  }
}
```
### Explanation
- Iterates through all open tabs

- Matches tab using title

- Switches to correct tab

## Scenario 6: Handle OAuth / Google Login Window
### Use Case
#### Clicking "Login with Google" opens authentication window.
```js
Code
javascript
Copy code
const [loginPage] = await Promise.all([
  context.waitForEvent('page'), // New OAuth window
  page.click('#googleLogin')    // Trigger login
]);

// Interact with login window
await loginPage.fill('#identifierId', 'test@gmail.com');
await loginPage.click('#identifierNext');
```
### Explanation
- OAuth login opens in new tab/window

- New window is treated as normal page

- Can interact using Playwright actions

## Scenario 7: Open New Tab Manually
### Use Case
#### Open Admin / Reports page manually within same session.
```js
Code
javascript
Copy code
// Create new tab manually
const adminPage = await context.newPage();

// Navigate to admin page
await adminPage.goto('https://admin.example.com');
```

### Explanation
- context.newPage() → Opens new tab

- Shares cookies and session with existing tabs

#### Best Practices
- Always use Promise.all() when handling new tabs

- Prefer waitForEvent() over static waits

- Close unused tabs to save memory

- Validate title or URL before switching tabs

