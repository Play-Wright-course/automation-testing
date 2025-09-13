# 11. Windows & Tabs Handling in Playwright (Java)

In Playwright, handling multiple **windows** or **tabs** is a common
scenario in web automation.\
Playwright treats each **new tab/window** as a `Page` object.

------------------------------------------------------------------------

## 🔹 Opening a New Window / Tab

When a link opens a new window or tab, Playwright can **listen for it**.

``` java
// Example: Click link that opens new tab/window
Page newPage = page.waitForPopup(() -> {
    page.locator("a#openNewTab").click();
});

System.out.println("New Page Title: " + newPage.title());
```

------------------------------------------------------------------------

## 🔹 Switching Window by Title

Suppose you want to switch to a tab/window with title **"hellpword"**.

``` java
for (Page p : page.context().pages()) {
    if (p.title().equalsIgnoreCase("hellpword")) {
        System.out.println("Switched to page with title: " + p.title());
        p.bringToFront();   // Make it active
        break;
    }
}
```

------------------------------------------------------------------------

## 🔹 Switching by Index of Tab

Each window/tab is stored in a list using `context.pages()`.\
You can switch by **index position**.

``` java
// Get all pages
List<Page> allPages = page.context().pages();

// Switch to second tab (index starts at 0)
Page secondTab = allPages.get(1);
secondTab.bringToFront();

System.out.println("Now on Tab: " + secondTab.title());
```

------------------------------------------------------------------------

## 🔹 Switching Using Keyboard (Tab Key)

Playwright supports **keyboard actions**.\
If you want to simulate switching tabs using **Ctrl + Tab**, you can
send key presses.

``` java
// Press CTRL + TAB to switch to next tab (browser level)
page.keyboard().press("Control+Tab");

// Or Shift+Control+Tab to move backwards
page.keyboard().press("Control+Shift+Tab");
```

⚠️ **Note:** Keyboard tab switching works only if the browser supports
shortcut handling.\
Preferred way is using `context().pages()`.

------------------------------------------------------------------------

## 🔹 Best Practices

-   Always **wait for popup** when new tab/window opens.\
-   Use `bringToFront()` to activate the desired tab.\
-   Prefer switching by **title or index**, keyboard shortcuts are less
    reliable.\
-   Clean up by closing unused tabs:\

``` java
for (Page p : page.context().pages()) {
    if (!p.title().equals("Main Page")) {
        p.close();
    }
}
```

------------------------------------------------------------------------

✅ With these methods, you can reliably handle **multiple windows/tabs**
in Playwright with Java.
