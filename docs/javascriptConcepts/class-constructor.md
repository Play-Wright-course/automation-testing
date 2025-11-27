📘 JavaScript Classes, Constructors, Objects & Using One Class in Another

A complete beginner-friendly guide with examples

1️⃣ What is a Class in JavaScript?

A class is a blueprint for creating objects.
It groups data (properties) and behaviors (methods).

class Car {
  // constructor is like the "setup" function for each object
  constructor(brand, color) {
    this.brand = brand;
    this.color = color;
  }

  displayInfo() {
    console.log(`Brand: ${this.brand}, Color: ${this.color}`);
  }
}

2️⃣ What is a Constructor?

The constructor is a special method inside a class that runs automatically when an object is created.

constructor(brand, color) {
  this.brand = brand;
  this.color = color;
}


✔ this.brand → property saved inside the object
✔ Values passed while creating object → become class properties

3️⃣ Creating an Object from a Class
const myCar = new Car("Toyota", "Red");
myCar.displayInfo();


Output:

Brand: Toyota, Color: Red

4️⃣ Adding More Methods
class Car {
  constructor(brand, color, price) {
    this.brand = brand;
    this.color = color;
    this.price = price;
  }

  start() {
    console.log(`${this.brand} is starting...`);
  }

  getPrice() {
    return this.price;
  }
}

const tesla = new Car("Tesla", "Blue", 50000);
tesla.start();
console.log(tesla.getPrice());

5️⃣ Calling One Class From Another

You will use this concept in Page Object Model, Playwright utilities, helper classes, etc.

There are 3 common ways:

✅ A) Use class instance inside another class (Composition)

Most common in Playwright

utils/logger.js
class Logger {
  log(message) {
    console.log(`[LOG]: ${message}`);
  }
}

module.exports = Logger;

pages/LoginPage.js
const Logger = require('../utils/logger');

class LoginPage {
  constructor(page) {
    this.page = page;
    this.logger = new Logger(); // using Logger class
  }

  async login(username, password) {
    this.logger.log("Trying to log in...");
    await this.page.fill("#user", username);
    await this.page.fill("#pass", password);
    await this.page.click("#loginBtn");
  }
}

module.exports = LoginPage;

test.js
const LoginPage = require('./pages/LoginPage');

const loginPage = new LoginPage(page);
await loginPage.login("admin", "admin123");


✔ This is how utilities are used in real-world automation.
✔ Easy to reuse utility classes.

✅ B) Import methods from another class using ES6 Modules
mathUtils.js
export class MathUtils {
  add(a, b) {
    return a + b;
  }
}

app.js
import { MathUtils } from "./mathUtils.js";

const utils = new MathUtils();
console.log(utils.add(5, 10));

✅ C) Inheritance (extends)

One class reuses properties/methods of another class.

class Animal {
  speak() {
    console.log("Animal makes sound");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Dog barks");
  }
}

const d = new Dog();
d.speak(); // from parent class
d.bark();  // from child class


✔ Useful when classes share common logic
✔ Common in frameworks with BasePage, BaseAPI, etc.

6️⃣ Real-World Automation Example
BasePage.js
class BasePage {
  constructor(page) {
    this.page = page;
  }

  async waitForPageLoad() {
    await this.page.waitForLoadState("domcontentloaded");
  }
}

module.exports = BasePage;

HomePage.js
const BasePage = require("./BasePage");

class HomePage extends BasePage {
  constructor(page) {
    super(page); // calling parent constructor
  }

  async clickMenu() {
    await this.page.click("#menu");
  }
}

module.exports = HomePage;


✔ HomePage inherits BasePage
✔ This is super common in Playwright

🎯 Summary
| Concept      | Meaning                        | Example                      |
|--------------|--------------------------------|-------------------------------|
| **Class**    | Blueprint for creating objects | `class Car {}`               |
| **Constructor** | Initializes object properties | `constructor(a, b)`          |
| **Object**   | Instance of a class            | `new Car()`                  |
| **Composition** | One class uses another class (HAS-A) | `new Logger()`           |
| **Inheritance** | One class extends another (IS-A) | `class Dog extends Animal` |
