Excellent question! **Inheritance** and **method overriding** are two of the most important concepts in Object-Oriented Programming. Let me explain them completely, from basics to advanced.

---

## The Big Picture

```
INHERITANCE = Child class GETS properties/methods from Parent class
OVERRIDING = Child class REPLACES a parent's method with its own version

Think of it like:
- Inheritance = You inherit your parent's house
- Overriding = You renovate a room to make it your own
```

---

## Part 1: Inheritance

### What is Inheritance?

**Inheritance** is a mechanism where one class (child/subclass) acquires the properties and behaviors of another class (parent/superclass).

```
Parent Class (Superclass)
    ↓ extends
Child Class (Subclass)

Child HAS everything Parent has, PLUS more!
```

### Basic Syntax:

```java
// Parent class
class Animal {
    String name;
    
    void eat() {
        System.out.println(name + " is eating");
    }
    
    void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Child class (inherits from Animal)
class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking");
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.name = "Buddy";     // Inherited from Animal
        dog.eat();               // Inherited from Animal
        dog.sleep();             // Inherited from Animal
        dog.bark();              // Dog's own method
    }
}
```

**Output:**
```
Buddy is eating
Buddy is sleeping
Buddy is barking
```

---

## Types of Inheritance in Java

Java supports **only single inheritance** for classes (one parent), but supports **multiple inheritance** for interfaces.

```java
// ✅ Single inheritance (one parent)
class A { }
class B extends A { }

// ✅ Multi-level inheritance (grandparent → parent → child)
class Grandparent { }
class Parent extends Grandparent { }
class Child extends Parent { }

// ❌ Multiple inheritance (NOT allowed for classes)
// class C extends A, B { }  // ERROR!

// ✅ Multiple inheritance for interfaces (allowed)
interface X { }
interface Y { }
class Z implements X, Y { }  // OK!
```

---

## The `super` Keyword

`super` refers to the parent class and is used to access parent members.

```java
class Animal {
    String name = "Generic Animal";
    
    Animal() {
        System.out.println("Animal constructor");
    }
    
    Animal(String name) {
        this.name = name;
        System.out.println("Animal parameterized constructor");
    }
    
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    String name = "Doggy";  // This shadows parent's name
    
    Dog() {
        super();  // Call parent's no-arg constructor (implicit if not written)
        System.out.println("Dog constructor");
    }
    
    Dog(String name) {
        super(name);  // Call parent's parameterized constructor
        System.out.println("Dog parameterized constructor");
    }
    
    void display() {
        System.out.println("Child name: " + this.name);    // Doggy
        System.out.println("Parent name: " + super.name);  // Generic Animal
    }
    
    @Override
    void sound() {
        super.sound();  // Call parent's sound method
        System.out.println("Dog barks: Woof! Woof!");
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Dog dog1 = new Dog();
        dog1.display();
        dog1.sound();
        
        Dog dog2 = new Dog("Max");
    }
}
```

**Output:**
```
Animal constructor
Dog constructor
Child name: Doggy
Parent name: Generic Animal
Animal makes sound
Dog barks: Woof! Woof!
Animal parameterized constructor
Dog parameterized constructor
```

---

## Part 2: Method Overriding

### What is Method Overriding?

**Method overriding** is when a child class provides its own implementation of a method that is already defined in the parent class.

```
Parent: makeSound() → "Some sound"
Child:  makeSound() → "Meow!" (overridden)

The child's version is called instead of parent's
```

### Rules for Overriding:

| Rule | Explanation |
|------|-------------|
| Same method name | Must match exactly |
| Same parameters | Same number, types, order |
| Same return type | Or covariant return type (subclass) |
| Cannot be more restrictive | Access can be same or wider, not narrower |
| Cannot override final methods | `final` methods are locked |
| Cannot override static methods | Can hide them, but not override |

### Basic Overriding Example:

```java
class Vehicle {
    void start() {
        System.out.println("Vehicle is starting");
    }
    
    void stop() {
        System.out.println("Vehicle is stopping");
    }
    
    protected void displayInfo() {
        System.out.println("This is a vehicle");
    }
}

class Car extends Vehicle {
    @Override  // Optional but recommended (catches errors)
    void start() {
        System.out.println("Car engine starts: Vroom!");
    }
    
    @Override
    void stop() {
        System.out.println("Car brakes smoothly");
    }
    
    @Override
    public void displayInfo() {  // Can increase visibility (protected → public)
        System.out.println("This is a car with 4 wheels");
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Vehicle v = new Vehicle();
        v.start();  // "Vehicle is starting"
        
        Car c = new Car();
        c.start();  // "Car engine starts: Vroom!"  (overridden)
        
        Vehicle carAsVehicle = new Car();  // Polymorphism
        carAsVehicle.start();  // "Car engine starts: Vroom!" (child's version!)
    }
}
```

---

## Overriding vs Overloading (Critical Distinction!)

```java
class Parent {
    void method() {
        System.out.println("Parent method");
    }
    
    void method(int x) {
        System.out.println("Parent method with int");
    }
}

class Child extends Parent {
    // OVERRIDING - same signature as parent
    @Override
    void method() {
        System.out.println("Child overridden method");
    }
    
    // OVERLOADING - different parameter
    void method(String s) {
        System.out.println("Child overloaded method: " + s);
    }
}

// Usage
Parent p = new Child();
p.method();      // "Child overridden method" (overriding)
p.method(5);     // "Parent method with int" (inherited, not overridden)
// p.method("hi");  // ERROR! Parent doesn't have method(String)
```

| Feature | Overriding | Overloading |
|---------|-----------|-------------|
| Relationship | Between classes (parent-child) | Same class (or child) |
| Method signature | SAME | DIFFERENT (parameters) |
| Return type | Same or covariant | Can be different |
| Annotation | `@Override` | No special annotation |
| Polymorphism | Runtime (dynamic) | Compile-time (static) |

---

## Real-World Complete Example

### Banking System

```java
// Parent class
class BankAccount {
    protected String accountNumber;
    protected double balance;
    protected String accountHolder;
    
    public BankAccount(String accountNumber, String accountHolder, double initialBalance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
    }
    
    // Method to be overridden
    public void calculateInterest() {
        double interest = balance * 0.01;  // 1% basic interest
        System.out.println("Basic interest: $" + interest);
        balance += interest;
    }
    
    public void displayInfo() {
        System.out.println("Account: " + accountNumber);
        System.out.println("Holder: " + accountHolder);
        System.out.println("Balance: $" + balance);
    }
    
    public void deposit(double amount) {
        balance += amount;
        System.out.println("Deposited: $" + amount);
    }
    
    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
            System.out.println("Withdrew: $" + amount);
        } else {
            System.out.println("Insufficient funds!");
        }
    }
}

// Child 1: Savings Account
class SavingsAccount extends BankAccount {
    private double interestRate = 0.04;  // 4% interest
    
    public SavingsAccount(String accountNumber, String accountHolder, double initialBalance) {
        super(accountNumber, accountHolder, initialBalance);
    }
    
    @Override
    public void calculateInterest() {
        double interest = balance * interestRate;
        System.out.println("Savings interest: $" + interest + " (4%)");
        balance += interest;
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();  // Call parent's display
        System.out.println("Account Type: Savings");
        System.out.println("Interest Rate: " + (interestRate * 100) + "%");
    }
}

// Child 2: Current Account
class CurrentAccount extends BankAccount {
    private double overdraftLimit = 5000;
    
    public CurrentAccount(String accountNumber, String accountHolder, double initialBalance) {
        super(accountNumber, accountHolder, initialBalance);
    }
    
    @Override
    public void calculateInterest() {
        // Current accounts don't earn interest
        System.out.println("Current accounts do not earn interest");
    }
    
    @Override
    public void withdraw(double amount) {
        if (amount <= balance + overdraftLimit) {
            balance -= amount;
            System.out.println("Withdrew: $" + amount);
            if (balance < 0) {
                System.out.println("Warning: Overdraft used. Negative balance: $" + balance);
            }
        } else {
            System.out.println("Overdraft limit exceeded!");
        }
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Account Type: Current");
        System.out.println("Overdraft Limit: $" + overdraftLimit);
    }
}

// Child 3: Fixed Deposit Account
class FixedDepositAccount extends BankAccount {
    private int termMonths;
    private double fixedRate = 0.08;  // 8% interest
    
    public FixedDepositAccount(String accountNumber, String accountHolder, 
                               double initialBalance, int termMonths) {
        super(accountNumber, accountHolder, initialBalance);
        this.termMonths = termMonths;
    }
    
    @Override
    public void calculateInterest() {
        double interest = balance * fixedRate;
        System.out.println("Fixed deposit interest: $" + interest + " (8%) for " + termMonths + " months");
        balance += interest;
    }
    
    @Override
    public void withdraw(double amount) {
        System.out.println("Cannot withdraw from Fixed Deposit before maturity!");
        System.out.println("Maturity period: " + termMonths + " months");
    }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Account Type: Fixed Deposit");
        System.out.println("Term: " + termMonths + " months");
        System.out.println("Interest Rate: " + (fixedRate * 100) + "%");
    }
}

// Polymorphism in action!
public class Bank {
    public static void main(String[] args) {
        // Array of BankAccount references (polymorphism)
        BankAccount[] accounts = {
            new SavingsAccount("SAV001", "Alice", 5000),
            new CurrentAccount("CUR001", "Bob", 3000),
            new FixedDepositAccount("FD001", "Charlie", 10000, 12)
        };
        
        // Process all accounts - notice how each behaves differently!
        for (BankAccount account : accounts) {
            System.out.println("\n" + "=".repeat(40));
            account.displayInfo();
            account.calculateInterest();  // Polymorphic call!
            System.out.println("Final Balance: $" + account.balance);
        }
    }
}
```

**Output:**
```
========================================
Account: SAV001
Holder: Alice
Balance: $5000.0
Account Type: Savings
Interest Rate: 4.0%
Savings interest: $200.0 (4%)
Final Balance: $5200.0

========================================
Account: CUR001
Holder: Bob
Balance: $3000.0
Account Type: Current
Overdraft Limit: $5000.0
Current accounts do not earn interest
Final Balance: $3000.0

========================================
Account: FD001
Holder: Charlie
Balance: $10000.0
Account Type: Fixed Deposit
Term: 12 months
Interest Rate: 8.0%
Fixed deposit interest: $800.0 (8%) for 12 months
Final Balance: $10800.0
```

---

## Covariant Return Types (Java 5+)

Child class can return a subtype of parent's return type.

```java
class Parent {
    Object getValue() {
        return new Object();
    }
}

class Child extends Parent {
    @Override
    String getValue() {  // String is a subtype of Object
        return "Hello";
    }
}
```

---

## The `@Override` Annotation

Always use it! It helps catch errors.

```java
class Parent {
    void method() { }
}

class Child extends Parent {
    @Override
    void method() { }  // ✅ Good - correctly overriding
    
    // @Override
    // void method2() { }  // ❌ ERROR! No such method in parent
    
    // @Override
    // void Method() { }    // ❌ ERROR! Case mismatch (method vs Method)
}
```

---

## Common Mistakes and Solutions

### ❌ Mistake 1: Forgetting `super` in constructor

```java
class Parent {
    Parent(String name) {
        System.out.println("Parent: " + name);
    }
}

class Child extends Parent {
    Child() {
        // super() is automatically called, but Parent has no no-arg constructor!
        // ERROR!
    }
}
```

**Solution:**
```java
class Child extends Parent {
    Child() {
        super("Default");  // Must explicitly call parent's constructor
    }
}
```

### ❌ Mistake 2: Narrowing access

```java
class Parent {
    public void method() { }
}

class Child extends Parent {
    @Override
    protected void method() { }  // ❌ ERROR! Cannot reduce visibility
}
```

### ❌ Mistake 3: Overriding static methods (not possible)

```java
class Parent {
    static void method() {
        System.out.println("Parent static");
    }
}

class Child extends Parent {
    // This is NOT overriding - it's HIDING
    static void method() {
        System.out.println("Child static");
    }
}
```

---

## Protected Access in Inheritance

```java
package package1;

public class Parent {
    private int privateVar = 1;      // Only Parent class
    int defaultVar = 2;              // package1 only
    protected int protectedVar = 3;  // package1 + subclasses anywhere
    public int publicVar = 4;        // everywhere
}

package package2;
import package1.Parent;

class Child extends Parent {
    void access() {
        // privateVar = 10;     // ❌ ERROR: private
        // defaultVar = 20;     // ❌ ERROR: different package
        protectedVar = 30;       // ✅ OK: protected in subclass
        publicVar = 40;          // ✅ OK: public
    }
}
```

---

## Inheritance and Constructors

```java
class Parent {
    Parent() {
        System.out.println("Parent constructor");
    }
    
    Parent(int x) {
        System.out.println("Parent constructor with x=" + x);
    }
}

class Child extends Parent {
    Child() {
        // super() is automatically called (Parent no-arg constructor)
        System.out.println("Child constructor");
    }
    
    Child(int x) {
        super(x);  // Must explicitly call if using parameterized constructor
        System.out.println("Child constructor with x=" + x);
    }
    
    Child(String s) {
        this();  // Can call another constructor
        System.out.println("Child constructor with s=" + s);
    }
}
```

---

## Object Class - The Ultimate Parent

Every class in Java implicitly extends `Object`.

```java
class MyClass { }  // Actually: class MyClass extends Object { }

// All classes inherit these Object methods:
// - toString()
// - equals()
// - hashCode()
// - getClass()
// - wait(), notify(), etc.

class Person {
    String name;
    
    @Override
    public String toString() {
        return "Person: " + name;
    }
    
    @Override
    public boolean equals(Object obj) {
        if (obj instanceof Person) {
            Person other = (Person) obj;
            return this.name.equals(other.name);
        }
        return false;
    }
}
```

---

## When to Use Inheritance (IS-A vs HAS-A)

```java
// ✅ IS-A relationship (use inheritance)
class Animal { }
class Dog extends Animal { }  // Dog IS-A Animal

// ✅ HAS-A relationship (use composition)
class Engine { }
class Car {
    private Engine engine;  // Car HAS-A Engine (better than extending Engine)
}
```

### Favor Composition over Inheritance:

```java
// ❌ Poor inheritance (Stack IS-A Vector? Not really)
class Stack extends Vector { }  // Problem: Stack has methods it shouldn't!

// ✅ Better composition
class Stack {
    private Vector storage;  // Stack HAS-A Vector (uses it, doesn't become it)
}
```

---

## Summary Comparison Table

| Feature               | Inheritance                      | Overriding                     |
| --------------------- | -------------------------------- | ------------------------------ |
| **What**              | Child gets parent's members      | Child replaces parent's method |
| **Keyword**           | `extends`                        | `@Override` annotation         |
| **Relationship**      | Parent-Child                     | Parent-Child                   |
| **When**              | Class definition                 | Method definition              |
| **Purpose**           | Code reuse, hierarchy            | Polymorphism, specialization   |
| **Number of parents** | One (classes), Many (interfaces) | One parent method per override |

---

## Quick Reference

### Inheritance Syntax:
```java
class Child extends Parent { }
interface Sub extends Super { }
class Class implements Interface1, Interface2 { }
```

### Overriding Rules:
```java
@Override
ReturnType methodName(Parameters) {
    // Must have same name, parameters
    // Return type must be same or subtype
    // Cannot be more restrictive
    // Cannot override final or static
}
```

---

## The Golden Rules

> **"Inheritance creates an IS-A relationship - a Dog IS-A Animal. A child class gets everything the parent has, then adds or modifies as needed."**

> **"Overriding allows a child to be BETTER or DIFFERENT than the parent while keeping the same interface - same method name, different behavior."**

**Memory trick:**
```
Inheritance = "I have what my parent has"
Overriding = "I do it MY way"
super = "Let me ask my parent"
```

Would you like me to explain **abstract classes** (incomplete parent classes) or **polymorphism in depth** next?