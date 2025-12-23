# Handling Auto-Suggestion Dropdown in Playwright (JavaScript)

Auto-suggestion dropdowns are widely used in modern web applications such as
search boxes, country selectors, city inputs, and address fields.

This document explains **how to handle auto-suggestion dropdowns in Playwright using JavaScript**
with a focus on the **`pressSequentially()`** method for realistic typing.

---

## Why `pressSequentially()`?

`pressSequentially()` types characters one by one, just like a real user.

### Advantages
- Triggers all keyboard events (`keydown`, `keyup`, `input`)
- Works reliably with JavaScript-based auto-suggestions
- More stable than `fill()` for dynamic dropdowns
- Mimics real user behavior

### Example
```js
await locator.pressSequentially('Ind');
```

---

## Scenario

### Requirement
- User types **"Ind"**
- Auto-suggestion list appears
- Select **"India"** from the dropdown

### Example Suggestions
- India
- Indonesia
- Indore

---

## Sample HTML Structure (Assumed)

```html
<input id="country" />
<ul class="suggestions">
  <li>India</li>
  <li>Indonesia</li>
  <li>Indore</li>
</ul>
```

---

## Step-by-Step Automation Approach

1. Navigate to the page
2. Locate the input field
3. Click the input
4. Type text using `pressSequentially()`
5. Wait for suggestions to appear
6. Read all suggestions
7. Select the required option

---

## Playwright JavaScript Example

```js
import { test, expect } from '@playwright/test';

test('Handle auto-suggestion dropdown using pressSequentially', async ({ page }) => {

  await page.goto('https://example.com');

  const countryInput = page.locator('#country');
  await countryInput.click();
  await countryInput.pressSequentially('Ind');

  const suggestions = page.locator('.suggestions li');
  await expect(suggestions).toHaveCountGreaterThan(0);

  const totalSuggestions = await suggestions.count();

  for (let i = 0; i < totalSuggestions; i++) {
    const suggestionText = await suggestions.nth(i).innerText();
    if (suggestionText.trim() === 'India') {
      await suggestions.nth(i).click();
      break;
    }
  }
});
```

---

## Keyboard-Based Selection

```js
await countryInput.pressSequentially('Ind');
await page.waitForTimeout(500);
await countryInput.press('ArrowDown');
await countryInput.press('Enter');
```

---

## Best Practices

- Use stable locators (`data-testid` if available)
- Avoid hard waits; use `expect()`
- Prefer `pressSequentially()` for dynamic suggestions

---

## Conclusion

Using `pressSequentially()` is the most reliable way to handle auto-suggestion
dropdowns in Playwright with JavaScript.
