
# 📘 Handling Radio Buttons in Playwright (JavaScript) — Complete Guide

Radio buttons allow users to select **ONLY ONE option** from a group.
Playwright provides clean and reliable APIs to handle radio buttons in both simple and complex real-world scenarios.

This guide covers **basic to advanced radio button handling**, including validations and edge cases.

---

## 🧠 What is a Radio Button?

- Represented by `<input type="radio">`
- Grouped using the same `name` attribute
- Only one option can be selected at a time

---

## 1️⃣ Basic HTML Radio Button

### Example HTML
```html
<input type="radio" name="gender" value="male" id="male">
<label for="male">Male</label>

<input type="radio" name="gender" value="female" id="female">
<label for="female">Female</label>
```

---

### ✔ Select radio button by ID
```js
await page.check('#male');
```

---

### ✔ Select by value
```js
await page.locator('input[name="gender"][value="female"]').check();
```

---

### ✔ Validate selected radio button
```js
await expect(page.locator('#male')).toBeChecked();
await expect(page.locator('#female')).not.toBeChecked();
```

---

## 2️⃣ Selecting Radio Button Using Label Text

```js
await page.getByLabel('Male').check();
```

---

## 3️⃣ Radio Button Group Handling

```js
const gender = 'female';

await page
  .locator('input[name="gender"]')
  .filter({ has: page.locator(`[value="${gender}"]`) })
  .check();
```

---

## 4️⃣ Disabled Radio Button

```html
<input type="radio" name="status" value="active" disabled>
```

```js
await expect(page.locator('input[value="active"]')).toBeDisabled();
```

---

## 5️⃣ Default Selected Radio Button

```html
<input type="radio" name="payment" value="upi" checked>
```

```js
await expect(page.locator('input[value="upi"]')).toBeChecked();
```

---

## 6️⃣ Custom Styled Radio Buttons

```js
await page.locator('.radio').filter({ hasText: 'Gold' }).click();
```

---

## 7️⃣ Dynamically Loaded Radio Buttons

```js
await page.waitForSelector('input[name="plan"]');
await page.locator('input[value="premium"]').check();
```

---

## 8️⃣ Radio Button Inside Iframe

```js
const frame = page.frameLocator('#settings-frame');
await frame.getByLabel('Dark Mode').check();
```

---

## 9️⃣ Keyboard Interaction

```js
await page.focus('#male');
await page.keyboard.press('ArrowRight');
```

---

# 🚀 Complex Real-World Scenario

```js
test('Complex radio button flow', async ({ page }) => {
  await page.goto('https://example.com/register');

  await page.waitForSelector('input[name="role"]');
  await expect(page.locator('input[value="admin"]')).toBeDisabled();

  await page.locator('input[value="user"]').check();
  await expect(page.locator('#subscription')).toBeVisible();

  await page.locator('input[value="pro"]').check();
  await expect(page.locator('input[value="pro"]')).toBeChecked();
  await expect(page.locator('input[value="pro"]').isChecked).toBeTruthy();
});
```

---

Happy Testing 🚀
