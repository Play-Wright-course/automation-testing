# 6. Arrays & Objects in JavaScript – Deep Dive

Arrays and objects are **fundamental data structures** in JavaScript used to store collections of data.

This guide covers **arrays, objects, basic operations, and common interview programs**.

---

## 🔹 Arrays

Arrays store multiple values in an ordered list.

### Creating Arrays

```javascript
let numbers = [1, 2, 3, 4, 5];
let fruits = ["apple", "banana", "mango"];
let mixed = [1, "apple", true, 'c']; // mixed data types

== OR ==
let marks = Array(6);
console.log(marks);   // [ <6 empty items> ]
console.log(marks.length);  // 6

for (let i = 0; i < marks.length; i++) {
  marks[i] = i * 10;
}
console.log(marks); // [0, 10, 20, 30, 40, 50]
```

### Accessing Elements

```javascript
console.log(numbers[0]); // 1
console.log(fruits[2]);  // mango
console.log(mixed[1]);   // apple
```

### Array Length

```javascript
console.log(numbers.length); // 5
```

### Adding Elements

```javascript
numbers.push(6);   // add at end
numbers.unshift(0); // add at beginning
```

### Removing Elements

```javascript
numbers.pop();    // remove last
numbers.shift();  // remove first
```

### Iterating Over an Array

```javascript
let arr = [10, 20, 30, 40];

// Using for loop
for(let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}

// Using for...of loop
for(let value of arr) {
  console.log(value);
}

// Using forEach
arr.forEach(value => console.log(value));
```

---

## 🔹 Common Array Programs (Interview Questions)

### 1. Reverse an Array

```javascript
let arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr); // [5,4,3,2,1]
```

### 2. Find Maximum & Minimum

```javascript
let arr = [5, 12, 7, 1, 19];
let max = Math.max(...arr);
let min = Math.min(...arr);
console.log(max); // 19
console.log(min); // 1
```

### 3. Sum of Array Elements

```javascript
let arr = [1,2,3,4,5];
let sum = arr.reduce((acc, val) => acc + val, 0);
console.log(sum); // 15
```

### 4. Find Average of Array

```javascript
let arr = [10,20,30,40];
let avg = arr.reduce((a,b) => a+b,0)/arr.length;
console.log(avg); // 25
```

### 5. Find Even and Odd Numbers

```javascript
let arr = [1,2,3,4,5,6];
let even = arr.filter(x => x % 2 === 0);
let odd = arr.filter(x => x % 2 !== 0);
console.log(even); // [2,4,6]
console.log(odd);  // [1,3,5]
```

### 6. Sort Array

```javascript
let arr = [5,1,8,3];
arr.sort((a,b) => a-b);
console.log(arr); // [1,3,5,8]
```

### 7. Find String with Max and Min Length

```javascript
let fruits = ["apple", "banana", "kiwi", "mango"];
let maxLen = fruits.reduce((a,b) => a.length >= b.length ? a : b);
let minLen = fruits.reduce((a,b) => a.length <= b.length ? a : b);
console.log(maxLen); // banana
console.log(minLen); // kiwi
```

---

## 🔹 Objects

Objects store data in **key-value pairs**.

### Creating Objects

```javascript
let person = {
  name: "Nitin",
  age: 25,
  city: "Mumbai"
};
```

### Accessing Properties

```javascript
console.log(person.name);  // Nitin
console.log(person['age']); // 25
```

### Adding & Updating Properties

```javascript
person.country = "India"; // add
person.age = 26;            // update
```

### Deleting Properties

```javascript
delete person.city;
```

### Iterating Over Object

```javascript
for (let key in person) {
  console.log(key, person[key]);
}
```

---

## ✅ Summary

* **Arrays** → Ordered collection of items, methods: push, pop, shift, unshift, reverse, sort, filter, reduce. Can contain **mixed data types**.
* **Objects** → Key-value storage, access via dot or bracket notation, dynamic addition/deletion, iteration with `for...in`.
* **Common Interview Programs** → Reverse array, max/min, sum, average, even/odd numbers, string with max/min length.
* **Iteration** → for loop, for...of loop, forEach method.

These are essential for **coding interviews, JavaScript development, and Playwright automation**.
