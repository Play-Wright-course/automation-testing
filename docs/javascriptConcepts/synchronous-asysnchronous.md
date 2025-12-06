# Playwright — Synchronous or Asynchronous?

## 1. JavaScript Execution Model
JavaScript is single‑threaded and synchronous by default, but supports asynchronous operations such as Promises and `async/await`.

## 2. Playwright Execution Model
Playwright actions (click, goto, fill, wait) are **asynchronous** because each operation returns a Promise.  
We use `await` to make them execute **sequentially**, giving a synchronous feel.

## 3. Diagram — How Async/Await Makes Playwright Look Synchronous

```
┌──────────────────────────────┐
│  Developer Code (sequential) │
└───────────────┬──────────────┘
                │ await
                ▼
        ┌─────────────────┐
        │ Playwright API  │  (async)
        └───────┬─────────┘
                │ Promise
                ▼
        ┌─────────────────┐
        │ Browser Action  │ (click, fill, wait)
        └─────────────────┘
```

### Without await (async chaos)

```
page.click()  ----> Promise starts
page.fill()   ----> Promise starts
page.goto()   ----> Promise starts

(No waiting… operations overlap)
```

### With await (synchronous flow feel)

```
await page.click()  ---- waits until complete
await page.fill()   ---- waits
await page.goto()   ---- waits
```

## 4. Correct Summary Table

| Statement | True? | Explanation |
|----------|-------|-------------|
| JavaScript is synchronous | ✅ | Single-threaded |
| JavaScript supports async | ✅ | Promises, async/await |
| Playwright is synchronous | ❌ | Internally async |
| Playwright looks synchronous | ✅ | Because await forces order |
| Playwright operations are async | ✅ | All APIs return Promises |

## 5. Interview Questions & Answers (3 Years Experience)

### **Q1. Is Playwright synchronous or asynchronous?**
**A:** Playwright is asynchronous under the hood. All operations return Promises. We use `await` to make tests run in sequence.

### **Q2. What happens if you don’t use await in Playwright?**
**A:** Multiple browser operations start simultaneously. This causes race conditions and flaky tests.

### **Q3. Why does Playwright depend on async/await?**
**A:** Browser operations depend on events, network, rendering, and DOM changes that take time. These require asynchronous execution.

### **Q4. What is the difference between Sync-looking code and Async behavior?**
**A:** Sync-looking code is just `await` pausing JavaScript execution. Internally Playwright continues using Promises.

### **Q5. Why does Selenium not require async/await?**
**A:** Selenium uses a WebDriver protocol and blocking HTTP calls. Playwright communicates directly with the browser using async events.

### **Q6. When would Playwright automatically wait?**
**A:** - Before clicks  
- During navigation  
- Waiting for elements to be attached/visible  
- Assertions with retries

### **Q7. Can Playwright execute steps in strict sequence?**
**A:** Yes, using `await`.  
Example:

```js
await page.goto(url);
await page.fill('#username', 'nitin');
await page.click('#submit');
```

### **Q8. How does Playwright handle auto-waiting?**
**A:** Playwright waits for:  
- element to be visible  
- not animating  
- not detached  
- ready to receive events

### **Q9. Why is async required in API testing using Playwright?**
**A:** HTTP calls (`request.get()`, `request.post()`) return Promises. Without async handling, the test cannot read the response.

### **Q10. What are common async issues beginners face?**
- Missing `await`  
- Parallel operations unintentionally  
- Race conditions  
- Tests passing locally but failing in CI  

---

End of file.
