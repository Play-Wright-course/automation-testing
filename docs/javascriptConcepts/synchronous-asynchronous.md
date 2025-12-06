# JavaScript Synchronous vs Asynchronous --- Deep Guide with Examples

## 🧩 1. Synchronous JavaScript (Default Behavior)

JavaScript executes code **line by line** and **blocks** until each line
finishes.

### Example 1: Simple Synchronous

``` js
console.log("A");
console.log("B");
console.log("C");
```

**Output**

    A
    B
    C

👉 Execution waits at each line until it completes.

------------------------------------------------------------------------

## 🧩 2. Asynchronous JavaScript

Asynchronous behavior uses **Web APIs**, **Promises**, **setTimeout**,
**fetch**, etc.

### Example 2: setTimeout (Async Task)

``` js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 1000);

console.log("C");
```

**Output**

    A
    C
    B

✔ `setTimeout` runs in background\
✔ JS continues execution\
✔ When timer completes, callback returns via **event loop**

------------------------------------------------------------------------

## 🧩 3. Promises --- Another Async Example

``` js
console.log("Start");

const promise = new Promise((resolve) => {
  setTimeout(() => resolve("Async Result"), 1500);
});

promise.then(result => console.log(result));

console.log("End");
```

**Output**

    Start
    End
    Async Result

📝 `promise.then()` executes later when async completes.

------------------------------------------------------------------------

## 🧩 4. Async/Await --- Cleaner Async Code

``` js
async function fetchData() {
  console.log("Fetching...");
  const data = await new Promise(res => setTimeout(() => res("Done"), 2000));
  console.log(data);
}

fetchData();
console.log("Next Line");
```

**Output**

    Fetching...
    Next Line
    Done

➡️ `await` pauses only inside async function\
➡️ Rest of code continues normally

------------------------------------------------------------------------

## 🧩 5. Real-World Async Example (API Request)

``` js
async function getUser() {
  const response = await fetch("https://jsonplaceholder.typicode.com/users/1");
  const user = await response.json();
  console.log(user.name);
}

console.log("Before API");
getUser();
console.log("After API");
```

**Possible Output**

    Before API
    After API
    Leanne Graham

✔ Fetch runs async\
✔ Doesn't block\
✔ `await` returns only when data is ready

------------------------------------------------------------------------

## 🧩 6. Parallel Async Example using Promise.all

``` js
async function run() {
  const p1 = new Promise(res => setTimeout(() => res("Task 1"), 2000));
  const p2 = new Promise(res => setTimeout(() => res("Task 2"), 1000));

  const results = await Promise.all([p1, p2]);
  console.log(results);
}

run();
```

**Output**

    ["Task 1", "Task 2"]

👉 Executes in parallel, then combines results.

------------------------------------------------------------------------

## 🧩 7. Event Loop Explanation (Simplified)

``` js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

console.log("4");
```

**Output**

    1
    4
    3
    2

Why? - `1` and `4` → synchronous - Promises → go to **microtask queue**
→ run before timeouts - Timeouts → run after microtasks

------------------------------------------------------------------------

## 🧠 Summary Table

  Feature     Synchronous    Asynchronous
  ----------- -------------- -----------------------------
  Execution   Line-by-line   Non-blocking
  Thread      Single         Still single (event loop)
  Example     console.log    setTimeout, fetch, Promises
  Blocking?   Yes            No
  Real-use    Calculations   API calls, DB calls, timers

------------------------------------------------------------------------

## 🔥 Final Summary

> JavaScript **is synchronous by default**, but it becomes
> **asynchronous** through its event loop using Promises, callbacks,
> timers, and async/await.
