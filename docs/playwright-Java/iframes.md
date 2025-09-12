# 8. Handling Frames & iFrames in Playwright (Java)

Frames (`<frame>`) and iFrames (`<iframe>`) allow embedding another HTML document inside the main page.  
Playwright provides APIs to **switch context into frames** and interact with elements inside them.

---

## ✅ Key Concepts

### What is an iFrame?
- An `<iframe>` is an HTML tag that loads another HTML page inside the current page.
- Each frame has its own **DOM** and context, isolated from the main document.
- To interact with elements inside frames, you must **switch to the correct frame**.

---

## 📌 Playwright Frame API

### 1. Access All Frames
```java
page.frames(); // returns List<Frame>
```
- Retrieves all frames in the page, including main frame + nested frames.

### 2. Access Frame by Name / URL
```java
Frame frameByName = page.frame("frameName");
Frame frameByUrl = page.frameByUrl(".*someFrameUrl.*");
```

### 3. Access Nested Frames by Index
```java
List<Frame> frames = page.frames();
Frame firstFrame = frames.get(1);   // index 0 is always the main page
```

### 4. Locate Frame Element and Get Frame Object
```java
Locator frameLocator = page.frameLocator("iframe[name='frame1']");
```
- Useful for directly chaining locators into frame elements.

---

## 📌 Example Code (Java + Playwright)

```java
import com.microsoft.playwright.*;

public class FramesExample {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            // Navigate to page with frames
            page.navigate("https://the-internet.herokuapp.com/nested_frames");

            // --- Get all frames ---
            for (Frame f : page.frames()) {
                System.out.println("Frame: " + f.name() + " | URL: " + f.url());
            }

            // --- Switch to top frame (by name) ---
            Frame topFrame = page.frame("frame-top");
            System.out.println("Inside Top Frame: " + topFrame.name());

            // --- Nested frame (by index) ---
            Frame nestedLeft = topFrame.childFrames().get(0);
            System.out.println("Inside Nested Left Frame: " + nestedLeft.name());

            // Example: get text inside nested frame
            String text = nestedLeft.locator("body").innerText();
            System.out.println("Nested Frame Text: " + text);

            // --- Access frame by locator ---
            Frame frameExample = page.frameLocator("iframe[name='mce_0_ifr']").frame();
            frameExample.locator("#tinymce").fill("Hello inside iframe!");

            browser.close();
        }
    }
}
```

---

## 🔑 Notes

- **Main Page vs Frames**:
  - `page` → represents the main document.
  - `frame` → represents an iframe’s DOM.

- **Indexing**:
  - `page.frames().get(0)` → main page.
  - `page.frames().get(1+)` → child frames.

- **Frame Locator vs Frame Object**:
  - `page.frame("name")` → switch to a frame by name/id/URL.
  - `page.frameLocator("selector")` → chain locators inside an iframe without switching.

- **Nested Frames**:
  - Use `.childFrames()` recursively to drill down multiple levels.

- **Best Practice**:
  - Prefer `frameLocator()` for simplicity when working with a single iframe.
  - Use `frames()` list traversal for **nested or multiple frame hierarchies**.

---

✅ With these techniques, you can reliably handle **single, nested, and multiple frames** in Playwright tests using Java.
