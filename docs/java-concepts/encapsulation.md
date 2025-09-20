# Encapsulation in Java

## 💌 Definition

Encapsulation is one of the **four pillars of OOP**.
It means **binding data (fields) and methods (functions) together into a single unit (class)** and **restricting direct access** to the data by making fields `private` and providing controlled access via `public` methods (getters/setters).

---

## 🔑 Why Encapsulation?

If fields are public:

* Anyone can directly access or modify them.
* No control over invalid data.
* Difficult to maintain or change internal representation later.

With encapsulation:

* Data is **hidden** from outside classes.
* Access is **controlled** through methods.
* Validation and business rules can be applied.

---

## ✅ Key Features

1. **Private fields** → data hiding.
2. **Public getters/setters** → controlled access.
3. **Validation** → prevent invalid values.
4. **Read-only / Write-only** → allow only getter or only setter.
5. **Flexibility** → change implementation without breaking outside code.

---

## 📝 Example Without Encapsulation (Problem)

```java
class Student {
    public int age;   // public field
}

public class Demo {
    public static void main(String[] args) {
        Student s = new Student();
        s.age = -10;   // ❌ invalid, but allowed
        System.out.println("Age: " + s.age);
    }
}
```

---

## 📝 Example With Encapsulation (Solution)

```java
class Student {
    private int age;  // private field

    // Setter with validation
    public void setAge(int age) {
        if(age > 0) {
            this.age = age;
        } else {
            System.out.println("❌ Age must be positive!");
        }
    }

    // Getter
    public int getAge() {
        return age;
    }
}

public class Demo {
    public static void main(String[] args) {
        Student s = new Student();
        s.setAge(-10); // blocked
        s.setAge(20);  // ✅ valid
        System.out.println("Age: " + s.getAge());
    }
}
```

---

## 🌟 Real-World Example: Bank Account

```java
class BankAccount {
    private double balance; // sensitive data

    public BankAccount(double initialBalance) {
        if(initialBalance >= 0) {
            this.balance = initialBalance;
        }
    }

    public double getBalance() {
        return balance; // read-only access
    }

    public void deposit(double amount) {
        if(amount > 0) balance += amount;
    }

    public void withdraw(double amount) {
        if(amount > 0 && amount <= balance) balance -= amount;
        else System.out.println("❌ Invalid transaction");
    }
}

public class BankDemo {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount(1000);
        acc.deposit(500);
        acc.withdraw(2000); // ❌ not allowed
        System.out.println("Final Balance: " + acc.getBalance());
    }
}
```

---

## ⭐ Advantages of Encapsulation

* Protects data integrity.
* Improves code maintainability.
* Provides flexibility to change internal implementation.
* Enhances security by exposing only necessary details.
* Supports abstraction (hiding unnecessary details).

---

## 📌 Summary

Encapsulation = **Data Hiding + Controlled Access**

* Keep fields `private`.
* Use **getter** and **setter** methods.
* Apply **validation logic** inside setters.
* Make class fields **read-only/write-only** when required.

---

## 🔹 Encapsulation in Selenium Java Framework

In Selenium frameworks, **Encapsulation is heavily used in Page Object Model (POM):**

### Example: Page Object

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.FindBy;
import org.openqa.selenium.support.PageFactory;

public class LoginPage {
    private WebDriver driver;  // private driver reference

    // Private WebElements
    @FindBy(id = "username")
    private WebElement usernameField;

    @FindBy(id = "password")
    private WebElement passwordField;

    @FindBy(id = "loginBtn")
    private WebElement loginButton;

    // Constructor
    public LoginPage(WebDriver driver) {
        this.driver = driver;
        PageFactory.initElements(driver, this);
    }

    // Public methods (encapsulation) to interact with elements
    public void enterUsername(String username) {
        usernameField.sendKeys(username);
    }

    public void enterPassword(String password) {
        passwordField.sendKeys(password);
    }

    public void clickLogin() {
        loginButton.click();
    }
}
```

**Explanation:**

* Fields (`WebElement`) are private → hidden from test classes.
* Test classes access elements **only via public methods** → controlled interaction.
* Improves maintainability: If locators change, only the Page class changes.

---

## 🔹 Encapsulation in Java Playwright Framework

Similarly, in **Playwright (Java)** framework, encapsulation is used for page objects:

### Example: Login Page

```java
import com.microsoft.playwright.Page;

public class LoginPage {
    private Page page;  // private Playwright page object

    // Private locators
    private final String usernameInput = "#username";
    private final String passwordInput = "#password";
    private final String loginBtn = "#loginBtn";

    // Constructor
    public LoginPage(Page page) {
        this.page = page;
    }

    // Public methods to interact with page
    public void enterUsername(String username) {
        page.locator(usernameInput).fill(username);
    }

    public void enterPassword(String password) {
        page.locator(passwordInput).fill(password);
    }

    public void clickLogin() {
        page.locator(loginBtn).click();
    }
}
```

**Explanation:**

* Locators are private → hidden from test scripts.
* Test scripts call **public methods** → controlled access.
* If locators change, only `LoginPage` needs update.

---

## ✅ Conclusion

Encapsulation in Java is **not just a theory**, it is **widely applied in automation frameworks**:

* Protects element locators and driver/page objects.
* Provides **controlled methods** to interact with UI.
* Improves maintainability, readability, and security of your automation code.
