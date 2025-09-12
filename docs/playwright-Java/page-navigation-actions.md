# 🌐 Playwright Java – Navigation Actions

This document explains all navigation-related actions available in **Java Playwright** with examples.

---

## 1. `page.navigate("https://example.com")`
👉 Navigates the browser to the given URL.  
- Waits until the page is loaded (`load` event by default).  
- Supports additional options like timeout, waiting for specific load states, etc.  

**Example:**
```java
Page page = context.newPage();
page.navigate("https://example.com");
```

**With options (wait until DOM content loaded):**
```java
page.navigate("https://example.com",
    new Page.NavigateOptions().setWaitUntil(LoadState.DOMCONTENTLOADED));
```

---

## 2. `page.goBack()`
👉 Simulates the **browser back button**.  
- Goes to the previous page in the history.  
- Returns a `Response` object if navigation is successful, or `null` if there’s no history.  

**Example:**
```java
page.navigate("https://example.com");
page.navigate("https://google.com");

// Go back to example.com
page.goBack();
```

---

## 3. `page.goForward()`
👉 Simulates the **browser forward button**.  
- Moves forward in the history if available.  
- Returns a `Response` object or `null` if no forward entry exists.  

**Example:**
```java
page.goBack();     // goes to example.com
page.goForward();  // goes to google.com again
```

---

## 4. `page.reload()`
👉 Reloads the current page.  
- Similar to pressing the refresh button.  
- By default waits for the `load` event, but you can customize wait states.  

**Example:**
```java
page.reload();
```

**With options:**
```java
page.reload(new Page.ReloadOptions().setWaitUntil(LoadState.DOMCONTENTLOADED));
```

---

## 5. `page.title()`
👉 Gets the **title of the current page** (the `<title>` tag content).  
- Returns a `String`.  

**Example:**
```java
String title = page.title();
System.out.println("Page title is: " + title);
```

---

## 6. `page.url()`
👉 Returns the **current page URL** as a `String`.  

**Example:**
```java
System.out.println("Current URL: " + page.url());
```

---

## 7. `page.content()`
👉 Returns the **full HTML content** of the page as a `String`.  
- Useful for debugging, parsing, or verifying HTML.  

**Example:**
```java
String html = page.content();
System.out.println(html);
```

---

# 🔑 Quick Notes
- `navigate`, `goBack`, `goForward`, and `reload` return a `Response` object → you can check status codes, headers, etc.  
- `title`, `url`, and `content` return **String values** → handy for validations in tests.  
- All navigation methods can take optional parameters like **timeout** and **waitUntil** (`load`, `domcontentloaded`, `networkidle`).  
