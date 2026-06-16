
# Java Classes, Files, and Main Method: Complete Reference Guide

This guide covers everything we've discussed about Java file structure, class declarations, naming rules, and the main method.

---

## Part 1: Basic Java File Structure

### What is a `.java` file?
- A text file containing Java source code
- Compiled into `.class` files (bytecode) by the Java compiler
- Can contain one or more class definitions

### Basic syntax:
```java
// Optional package declaration
package com.example;

// Optional import statements
import java.util.Scanner;

// Class definitions (one can be public)
class ClassName {
    // Fields, methods, constructors
}
```

---

## Part 2: Class Declarations and Access Levels

### Access Modifiers for Classes (Top-Level)

| Modifier | What it means | Can other files access it? |
|----------|--------------|---------------------------|
| `public` | Fully accessible anywhere | ✅ Yes |
| (no modifier) | Package-private (default) | ❌ Only within same package/folder |
| `private` | ❌ Not allowed for top-level classes | N/A |
| `protected` | ❌ Not allowed for top-level classes | N/A |

### Example:
```java
// Saved as "Example.java"
public class Example {      // ✅ Can be accessed from anywhere
    // ...
}

class Helper {              // ✅ Can only be accessed from same package
    // ...
}
```

---

## Part 3: File Naming Rules (Non-Negotiable)

### The Golden Rule:
> **If a class is `public`, the filename MUST exactly match that class name (case-sensitive)**

### Complete Naming Rules:

| Scenario                 | Filename        | Works? | Why?                               |
| ------------------------ | --------------- | ------ | ---------------------------------- |
| `public class Car`       | `Car.java`      | ✅      | Public class matches filename      |
| `public class Car`       | `Vehicle.java`  | ❌      | Mismatch - compilation error       |
| `public class Car`       | `car.java`      | ❌      | Case-sensitive mismatch            |
| `class Car` (not public) | `Anything.java` | ✅      | No public class, so no restriction |
| No classes (empty file)  | `Empty.java`    | ✅      | No public class to match           |

### Error message when rule is violated:
```
Car.java:1: error: class Vehicle is public, 
should be declared in a file named Vehicle.java
public class Vehicle {
       ^
```

---

## Part 4: Multiple Classes in One File

### Rules for Multiple Classes:

1. **At most ONE `public` class** per `.java` file
2. **Any number of non-public classes** (package-private)
3. Only the `public` class (if present) must match filename
4. Each class compiles to its own `.class` file

### Examples:

#### Example 1: One public class (most common)
```java
// Saved as "School.java"
public class School {           // ✅ Matches filename
    // ...
}

class Student {                 // ✅ OK - not public
    // ...
}

class Teacher {                 // ✅ OK - not public
    // ...
}
```

#### Example 2: No public class at all
```java
// Saved as "Anything.java" (filename doesn't matter)
class Dog {
    // ...
}

class Cat {
    // ...
}

class Main {
    public static void main(String[] args) {
        System.out.println("No public class here!");
    }
}
```
✅ Compiles and runs with `java Main`

#### Example 3: Invalid - two public classes
```java
// Saved as "Test.java"
public class Test {        // ✅ OK
    // ...
}

public class Helper {      // ❌ ERROR: Only one public class allowed
    // ...
}
```

---

## Part 5: The Main Method - Entry Point

### Required Signature (Strict Rules):

```java
public static void main(String[] args)
```

### Breakdown of each keyword:

| Keyword | Why it's required | Can it change? |
|---------|------------------|-----------------|
| `public` | JVM needs to call it from outside | ❌ No |
| `static` | JVM calls it without creating an object | ❌ No |
| `void` | Returns nothing to the JVM | ❌ No |
| `main` | Exact name the JVM looks for | ❌ No |
| `String[] args` | Command-line arguments array | ✅ Only `String... args` allowed as alternative |

### Valid variations (only these two):
```java
public static void main(String[] args) { }     // Standard
public static void main(String... args) { }    // Varargs - works too
```

### Invalid variations (will NOT work):
```java
public void main(String[] args) { }            // ❌ Missing static
static void main(String[] args) { }            // ❌ Missing public
public static void main(String args) { }       // ❌ Wrong parameter type
public static int main(String[] args) { }      // ❌ Wrong return type
public static void main() { }                  // ❌ Missing parameter
```

---

## Part 6: Main Method Location (Flexible!)

### Important: Main does NOT need to be in a public class!

The class containing `main` can be:
- ✅ `public` (common but not required)
- ✅ package-private (no modifier)
- ✅ Any name (doesn't need to match filename)
- ✅ Anywhere in the file (order doesn't matter)

### Examples of valid main locations:

#### Example 1: Main in public class (most common)
```java
// Saved as "Program.java"
public class Program {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```
Run: `java Program`

#### Example 2: Main in non-public class
```java
// Saved as "MyApp.java"
public class MyApp {           // Public class matches filename
    // No main here
}

class Starter {                // Not public
    public static void main(String[] args) {
        System.out.println("Main in non-public class!");
    }
}
```
Run: `java Starter` ✅ Works perfectly!

#### Example 3: Main in class with different name from file
```java
// Saved as "Car.java"
class Engine {
    public static void main(String[] args) {
        System.out.println("Main in Engine class");
    }
}
```
Run: `java Engine` ✅ Works even though file is `Car.java`

---

## Part 7: How Java Executes a Program

### Step-by-step process:

1. **Compile:**
   ```bash
   javac MyFile.java
   ```
   - Creates `.class` files for EVERY class in the source file
   - Example: If `MyFile.java` has 3 classes → creates 3 `.class` files

2. **Run:**
   ```bash
   java ClassName
   ```
   - JVM looks for a class named `ClassName`
   - JVM checks if that class has `public static void main(String[] args)`
   - JVM executes that method

### What Java does NOT care about:
- ❌ Original `.java` filename
- ❌ Whether the class with main is public
- ❌ The name of other classes in the file
- ❌ The order of classes in the file

### What Java DOES care about:
- ✅ The class name you type after `java` exists
- ✅ That class has the EXACT `main` method signature

---

## Part 8: Complete Working Examples

### Example A: Multiple mains in one file
```java
// Saved as "Test.java"
public class Test {              // Matches filename
    public static void main(String[] args) {
        System.out.println("Main 1 - Run with: java Test");
    }
}

class AnotherMain {
    public static void main(String[] args) {
        System.out.println("Main 2 - Run with: java AnotherMain");
    }
}

class YetAnother {
    public static void main(String[] args) {
        System.out.println("Main 3 - Run with: java YetAnother");
    }
}
```
✅ Compiles. You can run any of the three mains!

### Example B: Practical application structure
```java
// Saved as "ShoppingApp.java"
public class ShoppingApp {      // Public class - matches filename
    // This class defines the app structure
    private String storeName;
    
    public ShoppingApp(String name) {
        storeName = name;
    }
    
    public void run() {
        System.out.println("Welcome to " + storeName);
        Cart.processItems();
    }
}

class Cart {                     // Helper class - not public
    static void processItems() {
        System.out.println("Processing cart...");
    }
}

class Launcher {                 // Contains main - not public
    public static void main(String[] args) {
        ShoppingApp app = new ShoppingApp("MegaMart");
        app.run();
    }
}
```
Run with: `java Launcher`

---

## Part 9: Common Mistakes and Solutions

| Mistake | Error | Solution |
|---------|-------|----------|
| `Class` instead of `class` | `class, interface, or enum expected` | Use lowercase `class` |
| `string` instead of `String` | `cannot find symbol` | Use uppercase `String` |
| Missing `static` in main | `main method not found` | Add `static` keyword |
| Missing `public` in main | `main method not public` | Add `public` keyword |
| Wrong parameter: `String args` | `main method not found` | Use `String[] args` |
| Public class wrong filename | `class X is public, should be in X.java` | Rename file or remove `public` |
| Two public classes | `class X is public, should be in X.java` | Make only one public |

---

## Part 10: Best Practices (vs Actual Rules)

### Rules (Non-Negotiable):
| Rule | Must follow? |
|------|--------------|
| `class` not `Class` | ✅ YES |
| `String` not `string` | ✅ YES |
| Main signature exact | ✅ YES |
| Public class = filename | ✅ YES |
| Only one public class | ✅ YES |

### Conventions (Recommended but not required):
| Convention | Should you follow? |
|------------|-------------------|
| Put main in public class | ✅ Recommended (expected by others) |
| Make filename match main class | ✅ Recommended (clear organization) |
| One class per file | ✅ Recommended (easier maintenance) |
| Class names start uppercase | ✅ Standard convention |
| Main class name matches file | ✅ Expected in most projects |

---

## Quick Reference Summary Table

| Question | Answer |
|----------|--------|
| Can `Class` be used instead of `class`? | ❌ No |
| Can `string` be used instead of `String`? | ❌ No |
| Must filename match public class name? | ✅ Yes |
| Must filename match non-public class? | ❌ No |
| Can a file have multiple classes? | ✅ Yes (one public max) |
| Must main be in a public class? | ❌ No |
| Must main signature be exact? | ✅ Yes |
| What runs when you type `java ClassName`? | The `main` method in `ClassName` |
| Can a file have multiple main methods? | ✅ Yes (in different classes) |

---

## Final Key Takeaways

1. **Case sensitivity is strict** - `class` vs `Class`, `String` vs `string`

2. **Public class = filename match** - This is the only naming rule

3. **Main signature is set in stone** - No flexibility except `String[]` vs `String...`

4. **Main can be anywhere** - Any class, any name, public or not

5. **Multiple classes allowed** - But only one can be public

6. **Java runs the class you name** - Not the filename, not the public class

This reference covers everything we discussed. Keep it handy when writing Java programs!


---
# [[if confused about functions inside classes across public and non public folders and main functions]]

note: eeuta file ma only 1 public calss which can only be used in the same class as the file name 

