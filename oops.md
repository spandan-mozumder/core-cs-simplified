# 🧱 OOPs — Interview Questions & Answers

> Top Object-Oriented Programming interview questions with code examples in Java and Python.
> Source: [Intellipaat — OOPs Interview Questions](https://intellipaat.com/blog/interview-question/oops-interview-questions/)

---

### Q1. What is Object-Oriented Programming?

**OOP** is a programming paradigm based on the concept of **objects** that contain data (attributes) and code (methods). It models real-world entities.

---

### Q2. Four Pillars of OOP

| Pillar            | Description                                            |
| ----------------- | ------------------------------------------------------ |
| **Encapsulation** | Bundling data + methods; restricting direct access     |
| **Abstraction**   | Hiding complex implementation; showing only essentials |
| **Inheritance**   | Creating new classes from existing ones                |
| **Polymorphism**  | Same interface, different implementations              |

---

### Q3. Classes and Objects

```java
// Java
class Car {
    String brand;
    int speed;

    Car(String brand, int speed) {
        this.brand = brand;
        this.speed = speed;
    }

    void accelerate() {
        speed += 10;
        System.out.println(brand + " speed: " + speed);
    }
}

Car tesla = new Car("Tesla", 0); // Object
tesla.accelerate(); // Tesla speed: 10
```

```python
# Python
class Car:
    def __init__(self, brand, speed=0):
        self.brand = brand
        self.speed = speed

    def accelerate(self):
        self.speed += 10
        return f"{self.brand} speed: {self.speed}"

tesla = Car("Tesla")
print(tesla.accelerate())  # Tesla speed: 10
```

---

### Q4. Encapsulation

```java
class BankAccount {
    private double balance; // Private — cannot access directly

    public BankAccount(double initial) { this.balance = initial; }

    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) balance -= amount;
        else System.out.println("Insufficient funds");
    }

    public double getBalance() { return balance; } // Controlled access
}
```

```python
class BankAccount:
    def __init__(self, initial):
        self.__balance = initial  # Name mangling (private)

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def get_balance(self):
        return self.__balance
```

---

### Q5. Inheritance

```java
class Animal {
    String name;
    void eat() { System.out.println(name + " eats"); }
}

class Dog extends Animal {
    void bark() { System.out.println(name + " barks"); }
}

class Puppy extends Dog {  // Multi-level inheritance
    void play() { System.out.println(name + " plays"); }
}
```

**Types of Inheritance:**
| Type | Description | Java Support |
|------|-------------|-------------|
| Single | A → B | ✅ |
| Multi-level | A → B → C | ✅ |
| Hierarchical | A → B, A → C | ✅ |
| Multiple | A,B → C | ❌ (use interfaces) |
| Hybrid | Combination | ❌ (use interfaces) |

---

### Q6. Polymorphism

```java
// Compile-time (Method Overloading)
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
}

// Runtime (Method Overriding)
class Shape {
    double area() { return 0; }
}

class Circle extends Shape {
    double radius;
    Circle(double r) { this.radius = r; }

    @Override
    double area() { return Math.PI * radius * radius; }
}

class Rectangle extends Shape {
    double w, h;
    Rectangle(double w, double h) { this.w = w; this.h = h; }

    @Override
    double area() { return w * h; }
}

// Polymorphic behavior
Shape s1 = new Circle(5);
Shape s2 = new Rectangle(4, 6);
System.out.println(s1.area()); // 78.54
System.out.println(s2.area()); // 24.0
```

---

### Q7. Abstraction

```java
// Abstract class
abstract class Vehicle {
    abstract void start();      // No implementation
    void stop() {               // Has implementation
        System.out.println("Vehicle stopped");
    }
}

class Car extends Vehicle {
    @Override
    void start() { System.out.println("Car started with key"); }
}

// Interface (100% abstraction)
interface Flyable {
    void fly();  // implicitly abstract
    default void land() { System.out.println("Landing..."); }
}

class Airplane extends Vehicle implements Flyable {
    @Override
    void start() { System.out.println("Engines starting"); }

    @Override
    public void fly() { System.out.println("Flying at 30,000 ft"); }
}
```

---

### Q8. Constructors

```java
class Student {
    String name;
    int age;

    // Default constructor
    Student() {
        this.name = "Unknown";
        this.age = 0;
    }

    // Parameterized constructor
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Copy constructor
    Student(Student other) {
        this.name = other.name;
        this.age = other.age;
    }
}
```

---

### Q9. Diamond Problem

```java
// Diamond problem: Class inherits from two classes with same method
// Java solves it using interfaces

interface A { default void greet() { System.out.println("A"); } }
interface B { default void greet() { System.out.println("B"); } }

class C implements A, B {
    @Override
    public void greet() {
        A.super.greet(); // Explicitly choose
    }
}
```

---

### Q10. Static vs Non-Static

```java
class MathUtils {
    static int count = 0; // Shared across all instances

    static int add(int a, int b) { // No object needed
        return a + b;
    }

    int instanceMethod() { // Needs object
        return ++count;
    }
}

MathUtils.add(2, 3);   // 5 — called on class
MathUtils obj = new MathUtils();
obj.instanceMethod();   // Called on object
```

---

### Q11. Composition vs Inheritance

```java
// Inheritance (IS-A)
class Engine {
    void start() { System.out.println("Engine started"); }
}
class Car extends Engine {} // Car IS-A Engine? Not ideal.

// Composition (HAS-A) — preferred
class Car {
    private Engine engine; // Car HAS-A Engine ✅
    private Wheel[] wheels;

    Car() {
        this.engine = new Engine();
        this.wheels = new Wheel[4];
    }

    void start() {
        engine.start();
    }
}
```

---

### Q12. Operator Overloading (Python)

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(3, 4)
p3 = p1 + p2  # Uses __add__
print(p3)     # (4, 6)
```

---

### Q13. Access Specifiers

| Specifier   | Same Class | Same Package | Subclass | Other |
| ----------- | ---------- | ------------ | -------- | ----- |
| `public`    | ✅         | ✅           | ✅       | ✅    |
| `protected` | ✅         | ✅           | ✅       | ❌    |
| default     | ✅         | ✅           | ❌       | ❌    |
| `private`   | ✅         | ❌           | ❌       | ❌    |

---

### Q14. Virtual Functions (C++)

```cpp
class Base {
public:
    virtual void show() { // Virtual — enables runtime polymorphism
        cout << "Base" << endl;
    }
};

class Derived : public Base {
public:
    void show() override {
        cout << "Derived" << endl;
    }
};

Base* ptr = new Derived();
ptr->show(); // "Derived" — runtime binding

// Pure virtual function (abstract method)
class AbstractBase {
    virtual void mustImplement() = 0; // Pure virtual
};
```

---

### Q15. SOLID Principles (Brief)

| Principle                 | Description                                      |
| ------------------------- | ------------------------------------------------ |
| **S**ingle Responsibility | A class should have only one reason to change    |
| **O**pen/Closed           | Open for extension, closed for modification      |
| **L**iskov Substitution   | Subtypes must be substitutable for base types    |
| **I**nterface Segregation | Many specific interfaces > one general interface |
| **D**ependency Inversion  | Depend on abstractions, not concretions          |

---
