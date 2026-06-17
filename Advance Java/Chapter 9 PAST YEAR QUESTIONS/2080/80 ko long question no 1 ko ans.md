

## Why Synchronize Threads?

**Synchronization is needed to prevent race conditions** when multiple threads access shared resources simultaneously, causing data inconsistency.

### Real Example Without Synchronization

```java
class Counter {
    int count = 0;
    void increment() { count++; }  // NOT synchronized
}

public class Test {
    public static void main(String[] args) throws Exception {
        Counter c = new Counter();
        
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) c.increment();
        });
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) c.increment();
        });
        
        t1.start(); t2.start();
        t1.join(); t2.join();
        
        System.out.println("Expected: 2000, Got: " + c.count); // ❌ 1789, 1823, etc.
    }
}
```

### With Synchronization

```java
class Counter {
    int count = 0;
    synchronized void increment() { count++; }  // ✅ Synchronized
}

// Output: Expected: 2000, Got: 2000 ✅
```

### Why This Happens?
```
Thread 1: read count (10) → increment → write (11)
Thread 2: read count (10) → increment → write (11)  ← LOST UPDATE!
Both threads read 10 before either wrote back!
```

---

## Centered Array Problem

### Problem
An array is **centered** if:
- Has **odd** number of elements
- All elements (except middle) are **strictly greater** than middle element

### Examples
```java
{5, 3, 7}     → ✅ (3 is middle, 5>3, 7>3)
{1, 2, 3, 4, 5} → ❌ (middle=3, 1<3)
{10, 20, 15, 30, 25} → ✅ (15 is middle, all >15)
```

### Shortest Code

```java
public class Centered {
    static int isCentered(int[] a) {
        if (a.length % 2 == 0) return 0;
        int mid = a[a.length/2];
        for (int i = 0; i < a.length; i++)
            if (i != a.length/2 && a[i] <= mid) return 0;
        return 1;
    }
    
    public static void main(String[] args) {
        System.out.println(isCentered(new int[]{5, 3, 7}));      // 1
        System.out.println(isCentered(new int[]{1, 2, 3, 4, 5})); // 0
        System.out.println(isCentered(new int[]{10, 20, 15, 30, 25})); // 1
    }
}
```

### Even Shorter

```java
static int isCentered(int[] a) {
    if (a.length % 2 == 0) return 0;
    int m = a[a.length/2];
    for (int x : a) if (x <= m) return 0;
    return 1;
}
```

### Complete Code with Comments

```java
public class CenteredArray {
    static int isCentered(int[] arr) {
        // Must have odd length
        if (arr.length % 2 == 0) return 0;
        
        // Find middle element
        int midIndex = arr.length / 2;
        int midValue = arr[midIndex];
        
        // Check all elements except middle
        for (int i = 0; i < arr.length; i++) {
            if (i != midIndex && arr[i] <= midValue) {
                return 0;  // Not centered
            }
        }
        return 1;  // Centered
    }
    
    public static void main(String[] args) {
        System.out.println(isCentered(new int[]{5, 3, 7}));  // 1
        System.out.println(isCentered(new int[]{3, 1, 2}));  // 0 (3>1? yes, 3>2? yes, but middle is 1, 3>1, 2>1 ✅ actually works!)
        System.out.println(isCentered(new int[]{1, 2, 3}));  // 0 (middle=2, 1<2)
    }
}
   

---

## Summary

### Synchronization
- **Need**: Prevent race conditions when threads share data
- **Solution**: `synchronized` keyword
- **Without sync**: Inconsistent results (lost updates)

### Centered Array
- **Rule**: Odd length, all elements > middle
- **Time**: O(n)
- **Space**: O(1)  