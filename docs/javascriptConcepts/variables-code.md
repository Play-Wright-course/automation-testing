# JavaScript: var, let, const – Code Snippets with Explanations & Outputs

This file contains detailed explanations for every example to help you understand real-world JavaScript behavior clearly.

---

# 1. var Scope (Function Scoped)

```javascript
function testVarScope() {
  if (true) {
    var x = 10; // var is function-scoped
  }
  console.log("var x =", x); // Accessible here
}
testVarScope();
```

### Explanation
- `var` ignores block scope.
- Even though `x` is declared inside the `if` block, it becomes available throughout the entire function.

### Output
```
var x = 10
```

---

# 2. let Scope (Block Scoped)

```javascript
function testLetScope() {
  if (true) {
    let y = 20; // let is block-scoped
    console.log("Inside block y =", y);
  }
  // console.log(y); // ReferenceError
}
testLetScope();
```

### Explanation
- `let` respects block scope (`{}`).
- `y` is only available inside the `if` block.

### Output
```
Inside block y = 20
```

---

# 3. Hoisting with var

```javascript
console.log(a); // undefined
var a = 5;
```

### Explanation
- `var` is hoisted AND initialized with `undefined` during the memory creation phase.
- This allows accessing it before declaration (but value is undefined).

### Output
```
undefined
```

---

# 4. Hoisting with let (TDZ)

```javascript
// console.log(b); // ReferenceError
let b = 10;
```

### Explanation
- `let` is hoisted but NOT initialized.
- Accessing it before the declaration line results in a **Temporal Dead Zone (TDZ)** error.

---

# 5. Redeclaration Difference

```javascript
var name = "Nitin";
var name = "Patil"; // ✔ allowed

let city = "Pune";
// let city = "Mumbai"; // ❌ SyntaxError
city = "Mumbai"; // ✔ allowed
```

### Explanation
- `var` allows redeclaration in the same scope.
- `let` does not allow redeclaration but does allow reassignment.

### Output
```
var redeclared = Patil
let reassigned = Mumbai
```

---

# 6. Global Behavior (Browser Only)

```javascript
var aVar = 100;
let aLet = 200;

console.log(window.aVar); // 100
console.log(window.aLet); // undefined
```

### Explanation
- Global `var` variables become properties of the global object (`window`).
- Global `let` variables DO NOT attach to `window`.

### Output
```
100
undefined
```

---

# 7. Shadowing (Function Level)

```javascript
var x = 1;

function demo() {
  var x = 2; // shadows global x
  console.log("Inside function x =", x);
}
demo();
console.log("Outside x =", x);
```

### Explanation
- Re-declaring `x` inside the function creates a new variable, shadowing the global one.

### Output
```
Inside function x = 2
Outside x = 1
```

---

# 8. Shadowing with let (Block Level)

```javascript
let num = 10;

{
  let num = 20; // block-level shadowing
  console.log("Inside block =", num);
}

console.log("Outside block =", num);
```

### Explanation
- The inner `let num` shadows the outer variable only inside the block.

### Output
```
Inside block = 20
Outside block = 10
```

---

# 9. const with Mutable Objects

```javascript
const user = { name: "Nitin", city: "Pune" };

user.city = "Mumbai"; // allowed
console.log(user);

// user = {}; // ❌ not allowed
```

### Explanation
- `const` prevents reassignment, **not mutation**.
- You cannot assign a new object, but you can modify properties.

### Output
```
{ name: "Nitin", city: "Mumbai" }
```

---

# 10. for-loop Behavior (var vs let)

## var Example
```javascript
for (var i = 1; i <= 3; i++) {}
console.log("After loop, i =", i);
```

### Explanation
- `var` leaks outside the loop because it is function scoped.

### Output
```
After loop, i = 4
```

---

## let Example
```javascript
for (let j = 1; j <= 3; j++) {}
// console.log(j); // ReferenceError
```

### Explanation
- `let` is block-scoped → not available outside the loop.

---

# 11. Closures: var vs let

## Problem with var
```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(() => console.log("var i =", i), 100);
}
```

### Explanation
- `var i` is shared by all iterations.
- When timeout executes, `i` is already 4.

### Output
```
var i = 4
var i = 4
var i = 4
```

---

## Correct with let
```javascript
for (let i = 1; i <= 3; i++) {
  setTimeout(() => console.log("let i =", i), 100);
}
```

### Explanation
- `let` creates a new `i` for each loop iteration.

### Output
```
let i = 1
let i = 2
let i = 3
```

---

# 12. Temporal Dead Zone (TDZ) Example

```javascript
{
  // console.log(a); // ReferenceError
  let a = 50;
  console.log(a);
}
```

### Explanation
- Accessing `a` before line of declaration causes TDZ error.

### Output
```
50
```

---

# 13. Final Interview-Level Example

```javascript
var v = 1;
let l = 2;
const c = 3;

function show() {
  if (true) {
    var v = 10; // function scoped
    let l = 20; // block scoped
    const c2 = 30;
    console.log(v, l, c2);
  }
  console.log(v);
}
show();
```

### Explanation
- `var v` inside block overrides outer `v` inside function.
- `let l` and `const c2` remain block-scoped.

### Output
```
10 20 30
10
```

---

# End of File
