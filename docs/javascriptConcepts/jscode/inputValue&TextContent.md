# Playwright `inputValue()` & `textContent()` — What They REALLY Return

## ✅ Short Answer

- **`inputValue()`** → returns the current **`value` property** of form elements  
- **`textContent()`** → returns the **text inside an element**

They are **not interchangeable** and are used for **different types of elements**.

---

## 🧠 Correct Mental Model

### ❌ Incorrect understanding
> `inputValue()` returns what the user typed  
> `textContent()` works for everything

### ✅ Correct understanding
> **`inputValue()` → reads `element.value` (inputs, textareas, selects)**  
> **`textContent()` → reads inner text of normal elements**

---

## 🔹 `inputValue()` — Explained

### ✅ What it returns
`inputValue()` returns the **current value** of the input field —  
not *how* or *who* entered it.

That value can come from:
- User typing
- Playwright (`fill()`, `type()`)
- HTML default value
- JavaScript updates

Internally, Playwright reads:
```js
element.value
```

---

## 🧪 `inputValue()` Examples

### 1️⃣ User types manually

```html
<input id="name">
```

User types `Nitin`

```js
await page.locator('#name').inputValue();
// "Nitin"
```

---

### 2️⃣ Playwright fills the value

```js
await page.locator('#name').fill('Patil');

await page.locator('#name').inputValue();
// "Patil"
```

---

### 3️⃣ Value set via HTML

```html
<input id="city" value="Pune">
```

```js
await page.locator('#city').inputValue();
// "Pune"
```

---

### 4️⃣ Value changed via JavaScript

```js
await page.evaluate(() => {
  document.querySelector('#name').value = 'Mumbai';
});
```

```js
await page.locator('#name').inputValue();
// "Mumbai"
```

---

## ❌ What `inputValue()` Does NOT Do

- Track keyboard events
- Know who typed (user vs automation)
- Read visible text
- Read placeholders
- Read inner text

---

## 🔹 `textContent()` — Explained

### ✅ What it returns
`textContent()` returns the **text inside an element**, including hidden text.

It works for:
- `<div>`
- `<span>`
- `<p>`
- `<label>`
- `<button>`

❌ It does **NOT** work for `<input>` or `<textarea>`

Internally, Playwright reads:
```js
element.textContent
```

---

## 🧪 `textContent()` Examples

### 1️⃣ Reading visible text

```html
<div id="msg">Welcome Nitin</div>
```

```js
await page.locator('#msg').textContent();
// "Welcome Nitin"
```

---

### 2️⃣ Hidden text is included

```html
<div id="status">
  Success
  <span style="display:none">Hidden</span>
</div>
```

```js
await page.locator('#status').textContent();
// "SuccessHidden"
```

---

### 3️⃣ ❌ Common mistake

```js
await page.locator('#name').textContent(); // ❌ WRONG
```

Reason:
> `<input>` elements do not have inner text — only a `value`.

---

## 🆚 `inputValue()` vs `textContent()`

| Feature | `inputValue()` | `textContent()` |
|------|---------------|----------------|
| Used for | Input elements | Normal elements |
| Reads | `element.value` | `element.textContent` |
| Works on `<input>` | ✅ Yes | ❌ No |
| Includes hidden text | N/A | ✅ Yes |
| Tracks typing | ❌ No | ❌ No |

---

## 🆚 `inputValue()` vs `getAttribute('value')`

```html
<input id="email" value="initial@mail.com">
```

User types `changed@mail.com`

| Method | Returned Value |
|------|---------------|
| `inputValue()` | `changed@mail.com` |
| `getAttribute('value')` | `initial@mail.com` |

---

## ✅ Best Practice in Playwright (Recommended)

```js
await expect(page.locator('#email')).toHaveValue('changed@mail.com');
await expect(page.locator('#msg')).toHaveText('Welcome Nitin');
```

---

## 🧠 Easy Rule to Remember

> **User enters data → `inputValue()`**  
> **User sees text → `textContent()`**

---

## 📌 Final Answer

> **`inputValue()` returns the current `value` property of form fields.**  
> **`textContent()` returns the text inside normal DOM elements.**
