# Abstraction in Java

## 📌 Definition

Abstraction is an **OOP concept** that **hides the internal implementation details** and **shows only the functionality** to the user.
It allows developers to focus on **what an object does** instead of **how it does it**.

In Java, abstraction can be achieved using:

* **Abstract Classes**
* **Interfaces**

---

## 🔑 Why Abstraction?

* **Simplifies complex systems** by hiding unnecessary details.
* **Focus on essential features** rather than implementation.
* **Code maintainability** → changes in implementation don’t affect users.
* **Supports polymorphism**.

---

## ✅ Key Features

1. **Abstract Classes**: Can have abstract (no body) and non-abstract methods.
2. **Interfaces**: Only method signatures (Java 8+ allows default and static methods).
3. **Hides implementation details** from user.
4. **Supports multiple inheritance** (via interfaces).

---

## 📝 Example: Abstract Class

```java
abstract class Vehicle {
    abstract void start();  // abstract method

    void stop() {           // concrete method
        System.out.println("Vehicle stopped");
    }
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car started");
    }
}

public class AbstractionDemo {
    public static void main(String[] args) {
        Vehicle myCar = new Car();
        myCar.start(); // Car started
        myCar.stop();  // Vehicle stopped
    }
}
```

**Explanation:** Abstract method `start()` is implemented in child class, while `stop()` can be used as is.

---

## 📝 Example: Interface

```java
interface Drawable {
    void draw();  // method signature only
}

class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing Rectangle");
    }
}

public class InterfaceDemo {
    public static void main(String[] args) {
        Drawable c = new Circle();
        Drawable r = new Rectangle();

        c.draw(); // Drawing Circle
        r.draw(); // Drawing Rectangle
    }
}
```

**Explanation:** Users can call `draw()` without knowing implementation details.

---

## 🔹 Real-World Example in Selenium Java Framework

In Selenium Page Object Model, **Abstraction is used in BasePage / Page Objects**.

```java
import org.openqa.selenium.WebDriver;

public abstract class BasePage {
    protected WebDriver driver;

    public BasePage(WebDriver driver) {
        this.driver = driver;
    }

    public abstract void openPage();  // abstract method
}

public class LoginPage extends BasePage {
    public LoginPage(WebDriver driver) {
        super(driver);
    }

    @Override
    public void openPage() {
        driver.get("https://example.com/login");
    }

    public void login(String user, String pass) {
        // enter username/password and click login
    }
}
```

**Explanation:** Test scripts interact with `openPage()` and `login()` without worrying about implementation.

---

## 🔹 Real-World Example in Java Playwright Framework

```java
import com.microsoft.playwright.Page;

public abstract class BasePage {
    protected Page page;

    public BasePage(Page page) {
        this.page = page;
    }

    public abstract void openPage();
}

public class LoginPage extends BasePage {
    public LoginPage(Page page) {
        super(page);
    }

    @Override
    public void openPage() {
        page.navigate("https://example.com/login");
    }

    public void login(String user, String pass) {
        page.locator("#username").fill(user);
        page.locator("#password").fill(pass);
        page.locator("#loginBtn").click();
    }
}
```

**Explanation:** Users can call `openPage()` and `login()` without knowing underlying Playwright code.

---

## ⭐ Advantages of Abstraction

1. Simplifies complex systems by hiding details.
2. Promotes code reusability and maintainability.
3. Enhances security by exposing only necessary functionality.
4. Supports polymorphism and flexible framework design.

---

## 📌 Summary

Abstraction = **Hiding Implementation + Showing Functionality**

* Use **abstract classes** or **interfaces**.
* Users interact with **methods without knowing details**.
* Widely used in **automation frameworks** like Selenium and Playwright for maintainable Page Object Model design.
