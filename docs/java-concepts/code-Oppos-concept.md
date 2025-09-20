# OOP Concepts Java – Examples 1-20 with Explanation

### Example 1 – Encapsulation

```java
class Student {
    private int marks;
    public void setMarks(int marks) {
        this.marks = marks > 100 ? 100 : marks;
    }
    public int getMarks() {
        return marks;
    }
}

public class Test {
    public static void main(String[] args) {
        Student s = new Student();
        s.setMarks(120);
        System.out.println(s.getMarks());
    }
}
```

**Answer:** 100
**Explanation:** marks is private. setMarks(120) checks >100 → sets marks = 100. getMarks() returns 100.

---

### Example 2 – Encapsulation

```java
class Bank {
    private double balance = 1000;
    public void withdraw(double amount) {
        if(amount <= balance) balance -= amount;
        else balance = 0;
    }
    public double getBalance() {
        return balance;
    }
}

public class Test {
    public static void main(String[] args) {
        Bank b = new Bank();
        b.withdraw(1200);
        System.out.println(b.getBalance());
    }
}
```

**Answer:** 0.0
**Explanation:** withdraw(1200) > balance → balance = 0.

---

### Example 3 – Inheritance

```java
class Vehicle {
    void move() {
        System.out.println("Vehicle moves");
    }
}

class Car extends Vehicle {
    void move() {
        System.out.println("Car moves fast");
    }
}

public class Test {
    public static void main(String[] args) {
        Vehicle v = new Car();
        v.move();
    }
}
```

**Answer:** Car moves fast
**Explanation:** Vehicle reference points to Car object → runtime method overriding.

---

### Example 4 – Inheritance + Polymorphism

```java
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Bark");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("Meow");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a1 = new Dog();
        Animal a2 = new Cat();
        a1.sound();
        a2.sound();
    }
}
```

**Answer:**
Bark
Meow
**Explanation:** Parent reference calls child overridden methods → runtime polymorphism.

---

### Example 5 – Polymorphism (Overloading)

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}

public class Test {
    public static void main(String[] args) {
        Calculator c = new Calculator();
        System.out.println(c.add(5, 10));
        System.out.println(c.add(5, 10, 15));
    }
}
```

**Answer:**
15
30
**Explanation:** Overloaded methods resolved at compile time.

---

### Example 6 – Abstraction

```java
abstract class Shape {
    abstract void area();
}

class Circle extends Shape {
    int r = 5;
    void area() {
        System.out.println(3.14 * r * r);
    }
}

public class Test {
    public static void main(String[] args) {
        Shape s = new Circle();
        s.area();
    }
}
```

**Answer:** 78.5
**Explanation:** Abstract class reference calls implemented method in Circle.

---

### Example 7 – Abstraction + Polymorphism

```java
abstract class Account {
    abstract void getBalance();
}

class Savings extends Account {
    void getBalance() {
        System.out.println("Balance: 5000");
    }
}

class Current extends Account {
    void getBalance() {
        System.out.println("Balance: 10000");
    }
}

public class Test {
    public static void main(String[] args) {
        Account a = new Savings();
        a.getBalance();
        a = new Current();
        a.getBalance();
    }
}
```

**Answer:**
Balance: 5000
Balance: 10000
**Explanation:** Runtime polymorphism → parent reference points to child objects.

---

### Example 8 – Encapsulation

```java
class Employee {
    private String name = "John";
    public String getName() {
        return name;
    }
}

public class Test {
    public static void main(String[] args) {
        Employee e = new Employee();
        System.out.println(e.getName());
    }
}
```

**Answer:** John
**Explanation:** Private field accessed via getter.

---

### Example 9 – Inheritance + Constructor

```java
class A {
    A() {
        System.out.println("A constructor");
    }
}

class B extends A {
    B() {
        System.out.println("B constructor");
    }
}

public class Test {
    public static void main(String[] args) {
        B b = new B();
    }
}
```

**Answer:**
A constructor
B constructor
**Explanation:** Child constructor implicitly calls parent constructor first.

---

### Example 10 – Polymorphism + Casting

```java
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Bark");
    }
    void run() {
        System.out.println("Dog runs");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.sound();
        // a.run(); // Uncommenting gives compilation error
    }
}
```

**Answer:** Bark
**Explanation:** Parent reference can access overridden methods only.

---

### Example 11 – Encapsulation + Validation

```java
class Person {
    private int age;
    public void setAge(int age) {
        this.age = age < 0 ? 0 : age;
    }
    public int getAge() {
        return age;
    }
}

public class Test {
    public static void main(String[] args) {
        Person p = new Person();
        p.setAge(-5);
        System.out.println(p.getAge());
    }
}
```

**Answer:** 0
**Explanation:** Negative age is reset to 0.

---

### Example 12 – Inheritance + Method Overriding

```java
class Parent {
    void msg() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    void msg() {
        System.out.println("Child");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.msg();
    }
}
```

**Answer:** Child
**Explanation:** Runtime polymorphism → child method called.

---

### Example 13 – Polymorphism (Overloading)

```java
class Printer {
    void print(String s) {
        System.out.println(s);
    }
    void print(int n) {
        System.out.println(n);
    }
}

public class Test {
    public static void main(String[] args) {
        Printer p = new Printer();
        p.print("Hello");
        p.print(100);
    }
}
```

**Answer:**
Hello
100
**Explanation:** Overloaded methods resolved at compile time.

---

### Example 14 – Abstraction + Multiple Child

```java
abstract class Vehicle {
    abstract void run();
}

class Bike extends Vehicle {
    void run() {
        System.out.println("Bike runs");
    }
}

class Car extends Vehicle {
    void run() {
        System.out.println("Car runs");
    }
}

public class Test {
    public static void main(String[] args) {
        Vehicle v = new Bike();
        v.run();
        v = new Car();
        v.run();
    }
}
```

**Answer:**
Bike runs
Car runs
**Explanation:** Abstract class reference calls child implementations → runtime polymorphism.

---

### Example 15 – Inheritance + Field Hiding

```java
class A {
    int x = 10;
}

class B extends A {
    int x = 20;
}

public class Test {
    public static void main(String[] args) {
        B b = new B();
        System.out.println(b.x);
        System.out.println(((A)b).x);
    }
}
```

**Answer:**
20
10
**Explanation:** Fields are hidden, not overridden → reference type decides value.

---

### Example 16 – Encapsulation + Multiple Objects

```java
class Counter {
    private static int count = 0;
    public Counter() {
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
        System.out.println(c1.getCount());
        System.out.println(c2.getCount());
    }
}
```

**Answer:**
2
2
**Explanation:** Static field shared across all instances.

---

### Example 17 – Polymorphism + Interfaces

```java
interface Drawable {
    void draw();
}

class Circle implements Drawable {
    public void draw() {
        System.out.println("Circle");
    }
}

class Rectangle implements Drawable {
    public void draw() {
        System.out.println("Rectangle");
    }
}

public class Test {
    public static void main(String[] args) {
        Drawable d1 = new Circle();
        Drawable d2 = new Rectangle();
        d1.draw();
        d2.draw();
    }
}
```

**Answer:**
Circle
Rectangle
**Explanation:** Interface reference calls child implementations → runtime polymorphism.

---

### Example 18 – Abstraction + Method Call

```java
abstract class Device {
    abstract void turnOn();
}

class Phone extends Device {
    void turnOn() {
        System.out.println("Phone ON");
    }
}

public class Test {
    public static void main(String[] args) {
        Device d = new Phone();
        d.turnOn();
    }
}
```

**Answer:** Phone ON
**Explanation:** Abstract class reference calls child method.

---

### Example 19 – Inheritance + Super Keyword

```java
class A {
    void msg() {
        System.out.println("A");
    }
}

class B extends A {
    void msg() {
        super.msg();
        System.out.println("B");
    }
}

public class Test {
    public static void main(String[] args) {
        B b = new B();
        b.msg();
    }
}
```

**Answer:**
A
B
**Explanation:** super.msg() calls parent method before child.

---

### Example 20 – Polymorphism + Abstract Class

```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() {
        System.out.println("Circle drawn");
    }
}

class Rectangle extends Shape {
    void draw() {
        System.out.println("Rectangle drawn");
    }
}

public class Test {
    public static void main(String[] args) {
        Shape s1 = new Circle();
        Shape s2 = new Rectangle();
        s1.draw();
        s2.draw();
    }
}
```

**Answer:**
Circle drawn
Rectangle drawn
**Explanation:** Abstract class reference calls child methods → r
