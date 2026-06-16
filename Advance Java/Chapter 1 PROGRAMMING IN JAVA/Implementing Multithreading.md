Excellent! Let me explain **both ways** of creating threads in Java with clear comparisons.

---

## The Big Picture

**Java has TWO ways to create threads:**

| Way | Keyword | What you do |
|-----|---------|-------------|
| **Way 1** | `extends Thread` | Create a subclass of Thread class |
| **Way 2** | `implements Runnable` | Create a class that implements Runnable interface |

**Both work!** But one is preferred.

---

## Way 1: Extending Thread Class

```java
// Step 1: Create class that EXTENDS Thread
public class MyThread extends Thread {
    
    // Step 2: Override the run() method
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
        }
    }
}

// Step 3: Use it
public class Main {
    public static void main(String[] args) {
        // Create thread objects directly
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        
        // Name them (optional)
        t1.setName("Thread A");
        t2.setName("Thread B");
        
        // Start them
        t1.start();
        t2.start();
    }
}
```

**Output:**
```
Thread A: 1
Thread B: 1
Thread A: 2
Thread B: 2
Thread A: 3
Thread B: 3
...
```

---

## Way 2: Implementing Runnable Interface

```java
// Step 1: Create class that IMPLEMENTS Runnable
public class MyRunnable implements Runnable {
    
    // Step 2: Override the run() method
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
        }
    }
}

// Step 3: Use it
public class Main {
    public static void main(String[] args) {
        // Create Runnable object
        MyRunnable task = new MyRunnable();
        
        // Create Thread objects, passing the Runnable
        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);
        
        // Name them (optional)
        t1.setName("Thread A");
        t2.setName("Thread B");
        
        // Start them
        t1.start();
        t2.start();
    }
}
```

**Same output as before!**

---

## Complete Comparison Example

```java
// ============================================
// WAY 1: Extending Thread
// ============================================
class DownloadThread extends Thread {
    private String fileName;
    
    public DownloadThread(String fileName) {
        this.fileName = fileName;
    }
    
    @Override
    public void run() {
        for (int i = 1; i <= 100; i += 20) {
            System.out.println(getName() + " downloading " + fileName + ": " + i + "%");
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {}
        }
        System.out.println(getName() + " finished: " + fileName);
    }
}

// ============================================
// WAY 2: Implementing Runnable
// ============================================
class DownloadRunnable implements Runnable {
    private String fileName;
    
    public DownloadRunnable(String fileName) {
        this.fileName = fileName;
    }
    
    @Override
    public void run() {
        for (int i = 1; i <= 100; i += 20) {
            System.out.println(Thread.currentThread().getName() + " downloading " + fileName + ": " + i + "%");
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {}
        }
        System.out.println(Thread.currentThread().getName() + " finished: " + fileName);
    }
}

// ============================================
// MAIN CLASS - Compare both
// ============================================
public class CompareThreads {
    public static void main(String[] args) {
        
        System.out.println("=== WAY 1: Extending Thread ===\n");
        
        // With extends Thread - create thread objects directly
        DownloadThread t1 = new DownloadThread("movie.mp4");
        DownloadThread t2 = new DownloadThread("music.mp3");
        
        t1.setName("Downloader-1");
        t2.setName("Downloader-2");
        
        t1.start();
        t2.start();
        
        // Wait for them to finish (for demonstration)
        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {}
        
        System.out.println("\n=== WAY 2: Implementing Runnable ===\n");
        
        // With implements Runnable - separate task from thread
        DownloadRunnable task1 = new DownloadRunnable("document.pdf");
        DownloadRunnable task2 = new DownloadRunnable("image.jpg");
        
        Thread thread1 = new Thread(task1, "Downloader-A");
        Thread thread2 = new Thread(task2, "Downloader-B");
        
        thread1.start();
        thread2.start();
    }
}
```

---

## Key Differences

| Aspect | extends Thread | implements Runnable |
|--------|---------------|---------------------|
| **What you create** | Thread subclass | Task class (not a thread) |
| **Creating thread** | `new MyThread()` | `new Thread(new MyRunnable())` |
| **Access thread methods** | Direct (`getName()`) | Via `Thread.currentThread()` |
| **Inheritance** | Can't extend another class | Can extend another class |
| **Reusability** | Task tied to thread | Task can be reused |
| **Memory** | Slightly more | Slightly less |

---

## Visual Difference

```
Way 1: Extends Thread
┌─────────────────────────────────────────────────────────────┐
│                    Your Class                                │
│                 extends Thread                               │
│  ┌─────────────────────────────────────────────────────────┐│
│  │ class DownloadThread extends Thread {                   ││
│  │     void run() { download logic }                       ││
│  │ }                                                       ││
│  └─────────────────────────────────────────────────────────┘│
│                    Your object IS a thread                   │
│              DownloadThread t = new DownloadThread();        │
│                         t.start();  ← direct                 │
└─────────────────────────────────────────────────────────────┘

Way 2: Implements Runnable
┌─────────────────────────────────────────────────────────────┐
│                    Your Class                                │
│                implements Runnable                           │
│  ┌─────────────────────────────────────────────────────────┐│
│  │ class DownloadTask implements Runnable {                ││
│  │     void run() { download logic }                       ││
│  │ }                                                       ││
│  └─────────────────────────────────────────────────────────┘│
│                    Your object is a TASK                     │
│              DownloadTask task = new DownloadTask();         │
│                                                              │
│                    Thread worker = new Thread(task);         │
│                         worker.start();  ← via Thread        │
└─────────────────────────────────────────────────────────────┘
```

---

## Code Comparison Side by Side

```java
// ============================================
// SAME TASK - Two different implementations
// ============================================

// WAY 1: Extending Thread
class CounterThread extends Thread {
    private String name;
    
    CounterThread(String name) {
        this.name = name;
    }
    
    public void run() {
        for(int i = 1; i <= 5; i++) {
            System.out.println(name + ": " + i);
        }
    }
}

// Usage
CounterThread ct1 = new CounterThread("A");
CounterThread ct2 = new CounterThread("B");
ct1.start();
ct2.start();


// WAY 2: Implementing Runnable  
class CounterRunnable implements Runnable {
    private String name;
    
    CounterRunnable(String name) {
        this.name = name;
    }
    
    public void run() {
        for(int i = 1; i <= 5; i++) {
            System.out.println(name + ": " + i);
        }
    }
}

// Usage
Thread rt1 = new Thread(new CounterRunnable("A"));
Thread rt2 = new Thread(new CounterRunnable("B"));
rt1.start();
rt2.start();
```

---

## Real Example: Same Task, Multiple Threads

```java
// Runnable allows REUSING the same task object across multiple threads
class BankTransaction implements Runnable {
    private String transactionType;
    private int amount;
    
    BankTransaction(String type, int amount) {
        this.transactionType = type;
        this.amount = amount;
    }
    
    public void run() {
        System.out.println(Thread.currentThread().getName() + 
                          " processing " + transactionType + " of $" + amount);
        // Process transaction...
    }
}

public class Bank {
    public static void main(String[] args) {
        // ONE task object
        BankTransaction deposit = new BankTransaction("DEPOSIT", 500);
        
        // Can be used by MULTIPLE threads
        Thread t1 = new Thread(deposit, "ATM-1");
        Thread t2 = new Thread(deposit, "ATM-2");
        Thread t3 = new Thread(deposit, "Online");
        
        t1.start();
        t2.start();
        t3.start();
        
        // With extends Thread, you'd need separate objects
        // BankTransactionThread t1 = new BankTransactionThread(...);
        // BankTransactionThread t2 = new BankTransactionThread(...); // separate!
    }
}
```

---

## Inheritance Problem (Why Runnable is Preferred)

```java
// PROBLEM with extends Thread:
class MyTask extends Thread {
    // Can't extend any other class!
    // What if I also want to be a DatabaseConnection? Can't!
}

// SOLUTION with Runnable:
class MyTask implements Runnable {
    // Can still extend another class!
}

class AdvancedTask extends DatabaseConnection implements Runnable {
    // Now you can have BOTH!
    public void run() {
        // task code
    }
}
```

---

## Which One to Use?

| Scenario | Recommendation |
|----------|----------------|
| **You need to inherit from another class** | Runnable (must) |
| **Simple, one-time task** | Either (Runnable preferred) |
| **You need thread-specific methods often** | Extends Thread (direct access) |
| **You want to reuse the same task** | Runnable |
| **You're using thread pools** | Runnable |
| **Learning/teaching simple examples** | Either (both fine) |

---

## Modern Way (Lambda + Runnable)

```java
// The shortest way (Java 8+)
// This IS the Runnable approach (just shorter syntax)

public class ModernWay {
    public static void main(String[] args) {
        
        // No separate class needed!
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread 1: " + i);
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Thread 2: " + i);
            }
        });
        
        t1.start();
        t2.start();
    }
}
```

This is still **Runnable** internally! The lambda creates a Runnable object.

---

## Summary Table

| Feature | extends Thread | implements Runnable |
|---------|---------------|---------------------|
| **Class type** | Thread subclass | Regular class |
| **Object is** | A Thread | A Task (not Thread) |
| **How to start** | `obj.start()` | `new Thread(obj).start()` |
| **Access thread methods** | Direct (`this.getName()`) | Via `Thread.currentThread()` |
| **Can extend another class** | ❌ No | ✅ Yes |
| **Reuse task object** | ❌ Hard | ✅ Easy |
| **Memory overhead** | Slightly more | Slightly less |
| **Best for** | Simple cases | Most cases (preferred) |

---

## The Golden Rule

> **Use `implements Runnable` unless you have a specific reason to `extends Thread`. Runnable is more flexible because Java doesn't support multiple inheritance.**

**Memory trick:**
```
extends Thread = "I AM a thread"
implements Runnable = "I HAVE a task that can be run by a thread"
```

