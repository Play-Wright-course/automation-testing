# Playwright -- Handling Dropdowns (Java)

------------------------------------------------------------------------

## 1️⃣ Classic `<select>` Dropdown

**HTML Example:**

``` html
<select id="country">
  <option value="IN">India</option>
  <option value="US">USA</option>
  <option value="UK">UK</option>
</select>
```

### a) Select by Value

``` java
page.locator("#country").selectOption("IN");  
// Select India by value
```

### b) Select by Label (Visible Text)

``` java
page.locator("#country").selectOption(new SelectOption().setLabel("USA"));  
// Select USA by visible text
```

### c) Select by Index

``` java
page.locator("#country").selectOption(new SelectOption().setIndex(2));  
// Select 3rd option (UK) – index starts from 0
```

### d) Select Multiple Values

``` java
page.locator("#country").selectOption(new String[]{"IN", "US"});  
// Select India and USA (multi-select dropdowns only)
```

### e) Iterate All Options & Get Count

``` java
Locator options = page.locator("#country option");
int count = options.count();
System.out.println("Total options in dropdown: " + count);

for (int i = 0; i < count; i++) {
    System.out.println(options.nth(i).innerText());
}
```

-   **Explanation:**
    -   `count()` → total number of options.
    -   `.nth(i).innerText()` → retrieves text of each option.

### f) Example Full Flow

``` java
// Select India by value
page.locator("#country").selectOption("IN");

// Select USA by label
page.locator("#country").selectOption(new SelectOption().setLabel("USA"));

// Select multiple (India & UK)
page.locator("#country").selectOption(new String[]{"IN", "UK"});

// Iterate and print all options
Locator options = page.locator("#country option");
for (int i = 0; i < options.count(); i++) {
    System.out.println(options.nth(i).innerText());
}
```

------------------------------------------------------------------------

## 2️⃣ Auto-suggestion / Custom Dropdown

**HTML Example:**

``` html
<input id="searchCity" type="text" placeholder="Enter city" />
<ul id="cityList">
  <li>New York</li>
  <li>London</li>
  <li>Delhi</li>
</ul>
```

### a) Type to Filter Suggestions

``` java
page.locator("#searchCity").fill("Del");
```

### b) Click on Desired Option

``` java
page.locator("#cityList li", new Locator.LocatorOptions().setHasText("Delhi")).click();
```

### c) Full Auto-suggestion Flow

``` java
// Type in search box
page.locator("#searchCity").fill("Del");

// Wait for suggestion and click
page.locator("#cityList li", new Locator.LocatorOptions().setHasText("Delhi")).click();
```

### d) Iterate All Auto-suggestion Options & Get Count

``` java
Locator cities = page.locator("#cityList li");
int totalCities = cities.count();
System.out.println("Total suggestions: " + totalCities);

for (int i = 0; i < totalCities; i++) {
    System.out.println(cities.nth(i).innerText());
}
```

-   Retrieves all suggestions and their total count.

### e) Tips for Auto-suggestion Dropdowns

-   Use `fill()` instead of `type()` if you want instant input.
-   Use `.locator(...).filter(...).click()` to select the correct
    option.
-   Playwright handles **auto-waiting** automatically.

------------------------------------------------------------------------

## ✅ Summary

-   **Classic `<select>` dropdowns:**
    -   `selectOption("value")` → select by value.
    -   `selectOption(new SelectOption().setLabel("..."))` → select by
        visible text.
    -   `selectOption(new SelectOption().setIndex(i))` → select by
        index.
    -   `selectOption(new String[]{...})` → select multiple values.
    -   Iterate options with `.count()` & `.nth()`.
-   **Auto-suggestion / custom dropdowns:**
    -   Use `fill()` to type, then locate the suggestion and `click()`.
    -   Iterate options with `.count()` & `.nth()`.
-   **Pro tips:**
    -   Playwright auto-waits for dropdowns.
    -   Prefer semantic locators (`getByLabel`, `getByText`) for
        stability.
