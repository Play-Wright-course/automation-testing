# Java Playwright – File Upload & Download Examples

This guide explains how to handle **File Upload** and **File Download** in **Java Playwright** with code samples.

---

## 📌 File Upload Concept
- Playwright does not interact with the native OS file chooser.
- Instead, we use `setInputFiles()` to programmatically set files into `<input type="file">` elements.
- Supports single and multiple files.

### ✅ Upload Single File
```java
import com.microsoft.playwright.*;

public class FileUploadSingle {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            page.navigate("https://www.w3schools.com/howto/howto_html_file_upload_button.asp");

            // Upload a single file
            page.setInputFiles("input[type='file']", "C:\\Users\\Sandesh\\Desktop\\test.txt");

            // Assertion (Check if file input has value)
            String fileName = page.inputValue("input[type='file']");
            assert fileName.contains("test.txt");

            System.out.println("✅ Single File uploaded successfully");
        }
    }
}
```

---

### ✅ Upload Multiple Files
```java
import com.microsoft.playwright.*;

public class FileUploadMultiple {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            page.navigate("https://www.w3schools.com/howto/howto_html_file_upload_button.asp");

            // Upload multiple files
            page.setInputFiles("input[type='file']", new String[] {
                "C:\\Users\\Sandesh\\Desktop\\test1.txt",
                "C:\\Users\\Sandesh\\Desktop\\test2.txt"
            });

            // Assertion (Check both file names are uploaded)
            String fileNames = page.inputValue("input[type='file']");
            assert fileNames.contains("test1.txt") && fileNames.contains("test2.txt");

            System.out.println("✅ Multiple Files uploaded successfully");
        }
    }
}
```

---

## 📌 File Download Concept
- Use `page.waitForDownload()` to capture the `Download` object.
- Save the downloaded file to a desired location using `download.saveAs()`.

### ✅ File Download Example
```java
import com.microsoft.playwright.*;
import java.nio.file.Paths;

public class FileDownloadExample {
    public static void main(String[] args) {
        try (Playwright playwright = Playwright.create()) {
            Browser browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(false));
            Page page = browser.newPage();

            page.navigate("https://file-examples.com/index.php/sample-documents-download/");

            // Wait for download event
            Download download = page.waitForDownload(() -> {
                page.click("a[href*='sample.doc']"); // sample download link
            });

            // Save the file to desired location
            download.saveAs(Paths.get("C:\\Users\\Sandesh\\Downloads\\sample.doc"));

            // Assertion (Check file is downloaded successfully)
            assert download.path() != null;

            System.out.println("✅ File downloaded to: " + download.path());
        }
    }
}
```

---

### 🔹 Handling Dynamic Filenames
If the downloaded file has a random or dynamic name, you can:
```java
Download download = page.waitForDownload(() -> {
    page.click("a.download-link");
});

// Save with a custom name regardless of original name
download.saveAs(Paths.get("C:\\Users\\Sandesh\\Downloads\\myFile.docx"));
```
---

## 📌 Key Notes
- `setInputFiles()` works only on `<input type="file">` elements.
- Always use `waitForDownload()` to ensure the file is completely downloaded before accessing it.
- You can add assertions to verify file name, existence, or size.

---

✅ This covers **Single File Upload, Multiple File Upload with Assertions, and File Download Handling** in **Java Playwright**.
