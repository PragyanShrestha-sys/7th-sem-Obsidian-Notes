
```java
public class ThreadStatesDemo {
    public static void main(String[] args) throws InterruptedException {
        
        Object lock = new Object();
        
        // Thread 1: NEW state
        Thread t1 = new Thread(() -> {
            synchronized(lock) {
                System.out.println("Thread 1 running");
            }
        });
        System.out.println("1. NEW: " + t1.getState());  // NEW
        
        // Thread 2: RUNNABLE state
        t1.start();
        System.out.println("2. RUNNABLE: " + t1.getState());  // RUNNABLE
        
        // Thread 3: BLOCKED state
        Thread t2 = new Thread(() -> {
            synchronized(lock) {
                try { Thread.sleep(100); } catch (Exception e) {}
            }
        });
        t2.start();
        
        Thread t3 = new Thread(() -> {
            synchronized(lock) {
                System.out.println("Thread 3 got lock");
            }
        });
        t3.start();
        
        Thread.sleep(10);
        System.out.println("3. BLOCKED (maybe): " + t3.getState());  // BLOCKED
        
        // Thread 4: WAITING state
        Thread t4 = new Thread(() -> {
            try {
                t1.join();  // Wait for t1 to finish
            } catch (InterruptedException e) {}
        });
        t4.start();
        
        Thread.sleep(10);
        System.out.println("4. WAITING: " + t4.getState());  // WAITING
        
        // Thread 5: TIMED_WAITING state
        Thread t5 = new Thread(() -> {
            try {
                Thread.sleep(5000);
            } catch (InterruptedException e) {}
        });
        t5.start();
        
        Thread.sleep(10);
        System.out.println("5. TIMED_WAITING: " + t5.getState());  // TIMED_WAITING
        
        // Wait for t1 to finish
        t1.join();
        System.out.println("6. TERMINATED: " + t1.getState());  // TERMINATED
    }
}
```
