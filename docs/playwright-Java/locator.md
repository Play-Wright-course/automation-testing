# Playwright Locators – Complete Guide (Java)

This guide covers **all locator strategies in Playwright (Java)** with examples, including ARIA roles and accessibility-based locators.

---

## 🔹 Example HTML
```html
<input type="text" id="email" class="form-control" placeholder="Enter email" />

<button id="submitBtn" class="btn btn-primary" type="submit">Submit</button>

<span class="text">Title</span>

<a href="/home">Home</a>
```

---

## 🔹 Locator Types

### 1. By **ID**
```java
page.locator("#email");
page.locator("#submitBtn");
```

### 2. By **Class**
```java
page.locator(".form-control");
page.locator(".btn.btn-primary");
```

### 3. By **Tag Name**
```java
page.locator("button");
page.locator("input");
```

### 4. By **Text Content**
```java
page.getByText("Submit");
page.getByText("Home");
```

### 5. By **Role (ARIA Accessibility)**
**ARIA roles** are accessibility attributes in HTML that define the purpose of an element for screen readers. Playwright’s `getByRole` uses the accessibility tree.

```java
page.getByRole(AriaRole.BUTTON, new Page.GetByRoleOptions().setName("Submit"));
page.getByRole(AriaRole.LINK, new Page.GetByRoleOptions().setName("Home"));
```

- Use `getByRole` for buttons, links, headings, checkboxes, etc.
- More stable than CSS/XPath since roles rarely change.
- Filters elements by their **accessible name** (text or ARIA label).

**Example of explicit role in HTML:**
```html
<div role="button" aria-label="Submit Form">Submit</div>
```

**Rule of Thumb:** Prefer `getByRole` if a semantic role exists; fallback to XPath/CSS otherwise.

### 6. By **Placeholder**
```java
page.getByPlaceholder("Enter email");
```

### 7. By **Label**
```html
<label for="email">Email</label>
<input id="email" />
```
```java
page.getByLabel("Email");
```

### 8. By **Alt Text**
```html
<img src="logo.png" alt="Company Logo">
```
```java
page.getByAltText("Company Logo");
```

### 9. By **Title Attribute**
```html
<button title="Click to submit">Submit</button>
```
```java
page.getByTitle("Click to submit");
```

### 10. By **CSS Attribute Selector**
```java
page.locator("input[type='text']");
page.locator("button[type='submit']");
page.locator("a[href='/home']");
```

### 11. By **XPath**
```java
page.locator("//button[text()='Submit']");
page.locator("//input[@id='email']");
```

## 🔹 Handling Multiple Matches

```html
<ul>
  <li class="item">Apple</li>
  <li class="item">Banana</li>
  <li class="item">Cherry</li>
</ul>
```

```java
Locator items = page.locator(".item");
int count = items.count();

items.nth(0);  // Apple
items.nth(1);  // Banana
items.nth(2);  // Cherry

for (int i = 0; i < count; i++) {
    System.out.println(items.nth(i).innerText());
}

Locator banana = page.locator(".item").filter(new Locator.FilterOptions().setHasText("Banana"));

page.locator(".item").first();
page.locator(".item").last();
```

## 🔹 Summary

- Use **semantic locators** (`getByRole`, `getByLabel`, `getByPlaceholder`) for stable and accessibility-compliant tests.  
- Use **CSS/XPath** only if necessary.  
- Manage multiple elements using `.count()`, `.nth()`, `.first()`, `.last()`, `.filter()`.  
- **ARIA roles** ensure robust, readable, and accessible test selection.
