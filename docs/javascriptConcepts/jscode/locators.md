# Playwright Locators -- Complete Guide (JavaScript)

This guide covers **all locator strategies in Playwright (JavaScript)**
and explains *when and why* to use each type.

------------------------------------------------------------------------

## 🔹 Example Base HTML

``` html
<input type="text" id="email" class="form-control" placeholder="Enter email" />

<button id="submitBtn" class="btn btn-primary" type="submit">Submit</button>

<span class="text">Title</span>

<a href="/home">Home</a>
```

------------------------------------------------------------------------

# 🔹 Locator Types (With Context + HTML + JS Example)

## 1️⃣ Locate by **ID**

IDs are unique within a page, making them the most reliable and fastest
selectors.

### 🔸 HTML:

``` html
<input id="email" />
<button id="submitBtn">Submit</button>
```

### 🔸 Playwright:

``` js
page.locator("#email");
page.locator("#submitBtn").click();
```

------------------------------------------------------------------------

## 2️⃣ Locate by **Class**

Class selectors are useful when elements share styling or behavior.

### 🔸 HTML:

``` html
<input class="form-control" />
<button class="btn btn-primary">Save</button>
```

### 🔸 Playwright:

``` js
page.locator(".form-control");
page.locator(".btn.btn-primary").click();
```

------------------------------------------------------------------------

## 3️⃣ Locate by **Tag Name**

Used when selecting elements by their tag type.

### 🔸 HTML:

``` html
<button>Submit</button>
<input type="text" />
```

### 🔸 Playwright:

``` js
page.locator("button");
page.locator("input");
```

------------------------------------------------------------------------

## 4️⃣ Locate by **Text Content**

Useful for selecting elements based on visible text.

### 🔸 HTML:

``` html
<button>Submit</button>
<a>Home</a>
```

### 🔸 Playwright:

``` js
page.getByText("Submit").click();
page.getByText("Home");
```

------------------------------------------------------------------------

## 5️⃣ Locate by **ARIA Role** (Recommended)

This is Playwright's most powerful and stable locator type.

### 🔸 HTML:

``` html
<button type="submit">Submit</button>
<a href="/home">Home</a>
```

### 🔸 Playwright:

``` js
page.getByRole("button", { name: "Submit" }).click();
page.getByRole("link", { name: "Home" });
```

------------------------------------------------------------------------

## 6️⃣ Locate by **Placeholder**

Great for selecting input elements using placeholder text.

### 🔸 HTML:

``` html
<input placeholder="Enter email" />
```

### 🔸 Playwright:

``` js
page.getByPlaceholder("Enter email").fill("abc@test.com");
```

------------------------------------------------------------------------

## 7️⃣ Locate by **Label**

Automatically links `<label>` to its corresponding `<input>`.

### 🔸 HTML:
- It will work onlu when there is association with label field see below example.
- here you can see email is linked between label and input id.
- In some cases input field is wrapped in labes.

``` html
<label for="email">Email</label>
<input id="email" />
```

### 🔸 Playwright:

``` js
page.getByLabel("Email").fill("test@domain.com");
```

------------------------------------------------------------------------

## 8️⃣ Locate by **Alt Text**

Useful for images.

### 🔸 HTML:

``` html
<img src="logo.png" alt="Company Logo">
```

### 🔸 Playwright:

``` js
page.getByAltText("Company Logo");
```

------------------------------------------------------------------------

## 9️⃣ Locate by **Title Attribute**

Handy when elements do not have visible text.

### 🔸 HTML:

``` html
<button title="Click to submit">Submit</button>
```

### 🔸 Playwright:

``` js
page.getByTitle("Click to submit").click();
```

------------------------------------------------------------------------

## 🔟 Locate using **CSS Attribute Selectors**

### 🔸 HTML:

``` html
<input type="text" />
<button type="submit">Save</button>
<a href="/home">Home</a>
```

### 🔸 Playwright:

``` js
page.locator("input[type='text']");
page.locator("button[type='submit']");
page.locator("a[href='/home']");
```

------------------------------------------------------------------------

## 1️⃣1️⃣ Locate using **XPath**

### 🔸 HTML:

``` html
<input id="email" />
<button>Submit</button>
```

### 🔸 Playwright:

``` js
page.locator("//input[@id='email']");
page.locator("//button[text()='Submit']");
```

------------------------------------------------------------------------

# 🔹 Handling Multiple Elements

### 🔸 HTML:

``` html
<ul>
  <li class="item">Apple</li>
  <li class="item">Banana</li>
  <li class="item">Cherry</li>
</ul>
```

### 🔸 Playwright:

``` js
const items = page.locator(".item");
const count = await items.count();

await items.nth(0).innerText();
await items.nth(1).innerText();
await items.nth(2).innerText();

for (let i = 0; i < count; i++) {
  console.log(await items.nth(i).innerText());
}

const banana = page.locator(".item").filter({ hasText: "Banana" });

page.locator(".item").first();
page.locator(".item").last();
```

### 🔸 Snap code:

```js
import { test, expect } from '@playwright/test';
 
test('Playwright Special locators', async ({ page }) => {
  
    await page.goto("https://rahulshettyacademy.com/angularpractice/");
    await page.getByLabel("Check me out if you Love IceCreams!").click();
    await page.getByLabel("Employed").check();
    await page.getByLabel("Gender").selectOption("Female");
    await page.getByPlaceholder("Password").fill("abc123");
    await page.getByRole("button", {name: 'Submit'}).click();
    await page.getByText("Success! The Form has been submitted successfully!.").isVisible();
    await page.getByRole("link",{name : "Shop"}).click();
    await page.locator("app-card").filter({hasText: 'Nokia Edge'}).getByRole("button").click();
 
    //locator(css)
 
});
```

------------------------------------------------------------------------

# 🔹 Summary

-   Prefer semantic locators → `getByRole`, `getByLabel`,
    `getByPlaceholder`
-   Use CSS/XPath only when needed
-   Use `.nth()`, `.first()`, `.last()`, `.filter()` for multi-elements
