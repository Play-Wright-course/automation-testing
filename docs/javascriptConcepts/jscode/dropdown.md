
# 📘 Handling Dropdowns in Playwright (JavaScript) — Complete Guide

Dropdowns are very common UI elements in web applications.
Playwright provides **multiple ways** to handle different types of dropdowns depending on how they are implemented in HTML.

This guide covers **ALL real-world dropdown scenarios** with examples.

---

## 🧠 Types of Dropdowns in Web Applications

1. HTML `<select>` dropdown  
2. Custom dropdown (div / ul / li based)  
3. Autocomplete dropdown  
4. Multi-select dropdown  
5. Dynamic / async dropdown  
6. Shadow DOM dropdown  
7. Iframe dropdown  

---

## 1️⃣ HTML `<select>` Dropdown (Native Dropdown)

### Example HTML
```html
<select id="country">
  <option value="IN">India</option>
  <option value="US">USA</option>
  <option value="UK">UK</option>
</select>
```

### Select by value

```js
const dropdown=page.locator('#country');
dropdown.selectOption("IN");
```

```js
await page.selectOption('#country', 'IN');
```

### Select by label
```js
await page.selectOption('#country', { label: 'India' });
```

### Select by index
```js
await page.selectOption('#country', { index: 1 });
```

### Select multiple values
```js
await page.selectOption('#country', ['IN', 'US']);
```

### Validate selected value
```js
const value = await page.locator('#country').inputValue();
expect(value).toBe('IN');
```

---

## 2️⃣ Custom Dropdown (Div / UL / LI Based)

`selectOption()` does NOT work here.

### Example HTML
```html
<div class="dropdown">
  <div class="selected">Select City</div>
  <ul class="options">
    <li>Delhi</li>
    <li>Mumbai</li>
    <li>Pune</li>
  </ul>
</div>
```

### Handling custom dropdown
```js
await page.click('.selected');
await page.click('li:has-text("Pune")');
```

### Stable locator approach
```js
await page.locator('.dropdown').click();
await page.locator('.options li').filter({ hasText: 'Mumbai' }).click();
```

---

## 3️⃣ Autocomplete Dropdown

```html
<input id="search" />
<ul class="suggestions">
  <li>Apple</li>
  <li>Apricot</li>
</ul>
```

### Handling autocomplete
```js
await page.fill('#search', 'Ap');
await page.waitForSelector('.suggestions li');
await page.click('.suggestions li:has-text("Apple")');
```

### Keyboard selection
```js
await page.fill('#search', 'Ap');
await page.keyboard.press('ArrowDown');
await page.keyboard.press('Enter');
```

---

## 4️⃣ Multi-Select Dropdown

```html
<select id="skills" multiple>
  <option value="java">Java</option>
  <option value="js">JavaScript</option>
  <option value="py">Python</option>
</select>
```

```js
await page.selectOption('#skills', ['java', 'js']);
```

```js
const values = await page.locator('#skills').evaluate(
  el => Array.from(el.selectedOptions).map(o => o.value)
);
expect(values).toContain('java');
```

---

## 5️⃣ Dynamic / Async Dropdown

```js
await page.click('#country');
await page.waitForSelector('li:has-text("India")');
await page.click('li:has-text("India")');
```

---

## 6️⃣ Dropdown Inside Shadow DOM

```js
await page.locator('my-dropdown')
  .locator('li:has-text("Option 1")')
  .click();
```

---

## 7️⃣ Dropdown Inside Iframe

```js
const frame = page.frameLocator('#payment-frame');
await frame.locator('#month').selectOption('March');
```

---

## 8️⃣ Keyboard Actions

```js
await page.click('#country');
await page.keyboard.press('ArrowDown');
await page.keyboard.press('Enter');
```

---

## 9️⃣ Read All Options

```js
const options = await page.locator('#country option').allTextContents();
console.log(options);
```

---

## 🔥 Common Mistakes

- Using `selectOption()` on custom dropdowns
- Not waiting for dynamic options
- Clicking hidden elements

---

## 🏆 Best Practices

- Prefer label over value
- Use Playwright locators
- Use frameLocator for iframes
- Rely on auto-waiting

---

## 📌 Summary Table

| Dropdown Type | Recommended Method |
|--------------|-------------------|
| HTML select | selectOption |
| Custom dropdown | Click + text |
| Autocomplete | Type + click |
| Multi-select | Array values |
| Async | Wait + click |
| Shadow DOM | Locator chaining |
| Iframe | frameLocator |

---

Happy Testing 🚀
