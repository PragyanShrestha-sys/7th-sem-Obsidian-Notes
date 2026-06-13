Here's a **complete comparison table** of all the differences between Event Listener and Adapter Class. changes in java

---

## Complete Difference Table

| Point of Difference                     | Event Listener                      | Adapter Class                              |
| --------------------------------------- | ----------------------------------- | ------------------------------------------ |
| **Type**                                | Interface                           | Abstract Class                             |
| **Keyword to use**                      | `implements`                        | `extends`                                  |
| **Method bodies**                       | All methods are abstract (no body)  | All methods have empty body implementation |
| **Number of methods you must override** | ALL methods                         | ONLY methods you need                      |
| **Can instantiate directly?**           | ❌ No (must implement first)         | ❌ No (must extend first)                   |
| **Exists for multi-method listeners?**  | ✅ Yes (e.g., MouseListener)         | ✅ Yes (e.g., MouseAdapter)                 |
| **Code length**                         | Longer (must implement all methods) | Shorter (override only needed)             |
| **When to use**                         | Need to implement all methods       | Need only few methods                      |
| **Multiple inheritance**                | Can implement multiple listeners    | Can extend only one adapter                |
| **Lambda support**                      | ✅ Yes (functional interfaces)       | ❌ No (not an interface)                    |

---

## Listener vs Adapter Availability

| Event Type | Listener Interface | Adapter Class | Number of Methods |
|------------|-------------------|---------------|-------------------|
| Action Event | `ActionListener` | ❌ No adapter | 1 |
| Mouse Event | `MouseListener` | ✅ `MouseAdapter` | 5 |
| Mouse Motion | `MouseMotionListener` | ✅ `MouseMotionAdapter` | 2 |
| Key Event | `KeyListener` | ✅ `KeyAdapter` | 3 |
| Focus Event | `FocusListener` | ✅ `FocusAdapter` | 2 |
| Window Event | `WindowListener` | ✅ `WindowAdapter` | 7 |
| Item Event | `ItemListener` | ❌ No adapter | 1 |
| Container Event | `ContainerListener` | ✅ `ContainerAdapter` | 2 |

---

## Code Comparison Table

| Aspect | Event Listener | Adapter Class |
|--------|---------------|---------------|
| **Syntax** | `implements MouseListener` | `extends MouseAdapter` |
| **Required methods (Mouse)** | 5 methods | 0 methods (override only what you need) |
| **Empty methods needed** | Yes (for unused methods) | No (inherited empty) |
| **Example** | `public void mouseEntered() { }` | Not needed unless overriding |
| **Line of code (for 1 method)** | ~10 lines | ~5 lines |

---

## Example Comparison

### Using Listener
```java
button.addMouseListener(new MouseListener() {
    public void mouseClicked(MouseEvent e) { }
    public void mousePressed(MouseEvent e) { }
    public void mouseReleased(MouseEvent e) { }
    public void mouseEntered(MouseEvent e) { 
        doSomething();  // Only this matters
    }
    public void mouseExited(MouseEvent e) { }
});
```

### Using Adapter
```java
button.addMouseListener(new MouseAdapter() {
    public void mouseEntered(MouseEvent e) {
        doSomething();  // Only this method!
    }
});
```

---

## Summary Table (One-Line)

| Feature     | Listener                     | Adapter                  |
| ----------- | ---------------------------- | ------------------------ |
| Type        | Interface                    | Abstract Class           |
| Keyword     | `implements`                 | `extends`                |
| Override    | ALL methods                  | NEEDED methods only      |
| Code length | Long                         | Short                    |
| Best for    | Single-method or all methods | Multi-method, few needed |

---

## The Golden Rule

> **Listeners are interfaces that declare event methods. Adapters are classes that provide empty implementations of those methods. Use Adapters when you only need a few methods from a multi-method listener to avoid writing empty methods.**

**Memory trick:**
```
Listener = Menu (lists all dishes)
Adapter = Pre-made empty plate (fill only what you want to eat)

Listener with 1 method → No adapter needed
Listener with many methods → Use adapter to save work
```