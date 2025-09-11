# Playwright Interactions – Input & Buttons (Java)

---

## 1️⃣ Typing / Entering Text into Input Boxes

**Selenium Equivalent:**
```java
driver.findElement(By.id("searchBox")).sendKeys("Playwright");
```

### a) Using `fill()`
```java
page.locator("#searchBox").fill("Playwright");
```
- **What it does:** Clears any existing text and sets the new value.
- **Auto-waiting:** Waits until the element is visible and enabled.
- **Best for:** Setting values directly in forms.

### b) Using `type()`
```java
page.locator("#searchBox").type("Playwright");
```
- **What it does:** Types character by character, simulating real user typing.
- **Difference from `fill()`:**  
  1. `fill()` instantly sets the value.  
  2. `type()` simulates typing and triggers keyboard events.  
- **Best for:** Autocomplete, search boxes, or typing behavior testing.

### c) Pressing Keys
```java
page.locator("#searchBox").fill("Playwright");
page.locator("#searchBox").press("Enter");
```
- **Equivalent to:** `sendKeys(Keys.ENTER)` in Selenium.
- **Use case:** Submitting forms via keyboard.

### d) Example Full Search Box Flow
```java
page.locator("#searchBox").fill("Playwright");  // Type text instantly
page.locator("#searchBox").press("Enter");      // Submit by Enter key
```

### Difference Between `fill()` and `type()`

| Feature | `fill()` | `type()` |
|---------|----------|----------|
| Action | Sets value instantly | Types character by character |
| Auto-clear | Yes, clears existing text | No, appends to existing text unless cleared manually |
| Speed | Fast | Slower, simulates typing |
| Events triggered | Minimal | Triggers keypress, input events |
| Best for | Form filling | Autocomplete, typing simulation, keyboard events |

---

## 2️⃣ Clicking on Buttons

**Selenium Equivalent:**
```java
driver.findElement(By.id("submitBtn")).click();
```

### a) Simple Click
```java
page.locator("#submitBtn").click();
```
- Waits automatically for the button to be visible and enabled.
- No need for `Thread.sleep()` or explicit waits.

### b) Click by Text
```java
page.getByText("Submit").click();
```
- Finds element by visible text.
- Useful if ID or class is not available.

### c) Click by Role (ARIA)
```java
page.getByRole(AriaRole.BUTTON, new Page.GetByRoleOptions().setName("Submit")).click();
```
- Uses **accessibility info** (semantic role).
- Very **stable**; less likely to break if HTML changes.
- Recommended for **modern accessible web apps**.
