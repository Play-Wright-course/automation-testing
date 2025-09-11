# Playwright Locators – Complete Guide (Java)

This guide covers **all locator strategies in Playwright (Java)** with examples.

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

---

### 2. By **Class**
```java
page.locator(".form-control");
page.locator(".btn.btn-primary");
```

---

### 3. By **Tag Name**
```java
page.locator("button");
page.locator("input");
```

---

### 4. By **Text Content**
```java
page.getByText("Submit");   // <button>Submit</button>
page.getByText("Home");     // <a>Home</a>
```

---

### 5. By **Role (ARIA Accessibility)**
```java
page.getByRole(AriaRole.BUTTON, new Page.GetByRoleOptions().setName("Submit"));
page.getByRole(AriaRole.LINK, new Page.GetByRoleOptions().setName("Home"));
```

---

### 6. By **Placeholder**
```java
page.getByPlaceholder("Enter email");  // matches placeholder attribute
```

---

### 7. By **Label**
```html
<label for="email">Email</label>
<input id="email" />
```
```java
page.getByLabel("Email");
```

---

### 8. By **Alt Text**
```html
<img src="logo.png" alt="Company Logo">
```
```java
page.getByAltText("Company Logo");
```

---

### 9. By **Title Attribute**
```html
<button title="Click to submit">Submit</button>
```
```java
page.getByTitle("Click to submit");
```

---

### 10. By **CSS Attribute Selector**
```java
page.locator("input[type='text']");
page.locator("button[type='submit']");
page.locator("a[href='/home']");
```

---

### 11. By **XPath**
```java
page.locator("//button[text()='Submit']");
page.locator("//input[@id='email']");
```

---

## 🔹 Handling Multiple Matches

### Example HTML
```html
<ul>
  <li class="item">Apple</li>
  <li class="item">Banana</li>
  <li class="item">Cherry</li>
</ul>
```

### Code Examples

#### Get all elements
```java
Locator items = page.locator(".item");
int count = items.count();
System.out.println("Total items: " + count);
```

#### Pick by index
```java
items.nth(0);  // Apple
items.nth(1);  // Banana
items.nth(2);  // Cherry
```

#### Loop through elements
```java
int count = items.count();
for (int i = 0; i < count; i++) {
    System.out.println(items.nth(i).innerText());
}
```

#### Filter by text
```java
Locator banana = page.locator(".item").filter(new Locator.FilterOptions().setHasText("Banana"));
```

#### First and Last
```java
page.locator(".item").first();
page.locator(".item").last();
```

---

## 🔹 Summary

- Use **semantic locators** (`getByRole`, `getByLabel`, `getByPlaceholder`) for stable tests.  
- Use **CSS/XPath** only if necessary.  
- Locators returning multiple elements can be managed using `.count()`, `.nth()`, `.first()`, `.last()`, `.filter()`.  

