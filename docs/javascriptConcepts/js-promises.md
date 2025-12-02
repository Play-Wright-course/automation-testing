# JavaScript Promises --- Complete Guide (Beginner to Advanced)

This is an extended version with **extra explanations for every code
snippet**, making it easier to understand each concept deeply.

------------------------------------------------------------------------

# 1. What Are Promises?

A **Promise** is a JavaScript object that represents the result of an
asynchronous operation.

Asynchronous operations include: - Loading a webpage\
- Reading a file\
- Waiting for a timer\
- Calling an API\
- Browser actions in Playwright

Because these tasks take time, JavaScript needs a way to continue
running other code while waiting. Promises make this possible.

------------------------------------------------------------------------

# 2. Promise States (With Examples)

### A Promise has **3 states**:

  State                    Meaning
  ------------------------ ---------------------------------------------
  **Pending**              The async task has started but not finished
  **Resolved/Fulfilled**   The task completed successfully
  **Rejected**             The task failed

### Example:

``` js
let p = new Promise((resolve, reject) => {
  // Promise started → pending state
  resolve("Success!");
});
```

### Explanation:

-   When the Promise is created, it is **pending**.
-   After `resolve("Success!")` runs, it becomes **fulfilled**.
-   If `reject("error")` was called, it would become **rejected**.

------------------------------------------------------------------------

# 3. `.then()`, `.catch()`, `.finally()`

### 3.1 `.then()` --- Handle Success

``` js
p.then(result => {
  console.log(result);
});
```

### Explanation:

-   `.then()` runs **only when the Promise resolves**.
-   `result` contains `"Success!"`.

------------------------------------------------------------------------

### 3.2 `.catch()` --- Handle Errors

``` js
p.catch(error => {
  console.log("Error:", error);
});
```

### Explanation:

-   `.catch()` runs when a Promise **rejects**.
-   Example errors: network failure, invalid operation, timeouts.

------------------------------------------------------------------------

### 3.3 `.finally()` --- Always Runs

``` js
p.finally(() => {
  console.log("Task complete!");
});
```

### Explanation:

-   `.finally()` always runs whether resolved or rejected.
-   Useful for cleanup operations: closing browser, clearing cache, etc.

------------------------------------------------------------------------

### Full Example With All Three

``` js
let p = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Loaded!"), 2000);
});

p.then(res => console.log(res))
 .catch(err => console.log(err))
 .finally(() => console.log("Done"));
```

### Explanation:

-   After 2 seconds, Promise resolves with `"Loaded!"`.
-   `.then()` prints the result.
-   `.finally()` prints `"Done"` no matter what.
-   `.catch()` would only run if an error occurred.

------------------------------------------------------------------------

# 4. async/await --- Modern Way of Using Promises

The `async/await` keywords make asynchronous code look like synchronous
code.

### Example:

``` js
async function loadData() {
  try {
    const result = await p;
    console.log(result);
  } catch (err) {
    console.log("Error:", err);
  } finally {
    console.log("Finished");
  }
}
```

### Explanation:

-   `async` tells JavaScript that this function contains asynchronous
    code.
-   `await p` pauses execution until the Promise `p` resolves.
-   `try/catch` gives cleaner error handling than `.then().catch()`.
-   `finally` executes at the end.

------------------------------------------------------------------------

# 5. Promise.all() and Promise.race()

## 5.1 Promise.all()

Runs multiple Promises **in parallel** and waits for all to complete.

``` js
const p1 = new Promise(res => setTimeout(() => res("1 done"), 1000));
const p2 = new Promise(res => setTimeout(() => res("2 done"), 2000));

const result = await Promise.all([p1, p2]);
console.log(result);
```

### Explanation:

-   `p1` resolves in 1 sec.
-   `p2` resolves in 2 sec.
-   `Promise.all()` waits for **both** to finish.
-   Output will be: `["1 done", "2 done"]`.

If any Promise fails, the whole thing fails.

------------------------------------------------------------------------

## 5.2 Promise.race()

Resolves or rejects as soon as **any one** Promise completes.

``` js
const p1 = new Promise(res => setTimeout(() => res("First!"), 1000));
const p2 = new Promise(res => setTimeout(() => res("Second!"), 2000));

const result = await Promise.race([p1, p2]);
console.log(result); // First!
```

### Explanation:

-   `p1` resolves first → result becomes `"First!"`.
-   `p2` is ignored.

Useful when waiting for the fastest response (e.g., backup servers,
timeouts).

------------------------------------------------------------------------

# 6. How Playwright Uses Promises Internally

Playwright interacts with a real browser, and real-world browser actions
take time.

So every Playwright method returns a Promise:

``` js
await page.goto("https://google.com"); 
await page.click("#loginButton");
await page.waitForResponse("**/api/login");
```

### Explanation:

-   `page.goto()` waits for the webpage to load.
-   `page.click()` waits until the click action is complete.
-   `page.waitForResponse()` waits until an API completes.

These operations are asynchronous by nature, so Promises are required.

------------------------------------------------------------------------

# 7. Real Playwright Testing Examples That Use Promises

## 7.1 Clicking + Navigation (Promise.all)

``` js
await Promise.all([
  page.waitForNavigation(),
  page.click("text=Login")
]);
```

### Explanation:

-   Navigation and clicking happen together.
-   Without `Promise.all`, Playwright may miss the navigation event.

------------------------------------------------------------------------

## 7.2 Waiting for API calls

``` js
const [response] = await Promise.all([
  page.waitForResponse(res => res.url().includes("cart")),
  page.click("#addToCart")
]);

console.log(await response.json());
```

### Explanation:

-   Waits for both the button click and the API response.
-   Avoids flakiness due to race conditions.

------------------------------------------------------------------------

## 7.3 Iterating Locators (Each click returns a Promise)

``` js
const items = page.locator(".menu-item");
const count = await items.count();

for (let i = 0; i < count; i++) {
  await items.nth(i).click();
}
```

### Explanation:

-   Each `.click()` is asynchronous.
-   Loop ensures items are clicked in sequence.
-   Without `await`, clicks may happen out of order.

------------------------------------------------------------------------

# 8. Custom Promise Utility

A common use case: waiting for some time in tests.

``` js
function wait(seconds) {
  return new Promise(resolve => {
    setTimeout(() => resolve("Done"), seconds * 1000);
  });
}

await wait(2);
console.log("Finished!");
```

### Explanation:

-   Creates a custom Promise using `setTimeout`.
-   Useful for demo/testing async behavior.
-   (Not recommended for actual Playwright waits --- use built-in
    waits.)

------------------------------------------------------------------------

# 9. Summary Table

  Feature          Description
  ---------------- -----------------------------------
  Promise          Object representing an async task
  Promise States   Pending → Fulfilled → Rejected
  then()           Runs on success
  catch()          Runs on error
  finally()        Always runs
  async/await      Cleaner syntax for promises
  Promise.all()    Wait for multiple tasks
  Promise.race()   Return first completed
  Playwright       All actions return promises

------------------------------------------------------------------------

# 🎉 END OF EXTENDED PROMISES GUIDE

This file now includes **deeper explanations**, **step-by-step logic**,
and **fully commented code** for real-world understanding.
