# 📘 Playwright – All Ways to Enter or Send Text (Complete Guide)

This document explains all Playwright methods used to type, insert, or send data into input fields, including their behavior, usage, and differences.

## 🔥 Quick Summary Table
| Method | Clears existing text? | Types like human? | Triggers keyboard events? | Speed | Best For |
|--------|----------------------|------------------|--------------------------|-------|----------|
| fill() | ✔ Yes | ❌ No | Partial | Fast | Standard form input |
| type() | ❌ No (appends) | ✔ Yes | ✔ Full | Slow/realistic | Autocomplete, key events |
| keyboard.type() | ❌ No | ✔ Yes | ✔ Full | Slow/realistic | When element already focused |
| keyboard.press() | ❌ No | Key only | ✔ Full | Fast | Keyboards shortcuts, Enter/Tab |
| keyboard.insertText() | ❌ No | ❌ No | ❌ No | Fastest | Bypassing JS events |
| evaluate() | ✔ Yes | ❌ No | ❌ No | Fast | When normal methods fail |

## 1️⃣ fill() – Fast, Clears Field, No Keystrokes
✔ Important Points
- Clears existing text automatically
- Inserts value instantly (not typed)
- Does NOT trigger keydown/keyup for each character
- Only final input/change events fire
- Fastest common method

✔ Example
```js
  await page.locator("#username").fill("john");
```

✔ When to Use
- Standard form filling
- When old text must be removed
- When speed matters

## 2️⃣ type() – Human-Like Typing, Doesn’t Clear
✔ Important Points
- ❗ Does NOT clear existing text → it appends
- Types characters one by one
- Triggers keydown → keypress → keyup for every character
- Works like a human typing
- Supports typing delays

✔ Example
```js
  await page.locator("#username").type("john"); 
```
 
If field has `old`:
➡️ Result → `oldjohn`

✔ With delay
```js
await page.locator("#username").type("john", { delay: 150 });
```

✔ When to Use
- Autocomplete searches
- Events tied to keystrokes
- When simulating a real user

## 3️⃣ keyboard.type() – Type Into Focused Element
✔ Important Points
- Same as type(), but uses keyboard, not locator
- Requires clicking or focusing element first
- Triggers full key events
- Does not clear text

✔ Example
```js
await page.click("#username");
await page.keyboard.type("john doe");
```

✔ When to Use
- When interacting with dynamic editors (CodeMirror, Monaco)
- When locator typing fails

## 4️⃣ keyboard.press() – Single Key Press
✔ Important Points
- Sends one key press, not text
- Useful for shortcuts: Enter, Backspace, Tab, ArrowUp
- Triggers full keydown/keyup events
- Does not clear text

✔ Example
```js
await page.locator("#username").press("Control+A");
await page.locator("#username").press("Backspace");
await page.locator("#username").press("Enter");
```

✔ When to Use
- Submitting forms (Enter)
- Moving focus (Tab)
- Hotkeys & shortcuts

## 5️⃣ keyboard.insertText() – Insert Text Without Keystrokes
✔ Important Points
- Does NOT trigger any key events
- Does not simulate typing
- Does not clear text
- Inserts text directly into DOM
- Fastest method when keystrokes not needed

✔ Example
```js
await page.click("#username");
await page.keyboard.insertText("john");
```

✔ When to Use
- Avoiding event listeners
- Speed/performance testing
- Inputs that block simulated typing

## 6️⃣ evaluate() – Set Value Using JavaScript
✔ Important Points
- Uses page JS context to set .value
- Does not fire key events
- Does not simulate typing
- Completely bypasses frontend validations
- Clears existing text only if you set empty string

✔ Example
```js
await page.locator("#username").evaluate(el => el.value = 'john');
```

✔ When to Use
- When UI blocks typing/filling
- React/Angular controlled inputs
- Special custom editors

## 🔍 Detailed Comparison

#### Clearing Behavior

- ✔ fill() clears text
- ✔ evaluate() can clear if set to ""
- ❌ Others do not clear

#### Typing Simulation

Only these behave like real typing:
- type()
- keyboard.type()

#### Trigger Events
- type() / keyboard.type() → all key events
- fill() → only final input/change
- insertText() → no key events
- evaluate() → no events

#### Best for Reliability
| Scenario                  | Best Method    |
| ------------------------- | -------------- |
| Entering text normally    | `fill()`       |
| Simulating human typing   | `type()`       |
| Sending keys (Enter, Tab) | `press()`      |
| Bypassing event handlers  | `insertText()` |
| UI not accepting input    | `evaluate()`   |


## 🎉 Final Recommendation
| Need                         | Use                     |
| ---------------------------- | ----------------------- |
| Fast & clean                 | `fill()`                |
| Realistic typing             | `type()`                |
| Keyboard shortcuts           | `keyboard.press()`      |
| Insert text with zero events | `keyboard.insertText()` |
| Hard input fields            | `evaluate()`            |

