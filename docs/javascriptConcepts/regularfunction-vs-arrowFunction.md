# JavaScript Functions: Regular vs Arrow

We will explore the differences between **regular functions** and **arrow functions** using multiple examples.

---

## 1. Basic Syntax

```javascript
// Regular function
function add(a, b) {
  return a + b;
}
console.log(add(2, 3)); // 5

// Arrow function
const addArrow = (a, b) => a + b;
console.log(addArrow(2, 3)); // 5
```

**Key Difference:** Arrow functions are shorter and automatically return a value if there is only one expression.

---

## 2. Single Parameter

```javascript
// Regular function
function square(x) {
  return x * x;
}
console.log(square(5)); // 25

// Arrow function
const squareArrow = x => x * x;
console.log(squareArrow(5)); // 25
```

* Parentheses `()` around a single parameter can be omitted in arrow functions.

---

## 3. Multiple Statements

```javascript
// Regular function
function multiplyAndLog(a, b) {
  console.log("Multiplying", a, b);
  return a * b;
}
console.log(multiplyAndLog(2, 4)); // 8

// Arrow function
const multiplyAndLogArrow = (a, b) => {
  console.log("Multiplying", a, b);
  return a * b;
};
console.log(multiplyAndLogArrow(2, 4)); // 8
```

* Curly braces `{}` are required for multiple statements, and `return` must be used explicitly.

---

## 4. `this` Behavior

```javascript
// Regular function
function PersonRegular() {
  this.age = 0;

  setInterval(function() {
    this.age++; // `this` is undefined or global object
    console.log("Regular:", this.age);
  }, 1000);
}

// Arrow function
function PersonArrow() {
  this.age = 0;

  setInterval(() => {
    this.age++; // `this` refers to the PersonArrow instance
    console.log("Arrow:", this.age);
  }, 1000);
}

// Create instances
// new PersonRegular(); // won't work as expected
// new PersonArrow();   // `this` works correctly
```

**Key Difference:**

* Regular functions have their own `this`.
* Arrow functions inherit `this` from their surrounding context (lexical `this`).

---

## 5. Using with Array Methods

```javascript
const numbers = [1, 2, 3, 4, 5];

// Regular function
const squaredRegular = numbers.map(function(n) {
  return n * n;
});
console.log(squaredRegular); // [1, 4, 9, 16, 25]

// Arrow function
const squaredArrow = numbers.map(n => n * n);
console.log(squaredArrow); // [1, 4, 9, 16, 25]
```

* Arrow functions make array callbacks more concise.

---

## Summary of Differences

| Feature                    | Regular Function  | Arrow Function                          |
| -------------------------- | ----------------- | --------------------------------------- |
| Syntax                     | `function(){}`    | `() => {}`                              |
| `this` binding             | Own `this`        | Lexical `this` (from surrounding)       |
| Arguments object           | Available         | Not available                           |
| Can be used as constructor | Yes               | No                                      |
| Ideal for                  | General functions | Short callbacks, functional programming |

---

Arrow functions are mostly used for **concise code** and **lexical `this`**, while regular functions are still useful when you need `arguments` or constructor behavior.
