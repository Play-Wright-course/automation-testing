# 9. Handling Dialogs, Alerts, and Prompts in Playwright (Java)

Web applications often use **dialogs** like Alerts, Confirms, and Prompts for user interaction.  
Playwright provides APIs to handle these dialogs by **listening to the `dialog` event**.

---

## ✅ Types of JavaScript Dialogs

1. **Alert**
   - Simple message with **OK** button.
   - Example: `alert("This is an alert!");`

2. **Confirm**
   - Message with **OK** and **Cancel** buttons.
   - Example: `confirm("Are you sure?");`

3. **Prompt**
   - Message with input field + **OK/Cancel** buttons.
   - Example: `prompt("Enter your name:");`

4. **BeforeUnload**
   - Triggered when a user tries to close or reload a page.
   - Example: `window.onbeforeunload = () => true;`

---

## 📌 Playwright Dialog API

- **Event Listener for Dialog**
```java
page.onDialog(dialog -> {
    System.out.println("Dialog message: " + dialog.message());
    dialog.accept(); // or dialog.dismiss()
});
```

- **Dialog Methods**
  - `dialog.message()` → Get text of the dialog.
  - `dialog.type()` → Returns type (`alert`, `confirm`, `prompt`, `beforeunload`).
  - `dialog.accept([promptText])` → Accept the dialog (for prompt, send text).
  - `dialog.dismiss()` → Dismiss the dialog (Cancel).

---

## 📌 Example Code (Java + Playwright)

```java
import com.microsoft.playwright.*;

public class DialogsExample {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            // Navigate to sample page with dialogs
            page.navigate("https://the-internet.herokuapp.com/javascript_alerts");

            // --- Handle Alert ---
            page.onceDialog(dialog -> {
                System.out.println("Alert Text: " + dialog.message());
                dialog.accept();
            });
            page.click("text=Click for JS Alert");

            // --- Handle Confirm (OK) ---
            page.onceDialog(dialog -> {
                System.out.println("Confirm Text: " + dialog.message());
                dialog.accept(); // choose OK
            });
            page.click("text=Click for JS Confirm");

            // --- Handle Confirm (Cancel) ---
            page.onceDialog(dialog -> {
                System.out.println("Confirm Text: " + dialog.message());
                dialog.dismiss(); // choose Cancel
            });
            page.click("text=Click for JS Confirm");

            // --- Handle Prompt with input ---
            page.onceDialog(dialog -> {
                System.out.println("Prompt Text: " + dialog.message());
                dialog.accept("PlaywrightUser"); // enter text
            });
            page.click("text=Click for JS Prompt");

            // --- Handle BeforeUnload ---
            page.onceDialog(dialog -> {
                System.out.println("BeforeUnload triggered");
                dialog.accept();
            });
            page.evaluate("() => window.onbeforeunload = () => true;");
            page.reload();

            browser.close();
        }
    }
}
```

---

## 🔑 Notes

- Use `page.onDialog()` for handling dialogs **globally** (persistent listener).
- Use `page.onceDialog()` for handling a **single occurrence**.
- For **prompt dialogs**, always provide text inside `dialog.accept("yourText")`.
- Playwright will **auto-wait** until dialog is shown before executing callback.
- If dialogs are not handled → tests will fail (dialogs block execution).

---

✅ With these APIs, you can handle **Alerts, Confirms, Prompts, and BeforeUnload dialogs** in Playwright tests using Java.
