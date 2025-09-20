# Polymorphism in Java

## 📌 Definition

Polymorphism is an **OOP concept** that means **“one name, many forms”**.
It allows **a single method, object, or operator to behave differently** based on context.

**Types:**

1. Compile-Time (Method Overloading)
2. Run-Time (Method Overriding)

---

## 🔑 Why Polymorphism?

* Improves **code readability**.
* Reduces **complexity** by using the same method name for different tasks.
* Supports **flexibility** in code design.
* Helps in **maintainable and reusable code**.

---

## ✅ Types of Polymorphism

### 1. Compile-Time Polymorphism (Method Overloading)

* Same method name but **different parameter types or number**.
* Resolved by **compiler**.

**Example:**

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}

public class OverloadingDemo {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 3));       // int version
        System.out.println(calc.add(2.5, 3.5));   // double version
        System.out.println(calc.add(1, 2, 3));    // 3 params
    }
}
```

---

### 2. Run-Time Polymorphism (Method Overriding)

* Child class **overrides parent method** with same name & signature.
* Decided by **JVM at runtime** which method to call.

**Example:**

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound.");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks.");
    }
}

public class OverridingDemo {
    public static void main(String[] args) {
        Animal obj = new Dog();  // Parent reference, child object
        obj.sound();             // Runtime decides -> Dog barks.
    }
}
```

---

## 🔹 Complex Example: Polymorphism in Banking

```java
abstract class Account {
    abstract void calculateInterest();
}

class SavingsAccount extends Account {
    @Override
    void calculateInterest() {
        System.out.println("Savings Account interest: 4%");
    }
}

class FixedDepositAccount extends Account {
    @Override
    void calculateInterest() {
        System.out.println("Fixed Deposit interest: 6%");
    }
}

public class BankDemo {
    public static void main(String[] args) {
        Account acc1 = new SavingsAccount();
        Account acc2 = new FixedDepositAccount();

        acc1.calculateInterest();  // Savings Account interest: 4%
        acc2.calculateInterest();  // Fixed Deposit interest: 6%
    }
}
```

**Explanation:** Same method `calculateInterest()` behaves differently → **runtime polymorphism**.

---

## 🔹 Polymorphism in Selenium Java Framework

```java
import org.openqa.selenium.WebDriver;

public class BasePage {
    protected WebDriver driver;

    public BasePage(WebDriver driver) {
        this.driver = driver;
    }

    // Overloaded method example
    public void openUrl(String url) {
        driver.get(url);
    }

    public void openUrl(String url, boolean maximize) {
        driver.get(url);
        if(maximize) driver.manage().window().maximize();
    }
}
```

**Explanation:**

* `openUrl()` is **overloaded** → compile-time polymorphism.
* All pages inherit BasePage → runtime polymorphism when child overrides methods.

---

## 🔹 Polymorphism in Java Playwright Framework

```java
import com.microsoft.playwright.Page;

public class BasePage {
    protected Page page;

    public BasePage(Page page) {
        this.page = page;
    }

    // Compile-time polymorphism
    public void navigate(String url) {
        page.navigate(url);
    }

    public void navigate(String url, int timeout) {
        page.navigate(url, new Page.NavigateOptions().setTimeout(timeout));
    }
}

public class LoginPage extends BasePage {
    public LoginPage(Page page) {
        super(page);
    }

    // Runtime polymorphism
    @Override
    public void navigate(String url) {
        System.out.println("LoginPage custom navigate");
        super.navigate(url);
    }
}
```

**Explanation:**

* Overloaded `navigate()` → compile-time polymorphism.
* Overridden `navigate()` → runtime polymorphism.

---

## ⭐ Advantages of Polymorphism

1. Improves **code readability**.
2. Promotes **reusability**.
3. Reduces **complex code** with common methods.
4. Supports **flexible and maintainable automation frameworks**.
