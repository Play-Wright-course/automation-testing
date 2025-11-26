# JavaScript Objects — Complete Guide

## 1. What is an Object?

An object in JavaScript is a collection of key-value pairs.
Objects are used to store structured data.

```js
const person = {
  name: "Nitin",
  age: 25,
  city: "Pune"
};
```

* Keys are also called **properties**
* Values can be **string, number, boolean, array, function, or another object**

---

## 2. Nested Objects

Objects can have other objects as values (nested objects).

```js
const person = {
  name: "Nitin",
  age: 25,
  city: "Pune",
  address: {
    street: "MG Road",
    zip: 411001,
    state: "Maharashtra"
  }
};
```

### Accessing Nested Properties

```js
console.log(person.address.street);  // MG Road
console.log(person["address"]["zip"]); // 411001
```

---

## 3. Adding Functions in Objects

Objects can have methods (functions as values):

```js
const person = {
  name: "Nitin",
  greet: function() {
    console.log("Hello, " + this.name);
  },
  greetES6() {
    console.log(`Hello, ${this.name}`);
  }
};

person.greet();   // Hello, Nitin
person.greetES6(); // Hello, Nitin
```

---

## 4. Adding, Updating, and Deleting Properties

### Add New Property

```js
person.country = "India";
person["language"] = "English";
```

### Update Existing Property

```js
person.age = 26;
```

### Delete Property

```js
delete person.city;
```

---

## 5. Checking if Property Exists

```js
"name" in person;               // true
person.hasOwnProperty("city");  // false (if deleted above)
```

---

## 6. Iterating Over Object Properties

### Using for...in loop

```js
for (let key in person) {
  console.log(key, person[key]);
}
```

### Using Object Methods

```js
// Keys
Object.keys(person); // ["name", "age", "country", "language", "greet", "greetES6"]

// Values
Object.values(person); // ["Nitin", 26, "India", "English", f, f]

// Entries
Object.entries(person);
/*
[
  ["name","Nitin"],
  ["age",26],
  ["country","India"],
  ["language","English"],
  ["greet", f],
  ["greetES6", f]
]
*/
```

---

## 7. Nested Objects and Arrays

```js
const person = {
  name: "Nitin",
  hobbies: ["reading", "coding", "travelling"],
  address: {
    city: "Pune",
    history: [
      { year: 2019, city: "Nagpur" },
      { year: 2020, city: "Delhi" }
    ]
  }
};

console.log(person.hobbies[1]);             // coding
console.log(person.address.history[1].city); // Delhi
```

---

## 8. Summary Table

| Operation             | Syntax                                | Example                                              |
| --------------------- | ------------------------------------- | ---------------------------------------------------- |
| Create simple object  | `const obj = { key: value }`          | `{ name: "Nitin", age: 25 }`                         |
| Create nested object  | `obj = { key: { nestedKey: value } }` | `{ address: { city: "Pune" } }`                      |
| Add property          | `obj.newKey = value`                  | `person.country = "India"`                           |
| Update property       | `obj.key = newValue`                  | `person.age = 26`                                    |
| Delete property       | `delete obj.key`                      | `delete person.city`                                 |
| Add function (method) | `obj.method = function(){}`           | `person.greet = function(){}`                        |
| Access property       | `obj.key` or `obj["key"]`             | `person.name`                                        |
| Loop through object   | `for...in`                            | `for(let k in person){ console.log(k, person[k]); }` |
| Get keys              | `Object.keys(obj)`                    | `Object.keys(person)`                                |
| Get values            | `Object.values(obj)`                  | `Object.values(person)`                              |
| Get entries           | `Object.entries(obj)`                 | `Object.entries(person)`                             |

---

# End of JavaScript Objects Guide
