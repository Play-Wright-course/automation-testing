# Inheritance in Java

## 📌 Definition

Inheritance is an **OOP concept** where one class (**child/subclass**) **inherits properties and methods** from another class (**parent/superclass**).
It allows **code reuse** and **hierarchical class structure**.

**Syntax:**

```java
class Parent {
    // parent class code
}

class Child extends Parent {
    // child class code
}
```

---

## 🔑 Why Inheritance?

* **Reusability**: Write common code in parent, reuse in child.
* **Maintainability**: Changes in parent reflect in child classes.
* **Polymorphism**: Parent reference can refer to child object.
* **Hierarchical structure**: Model real-world relationships.

---

## ✅ Types of Inheritance in Java

1. **Single Inheritance**: One child, one parent
2. **Multilevel Inheritance**: A → B → C
3. **Hierarchical Inheritance**: One parent, multiple children

> Note: Java **does not support multiple inheritance** with classes (can use interfaces for that).

---

## 📝 Basic Example: Single Inheritance

```java
// Parent class
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Child class
class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks.");
    }
}

public class InheritanceDemo {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();  // inherited method
        d.bark(); // child’s own method
    }
}
```

---

## 📝 Example: Multilevel Inheritance

```java
class Vehicle {
    void start() {
        System.out.println("Vehicle starts");
    }
}

class Car extends Vehicle {
    void honk() {
        System.out.println("Car honks");
    }
}

class SportsCar extends Car {
    void turbo() {
        System.out.println("SportsCar turbo mode");
    }
}

public class MultilevelDemo {
    public static void main(String[] args) {
        SportsCar sc = new SportsCar();
        sc.start(); // from Vehicle
        sc.honk();  // from Car
        sc.turbo(); // from SportsCar
    }
}
```

---

## 📝 Example: Hierarchical Inheritance

```java
class Vehicle {
    void start() {
        System.out.println("Vehicle starts");
    }
}

class Car extends Vehicle {
    void honk() {
        System.out.println("Car honks");
    }
}

class Bike extends Vehicle {
    void ringBell() {
        System.out.println("Bike rings bell");
    }
}

public class HierarchicalDemo {
    public static void main(String[] args) {
        Car car = new Car();
        car.start();
        car.honk();

        Bike bike = new Bike();
        bike.start();
        bike.ringBell();
    }
}
```

---

## 🔹 Real-World Example in Selenium Java Framework

In **Page Object Model**, inheritance is used for **BasePage**:

```java
import org.openqa.selenium.WebDriver;

public class BasePage {
    protected WebDriver driver;

    public BasePage(WebDriver driver) {
        this.driver = driver;
    }

    public void openUrl(String url) {
        driver.get(url);
    }
}

// Child Page inherits BasePage
public class LoginPage extends BasePage {
    public LoginPage(WebDriver driver) {
        super(driver); // call parent constructor
    }

    public void login(String user, String pass) {
        // code to perform login
    }
}
```

**Explanation:**

* Common methods like `openUrl()` are in **BasePage** → reused in all pages.
* Child pages inherit these methods → avoids duplicate code.

---

## 🔹 Real-World Example in Java Playwright Framework

```java
import com.microsoft.playwright.Page;

// Base class
public class BasePage {
    protected Page page;

    public BasePage(Page page) {
        this.page = page;
    }

    public void navigateTo(String url) {
        page.navigate(url);
    }
}

// Child Page
public class LoginPage extends BasePage {
    private final String usernameInput = "#username";
    private final String passwordInput = "#password";
    private final String loginBtn = "#loginBtn";

    public LoginPage(Page page) {
        super(page);
    }

    public void login(String user, String pass) {
        page.locator(usernameInput).fill(user);
        page.locator(passwordInput).fill(pass);
        page.locator(loginBtn).click();
    }
}
```

**Explanation:**

* `BasePage` contains common page methods (like `navigateTo()`).
* `LoginPage` inherits them → can reuse in all other page objects.

---

## ⭐ Advantages of Inheritance

1. Code reusability → avoids duplication.
2. Logical structure → parent-child relationship.
3. Easy maintenance → modify in parent, affects all children.
4. Supports **polymorphism** (child object can be referenced by parent type).

---
