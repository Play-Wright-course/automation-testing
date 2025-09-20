# OOP Concepts Java – Examples 21-50

### Example 21 – Encapsulation

```java
class Account {
    private double balance = 5000;
    public void deposit(double amount) {
        balance += amount;
    }
    public void withdraw(double amount) {
        balance -= amount;
    }
    public double getBalance() {
        return balance;
    }
}

public class Test {
    public static void main(String[] args) {
        Account acc = new Account();
        acc.deposit(1000);
        acc.withdraw(2000);
        System.out.println(acc.getBalance());
    }
}
```

**Question:** Output?

---

### Example 22 – Encapsulation with Validation

```java
class Temperature {
    private double tempCelsius;
    public void setTempCelsius(double tempCelsius) {
        this.tempCelsius = tempCelsius < -273 ? -273 : tempCelsius;
    }
    public double getTempCelsius() {
        return tempCelsius;
    }
}

public class Test {
    public static void main(String[] args) {
        Temperature t = new Temperature();
        t.setTempCelsius(-300);
        System.out.println(t.getTempCelsius());
    }
}
```

**Question:** Output?

---

### Example 23 – Inheritance + Multi-Level

```java
class Animal {
    void eat() {
        System.out.println("Animal eats");
    }
}

class Mammal extends Animal {
    void walk() {
        System.out.println("Mammal walks");
    }
}

class Dog extends Mammal {
    void bark() {
        System.out.println("Dog barks");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();
        d.walk();
        d.bark();
    }
}
```

**Question:** Output?

---

### Example 24 – Inheritance + Constructor Chaining

```java
class A {
    A() { System.out.println("A Constructor"); }
}

class B extends A {
    B() { System.out.println("B Constructor"); }
}

class C extends B {
    C() { System.out.println("C Constructor"); }
}

public class Test {
    public static void main(String[] args) {
        C obj = new C();
    }
}
```

**Question:** Output?

---

### Example 25 – Polymorphism (Overriding)

```java
class Printer {
    void print() {
        System.out.println("Printing from base printer");
    }
}

class ColorPrinter extends Printer {
    void print() {
        System.out.println("Printing in color");
    }
}

public class Test {
    public static void main(String[] args) {
        Printer p = new ColorPrinter();
        p.print();
    }
}
```

**Question:** Output?

---

### Example 26 – Polymorphism + Super Keyword

```java
class Vehicle {
    void start() {
        System.out.println("Vehicle starts");
    }
}

class Car extends Vehicle {
    void start() {
        super.start();
        System.out.println("Car starts");
    }
}

public class Test {
    public static void main(String[] args) {
        Car c = new Car();
        c.start();
    }
}
```

**Question:** Output?

---

### Example 27 – Abstraction

```java
abstract class Instrument {
    abstract void play();
}

class Guitar extends Instrument {
    void play() {
        System.out.println("Guitar is playing");
    }
}

public class Test {
    public static void main(String[] args) {
        Instrument ins = new Guitar();
        ins.play();
    }
}
```

**Question:** Output?

---

### Example 28 – Abstraction + Polymorphism

```java
abstract class Employee {
    abstract double getSalary();
}

class Developer extends Employee {
    double getSalary() {
        return 70000;
    }
}

class Tester extends Employee {
    double getSalary() {
        return 50000;
    }
}

public class Test {
    public static void main(String[] args) {
        Employee e1 = new Developer();
        Employee e2 = new Tester();
        System.out.println(e1.getSalary());
        System.out.println(e2.getSalary());
    }
}
```

**Question:** Output?

---

### Example 29 – Encapsulation + Multiple Objects

```java
class Counter {
    private int count = 0;
    public void increment() {
        count++;
    }
    public int getCount() {
        return count;
    }
}

public class Test {
    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        c1.increment();
        c1.increment();
        c2.increment();
        System.out.println(c1.getCount());
        System.out.println(c2.getCount());
    }
}
```

**Question:** Output?

---

### Example 30 – Inheritance + Method Hiding

```java
class A {
    static void msg() {
        System.out.println("A");
    }
}

class B extends A {
    static void msg() {
        System.out.println("B");
    }
}

public class Test {
    public static void main(String[] args) {
        A a = new B();
        a.msg();
    }
}
```

**Question:** Output?

---

### Example 31 – Polymorphism (Overloading)

```java
class Calculator {
    int multiply(int a, int b) {
        return a * b;
    }
    double multiply(double a, double b) {
        return a * b;
    }
}

public class Test {
    public static void main(String[] args) {
        Calculator c = new Calculator();
        System.out.println(c.multiply(5, 4));
        System.out.println(c.multiply(2.5, 3.0));
    }
}
```

**Question:** Output?

---

### Example 32 – Interface Implementation

```java
interface Shape {
    void draw();
}

class Triangle implements Shape {
    public void draw() {
        System.out.println("Triangle drawn");
    }
}

class Square implements Shape {
    public void draw() {
        System.out.println("Square drawn");
    }
}

public class Test {
    public static void main(String[] args) {
        Shape s1 = new Triangle();
        Shape s2 = new Square();
        s1.draw();
        s2.draw();
    }
}
```

**Question:** Output?

---

### Example 33 – Inheritance + Multiple Child

```java
class Parent {
    void show() {
        System.out.println("Parent method");
    }
}

class Child1 extends Parent {
    void show() {
        System.out.println("Child1 method");
    }
}

class Child2 extends Parent {
    void show() {
        System.out.println("Child2 method");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p;
        p = new Child1();
        p.show();
        p = new Child2();
        p.show();
    }
}
```

**Question:** Output?

---

### Example 34 – Abstraction + Interface

```java
interface Vehicle {
    void start();
}

class Bike implements Vehicle {
    public void start() {
        System.out.println("Bike starts");
    }
}

class Car implements Vehicle {
    public void start() {
        System.out.println("Car starts");
    }
}

public class Test {
    public static void main(String[] args) {
        Vehicle v1 = new Bike();
        Vehicle v2 = new Car();
        v1.start();
        v2.start();
    }
}
```

**Question:** Output?

---

### Example 35 – Polymorphism + Type Casting

```java
class Animal {
    void eat() { System.out.println("Animal eats"); }
}

class Dog extends Animal {
    void eat() { System.out.println("Dog eats"); }
    void bark() { System.out.println("Dog barks"); }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.eat();
        ((Dog)a).bark();
    }
}
```

**Question:** Output?

---

### Example 36 – Encapsulation + Static Field

```java
class Counter {
    private static int count = 0;
    public Counter() { count++; }
    public static int getCount() { return count; }
}

public class Test {
    public static void main(String[] args) {
        new Counter();
        new Counter();
        System.out.println(Counter.getCount());
    }
}
```

**Question:** Output?

---

### Example 37 – Abstraction + Multiple Method

```java
abstract class Employee {
    abstract void work();
}

class Manager extends Employee {
    void work() {
        System.out.println("Managing team");
    }
}

class Developer extends Employee {
    void work() {
        System.out.println("Writing code");
    }
}

public class Test {
    public static void main(String[] args) {
        Employee e1 = new Manager();
        Employee e2 = new Developer();
        e1.work();
```
