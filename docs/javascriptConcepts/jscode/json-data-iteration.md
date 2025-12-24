# 📘 Iterating Data from JSON in JavaScript (Complete Guide)

This document explains **how to load, parse, and iterate JSON data** in JavaScript, from **simple JSON** to **complex nested JSON**, including **Playwright usage**.

---

## 📌 1. Loading External JSON File

### Example: `testdata/login.json`
```json
{
  "username": "admin",
  "password": "admin123"
}
```

### Load JSON
```js
const loginData = require('../testdata/login.json');
console.log(loginData.username);
```
---

## 📌 2. Iterating Simple JSON Object
```js
const user = {
  name: "Nitin",
  role: "DevOps",
  experience: 3
};

for (const key in user) {
  console.log(key + " : " + user[key]);
}
```
---

## 📌 3. Iterating JSON Array
```js
const data = { skills: ["Java", "Docker", "Kubernetes"] };

data.skills.forEach(skill => {
  console.log(skill);
});
```
---

## 📌 4. Array of Objects (Common)
```json
{
  "users": [
    { "id": 1, "name": "Amit", "role": "QA" },
    { "id": 2, "name": "Nitin", "role": "DevOps" }
  ]
}
```

```js
usersData.users.forEach(user => {
  console.log(user.name + " - " + user.role);
});
```
---

## 📌 5. Nested JSON Iteration
```js
orderData.order.items.forEach(item => {
  console.log(item.product);
});
```
---

## 📌 6. Safe Iteration
```js
orderData?.order?.items?.forEach(item => {
  console.log(item.product);
});
```
---

## 📌 7. Deep Copy Before Iteration
```js
const data = JSON.parse(JSON.stringify(require('./users.json')));
```
---

## 📌 8. Playwright Example
```js
usersData.users.forEach(user => {
  test(`Login test for ${user.name}`, async ({ page }) => {
    await page.fill('#username', user.name);
  });
});
```
---

## 🔥 Best Practices
- Keep JSON in testdata folder
- Avoid mutating shared JSON
- Use deep clone when needed
- Prefer optional chaining

---

📘 End of Document
