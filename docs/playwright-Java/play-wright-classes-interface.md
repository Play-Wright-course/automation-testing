# Playwright Components: Class vs Interface (Java)

| Component       | Type in Java                                   | Explanation                                                                                  |
|-----------------|-----------------------------------------------|----------------------------------------------------------------------------------------------|
| Playwright      | Class (`com.microsoft.playwright.Playwright`) | Entry point for creating browsers. You call `Playwright.create()` to get an instance.       |
| Browser         | Interface (`com.microsoft.playwright.Browser`) | Represents a running browser (Chromium, Firefox, WebKit). You don’t instantiate it directly; Playwright returns it when you launch a browser. |
| BrowserContext  | Interface (`com.microsoft.playwright.BrowserContext`) | Represents an isolated session within a browser. Returned by `browser.newContext()`.        |
| Page            | Interface (`com.microsoft.playwright.Page`)   | Represents a tab or page inside a context. Returned by `context.newPage()`.                 |
