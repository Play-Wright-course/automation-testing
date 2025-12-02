# 🚀 JavaScript Promises — From Simple to Real-Time Complex Examples  
### With Playwright-Like Use Cases + Console Outputs

This guide takes you from **simple → intermediate → real-time complex** Promise usage so you understand how Promises actually help in real testing or backend flows.

---

# 1️⃣ Simple Promise (Basic Understanding)

```javascript
const simpleTask = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Simple Task Done!");
  }, 1000);
});

simpleTask.then((msg) => console.log("Output:", msg));
```

✅ Output
```
arduino
Copy code
Output: Simple Task Done!
```

# 2️⃣ Intermediate Example — Multiple Promises (Promise Chaining)

```
function step1() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Step 1 completed"), 1000);
  });
}

function step2() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Step 2 completed"), 1000);
  });
}

function step3() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Step 3 completed"), 1000);
  });
}

step1()
  .then((res1) => {
    console.log(res1);
    return step2();
  })
  .then((res2) => {
    console.log(res2);
    return step3();
  })
  .then((res3) => console.log(res3));
```

✅ Output

```
Copy code
Step 1 completed
Step 2 completed
Step 3 completed
```

# 3️⃣ Real-Time Example — Calling API With Promises
(Useful for Playwright API testing)

```
javascript
Copy code
function getUserData() {
  return fetch("https://jsonplaceholder.typicode.com/users/1")
    .then(response => response.json());
}

getUserData().then((data) => {
  console.log("User Name:", data.name);
});
```

✅ Output
```
Copy code
User Name: Leanne Graham
```

# 4️⃣ Complex Example — Run Tasks in Parallel
(Real-Time Use Case: Fetch multiple APIs or run multiple operations simultaneously)

```
const fetchUser = () =>
  new Promise((resolve) => {
    setTimeout(() => resolve("User Fetched"), 1500);
  });

const fetchOrders = () =>
  new Promise((resolve) => {
    setTimeout(() => resolve("Orders Fetched"), 1000);
  });

const fetchPayments = () =>
  new Promise((resolve) => {
    setTimeout(() => resolve("Payments Fetched"), 2000);
  });

Promise.all([fetchUser(), fetchOrders(), fetchPayments()])
  .then((results) => {
    console.log("All tasks completed:");
    console.log(results);
  });
```

✅ Output
```
All tasks completed:
[ 'User Fetched', 'Orders Fetched', 'Payments Fetched' ]
```

# 5️⃣ Complex Example — Promise.race()
```
const fast = new Promise((resolve) => setTimeout(() => resolve("Fast API"), 500));
const slow = new Promise((resolve) => setTimeout(() => resolve("Slow API"), 2000));

Promise.race([fast, slow]).then((result) => console.log("Winner:", result));
```

✅ Output

```
Winner: Fast API
```
# 6️⃣ Complex Example — Retry Mechanism With Promises
(Real-Time: Retry API/network calls)

```
function fetchWithRetry(retries = 3) {
  return new Promise((resolve, reject) => {
    const success = Math.random() > 0.5; // Random fail/success

    console.log("Trying API…");

    if (success) {
      resolve("API Success!");
    } else if (retries > 0) {
      console.log("Retrying…");
      return resolve(fetchWithRetry(retries - 1));
    } else {
      reject("API Failed after retries");
    }
  });
}

fetchWithRetry()
  .then((res) => console.log(res))
  .catch((err) => console.log(err));
```

Possible Output
```
mathematica
Copy code
Trying API…
Retrying…
Trying API…
Retrying…
Trying API…
API Success!
```
OR
```
nginx
Copy code
Trying API…
Retrying…
Trying API…
Retrying…
Trying API…
API Failed after retries
```
# 7️⃣ Real-Time Playwright-Style Example — Custom Wait Using Promises
```
function waitForElement(selector) {
  return new Promise((resolve) => {
    const check = setInterval(() => {
      const el = document.querySelector(selector);
      if (el) {
        clearInterval(check);
        resolve("Element found: " + selector);
      }
    }, 200);
  });
}

waitForElement("#login-button").then((msg) => console.log(msg));
```
Example Output
```
Element found: #login-button
```

# 8️⃣ Real-Time Example — Playwright Test Simulated With Promises
```
function navigateTo(url) {
  return new Promise((resolve) => {
    console.log("Navigating to:", url);
    setTimeout(() => resolve("Page Loaded"), 1000);
  });
}

function clickButton() {
  return new Promise((resolve) => {
    console.log("Clicking Login Button");
    setTimeout(() => resolve("Button Clicked"), 500);
  });
}

function validateHomePage() {
  return new Promise((resolve) => {
    console.log("Validating Home Page");
    setTimeout(() => resolve("Home Page Validated"), 800);
  });
}

async function runTest() {
  const pageLoad = await navigateTo("https://example.com");
  console.log(pageLoad);

  const click = await clickButton();
  console.log(click);

  const validate = await validateHomePage();
  console.log(validate);

  console.log("Test Completed");
}

runTest();
```

Output

```
Navigating to: https://example.com
Page Loaded
Clicking Login Button
Button Clicked
Validating Home Page
Home Page Validated
Test Completed
```
