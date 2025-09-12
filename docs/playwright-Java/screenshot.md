# Java Playwright – Screenshots & Videos Examples

This guide explains how to handle **Screenshots** and **Videos** in **Java Playwright** with practical code examples.

---

## 📸 Screenshots in Playwright

### ✅ Full Page Screenshot
```java
import com.microsoft.playwright.*;
import java.nio.file.Paths;

public class FullPageScreenshot {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            page.navigate("https://example.com");

            // Capture full page screenshot
            page.screenshot(new Page.ScreenshotOptions()
                .setPath(Paths.get("C:\\Users\\Sandesh\\Desktop\\fullpage.png"))
                .setFullPage(true));

            System.out.println("✅ Full page screenshot captured");
        }
    }
}
```

---

### ✅ Element Screenshot
```java
import com.microsoft.playwright.*;
import java.nio.file.Paths;

public class ElementScreenshot {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            page.navigate("https://example.com");

            // Take screenshot of a specific element
            Locator heading = page.locator("h1");
            heading.screenshot(new Locator.ScreenshotOptions()
                .setPath(Paths.get("C:\\Users\\Sandesh\\Desktop\\element.png")));

            System.out.println("✅ Element screenshot captured");
        }
    }
}
```

---

### ✅ Screenshot After Assertion
```java
import com.microsoft.playwright.*;
import java.nio.file.Paths;

public class ScreenshotWithAssertion {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            page.navigate("https://example.com");

            // Assertion
            String title = page.title();
            assert title.contains("Example");

            // Capture screenshot after validation
            page.screenshot(new Page.ScreenshotOptions()
                .setPath(Paths.get("C:\\Users\\Sandesh\\Desktop\\assertion.png")));

            System.out.println("✅ Screenshot captured after assertion");
        }
    }
}
```

---

## 🎥 Videos in Playwright

### ✅ Record Video for a Single Page
```java
import com.microsoft.playwright.*;
import java.nio.file.Paths;

public class RecordVideoExample {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));

            // Enable video recording when creating context
            BrowserContext context = browser.newContext(new Browser.NewContextOptions()
                .setRecordVideoDir(Paths.get("C:\\Users\\Sandesh\\Desktop\\videos"))
                .setRecordVideoSize(1280, 720));

            Page page = context.newPage();
            page.navigate("https://example.com");
            page.click("a"); // some action

            // Close context to ensure video is saved
            context.close();

            System.out.println("✅ Video recorded and saved");
        }
    }
}
```

---

### ✅ Record Video for Each Test (Dynamic Naming)
```java
import com.microsoft.playwright.*;
import java.nio.file.Paths;

public class RecordVideoDynamicName {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch();

            // Set folder where videos will be stored
            BrowserContext context = browser.newContext(new Browser.NewContextOptions()
                .setRecordVideoDir(Paths.get("C:\\Users\\Sandesh\\Desktop\\videos"))
                .setRecordVideoSize(1920, 1080));

            Page page = context.newPage();
            page.navigate("https://example.com");

            // Perform some actions
            page.click("a");

            // Retrieve video path after context closes
            context.close();

            for (Page p : context.pages()) {
                System.out.println("Video Path: " + p.video().path());
            }
        }
    }
}
```

---

## 📌 Key Notes
- **Screenshots**:
  - Use `page.screenshot()` for full page.
  - Use `locator.screenshot()` for specific elements.
  - Can be combined with assertions for debugging.

- **Videos**:
  - Videos are recorded at the **context level** (not page level).
  - Use `setRecordVideoDir()` to specify folder for saving videos.
  - Close the context (`context.close()`) to ensure videos are written to disk.
  - Use `p.video().path()` to get the file path of the recorded video.

---

✅ This covers **Full Page Screenshots, Element Screenshots, Assertion-based Screenshots, and Video Recording Scenarios** in **Java Playwright**.
