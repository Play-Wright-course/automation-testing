# Playwright – Drag & Drop and Keyboard Interactions (Java)

---

## 1️⃣ Drag and Drop

### Example HTML

```html
<div id="source" draggable="true">Drag me</div>
<div id="target">Drop here</div>
```

### a) Simple Drag and Drop using `dragTo()`

```java
Locator source = page.locator("#source");
Locator target = page.locator("#target");

source.dragTo(target);
```

* Simulates dragging from source element to target element.
* Handles mouse events automatically.
* Auto-waits for elements to be visible.

### b) Drag and Drop Using Mouse Actions

```java
page.mouse().move(100, 200);  // Move to source coordinates
page.mouse().down();           // Click and hold
page.mouse().move(300, 400);  // Move to target coordinates
page.mouse().up();             // Release
```

* Useful if elements are custom draggable items not directly supported by `dragTo()`.

### c) Iterating Multiple Draggable Items

```java
Locator items = page.locator(".draggable");
int count = items.count();
for (int i = 0; i < count; i++) {
    items.nth(i).dragTo(page.locator("#target"));
}
```

* Allows dragging multiple items to the target container.

### d) Tips

* Use `dragTo()` for standard HTML5 draggable elements.
* Use `mouse()` actions for custom implementations.
* Combine with assertions to verify drop success.

---

## 2️⃣ Keyboard Interactions

### a) Typing Text (`fill` and `type`)

```java
page.locator("#searchBox").fill("Playwright");  // Instant fill
page.locator("#searchBox").type("Automation");  // Simulate typing character by character
```

* `fill()` sets value instantly.
* `type()` triggers keyboard events.

### b) Pressing Keys

```java
page.locator("#searchBox").press("Enter");     // Press Enter key
page.locator("#searchBox").press("Tab");       // Move focus to next element
```

* Equivalent to `sendKeys(Keys.ENTER)` in Selenium.
* Triggers keypress events.

### c) Keyboard Shortcuts / Combination Keys

```java
page.keyboard().press("Control+A");  // Select all text
page.keyboard().press("Control+C");  // Copy
page.keyboard().press("Control+V");  // Paste
```

* Can simulate shortcuts for copy, paste, undo, etc.

### d) Using `keyboard.type()` for Raw Input

```java
page.keyboard().type("Hello World");  // Types text anywhere the focus is active
```

* Useful when no input locator is available but you need to send keys globally.

### e) Full Example Flow

```java
// Focus search box
page.locator("#searchBox").click();

// Fill and submit
page.locator("#searchBox").fill("Playwright");
page.locator("#searchBox").press("Enter");

// Select all text and delete
page.keyboard().press("Control+A");
page.keyboard().press("Backspace");
```

### ✅ Tips

* Playwright auto-waits for elements to be visible before keyboard interactions.
* Use `.press()` for single keys or shortcuts, `.type()` for simulating typing character by character.
* Drag & Drop and Keyboard methods can be combined for complex flows (e.g., drag + keyboard shortcuts).

---

## 3️⃣ Mouse Actions

### a) Click

```java
Locator button = page.locator("#submitBtn");
button.click();
```

* Simulates a single left mouse click on the element.

### b) Double Click

```java
Locator textBox = page.locator("#inputBox");
textBox.dblclick();
```

* Selects text or activates default double-click behavior.

### c) Hover

```java
Locator menu = page.locator("#menu");
menu.hover();
```

* Moves mouse over the element (useful for dropdowns, tooltips).

### d) Move Mouse

```java
page.mouse().move(200, 300);
```

* Moves mouse pointer to specific screen coordinates.

### e) Mouse Down and Up

```java
page.mouse().move(100, 200); // Move to element
page.mouse().down();         // Press and hold mouse button
page.mouse().up();           // Release mouse button
```

* Useful for drag-and-drop or click-and-hold actions.

### f) Click at Coordinates

```java
page.mouse().click(150, 250);
```

* Clicks at absolute screen coordinates, bypassing locators.

### g) Right Click

```java
Locator element = page.locator("#contextMenu");
element.click(new Locator.ClickOptions().setButton(MouseButton.RIGHT));
```

* Opens context menus.

---

## 4️⃣ Advanced Keyboard Actions

### a) Type Text

```java
page.keyboard().type("Hello");
```

* Types text wherever the focus is set.

### b) Press Enter

```java
page.keyboard().press("Enter");
```

* Simulates pressing Enter key.

### c) Key Down and Key Up

```java
page.keyboard().down("Shift");   // Hold Shift
page.keyboard().up("Shift");     // Release Shift
```

* Useful for combinations like Shift+Click.

### d) Sequential Typing

```java
Locator field = page.locator("#username");
field.pressSequentially("Playwright");
```

* Types text character by character into a field (human-like typing).
