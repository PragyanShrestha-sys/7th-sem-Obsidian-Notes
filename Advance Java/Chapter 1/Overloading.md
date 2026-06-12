
## What is Overloading?

**Overloading** = Same method name, **different parameter lists** (number, type, or order of parameters)

```
Same name + Different parameters = Overloading
```

### The Short Version:

```java
// All these methods have the SAME name but DIFFERENT parameters
void display() { }
void display(String message) { }
void display(int number) { }
void display(String message, int count) { }
```

---

## Why Use Overloading?

| Benefit | Explanation |
|---------|-------------|
| **Flexibility** | Same action works with different inputs |
| **Readability** | One intuitive name instead of many |
| **Clean Code** | No need for `printString()`, `printInt()`, `printDouble()` |
| **Default values** | Provide simplified versions of complex methods |

---

## Three Ways to Overload Methods

### 1. Different Number of Parameters

```java
public class Calculator {
    
    // Same name, different NUMBER of parameters
    public int add(int a, int b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    public int add(int a, int b, int c, int d) {
        return a + b + c + d;
    }
}

// Usage
Calculator calc = new Calculator();
System.out.println(calc.add(5, 10));           // 15 (2 params)
System.out.println(calc.add(5, 10, 15));       // 30 (3 params)
System.out.println(calc.add(5, 10, 15, 20));   // 50 (4 params)
```

### 2. Different Parameter Types

```java
public class Display {
    
    // Same name, different TYPE of parameters
    public void print(int value) {
        System.out.println("Integer: " + value);
    }
    
    public void print(double value) {
        System.out.println("Double: " + value);
    }
    
    public void print(String value) {
        System.out.println("String: " + value);
    }
    
    public void print(boolean value) {
        System.out.println("Boolean: " + value);
    }
}

// Usage
Display d = new Display();
d.print(10);        // "Integer: 10"
d.print(3.14);      // "Double: 3.14"
d.print("Hello");   // "String: Hello"
d.print(true);      // "Boolean: true"
```

### 3. Different Order of Parameters

```java
public class Student {
    
    // Same name, different ORDER of parameters
    public void register(String name, int id) {
        System.out.println("Student: " + name + ", ID: " + id);
    }
    
    public void register(int id, String name) {
        System.out.println("ID: " + id + ", Name: " + name);
    }
}

// Usage
Student s = new Student();
s.register("Alice", 101);    // "Student: Alice, ID: 101"
s.register(102, "Bob");      // "ID: 102, Name: Bob"
```

---

## Complete Real-World Example

### Example 1: MathOperations Class

```java
public class MathOperations {
    
    // Overloaded add methods
    public int add(int a, int b) {
        System.out.print("int + int = ");
        return a + b;
    }
    
    public double add(double a, double b) {
        System.out.print("double + double = ");
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        System.out.print("int + int + int = ");
        return a + b + c;
    }
    
    public String add(String a, String b) {
        System.out.print("String + String = ");
        return a + b;
    }
    
    // Overloaded multiply methods
    public int multiply(int a, int b) {
        return a * b;
    }
    
    public double multiply(double a, double b) {
        return a * b;
    }
    
    public int multiply(int a, int b, int c) {
        return a * b * c;
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        MathOperations math = new MathOperations();
        
        System.out.println(math.add(5, 10));           // 15
        System.out.println(math.add(5.5, 10.5));       // 16.0
        System.out.println(math.add(5, 10, 15));       // 30
        System.out.println(math.add("Hello", "World")); // HelloWorld
        
        System.out.println(math.multiply(5, 10));      // 50
        System.out.println(math.multiply(5.5, 2.0));    // 11.0
        System.out.println(math.multiply(2, 3, 4));     // 24
    }
}
```

### Example 2: Logger Class (Practical Use)

```java
public class Logger {
    
    // Overloaded log methods - different levels of detail
    
    // Just a message
    public void log(String message) {
        System.out.println("[LOG] " + message);
    }
    
    // Message with severity level
    public void log(String message, String level) {
        System.out.println("[" + level.toUpperCase() + "] " + message);
    }
    
    // Message with timestamp
    public void log(String message, boolean includeTimestamp) {
        if (includeTimestamp) {
            System.out.println("[LOG] " + new java.util.Date() + " - " + message);
        } else {
            log(message);
        }
    }
    
    // Message with error code
    public void log(String message, int errorCode) {
        System.out.println("[ERROR " + errorCode + "] " + message);
    }
    
    // Multiple messages
    public void log(String[] messages) {
        System.out.println("[LOG] Multiple messages:");
        for (String msg : messages) {
            System.out.println("  - " + msg);
        }
    }
}

// Usage
public class Application {
    public static void main(String[] args) {
        Logger logger = new Logger();
        
        logger.log("Application started");                              // Simple
        logger.log("User logged in", "INFO");                          // With level
        logger.log("Database connection failed", true);                // With timestamp
        logger.log("File not found", 404);                              // With error code
        
        String[] errors = {"Network error", "Timeout", "Retry failed"};
        logger.log(errors);                                             // Multiple messages
    }
}
```

### Example 3: Order Processing System

```java
public class Order {
    
    // Different ways to create an order
    
    // 1. Simple order with just product name
    public void addItem(String productName) {
        System.out.println("Added 1 x " + productName);
    }
    
    // 2. Order with quantity
    public void addItem(String productName, int quantity) {
        System.out.println("Added " + quantity + " x " + productName);
    }
    
    // 3. Order with quantity and price
    public void addItem(String productName, int quantity, double price) {
        double total = quantity * price;
        System.out.println("Added " + quantity + " x " + productName + " @ $" + price);
        System.out.println("  Subtotal: $" + total);
    }
    
    // 4. Order with product ID (instead of name)
    public void addItem(int productId, int quantity) {
        System.out.println("Added product ID " + productId + ", quantity: " + quantity);
    }
    
    // 5. Order with discount code
    public void addItem(String productName, int quantity, String discountCode) {
        System.out.println("Added " + quantity + " x " + productName);
        System.out.println("  Discount code applied: " + discountCode);
    }
}

// Usage
public class ShoppingCart {
    public static void main(String[] args) {
        Order order = new Order();
        
        order.addItem("Laptop");                          // Just product
        order.addItem("Mouse", 2);                        // Product + quantity
        order.addItem("Keyboard", 1, 49.99);              // Product + quantity + price
        order.addItem(1001, 3);                           // Product ID + quantity
        order.addItem("Monitor", 1, "SAVE10");            // Product + quantity + discount
    }
}
```

---

## Overloading Constructors (Very Common!)

```java
public class Employee {
    String name;
    int id;
    String department;
    double salary;
    
    // Constructor 1: No parameters
    public Employee() {
        this.name = "Unknown";
        this.id = 0;
        this.department = "Not assigned";
        this.salary = 0.0;
    }
    
    // Constructor 2: Just name and ID
    public Employee(String name, int id) {
        this.name = name;
        this.id = id;
        this.department = "General";
        this.salary = 30000.0;
    }
    
    // Constructor 3: All details
    public Employee(String name, int id, String department, double salary) {
        this.name = name;
        this.id = id;
        this.department = department;
        this.salary = salary;
    }
    
    void display() {
        System.out.println("Name: " + name + ", ID: " + id + 
                         ", Dept: " + department + ", Salary: $" + salary);
    }
}

// Usage
public class Company {
    public static void main(String[] args) {
        Employee emp1 = new Employee();                          // Default
        Employee emp2 = new Employee("Alice", 101);              // Basic
        Employee emp3 = new Employee("Bob", 102, "IT", 75000);   // Complete
        
        emp1.display();  // Name: Unknown, ID: 0, Dept: Not assigned, Salary: $0.0
        emp2.display();  // Name: Alice, ID: 101, Dept: General, Salary: $30000.0
        emp3.display();  // Name: Bob, ID: 102, Dept: IT, Salary: $75000.0
    }
}
```

---

## Overloading vs Overriding (Don't Confuse!)

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| **Purpose** | Same method name, different parameters | Same method signature, different implementation |
| **Parameters** | MUST be different | MUST be same |
| **Return type** | Can be different | MUST be same |
| **Class** | Same class (or subclass) | Different class (subclass) |
| **Inheritance** | Not required | Required (extends or implements) |
| **Compile/Runtime** | Compile-time polymorphism | Runtime polymorphism |

```java
// OVERLOADING (same class, different parameters)
public class Math {
    public int add(int a, int b) { return a + b; }
    public double add(double a, double b) { return a + b; }
}

// OVERRIDING (different classes, same parameters)
class Animal {
    public void speak() { System.out.println("Animal sound"); }
}
class Dog extends Animal {
    @Override
    public void speak() { System.out.println("Bark!"); }  // Overrides parent
}
```

---

## Important Rules for Overloading

### ✅ ALLOWED:

```java
public class Example {
    // 1. Different number of parameters
    void method(int a) { }
    void method(int a, int b) { }
    
    // 2. Different parameter types
    void method(String s) { }
    void method(int i) { }
    
    // 3. Different order of parameters
    void method(int a, String b) { }
    void method(String a, int b) { }
    
    // 4. Different return types (with different parameters)
    int method(int a) { return a; }
    String method(String s) { return s; }
    
    // 5. Access modifiers can differ
    public void test(int a) { }
    private void test(String s) { }
}
```

### ❌ NOT ALLOWED:

```java
public class Example {
    // 1. Only return type different (same parameters)
    int method(int a) { return a; }
    double method(int a) { return a; }  // ❌ ERROR! Same parameters
    
    // 2. Only access modifier different (same parameters)
    public void test(int a) { }
    private void test(int a) { }  // ❌ ERROR! Same parameters
    
    // 3. Only parameter names different (same types)
    void method(int x) { }
    void method(int y) { }  // ❌ ERROR! Same parameter types
}
```

---

## Type Promotion and Overloading

Java automatically promotes smaller types to larger types:

```java
public class Promotion {
    void display(int x) {
        System.out.println("int: " + x);
    }
    
    void display(double x) {
        System.out.println("double: " + x);
    }
    
    public static void main(String[] args) {
        Promotion p = new Promotion();
        
        p.display(5);        // int: 5 (matches int)
        p.display(5.5);      // double: 5.5 (matches double)
        p.display(5L);       // double: 5.0 (long promoted to double)
        p.display('A');      // int: 65 (char promoted to int)
    }
}
```

### Ambiguous Overloading (What Java Can't Resolve):

```java
public class Ambiguous {
    void method(int a, double b) {
        System.out.println("int, double");
    }
    
    void method(double a, int b) {
        System.out.println("double, int");
    }
    
    public static void main(String[] args) {
        Ambiguous a = new Ambiguous();
        
        a.method(5, 5);  // ❌ ERROR! Ambiguous
        // Both methods could work with type promotion
    }
}
```

---

## Real-World Examples from Java Libraries

### System.out.println() - Overloaded!

```java
System.out.println();           // No parameters
System.out.println("Hello");    // String parameter
System.out.println(123);        // int parameter
System.out.println(3.14);       // double parameter
System.out.println(true);       // boolean parameter
System.out.println('A');        // char parameter
```

### String Class - Overloaded Methods

```java
String str = "Hello World";

// Overloaded substring()
str.substring(6);        // "World" - start index only
str.substring(0, 5);     // "Hello" - start and end index

// Overloaded indexOf()
str.indexOf('o');        // 4 - char
str.indexOf('o', 5);     // 7 - char with start position
str.indexOf("World");    // 6 - string
str.indexOf("World", 3); // 6 - string with start position

// Overloaded replace()
str.replace('o', 'a');   // "Hella Warld" - char to char
str.replace("World", "Java"); // "Hello Java" - string to string
```

---

## Summary: Quick Reference

```java
// Overloading allows multiple methods with SAME name, DIFFERENT parameters

// Valid overloads:
✅ method(int a)
✅ method(int a, int b)
✅ method(String s)
✅ method(int a, String s)
✅ method(String s, int a)

// Invalid overloads:
❌ method(int a) and method(int b)  // Same parameters
❌ method(int a) and int method(int a)  // Return type not enough
❌ method(int a) and private method(int a)  // Access modifier not enough
```

---

## The Golden Rule

> **Overloading is determined at COMPILE TIME by looking at the number, type, and order of arguments. The method name alone is NOT enough - Java needs the full signature!**

**Memory trick:**
```
Overloading = "Same name, different game" (different parameters)
```

Would you like me to explain **overriding** (inheritance-based polymorphism) next?