![[Pasted image 20260617095215.png]]## What is Multithreading?

**Multithreading** is a Java feature that allows **concurrent execution of two or more threads** (lightweight processes) to maximize CPU utilization. Each thread runs independently but shares the same memory space.

### Key Concepts
- **Thread**: Smallest unit of execution
- **Concurrency**: Multiple threads running simultaneously
- **Parallelism**: Actually executing on multiple CPU cores

## Two Ways to Create Threads in Java

### Method 1: Extending Thread Class

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        t1.start();  // Start thread 1
        t2.start();  // Start thread 2
    }
}
```

### Method 2: Implementing Runnable Interface (Recommended)

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable());
        Thread t2 = new Thread(new MyRunnable());
        t1.start();
        t2.start();
    }
}
```


## Shortest Multithreading Example

```java
public class T {
    public static void main(String[] args) {
        new Thread(() -> {
            for (int i = 0; i < 3; i++) 
                System.out.println(Thread.currentThread().getName());
        }).start();
        new Thread(() -> {
            for (int i = 0; i < 3; i++) 
                System.out.println(Thread.currentThread().getName());
        }).start();
    }
}
```

## Output (Threads Interleave)

```
Thread-0
Thread-1
Thread-0
Thread-1
Thread-0
Thread-1
```

## Important Rules

1. **Always call `start()`**, not `run()` directly
2. **Runnable is preferred** over extending Thread
3. **Threads run concurrently** - order is unpredictable
4. **Use `sleep()` for delays** (wrap in try-catch)
5. **Don't restart a thread** - create new one instead

---
![[Pasted image 20260617102545.png]]

[[Layout Management]] ; swing ko 
[[JavaFX Layout Panes (extends application)]] ; java fx ko 

---
![[Pasted image 20260617104146.png]]
[[Handling Events]]

---
![[Pasted image 20260617105906.png]]
[[JDBC Driver Types]]
[[ResultSet Types & Concurrency]]

---
![[Pasted image 20260617121816.png]]

[[tcp client and server returing greatest number among other numbers]]

---
![[Pasted image 20260617123028.png]]

[[JavaFX Layout Panes (extends application)]]

---
![[Pasted image 20260617124651.png]]

| Aspect                 | Servlet                        | JSP                     |
| ---------------------- | ------------------------------ | ----------------------- |
| **Creation**           | Class that extends HttpServlet | HTML page with JSP tags |
| **Java Code**          | All code is Java               | Java embedded in HTML   |
| **HTML Code**          | Written inside out.println()   | Direct HTML             |
| **Request Processing** | doGet(), doPost() methods      | _jspService() method    |
| **Initialization**     | init() method                  | jspInit() method        |
| **Destruction**        | destroy() method               | jspDestroy() method     |
| **Output**             | response.getWriter()           | out implicit object     |
| **Use Case**           | Business logic, control flow   | UI design, presentation |
| **MVC Role**           | Controller (C)                 | View (V)                |
| **Recompilation**      | Manual                         | Automatic (if changed)  |

| Object        | Type                  | Description                     |
| ------------- | --------------------- | ------------------------------- |
| `out`         | `JspWriter`           | Sends output to browser         |
| `request`     | `HttpServletRequest`  | Client request data             |
| `response`    | `HttpServletResponse` | Server response                 |
| `session`     | `HttpSession`         | User session data               |
| `application` | `ServletContext`      | Application-wide data           |
| `config`      | `ServletConfig`       | Servlet configuration           |
| `pageContext` | `PageContext`         | Page-scoped data and utilities  |
| `page`        | `Object`              | Current servlet instance        |
| `exception`   | `Throwable`           | Error object (error pages only) |i

[[JSP implicit objects]]

---
![[Pasted image 20260617125113.png]]

### Final Class

- A **final class** cannot be **extended** (no subclasses allowed)
- Used for **immutable classes** (e.g., `String`, `Integer`, `Math`)
- Provides **security** and **design control**
- All methods in a final class are **implicitly final**
- Cannot be **abstract** (final and abstract are opposites)

```java
final class Parent {
    void display() {
        System.out.println("Hello");
    }
}

// ❌ ERROR: Cannot inherit from final class
class Child extends Parent { } 
```

### ResultSet

- Represents a **table of data** returned from a **database query**
- Provides **cursor-based navigation** through rows
- Contains **getter methods** to retrieve column values
- Types: **Forward-only**, **Scrollable**, **Updatable**
- Must be **closed** after use to free resources

```java
ResultSet rs = stmt.executeQuery("SELECT * FROM users");
while (rs.next()) {
    String name = rs.getString("name");
    int age = rs.getInt("age");
}
rs.close();
```

## Quick Comparison

| Feature | Final Class | ResultSet |
|---------|-------------|-----------|
| **Purpose** | Prevent inheritance | Store query results |
| **Used in** | OOP, immutability | JDBC, Database |
| **Key property** | Cannot be extended | Cursor navigation |
| **Example** | `String`, `Integer` | Query result data |
