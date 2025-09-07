# 5. Data Types in JavaScript – Deep Dive

JavaScript has **different types of data** used to store values and perform operations. Understanding data types is crucial for writing efficient code.

This guide covers **primitive types, non-primitive types, type checking, and common interview programs**.

---

## 🔹 Primitive Data Types

Primitive data types are **immutable** and include:

1. **Number** – Numeric values
2. **String** – Sequence of characters
3. **Boolean** – true or false
4. **Undefined** – Variable declared but not assigned
5. **Null** – Intentionally empty value
6. **Symbol** – Unique and immutable value
7. **BigInt** – Large integer values

### Examples

```javascript
// Number
let age = 25;

// String
let name = "Nitin";

// Boolean
let isActive = true;

// Undefined
let city;

// Null
let country = null;

// Symbol
let sym = Symbol('id');

// BigInt
let bigNumber = 123456789012345678901234567890n;
```

### Checking Data Types

```javascript
console.log(typeof age);       // number
console.log(typeof name);      // string
console.log(typeof isActive);  // boolean
console.log(typeof city);      // undefined
console.log(typeof country);   // object (this is a known JS quirk)
console.log(typeof sym);       // symbol
console.log(typeof bigNumber); // bigint
```

---

## 🔹 Non-Primitive Data Types

Non-primitive types are **mutable** and include:

1. **Object** – Key-value pairs
2. **Array** – Ordered collection (special type of object)
3. **Function** – Callable objects

### Examples

```javascript
// Object
let person = { name: "Nitin", age: 25 };

// Array
let fruits = ["apple", "banana", "mango"];

// Function
function greet() {
  console.log("Hello");
}
```

### Checking Data Types

```javascript
console.log(typeof person); // object
console.log(typeof fruits); // object
console.log(typeof greet);  // function
```

---

## 🔹 Type Conversion

JavaScript allows **explicit and implicit type conversions**.

### Implicit Conversion

```javascript
let result = '5' + 5; // '55' (number converted to string)
console.log(result);

let value = '10' - 2; // 8 (string converted to number)
console.log(value);
```

### Explicit Conversion

```javascript
let str = String(123); // '123'
let num = Number('456'); // 456
let bool = Boolean(0);    // false
```

---

## 🔹 Common Interview Programs

### 1. Check if Variable is Array

```javascript
let arr = [1,2,3];
console.log(Array.isArray(arr)); // true
```

### 2. Convert String to Number

```javascript
let str = '123';
let num = Number(str);
console.log(num); // 123
```

### 3. Convert Number to String

```javascript
let num = 456;
let str = String(num);
console.log(str); // '456'
```

### 4. Check Data Type

```javascript
let value = true;
console.log(typeof value); // boolean
```

---

## ✅ Summary

* **Primitive types** → number, string, boolean, undefined, null, symbol, bigint. Immutable.
* **Non-primitive types** → object, array, function. Mutable.
* **Type checking** → `typeof`, `Array.isArray()`.
* **Type conversion** → Implicit (coercion) and explicit (String(), Number(), Boolean()).

Understanding data types is fundamental for **JavaScript development, debugging, and coding interviews**.
