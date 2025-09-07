# 5. Functions in JavaScript – Basics

Functions in JavaScript are **reusable blocks of code** that perform a specific task. They help organize code, reduce repetition, and return values.

This guide covers **how to create functions, call them, pass parameters, return values (int, list/array), and basic usage**.

---

## 🔹 Function Declaration
A standard way to define a named function.

### Syntax
```javascript
function functionName(parameters) {
  // code
  return result;
}
```

### Example – Add two numbers
```javascript
function add(a, b) {
  return a + b;
}

let sum = add(5, 3);
console.log(sum); // 8
```

**Playwright Use Case:** Reusable function to click buttons or fill forms.

---

## 🔹 Function Expression
Assign a function to a variable. Can be anonymous.

### Syntax
```javascript
const functionName = function(parameters) {
  // code
  return result;
};
```

### Example – Multiply two numbers
```javascript
const multiply = function(a, b) {
  return a * b;
};

console.log(multiply(4, 5)); // 20
```

**Note:** You can also create the same function using a **function declaration** as shown below. Both are valid.

### Example – Function Declaration vs Function Expression
```javascript
// Function Declaration
function multiplyDecl(a, b) {
  return a * b;
}
console.log(multiplyDecl(4, 5)); // 20

// Function Expression
const multiplyExpr = function(a, b) {
  return a * b;
};
console.log(multiplyExpr(4, 5)); // 20
```

**Key Difference:**
- Function Declarations are **hoisted** → can be called before definition.
- Function Expressions are **not hoisted** → cannot be called before definition.

---

## 🔹 Function with No Parameters
```javascript
function greet() {
  console.log("Hello!");
}

greet(); // Hello!
```

---

## 🔹 Function Returning Integer
```javascript
function square(x) {
  return x * x;
}

let result = square(6);
console.log(result); // 36
```

---

## 🔹 Function Returning Array/List
```javascript
function createList() {
  return [1, 2, 3, 4, 5];
}

let numbers = createList();
console.log(numbers); // [1, 2, 3, 4, 5]
```

---

## 🔹 Function with Default Parameters
```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}!`);
}

greet("Nitin"); // Hello, Nitin!
greet();         // Hello, Guest!
```

---

## 🔹 Calling a Function
- Use the function name followed by parentheses: `functionName()`
- Pass arguments inside parentheses if needed: `functionName(arg1, arg2)`

### Example
```javascript
function add(a, b) {
  return a + b;
}

let result = add(10, 20);
console.log(result); // 30
```

---

## ✅ Summary
- **Function Declaration:** Named, hoisted, reusable.
- **Function Expression:** Anonymous or named, assigned to a variable.
- **Call a function:** `functionName()`
- **Return values:** Can return integers, arrays, or other data types.
- **Default parameters:** Provide fallback values.
- **Hoisting:** Declarations are hoisted, expressions are not.

Functions are **fundamental building blocks** for organizing and reusing code in JavaScript.
