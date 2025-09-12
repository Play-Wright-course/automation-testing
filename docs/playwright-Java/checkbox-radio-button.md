# 7. Checkbox & Radio Button in Playwright (Java)

Checkboxes and Radio buttons are common form elements used for **binary selections** (true/false, yes/no, option A/B).  
Playwright provides a clean API to handle these elements.

---

## ✅ Key Playwright Methods

### 1. `locator.check()`
- Ensures the checkbox or radio button is **checked**.
- If it’s already checked → does nothing.
- If it’s disabled or hidden → Playwright waits until it’s actionable.

### 2. `locator.uncheck()`
- Ensures the checkbox is **unchecked**.
- Applicable only to checkboxes (not radio buttons).
- If already unchecked → does nothing.

### 3. `locator.isChecked()`
- Returns a **boolean** (`true/false`) if the checkbox or radio button is selected.

---

## 📌 Example Code (Java + Playwright)

```java
import com.microsoft.playwright.*;

public class CheckboxRadioExample {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            // Navigate to sample page
            page.navigate("https://the-internet.herokuapp.com/checkboxes");

            // ✅ Locate checkbox
            Locator checkbox1 = page.locator("//form[@id='checkboxes']/input[1]");

            // --- Check a checkbox ---
            checkbox1.check();
            System.out.println("Checkbox 1 checked: " + checkbox1.isChecked());

            // --- Uncheck a checkbox ---
            checkbox1.uncheck();
            System.out.println("Checkbox 1 checked after uncheck: " + checkbox1.isChecked());

            // ✅ Radio button example
            page.navigate("https://demoqa.com/radio-button");

            Locator yesRadio = page.locator("input[id='yesRadio']");

            // --- Select radio button ---
            yesRadio.check();
            System.out.println("Yes Radio selected: " + yesRadio.isChecked());

            browser.close();
        }
    }
}
```

---

## 🔑 Notes
- **Radio buttons**: You can only select one option in a group.
- **Checkboxes**: Can select multiple options unless restricted by form logic.
- Use `.isChecked()` to verify the state before performing an action if needed.
- Playwright automatically waits for the element to be visible, enabled, and ready for action.

---

✅ With these methods, you can reliably handle **checkboxes and radio buttons** in Playwright tests using Java.
