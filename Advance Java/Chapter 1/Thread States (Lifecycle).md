
### The 6 Thread States

| State | What happens | Analogy |
|-------|--------------|---------|
| **NEW** | Thread created, not started | You're hired but haven't started work |
| **RUNNABLE** | Thread is running or ready to run | You're working at your desk |
| **BLOCKED** | Waiting for a lock | Waiting for the printer (someone else using it) |
| **WAITING** | Waiting indefinitely | Waiting for boss's signal (could be forever) |
| **TIMED_WAITING** | Waiting for specific time | Taking a 10-minute break |
| **TERMINATED** | Thread finished | You quit or retired |

---

### Visual Lifecycle

```
                    ┌─────────────────┐
                    │      NEW        │
                    │ (Thread created)│
                    └────────┬────────┘
                             │ start()
                             ↓
                    ┌─────────────────┐
                    │   RUNNABLE       │
                    │ (Running/Ready)  │
                    └────────┬────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
        ↓                    ↓                    ↓
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   BLOCKED    │    │   WAITING    │    │TIMED_WAITING │
│ (Waiting for │    │ (Waiting     │    │ (Waiting for │
│  lock)       │    │  forever)    │    │  time period)│
└──────────────┘    └──────────────┘    └──────────────┘
        │                    │                    │
        └────────────────────┼────────────────────┘
                             │
                             ↓
                    ┌─────────────────┐
                    │  TERMINATED      │
                    │ (Thread ended)   │
                    └─────────────────┘
```

---

### Detailed State Explanations

#### 1. NEW - Created but Not Started

```java
Thread t = new Thread(() -> System.out.println("Hello"));
// t is in NEW state - exists but not running

System.out.println(t.getState());  // NEW
```

**Analogy:** You filled out job application but haven't started working.

---

#### 2. RUNNABLE - Running or Ready

```java
t.start();  // Now t moves to RUNNABLE
System.out.println(t.getState());  // RUNNABLE
```

**Analogy:** You're at your desk, either working or ready to work.

**Note:** RUNNABLE includes both "actually running on CPU" and "waiting for CPU turn" (you can't tell the difference).

---

#### 3. BLOCKED - Waiting for a Lock

```java
synchronized(lock) {
    // Thread tries to enter here
    // If another thread has the lock, this thread becomes BLOCKED
}
```

**Analogy:** Waiting for the printer because someone else is using it.

---

#### 4. WAITING - Waiting Indefinitely

```java
t.join();        // Wait for t to finish
t.wait();        // Wait for notification
```

**Analogy:** Waiting for boss's signal - could be 1 second or never.

---

#### 5. TIMED_WAITING - Waiting with Timeout

```java
Thread.sleep(1000);   // Wait 1 second
t.join(1000);         // Wait max 1 second
t.wait(1000);         // Wait max 1 second for notification
```

**Analogy:** Taking a 10-minute break - you'll wake up automatically.

---

#### 6. TERMINATED - Finished

```java
// When run() method completes
System.out.println(t.getState());  // TERMINATED
```

**Analogy:** You quit or retired - no more work.

---

### [[Complete Example Showing All States]]

---

### Quick Reference Card

| State | How to enter | How to leave |
|-------|--------------|--------------|
| **NEW** | `new Thread()` | `start()` |
| **RUNNABLE** | `start()` | Scheduler decides |
| **BLOCKED** | `synchronized` block (lock taken) | Lock becomes available |
| **WAITING** | `wait()`, `join()`, `park()` | `notify()`, `notifyAll()`, thread finishes |
| **TIMED_WAITING** | `sleep()`, `wait(time)`, `join(time)` | Time expires or notification |
| **TERMINATED** | `run()` completes | End of life |

---

### The Golden Rule

> **A thread starts in NEW, moves to RUNNABLE when started, cycles through various waiting states, and ends in TERMINATED. You cannot restart a terminated thread.**

**Memory trick:**
```
NEW = Born
RUNNABLE = Working
BLOCKED/WAITING = Waiting
TERMINATED = Dead
```

Would you like me to explain **how to create threads** (extends Thread vs implements Runnable) or **synchronization** next?