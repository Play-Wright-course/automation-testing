
# 3. Operators in JavaScript – Deep Dive

JavaScript provides a variety of operators to perform operations on values and variables.  
Operators can be categorized as **Arithmetic, Assignment, Comparison, Logical, Bitwise, and Ternary**.  

---

## 🔹 Arithmetic Operators
Used to perform mathematical operations.

| Operator | Description |
|----------|-------------|
| `+`      | Addition |
| `-`      | Subtraction |
| `*`      | Multiplication |
| `/`      | Division |
| `%`      | Modulus (remainder) |
| `**`     | Exponentiation |
| `++`     | Increment |
| `--`     | Decrement |

### Examples – Arithmetic
```javascript
let a = 10;
let b = 3;

console.log(a + b);  // 13
console.log(a - b);  // 7
console.log(a * b);  // 30
console.log(a / b);  // 3.3333
console.log(a % b);  // 1
console.log(a ** 2); // 100

a++;
console.log(a);      // 11
b--;
console.log(b);      // 2



```

**Playwright Use Case:** Calculating dynamic index for lists of elements or iterations.

---

## 🔹 Assignment Operators
Used to assign values to variables.

| Operator | Description |
|----------|-------------|
| `=`      | Assign |
| `+=`     | Add and assign |
| `-=`     | Subtract and assign |
| `*=`     | Multiply and assign |
| `/=`     | Divide and assign |
| `%=`     | Modulus and assign |

### Examples – Assignment
```javascript

let x;

// Assignment (=)
x = 10;
console.log(x); // 10

// Add and assign (+=)
x += 5;          // x = x + 5
console.log(x);  // 15

// Subtract and assign (-=)
x -= 3;          // x = x - 3
console.log(x);  // 12

// Multiply and assign (*=)
x *= 2;          // x = x * 2
console.log(x);  // 24

// Divide and assign (/=)
x /= 4;          // x = x / 4
console.log(x);  // 6

// Modulus and assign (%=)
x %= 5;          // x = x % 5
console.log(x);  // 1

// Exponentiate and assign (**=)
x **= 3;         // x = x ** 3
console.log(x);  // 1

// Bitwise AND and assign (&=)
x = 5;
x &= 3;          // x = x & 3
console.log(x);  // 1

// Bitwise OR and assign (|=)
x |= 2;          // x = x | 2
console.log(x);  // 3

// Bitwise XOR and assign (^=)
x ^= 1;          // x = x ^ 1
console.log(x);  // 2

// Left shift and assign (<<=)
x <<= 2;         // x = x << 2
console.log(x);  // 8

// Right shift and assign (>>=)
x >>= 1;         // x = x >> 1
console.log(x);  // 4

// Unsigned right shift and assign (>>>=)
x >>>= 1;        // x = x >>> 1
console.log(x);  // 2
```

---

## 🔹 Comparison Operators
Used to compare values, return `true` or `false`.

| Operator | Description |
|----------|-------------|
| `==`     | Equal (value only) |
| `===`    | Strict equal (value + type) |
| `!=`     | Not equal |
| `!==`    | Strict not equal |
| `>`      | Greater than |
| `<`      | Less than |
| `>=`     | Greater or equal |
| `<=`     | Less or equal |

### Examples – Comparison
```javascript
let a = 5;
let b = "5";

console.log(a == b);  // true (value equal)
console.log(a === b); // false (type mismatch)
console.log(a != b);  // false
console.log(a !== b); // true
console.log(a > 3);   // true
console.log(a <= 5);  // true
```

**Playwright Use Case:** Assertions for element counts, text lengths, or response values.

---

## 🔹 Logical Operators
Used to combine boolean expressions.

| Operator | Description |
|----------|-------------|
| `&&`     | AND |
| `||`     | OR |
| `!`      | NOT |

### Examples – Logical
```javascript
let isLoggedIn = true;
let hasAccess = false;

console.log(isLoggedIn && hasAccess); // false
console.log(isLoggedIn || hasAccess); // true
console.log(!isLoggedIn);             // false
```

**Playwright Use Case:** Conditional checks before clicking or filling fields.

---

## 🔹 Ternary Operator
A shorthand for `if...else` statements.

### Syntax
```javascript
condition ? expression_if_true : expression_if_false;
```

### Examples – Ternary
```javascript
let age = 18;
let message = age >= 18 ? "Adult" : "Minor";
console.log(message); // "Adult"
```

**Playwright Use Case:** Quick decision-making for optional actions, like filling optional forms.

---

## 🔹 Bitwise Operators
Operate on binary representations of numbers. Rarely used in Playwright but good to know.

| Operator | Description |
|----------|-------------|
| `&`      | AND |
| `|`      | OR |
| `^`      | XOR |
| `~`      | NOT |
| `<<`     | Left shift |
| `>>`     | Right shift |
| `>>>`    | Zero-fill right shift |

### Examples – Bitwise
```javascript
let a = 5;  // 0101
let b = 3;  // 0011

console.log(a & b); // 1  (0001)
console.log(a | b); // 7  (0111)
console.log(a ^ b); // 6  (0110)
console.log(~a);    // -6
```

---

## ✅ Summary
- **Arithmetic** → `+`, `-`, `*`, `/`, `%`, `++`, `--`, `**`  
- **Assignment** → `=`, `+=`, `-=`, `*=`, `/=`, `%=`  
- **Comparison** → `==`, `===`, `!=`, `!==`, `>`, `<`, `>=`, `<=`  
- **Logical** → `&&`, `||`, `!`  
- **Ternary** → `condition ? expr1 : expr2`  
- **Bitwise** → `&`, `|`, `^`, `~`, `<<`, `>>`, `>>>`  

These operators are essential for **calculations, validations, and conditional logic** in Playwright tests.
