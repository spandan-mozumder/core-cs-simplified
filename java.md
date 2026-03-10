# ☕ Java — Interview Questions & Answers

> Top Java interview questions with theoretical answers and code examples.
> Source: [Intellipaat — Java Interview Questions](https://intellipaat.com/blog/interview-question/java-interview-questions/)

---

## Module 1: JVM, Core Fundamentals & Memory

### Q1. What makes Java platform-independent?

Java code compiles into **bytecode** (.class files) which runs on the **JVM** (Java Virtual Machine). The JVM is platform-specific, but bytecode is universal → "Write Once, Run Anywhere."

```java
// Source code → javac → bytecode → JVM → Machine code
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

---

### Q2. How does the JVM work?

1. **Class Loader** loads `.class` files
2. **Bytecode Verifier** checks validity
3. **Interpreter** executes bytecode line by line
4. **JIT Compiler** compiles hot code paths to native machine code for performance

**Memory Areas:** Method Area, Heap, Stack, PC Register, Native Method Stack.

---

### Q3. Explain `public static void main(String args[])`

- `public` — accessible from anywhere
- `static` — no object needed to call it
- `void` — returns nothing
- `main` — entry point recognized by JVM
- `String[] args` — command-line arguments

---

### Q4. int vs Integer

| `int`           | `Integer`              |
| --------------- | ---------------------- |
| Primitive type  | Wrapper class (Object) |
| Stored on stack | Stored on heap         |
| Cannot be null  | Can be null            |
| Faster          | Slower (autoboxing)    |

```java
int a = 5;              // Primitive
Integer b = 5;           // Autoboxing (int → Integer)
int c = b;               // Unboxing (Integer → int)
Integer d = null;        // Allowed
```

---

### Q5. Garbage Collection in Java

Java automatically reclaims memory from unreferenced objects.

```java
public class GCDemo {
    public static void main(String[] args) {
        Object obj = new Object();  // Object on heap
        obj = null;                  // Now eligible for GC
        System.gc();                 // Request GC (not guaranteed)
    }

    @Override
    protected void finalize() throws Throwable {
        System.out.println("Object garbage collected");
    }
}
```

**Collectors:** Serial, Parallel, CMS, G1 (default in Java 9+), ZGC.

---

## Module 2: OOP Concepts & Exception Handling

### Q6. Classes, Objects, Inheritance, Encapsulation

```java
// Encapsulation
public class Employee {
    private String name;
    private double salary;

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public String getName() { return name; }
    public double getSalary() { return salary; }
    public void setSalary(double salary) {
        if (salary > 0) this.salary = salary;
    }
}

// Inheritance
public class Manager extends Employee {
    private int teamSize;

    public Manager(String name, double salary, int teamSize) {
        super(name, salary);
        this.teamSize = teamSize;
    }
}
```

---

### Q7. Method Overloading vs Overriding

```java
class Animal {
    // Overloading (compile-time polymorphism)
    void speak() { System.out.println("..."); }
    void speak(String sound) { System.out.println(sound); }

    // Method to be overridden
    void move() { System.out.println("Animal moves"); }
}

class Dog extends Animal {
    // Overriding (runtime polymorphism)
    @Override
    void move() { System.out.println("Dog runs"); }
}
```

| Feature      | Overloading  | Overriding        |
| ------------ | ------------ | ----------------- |
| Where        | Same class   | Subclass          |
| Parameters   | Must differ  | Must be same      |
| Return type  | Can differ   | Same or covariant |
| Polymorphism | Compile-time | Runtime           |

---

### Q8. Abstract Class vs Interface

```java
// Abstract class
abstract class Shape {
    String color;
    abstract double area(); // No body
    void display() { System.out.println("Shape: " + color); } // Has body
}

// Interface (Java 8+)
interface Drawable {
    void draw(); // implicitly public abstract
    default void log() { System.out.println("Drawing..."); } // default method
    static int getVersion() { return 1; } // static method
}

class Circle extends Shape implements Drawable {
    double radius;
    Circle(double r) { this.radius = r; }

    @Override
    double area() { return Math.PI * radius * radius; }

    @Override
    public void draw() { System.out.println("Drawing circle"); }
}
```

---

### Q9. Exception Handling

```java
public class ExceptionDemo {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero: " + e.getMessage());
        } finally {
            System.out.println("Always executes");
        }

        // throw vs throws
        try {
            validateAge(15);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }

    // throws declares, throw actually throws
    static void validateAge(int age) throws IllegalArgumentException {
        if (age < 18) throw new IllegalArgumentException("Must be 18+");
    }
}

// Custom exception
class InsufficientFundsException extends Exception {
    private double amount;
    public InsufficientFundsException(double amount) {
        super("Insufficient funds: need " + amount + " more");
        this.amount = amount;
    }
}
```

---

### Q10. Access Modifiers

| Modifier    | Class | Package | Subclass | World |
| ----------- | ----- | ------- | -------- | ----- |
| `public`    | ✅    | ✅      | ✅       | ✅    |
| `protected` | ✅    | ✅      | ✅       | ❌    |
| _default_   | ✅    | ✅      | ❌       | ❌    |
| `private`   | ✅    | ❌      | ❌       | ❌    |

---

## Module 3: Collections Framework

### Q11. ArrayList vs LinkedList

```java
import java.util.*;

ArrayList<String> arrayList = new ArrayList<>();  // Dynamic array
LinkedList<String> linkedList = new LinkedList<>(); // Doubly linked list

arrayList.add("A"); // O(1) amortized
linkedList.add("B"); // O(1)

arrayList.get(0);    // O(1) — fast random access
linkedList.get(0);   // O(n) — slow random access
```

---

### Q12. HashMap Internals

```java
Map<String, Integer> map = new HashMap<>();
map.put("Alice", 90);  // hashCode("Alice") → bucket index → store
map.put("Bob", 85);
map.get("Alice");       // O(1) average

// HashMap uses array of linked lists (Java 8+: tree after 8 entries)
// Key.hashCode() → index = hash & (capacity - 1) → bucket
```

| Feature     | HashMap    | TreeMap       | LinkedHashMap   |
| ----------- | ---------- | ------------- | --------------- |
| Order       | No order   | Sorted by key | Insertion order |
| Null keys   | 1 null key | No null keys  | 1 null key      |
| Performance | O(1)       | O(log n)      | O(1)            |

---

### Q13. HashSet vs TreeSet

```java
Set<Integer> hashSet = new HashSet<>(Arrays.asList(3, 1, 2));
// [1, 2, 3] or any order — no guarantee

Set<Integer> treeSet = new TreeSet<>(Arrays.asList(3, 1, 2));
// [1, 2, 3] — always sorted
```

---

## Module 4: Java 8+ Features

### Q14. Lambda Expressions & Functional Interfaces

```java
// Without lambda
Runnable r1 = new Runnable() {
    @Override
    public void run() { System.out.println("Hello"); }
};

// With lambda
Runnable r2 = () -> System.out.println("Hello");

// Functional interfaces
List<String> names = Arrays.asList("Charlie", "Alice", "Bob");
names.sort((a, b) -> a.compareTo(b));       // Comparator
names.forEach(name -> System.out.println(name)); // Consumer
```

---

### Q15. Stream API

```java
List<Employee> employees = List.of(
    new Employee("Alice", 75000),
    new Employee("Bob", 50000),
    new Employee("Charlie", 90000)
);

// Filter + Map + Collect
List<String> highEarners = employees.stream()
    .filter(e -> e.getSalary() > 60000)
    .map(Employee::getName)
    .sorted()
    .collect(Collectors.toList());
// ["Alice", "Charlie"]

// Reduce
double totalSalary = employees.stream()
    .mapToDouble(Employee::getSalary)
    .sum();

// Group by
Map<String, List<Employee>> byDept = employees.stream()
    .collect(Collectors.groupingBy(Employee::getDepartment));
```

---

### Q16. Optional Class

```java
import java.util.Optional;

Optional<String> opt = Optional.ofNullable(getUserName());

// Instead of null checks
String name = opt.orElse("Unknown");
String name2 = opt.orElseGet(() -> fetchDefault());
opt.ifPresent(n -> System.out.println("Name: " + n));

// Chaining
String result = Optional.ofNullable(user)
    .map(User::getAddress)
    .map(Address::getCity)
    .orElse("Unknown City");
```

---

## Module 5: Multithreading & Concurrency

### Q17. Creating Threads

```java
// Method 1: Extend Thread
class MyThread extends Thread {
    public void run() { System.out.println("Thread: " + getName()); }
}

// Method 2: Implement Runnable
class MyRunnable implements Runnable {
    public void run() { System.out.println("Runnable thread"); }
}

// Method 3: Lambda
Thread t = new Thread(() -> System.out.println("Lambda thread"));
t.start();
```

---

### Q18. Synchronized & Volatile

```java
class Counter {
    private volatile int count = 0; // visible across threads

    // Synchronized method
    public synchronized void increment() {
        count++;
    }

    // Synchronized block (more granular)
    public void add(int value) {
        synchronized (this) {
            count += value;
        }
    }

    public int getCount() { return count; }
}
```

---

### Q19. CompletableFuture

```java
import java.util.concurrent.CompletableFuture;

CompletableFuture<String> future = CompletableFuture
    .supplyAsync(() -> fetchFromDB())        // Async call
    .thenApply(data -> transform(data))       // Transform result
    .thenApply(result -> format(result))      // Chain
    .exceptionally(ex -> "Error: " + ex);     // Handle error

// Combine multiple futures
CompletableFuture<String> f1 = CompletableFuture.supplyAsync(() -> "Hello");
CompletableFuture<String> f2 = CompletableFuture.supplyAsync(() -> "World");
CompletableFuture<String> combined = f1.thenCombine(f2, (a, b) -> a + " " + b);
```

---

### Q20. Deadlock Prevention

```java
// DEADLOCK EXAMPLE (BAD)
class DeadlockDemo {
    final Object lock1 = new Object();
    final Object lock2 = new Object();

    void method1() {
        synchronized (lock1) {
            synchronized (lock2) { /* work */ }
        }
    }
    void method2() {
        synchronized (lock2) {  // Opposite order = deadlock!
            synchronized (lock1) { /* work */ }
        }
    }
}

// PREVENTION: Always acquire locks in the same order
void method2Fixed() {
    synchronized (lock1) {  // Same order as method1
        synchronized (lock2) { /* work */ }
    }
}
```

---

## Module 6: Design Patterns

### Q21. Singleton Pattern (Thread-Safe)

```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {} // Private constructor

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) { // Double-check locking
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}

// Modern approach (enum — simplest & safest)
public enum SingletonEnum {
    INSTANCE;
    public void doSomething() { /* ... */ }
}
```

---

### Q22. String vs StringBuilder vs StringBuffer

```java
// String — immutable
String s = "Hello";
s = s + " World"; // Creates new object

// StringBuilder — mutable, NOT thread-safe (faster)
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // Modifies same object

// StringBuffer — mutable, thread-safe (slower)
StringBuffer sbf = new StringBuffer("Hello");
sbf.append(" World");
```

---
