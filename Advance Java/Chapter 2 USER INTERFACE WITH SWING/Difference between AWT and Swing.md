Here's a **clear, simple comparison** between AWT and Swing.

---

## Quick Summary

| Aspect                   | AWT                       | Swing                        |
| ------------------------ | ------------------------- | ---------------------------- |
| **Full form**            | Abstract Window Toolkit   | No full form (just "Swing")  |
| **Introduced in**        | Java 1.0 (1995)           | Java 1.2 (1998)              |
| **Components**           | Heavyweight               | Lightweight                  |
| **Look & Feel**          | OS-dependent (native)     | Same across all platforms    |
| **Number of components** | Few (basic only)          | Many (rich components)       |
| **Speed**                | Faster                    | Slightly slower              |
| **Package**              | `java.awt`                | `javax.swing`                |
| **Component prefix**     | No prefix (Button, Frame) | "J" prefix (JButton, JFrame) |
| **Current status**       | Legacy (old)              | Modern (current)             |

---

## Main Differences (Detailed)

### 1. Heavyweight vs Lightweight

| AWT (Heavyweight) | Swing (Lightweight) |
|-------------------|---------------------|
| Uses real OS component | Java draws the component |
| OS manages it completely | Java manages it |
| More memory usage | Less memory usage |
| Slower to create | Faster to create |
| Each button = real OS button | Each button = drawn by Java |

```java
// AWT - creates REAL Windows/Mac/Linux button
Button awtButton = new Button("Click");

// Swing - Java DRAWS the button
JButton swingButton = new JButton("Click");
```

**Analogy:**
```
AWT = Renting a fully furnished apartment (OS provides everything)
Swing = Building your own furniture (Java creates it)
```

---

### 2. Look and Feel

| AWT | Swing |
|-----|-------|
| Native look (matches OS) | Same look everywhere (pluggable) |
| Windows: looks like Windows | Windows: looks like Java's style |
| Mac: looks like Mac | Mac: looks like Java's style |
| Linux: looks like Linux | Linux: looks like Java's style |

**Visual example:**

```
AWT Button on Windows:  [  OK  ]  (Windows style)
AWT Button on Mac:      [  OK  ]  (Mac style - rounder)

Swing Button on Windows: [  OK  ]  (Same style)
Swing Button on Mac:     [  OK  ]  (Same style)
```

---

### 3. Components Available

| Component Type | AWT | Swing |
|----------------|-----|-------|
| Button | ✅ Button | ✅ JButton |
| Label | ✅ Label | ✅ JLabel |
| Text Field | ✅ TextField | ✅ JTextField |
| Checkbox | ✅ Checkbox | ✅ JCheckBox |
| List | ✅ List | ✅ JList |
| Table | ❌ No | ✅ JTable |
| Tree | ❌ No | ✅ JTree |
| Slider | ❌ No | ✅ JSlider |
| Progress Bar | ❌ No | ✅ JProgressBar |
| Tabbed Pane | ❌ No | ✅ JTabbedPane |
| Color Picker | ❌ No | ✅ JColorChooser |
| File Chooser | ❌ No | ✅ JFileChooser |

**Swing has MANY more components!**

---

### 4. Package and Naming

| AWT | Swing |
|-----|-------|
| `import java.awt.*;` | `import javax.swing.*;` |
| `Button btn = new Button();` | `JButton btn = new JButton();` |
| `Frame f = new Frame();` | `JFrame f = new JFrame();` |
| `Panel p = new Panel();` | `JPanel p = new JPanel();` |
| `TextField tf = new TextField();` | `JTextField tf = new JTextField();` |

**Memory trick:** Swing components start with letter **"J"** (JButton, JFrame, JPanel)

---

### 5. Platform Independence

| AWT | Swing |
|-----|-------|
| Less platform independent | More platform independent |
| Depends on OS's GUI capabilities | No dependency on OS |
| May behave differently on different OS | Behaves identically everywhere |

---

### 6. MVC Pattern Support

| AWT | Swing |
|-----|-------|
| Does not use MVC | Uses MVC pattern |
| Simple architecture | Model-View-Controller architecture |

**MVC = Model-View-Controller** (separates data, display, and logic)

---

### 7. Code Example Comparison

**Same program in AWT:**
```java
import java.awt.*;

public class AWTExample {
    public static void main(String[] args) {
        Frame frame = new Frame("AWT Window");
        Button button = new Button("Click Me");
        Label label = new Label("Hello AWT");
        
        frame.setLayout(new FlowLayout());
        frame.add(button);
        frame.add(label);
        frame.setSize(300, 200);
        frame.setVisible(true);
    }
}
```

**Same program in Swing:**
```java
import javax.swing.*;

public class SwingExample {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Swing Window");
        JButton button = new JButton("Click Me");
        JLabel label = new JLabel("Hello Swing");
        
        frame.setLayout(new FlowLayout());
        frame.add(button);
        frame.add(label);
        frame.setSize(300, 200);
        frame.setVisible(true);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}
```

**Note:** Swing requires `setDefaultCloseOperation()` to exit properly.

---

## When to Use Which?

| Scenario | Use | Reason |
|----------|-----|--------|
| **New desktop application** | Swing | More components, consistent look |
| **Learning GUI programming** | Swing | Modern, still used |
| **Very limited devices** | AWT | Lightweight (historically) |
| **Maintaining old code** | AWT | Legacy code exists |
| **Modern professional apps** | Swing or JavaFX | Industry standard |

---

## Quick Comparison Table

| Feature | AWT | Swing |
|---------|-----|-------|
| Release year | 1995 | 1998 |
| Components | Heavyweight | Lightweight |
| Look & Feel | Native (OS) | Pluggable (same everywhere) |
| Component count | ~20 | ~50+ |
| Speed | Faster | Slightly slower |
| Memory usage | More | Less |
| Package | java.awt | javax.swing |
| Naming | Button, Frame | JButton, JFrame |
| MVC support | No | Yes |
| Tooltips | No | Yes |
| Icons on buttons | No | Yes |
| Borders | Limited | Many options |
| Current status | Legacy | Active/Modern |

---

## The Golden Rule

> **AWT is the older, OS-dependent GUI toolkit with basic components. Swing is the newer, platform-independent GUI toolkit with rich components. For new projects, ALWAYS use Swing (or JavaFX).**

**Memory trick:**
```
AWT = Old, OS-based, Basic components (Limited)
Swing = New, Self-drawn, Many components (Rich)

"J" before everything = Swing (JButton, JFrame, JPanel)
No "J" = AWT (Button, Frame, Panel)
```

Would you like me to explain **JavaFX** (the even newer GUI toolkit that replaces Swing) next?