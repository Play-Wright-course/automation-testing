# JavaScript Classes & Object-Oriented Concepts  
A GitHub-ready guide covering classes, constructors, object creation, dependency usage, and interview-specific examples.

---

## 📌 Table of Contents
- [Introduction](#introduction)
- [1. Classes & Constructors](#1-classes--constructors)
- [2. Object Creation](#2-object-creation)
- [3. Using One Class Inside Another](#3-using-one-class-inside-another)
  - [Direct Instantiation](#a-direct-instantiation)
  - [Dependency Injection](#b-dependency-injection)
- [4. Interview-Based Examples](#4-interview-based-examples)
  - [Static Methods](#static-methods)
  - [Inheritance](#inheritance)
  - [Private Fields](#private-fields)
  - [Singleton Pattern](#singleton-pattern)
- [Summary](#summary)

---

## Introduction
JavaScript supports Object-Oriented Programming using **classes**, introduced in ES6.  
This guide explains how to create classes, use constructors, create objects, share utilities across classes, and prepare for interviews.

---

## 1. Classes & Constructors

### ✔ Defining a Class
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hello, I am ${this.name}`);
    }
}
```
### ✔ Creating an Object
``` javascript
Copy code
const p1 = new Person("Alice", 25);
p1.greet();
```
### 2. Object Creation
Objects are created using the new keyword:

``` javascript
Copy code
const obj = new ClassName(args);
```
Example:

``` javascript
Copy code
const p = new Person("John", 30);
```
### 3. Using One Class Inside Another

####  A) Direct Instantiation
Most common in utility-based architectures.

``` javascript
Copy code
class Logger {
    log(message) {
        console.log("[LOG]:", message);
    }
}

class UserService {
    constructor() {
        this.logger = new Logger(); // direct object creation
    }

    createUser(username) {
        this.logger.log(`User '${username}' created`);
    }
}

const service = new UserService();
service.createUser("rahul123");
```
####  B) Dependency Injection
Preferred in scalable or testable systems.

``` javascript
class Logger {
    log(message) {
        console.log("[LOG]:", message);
    }
}

class OrderService {
    constructor(logger) {
        this.logger = logger;
    }

    placeOrder(id) {
        this.logger.log(`Order #${id} placed`);
    }
}

const logger = new Logger();
const orderService = new OrderService(logger);
orderService.placeOrder(101);
```

### 4. Interview-Based Examples
⭐ Static Methods

``` javascript
Copy code
class MathUtil {
    static add(a, b) {
        return a + b;
    }
}

console.log(MathUtil.add(5, 7));
```

⭐ Inheritance

``` javascript
Copy code
class Animal {
    constructor(name) {
        this.name = name;
    }

    speak() {
        console.log(`${this.name} makes a sound`);
    }
}

class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks`);
    }
}

const d = new Dog("Tommy");
d.speak();
```

⭐ Private Fields

``` javascript
Copy code
class BankAccount {
    #balance = 0;

    deposit(amount) {
        this.#balance += amount;
    }

    getBalance() {
        return this.#balance;
    }
}

const acc = new BankAccount();
acc.deposit(500);
console.log(acc.getBalance());
```

⭐ Singleton Pattern

``` javascript
Copy code
class Config {
    constructor() {
        if (Config.instance) return Config.instance;
        this.settings = {};
        Config.instance = this;
    }

    set(key, value) {
        this.settings[key] = value;
    }
}

const c1 = new Config();
const c2 = new Config();

console.log(c1 === c2); // true
```

### Summary
- Use classes to structure reusable objects.
- Constructors initialize values.
- Objects can be created directly or injected.
- Understand OOP concepts: inheritance, static methods, encapsulation, and patterns.
- Practice real interview examples like Singleton and private fields.


