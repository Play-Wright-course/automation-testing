# OOP Concepts Java – Examples 51-80

### Example 51 – Complex Inheritance (5-Level)

```java
class Device {
    void powerOn() { System.out.println("Device power on"); }
}

class Computer extends Device {
    void startOS() { System.out.println("Computer OS started"); }
}

class Laptop extends Computer {
    void openLid() { System.out.println("Laptop lid opened"); }
}

class GamingLaptop extends Laptop {
    void launchGame() { System.out.println("Game launched"); }
}

class Alienware extends GamingLaptop {
    void rgbLighting() { System.out.println("RGB lighting activated"); }
}

public class Test {
    public static void main(String[] args) {
        Alienware a = new Alienware();
        a.powerOn();
        a.startOS();
        a.openLid();
        a.launchGame();
        a.rgbLighting();
    }
}
```

**Question:** Predict the output.

---

### Example 52 – Polymorphism + Inheritance (Overriding)

```java
class Vehicle {
    void move() { System.out.println("Vehicle moves"); }
}

class Car extends Vehicle {
    void move() { System.out.println("Car moves fast"); }
}

class SportsCar extends Car {
    void move() { System.out.println("SportsCar zooms"); }
}

public class Test {
    public static void main(String[] args) {
        Vehicle v1 = new Car();
        Vehicle v2 = new SportsCar();
        v1.move();
        v2.move();
    }
}
```

**Question:** Predict the output.

---

### Example 53 – Abstraction + Multiple Children

```java
abstract class Employee {
    abstract void work();
}

class Developer extends Employee {
    void work() { System.out.println("Writing code"); }
}

class Tester extends Employee {
    void work() { System.out.println("Testing code"); }
}

class Manager extends Employee {
    void work() { System.out.println("Managing team"); }
}

public class Test {
    public static void main(String[] args) {
        Employee[] employees = {new Developer(), new Tester(), new Manager()};
        for(Employee e : employees) e.work();
    }
}
```

**Question:** Predict the output.

---

### Example 54 – Encapsulation + Validation + Multiple Objects

```java
class BankAccount {
    private double balance;
    public BankAccount(double initialBalance) {
        balance = initialBalance < 0 ? 0 : initialBalance;
    }
    public void deposit(double amount) {
        if(amount > 0) balance += amount;
    }
    public void withdraw(double amount) {
        if(amount <= balance) balance -= amount;
        else System.out.println("Insufficient funds");
    }
    public double getBalance() { return balance; }
}

public class Test {
    public static void main(String[] args) {
        BankAccount a1 = new BankAccount(1000);
        BankAccount a2 = new BankAccount(-500);
        a1.deposit(500);
        a2.withdraw(100);
        System.out.println(a1.getBalance());
        System.out.println(a2.getBalance());
    }
}
```

**Question:** Predict the output.

---

### Example 55 – Polymorphism + Interface + Runtime

```java
interface Drawable {
    void draw();
}

class Circle implements Drawable {
    public void draw() { System.out.println("Circle drawn"); }
}

class Rectangle implements Drawable {
    public void draw() { System.out.println("Rectangle drawn"); }
}

public class Test {
    public static void main(String[] args) {
        Drawable[] shapes = {new Circle(), new Rectangle()};
        for(Drawable d : shapes) d.draw();
    }
}
```

**Question:** Predict the output.

---

### Example 56 – Complex Inheritance + Super Constructor

```java
class Animal {
    Animal(String msg) { System.out.println(msg); }
}

class Mammal extends Animal {
    Mammal() { super("Animal is alive"); System.out.println("Mammal created"); }
}

class Dog extends Mammal {
    Dog() { System.out.println("Dog created"); }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
    }
}
```

**Question:** Predict the output.

---

### Example 57 – Polymorphism + Method Overloading + Overriding

```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

class AdvancedCalculator extends Calculator {
    int add(int a, int b, int c) { return a + b + c; }
}

public class Test {
    public static void main(String[] args) {
        AdvancedCalculator calc = new AdvancedCalculator();
        System.out.println(calc.add(5,10));
        System.out.println(calc.add(2.5,3.5));
        System.out.println(calc.add(1,2,3));
    }
}
```

**Question:** Predict the output.

---

### Example 58 – Interface + Multiple Implementations

```java
interface Vehicle {
    void start();
}

class Car implements Vehicle {
    public void start() { System.out.println("Car starts"); }
}

class Bike implements Vehicle {
    public void start() { System.out.println("Bike starts"); }
}

public class Test {
    public static void main(String[] args) {
        Vehicle v1 = new Car();
        Vehicle v2 = new Bike();
        v1.start();
        v2.start();
    }
}
```

**Question:** Predict the output.

---

### Example 59 – Abstraction + Polymorphism + Array

```java
abstract class Shape {
    abstract void area();
}

class Circle extends Shape {
    double r = 3;
    void area() { System.out.println(3.14 * r * r); }
}

class Square extends Shape {
    double side = 4;
    void area() { System.out.println(side * side); }
}

public class Test {
    public static void main(String[] args) {
        Shape[] shapes = {new Circle(), new Square()};
        for(Shape s : shapes) s.area();
    }
}
```

**Question:** Predict the output.

---

### Example 60 – Encapsulation + Static Field + Multiple Objects

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
        new Counter();
        System.out.println(Counter.getCount());
    }
}
```

**Question:** Predict the output.

---

### Example 61 – Multi-Level Inheritance + Method Overriding

```java
class A { void msg() { System.out.println("A"); } }
class B extends A { void msg() { System.out.println("B"); } }
class C extends B { void msg() { System.out.println("C"); } }
class D extends C { void msg() { System.out.println("D"); } }
class E extends D { void msg() { System.out.println("E"); } }

public class Test {
    public static void main(String[] args) {
        A obj = new E();
        obj.msg();
    }
}
```

**Question:** Predict the output.

---

### Example 62 – Polymorphism + Casting

```java
class Animal { void sound() { System.out.println("Animal sound"); } }
class Dog extends Animal { void sound() { System.out.println("Dog barks"); } void run() { System.out.println("Dog runs"); } }

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.sound();
        ((Dog)a).run();
    }
}
```

**Question:** Predict the output.

---

### Example 63 – Abstraction + Constructor + Polymorphism

```java
abstract class Device {
    Device() { System.out.println("Device created"); }
    abstract void start();
}

class Phone extends Device {
    Phone() { System.out.println("Phone created"); }
    void start() { System.out.println("Phone starts"); }
}

public class Test {
    public static void main(String[] args) {
        Device d = new Phone();
        d.start();
    }
}
```

**Question:** Predict the output.

---

### Example 64 – Interface + Default Methods

```java
interface Vehicle {
    void start();
    default void stop() { System.out.println("Vehicle stopped"); }
}

class Car implements Vehicle {
    public void start() { System.out.println("Car started"); }
}

public class Test {
    public static void main(String[] args) {
        Car c = new Car();
        c.start();
        c.stop();
    }
}
```

**Question:** Predict the output.

---

### Example 65 – Encapsulation + Method Validation

```java
class Product {
    private int price;
    public void setPrice(int price) { this.price = price<0?0:price; }
    public int getPrice() { return price; }
}

public class Test {
    public static void main(String[] args) {
        Product p = new Product();
        p.setPrice(-100);
        System.out.println(p.getPrice());
   

```
