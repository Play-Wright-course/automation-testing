# JavaScript Variables and Loops – Interview Snippets

This file contains **popular JavaScript code examples** on variables, loops, and array operations commonly asked in interviews. Each snippet includes **explanation** and **output**.

---

## 1️⃣ Variable Hoisting (`var` vs `let`)

```js
console.log(a); // undefined
var a = 10;

console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 20;
```

**Explanation:**

* `var` is **hoisted** and initialized with `undefined`.
* `let` is hoisted but in **Temporal Dead Zone** until declaration.

---

## 2️⃣ Re-declaration and Re-assignment

```js
var x = 5;
var x = 10; // ✅ Allowed
x = 15;     // ✅ Allowed

let y = 20;
// let y = 25; // ❌ Error
y = 30;      // ✅ Allowed

const z = 50;
// z = 60; // ❌ Error
```

**Explanation:**

* `var` allows re-declare + reassign.
* `let` allows reassign only.
* `const` allows neither.

---

## 3️⃣ For Loop Basics

```js
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

**Output:**

```
0
1
2
3
4
```

---

## 4️⃣ Loop Over Array

```js
const arr = [10, 20, 30, 40];

// Using traditional for
for (let i = 0; i < arr.length; i++) console.log(arr[i]);

// Using for...of
for (let value of arr) console.log(value);

// Using forEach
arr.forEach(value => console.log(value));
```

**Output:**

```
10 20 30 40 (3 times for each loop)
```

---

## 5️⃣ Sum of Array Using Loop

```js
const nums = [1, 2, 3, 4, 5];
let sum = 0;

for (let i = 0; i < nums.length; i++) sum += nums[i];

console.log("Sum:", sum);
```

**Output:**

```
Sum: 15
```

---

## 6️⃣ Reverse a String

```js
const str = "Playwright";
let reversed = "";

for (let i = str.length - 1; i >= 0; i--) reversed += str[i];

console.log(reversed);
```

**Output:**

```
thgiryalP
```

---

## 7️⃣ Nested Loops (Multiplication Table)

```js
for (let i = 1; i <= 3; i++) {
    let row = "";
    for (let j = 1; j <= 3; j++) row += i * j + " ";
    console.log(row);
}
```

**Output:**

```
1 2 3
2 4 6
3 6 9
```

---

## 8️⃣ Variable Scope in Loops (`var` vs `let`)

```js
for (var i = 0; i < 3; i++) {}
console.log(i); // 3 ✅ var is function-scoped

for (let j = 0; j < 3; j++) {}
// console.log(j); // ❌ ReferenceError
```

---

## 9️⃣ Filtering Even Numbers Using Loops

```js
const numbers = [1,2,3,4,5,6];
let evens = [];

for (let n of numbers) if (n % 2 === 0) evens.push(n);

console.log(evens);
```

**Output:**

```
[2,4,6]
```

---

## 1️⃣0️⃣ Loop with `break` and `continue`

```js
for (let i = 0; i <= 5; i++) {
    if (i === 3) break;      // Stops loop
    console.log(i);
}

for (let i = 0; i <= 5; i++) {
    if (i === 3) continue;   // Skips current iteration
    console.log(i);
}
```

**Output:**

```
0 1 2
0 1 2 4 5
```

---

## 1️⃣1️⃣ Array Methods – filter(), map(), reduce()

### Filter even numbers

```js
const nums = [1,2,3,4,5];
let evens = nums.filter(n => n % 2 === 0);
console.log(evens); // [2,4]
```

### Sum using reduce

```js
let sum = nums.reduce((acc, val) => acc + val, 0);
console.log(sum); // 15
```

### Square of each number using map

```js
let squares = nums.map(n => n*n);
console.log(squares); // [1,4,9,16,25]
```

---

## 1️⃣2️⃣ Arrow Function vs Traditional Function

```js
// Traditional function
let squares1 = nums.map(function(n) { return n * n; });

// Arrow function
let squares2 = nums.map(n => n * n);

console.log(squares1); // [1,4,9,16,25]
console.log(squares2); // [1,4,9,16,25]
```

---

## 1️⃣3️⃣ Unique Array Elements

```js
let arr = [1,2,2,3,4,4,5];
let unique = arr.filter((n, i, self) => self.indexOf(n) === i);
console.log(unique); // [1,2,3,4,5]
```

---

## 1️⃣4️⃣ Nested Loops – 2D Array Traversal

```js
const matrix = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
];

for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix[i].length; j++)
        console.log(matrix[i][j]);
}
```

---

## 1️⃣5️⃣ Loop with Objects

```js
const users = [
  {name:"Nitin", age:25},
  {name:"Rahul", age:17},
  {name:"Sneha", age:30}
];

for (let user of users) {
    if (user.age >= 18) console.log(user.name);
}
```

**Output:**

```
Nitin
Sneha
```

---

### 🎯 Tips for Interview Preparation

* Know `var` vs `let` vs `const`
* Understand hoisting and scope
* Be comfortable with `for`, `for...of`, `forEach`
* Practice array methods: `filter`, `map`, `reduce`
* Understand arrow functions vs traditional functions
* Solve nested loop and object iteration problems

---

This file covers **all essential variable and loop questions** often asked in JavaScript interviews.
You can use it as a **cheat sheet** for Playwright automation scripts or general JS coding.
