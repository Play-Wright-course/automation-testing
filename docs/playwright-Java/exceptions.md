# Java Playwright – Common Exceptions and How to Handle Them

Playwright in Java provides powerful automation features, but you may encounter **exceptions** during execution.  
This guide lists the most common exceptions, their **causes**, and **solutions with code snippets**.

---

## 1. TimeoutError
**Cause:**  
- An action (like `click`, `fill`, `waitForSelector`) did not complete within the default timeout (usually 30 seconds).  
- Element is not visible, attached, or ready for interaction.

**Solution:**  
- Increase timeout using `setTimeout()` or pass custom timeout in action options.  
- Ensure element is visible before interacting.

**Code Example:**
```java
page.click("button#submit", new Page.ClickOptions().setTimeout(10000)); // 10 sec timeout

// Or set default timeout for the page
page.setDefaultTimeout(15000);
```

---

## 2. PlaywrightException (Generic Exception)
**Cause:**  
- Incorrect selectors (e.g., wrong CSS/XPath).  
- Performing actions on detached or invalid elements.  

**Solution:**  
- Always validate selectors with `page.locator()` or `page.isVisible()`.  
- Use `waitForSelector()` before performing action.

**Code Example:**
```java
if (page.isVisible("input#username")) {
    page.fill("input#username", "sandesh");
} else {
    System.out.println("Element not found!");
}
```

---

## 3. ElementHandleException
**Cause:**  
- Attempting to interact with a `Locator` or `ElementHandle` that is no longer attached to the DOM.  
- Example: Page refreshed or element re-rendered.

**Solution:**  
- Re-locate the element before interaction.  
- Use `locator` API instead of `elementHandle` where possible (auto-handles re-attachment).

**Code Example:**
```java
Locator loginBtn = page.locator("#login");
loginBtn.click(); // safer than elementHandle

// If using elementHandle
ElementHandle handle = page.querySelector("#login");
handle.click(); // might fail if DOM changes
```

---

## 4. DownloadFailureException
**Cause:**  
- Download interrupted, canceled, or file not generated.  
- Permissions issue writing file.

**Solution:**  
- Ensure `waitForDownload()` is used properly.  
- Use `download.saveAs()` to explicitly save file to desired location.

**Code Example:**
```java
Download download = page.waitForDownload(() -> {
    page.click("a#downloadLink");
});

download.saveAs(Paths.get("C:\\Users\\Sandesh\\Downloads\\file.txt"));
```

---

## 5. NavigationException
**Cause:**  
- Page fails to navigate to a URL (e.g., network issues, invalid URL).  
- Timeout while waiting for page load.

**Solution:**  
- Use `page.navigate()` with explicit timeout.  
- Add retries for flaky connections.

**Code Example:**
```java
page.navigate("https://example.com", new Page.NavigateOptions().setTimeout(20000));
```

---

## 6. WebSocketException
**Cause:**  
- Playwright internally communicates with browser over WebSocket.  
- Exception occurs when connection is lost (browser crash, closed unexpectedly).

**Solution:**  
- Restart browser context/session.  
- Add retry logic in test framework.

**Code Example:**
```java
try {
    page.navigate("https://example.com");
} catch (PlaywrightException e) {
    System.out.println("Browser disconnected. Restarting...");
    // re-launch browser
}
```

---

## 7. SelectorResolutionException
**Cause:**  
- Invalid selector syntax (CSS or XPath).  
- Element does not exist.

**Solution:**  
- Test selector validity in browser dev tools.  
- Use `page.locator()` instead of `page.querySelector()` for better debugging.

**Code Example:**
```java
Locator button = page.locator("button:has-text('Login')");
button.click();
```

---

## 8. AssertionError
**Cause:**  
- Assertions fail due to unexpected values.  
- Example: Page title mismatch.

**Solution:**  
- Print actual vs expected values for debugging.  
- Use retries or waits if data loads asynchronously.

**Code Example:**
```java
String title = page.title();
assert title.equals("Expected Title") : "Title mismatch! Actual: " + title;
```

---

## 9. FileAlreadyExistsException
**Cause:**  
- While saving downloads/screenshots, file already exists at the same path.

**Solution:**  
- Save with a unique name using timestamp or UUID.

**Code Example:**
```java
String fileName = "screenshot_" + System.currentTimeMillis() + ".png";
page.screenshot(new Page.ScreenshotOptions().setPath(Paths.get(fileName)));
```

---

## 10. IllegalStateException (Playwright Context)
**Cause:**  
- Trying to use closed browser/page/context.  
- Example: Performing action after calling `browser.close()`.

**Solution:**  
- Ensure context/page is open before using.  
- Wrap in try-catch for cleanup.

**Code Example:**
```java
try {
    page.click("#btn");
} catch (IllegalStateException e) {
    System.out.println("Page is already closed.");
}
```

---

# 📌 Summary

| Exception | Cause | Solution |
|-----------|-------|----------|
| TimeoutError | Action exceeds wait time | Increase timeout, wait for selector |
| PlaywrightException | Generic errors | Validate selectors, wait for elements |
| ElementHandleException | Detached elements | Use `locator` API |
| DownloadFailureException | Download failed | Use `waitForDownload()` |
| NavigationException | Navigation failed | Add timeout/retry |
| WebSocketException | Browser connection lost | Restart session |
| SelectorResolutionException | Invalid selector | Validate selector syntax |
| AssertionError | Assertion failed | Print debug info, add waits |
| FileAlreadyExistsException | File path already exists | Save with unique names |
| IllegalStateException | Using closed context | Check before use |

---

✅ This document covers **all major exceptions in Java Playwright**, with their **causes, solutions, and code snippets**.
