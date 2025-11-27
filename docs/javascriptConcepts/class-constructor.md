# JavaScript Classes, Constructors, and Objects

## 📘 What is a Class?

A **class** is a blueprint to create objects.

``` javascript
class Car {
  // Constructor
  constructor(brand, color) {
    this.brand = brand;
    this.color = color;
  }

  start() {
    console.log(`${this.brand} is starting...`);
  }
}
```

------------------------------------------------------------------------

## 🔧 What is a Constructor?

A **constructor** initializes object properties when an object is
created.

------------------------------------------------------------------------

## 🚗 What is an Object?

An **object** is an instance of a class.

``` javascript
const myCar = new Car("BMW", "Black");
myCar.start();
```

------------------------------------------------------------------------

## 🧩 Composition (Using one class inside another)

``` javascript
class Logger {
  log(message) {
    console.log("LOG:", message);
  }
}

class UserService {
  constructor() {
    this.logger = new Logger(); // composition
  }

  createUser(name) {
    this.logger.log(`User created: ${name}`);
  }
}
```

------------------------------------------------------------------------

## 🧬 Inheritance (One class extending another)

``` javascript
class Animal {
  speak() {
    console.log("Animal speaks");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Dog barks");
  }
}

const d = new Dog();
d.speak(); 
d.bark();
```

------------------------------------------------------------------------

## 🎯 Summary Table

  Concept       Meaning                     Example
  ------------- --------------------------- ----------------------------
  Class         Blueprint                   `class Car {}`
  Constructor   Initializes object          `constructor(a,b)`
  Object        Instance of class           `new Car()`
  Composition   Class uses another class    `new Logger()`
  Inheritance   One class extends another   `class Dog extends Animal`
