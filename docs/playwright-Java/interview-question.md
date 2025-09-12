# Java Playwright UI Testing Interview Questions & Answers

This document contains 20+ real-time interview questions for **Java Playwright UI Testing** with in-depth explanations and example code snippets.

---

## 1. What is Playwright, and how is it different from Selenium?

**Answer:**
Playwright is an open-source automation library developed by Microsoft for web UI testing. Unlike Selenium, it supports:
- Multiple browsers (Chromium, Firefox, WebKit) with a single API.
- Auto-waiting for elements.
- Network interception and mocking.
- Headless and headful execution.

```java
import com.microsoft.playwright.*;

public class LaunchBrowser {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();
            page.navigate("https://example.com");
            System.out.println(page.title());
        }
    }
}
```

---

## 2. How do you launch a browser in Playwright with Java?

```java
Playwright playwright = Playwright.create();
Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
Page page = browser.newPage();
page.navigate("https://example.com");
```

---

## 3. How does Playwright handle synchronization (auto-waiting)?

**Answer:**
Playwright automatically waits for elements to be actionable before performing actions like `click()` or `fill()`. Unlike Selenium, explicit waits are less frequently needed.

```java
page.click("button#submit"); // Playwright waits until the button is clickable
```

---

## 4. How do you select elements in Playwright?

**Answer:**
Selectors can be:
- CSS selectors
- XPath
- Text selectors

```java
page.click("text=Login");
page.fill("#username", "admin");
page.fill("input[name='password']", "pass123");
```

---

## 5. How do you handle multiple browser contexts?

**Answer:**
Contexts allow isolated sessions, similar to incognito windows.

```java
BrowserContext context1 = browser.newContext();
Page page1 = context1.newPage();
page1.navigate("https://example1.com");

BrowserContext context2 = browser.newContext();
Page page2 = context2.newPage();
page2.navigate("https://example2.com");
```

---

## 6. How do you handle multiple pages/tabs?

```java
Page newPage = page.waitForPopup(() -> page.click("a[target='_blank']"));
newPage.waitForLoadState();
System.out.println(newPage.title());
```

---

## 7. How do you handle alerts in Playwright?

```java
page.onceDialog(dialog -> {
    System.out.println("Alert message: " + dialog.message());
    dialog.accept();
});
page.click("#trigger-alert");
```

---

## 8. How do you perform assertions in Playwright with Java?

Playwright provides `Assertions`.

```java
import static com.microsoft.playwright.assertions.PlaywrightAssertions.assertThat;

assertThat(page.locator("h1")).hasText("Welcome");
```

---

## 9. How do you upload files in Playwright?

```java
page.setInputFiles("input[type='file']", Paths.get("C:/files/sample.txt"));
```

---

## 10. How do you download files in Playwright?

```java
Download download = page.waitForDownload(() -> {
    page.click("a#downloadLink");
});
System.out.println("Downloaded file: " + download.path());
```

---

## 11. How do you handle frames in Playwright?

```java
Frame frame = page.frameByName("frameName");
frame.fill("#inputField", "Hello");
```

---

## 12. How do you take screenshots in Playwright?

```java
page.screenshot(new Page.ScreenshotOptions().setPath(Paths.get("screenshot.png")));
```

---

## 13. How do you handle hover actions in Playwright?

```java
page.hover("button#menu");
```

---

## 14. How do you handle drag and drop in Playwright?

```java
page.dragAndDrop("#source", "#target");
```

---

## 15. How do you emulate devices in Playwright?

```java
BrowserContext context = browser.newContext(new Browser.NewContextOptions()
    .setViewportSize(375, 667)
    .setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 13_5 like Mac OS X)"));
Page mobilePage = context.newPage();
mobilePage.navigate("https://example.com");
```

---

## 16. How do you intercept and modify network requests?

```java
page.route("**/api/**", route -> {
    route.fulfill(new Route.FulfillOptions().setBody("{"status":"mocked"}"));
});
page.navigate("https://example.com/api/test");
```

---

## 17. How do you wait for specific network responses?

```java
Response response = page.waitForResponse("**/api/data", () -> {
    page.click("#fetchData");
});
System.out.println(response.status());
```

---

## 18. How do you record a video of test execution?

```java
BrowserContext context = browser.newContext(new Browser.NewContextOptions()
    .setRecordVideoDir(Paths.get("videos/")));
Page videoPage = context.newPage();
videoPage.navigate("https://example.com");
context.close(); // saves video
```

---

## 19. How do you mock geolocation in Playwright?

```java
BrowserContext context = browser.newContext(new Browser.NewContextOptions()
    .setGeolocation(37.7749, -122.4194)
    .setPermissions(Arrays.asList("geolocation")));
Page page = context.newPage();
page.navigate("https://maps.google.com");
```

---

## 20. How do you run tests in parallel with Playwright + TestNG?

**Answer:**
Each test can run in its own browser context.

```java
import org.testng.annotations.Test;

public class ParallelTest {
    @Test
    public void test1() {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch();
            BrowserContext context = browser.newContext();
            Page page = context.newPage();
            page.navigate("https://example.com");
        }
    }
}
```

---

## 21. How do you integrate Playwright with CI/CD pipelines?

**Answer:**
- Install Playwright browsers in the pipeline.
- Run tests using Maven/Gradle.
- Publish results.

Example GitHub Actions YAML:
```yaml
name: Playwright Tests

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Java
        uses: actions/setup-java@v3
        with:
          java-version: '17'
      - name: Install Playwright
        run: mvn exec:java -Dexec.mainClass="com.microsoft.playwright.CLI" -Dexec.args="install"
      - name: Run Tests
        run: mvn test
```


---

## 22. How do you handle cookies in Playwright?

```java
// Get cookies
System.out.println(context.cookies());

// Add cookies
context.addCookies(Arrays.asList(new BrowserContext.AddCookiesOptions()
    .setName("session_id")
    .setValue("12345")
    .setUrl("https://example.com")));
```

---

## 23. How do you handle authentication in Playwright?

```java
BrowserContext context = browser.newContext(new Browser.NewContextOptions()
    .setHttpCredentials("username", "password"));
Page page = context.newPage();
page.navigate("https://secure-site.com");
```

---

## 24. How do you handle shadow DOM elements?

```java
page.locator("css=custom-element >>> button").click();
```

---

## 25. How do you handle slow networks in Playwright?

```java
BrowserContext context = browser.newContext(new Browser.NewContextOptions()
    .setOffline(false));
context.setDefaultNavigationTimeout(10000); // 10 seconds
```

---

## 26. How do you use Playwright Trace Viewer?

```java
BrowserContext context = browser.newContext(new Browser.NewContextOptions()
    .setRecordHarPath(Paths.get("trace.zip")));
Page page = context.newPage();
page.navigate("https://example.com");
context.close(); // trace saved
```

---

## 27. How do you mock API responses in Playwright?

```java
page.route("**/api/data", route -> {
    route.fulfill(new Route.FulfillOptions()
        .setStatus(200)
        .setContentType("application/json")
        .setBody("{"message":"Mocked Response"}"));
});
```

---

## 28. How do you retry failed tests in Playwright with Java?

**Answer:**
Use TestNG retry analyzers or JUnit retry rules. Playwright itself retries only locator actions.

```java
for (int i = 0; i < 3; i++) {
    try {
        page.click("#submit");
        break;
    } catch (Exception e) {
        if (i == 2) throw e;
    }
}
```

---

## 29. How do you handle basic authentication popups?

```java
BrowserContext context = browser.newContext(new Browser.NewContextOptions()
    .setHttpCredentials("user", "pass"));
Page page = context.newPage();
page.navigate("https://auth-site.com");
```

---

## 30. How do you test responsive design with Playwright?

```java
Page mobilePage = browser.newContext(new Browser.NewContextOptions()
    .setViewportSize(375, 667)).newPage();
mobilePage.navigate("https://example.com");
```

---

## 31. How do you test web accessibility with Playwright?

Playwright integrates with `axe-core` for accessibility testing.

```java
Object accessibilityTree = page.accessibility().snapshot();
System.out.println(accessibilityTree.toString());
```

---

## 32. How do you handle retries and flaky tests?

**Answer:**
- Use `retry` in CI/CD pipelines.
- Avoid `Thread.sleep()`, prefer auto-wait or `waitForSelector`.
- Stabilize locators.

```java
page.locator("button#login").click(new Locator.ClickOptions().setTrial(true));
```

---

## 33. How do you run Playwright tests in Docker?

- Create a Dockerfile with Java + Playwright installed.
- Run tests inside container.

```dockerfile
FROM mcr.microsoft.com/playwright/java:v1.49.0-jammy
COPY . /app
WORKDIR /app
RUN mvn test
```

---

## 34. How do you debug Playwright tests?

- Use `setHeadless(false)`
- Use `page.pause()` to inspect manually.

```java
page.pause(); // Opens Playwright Inspector
```

---

## 35. How do you handle rate-limiting in API calls during tests?

**Answer:**
- Add delays using `page.waitForTimeout(ms)`.
- Use network interception to simulate rate limits.

```java
page.waitForTimeout(2000); // wait for 2 seconds
```

---

## 36. How do you capture console logs in Playwright?

```java
page.onConsoleMessage(msg -> System.out.println("Console: " + msg.text()));
page.navigate("https://example.com");
```

---

## 37. How do you capture network requests and responses?

```java
page.onRequest(request -> System.out.println("Request: " + request.url()));
page.onResponse(response -> System.out.println("Response: " + response.url()));
```

---

## 38. How do you handle multiple downloads in Playwright?

```java
Download download = page.waitForDownload(() -> {
    page.click("a.download-all");
});
System.out.println(download.path());
```

---

## 39. How do you assert element visibility?

```java
import static com.microsoft.playwright.assertions.PlaywrightAssertions.assertThat;
assertThat(page.locator("#logo")).isVisible();
```

---

## 40. How do you run Playwright tests with Gradle?

```gradle
plugins {
    id 'java'
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.microsoft.playwright:playwright:1.49.0'
    testImplementation 'org.testng:testng:7.9.0'
}
```

---

## 41. How do you test single-page applications (SPAs) with Playwright?

**Answer:**
Use `waitForLoadState("networkidle")` to ensure all async calls are complete.

```java
page.click("#loadData");
page.waitForLoadState(LoadState.NETWORKIDLE);
```

---

## 42. How do you manage test data in Playwright?

**Answer:**
- Use external files (JSON/CSV).
- Use environment variables.

```java
String username = System.getenv("TEST_USER");
page.fill("#username", username);
```

---
