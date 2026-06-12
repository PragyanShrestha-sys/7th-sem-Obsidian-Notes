
Here's a **concise exam-friendly explanation** with shorter code examples for each event type.

---

## Event Handling - Quick Reference for Exams

**What is Event Handling?** Mechanism that responds to user actions (clicks, typing, etc.) in GUI programs.

**Three Components:**
1. **Event Source** - Component that triggers event (Button, TextField)
2. **Event Object** - Carries event information (ActionEvent, MouseEvent)
3. **Event Listener** - Handles the event (ActionListener, MouseListener)

---

## 1. ActionEvent (Button Click, Menu Select)

```java
button.addActionListener(e -> {
    System.out.println("Button clicked");
    String cmd = e.getActionCommand();  // Gets button text or custom command
});
```

**When used:** Button clicks, menu selection, Enter in text field

---

## 2. KeyEvent (Keyboard Input)

```java
textField.addKeyListener(new KeyAdapter() {
    public void keyPressed(KeyEvent e) {
        if (e.getKeyCode() == KeyEvent.VK_ENTER) {
            System.out.println("Enter pressed");
        }
    }
});
```

**Common key codes:** `VK_ENTER`, `VK_ESCAPE`, `VK_A` to `VK_Z`, `VK_F1` to `VK_F12`

**Methods:** `getKeyCode()`, `getKeyChar()`, `isControlDown()`

---

## 3. FocusEvent (Field Active/Inactive)

```java
textField.addFocusListener(new FocusAdapter() {
    public void focusGained(FocusEvent e) {
        textField.setBackground(Color.YELLOW);  // Highlight active field
    }
    public void focusLost(FocusEvent e) {
        textField.setBackground(Color.WHITE);   // Remove highlight
    }
});
```

**When used:** Form validation, highlighting active field

---

## 4. MouseEvent (Mouse Clicks, Movement)

```java
panel.addMouseListener(new MouseAdapter() {
    public void mouseClicked(MouseEvent e) {
        System.out.println("Clicked at (" + e.getX() + "," + e.getY() + ")");
        
        if (e.getClickCount() == 2) {
            System.out.println("Double click");
        }
    }
    
    public void mouseEntered(MouseEvent e) {
        panel.setBackground(Color.CYAN);  // Hover effect
    }
});
```

**Methods:** `getX()`, `getY()`, `getClickCount()`, `isPopupTrigger()`

---

## 5. WindowEvent (Window Close, Minimize)

```java
frame.addWindowListener(new WindowAdapter() {
    public void windowClosing(WindowEvent e) {
        int confirm = JOptionPane.showConfirmDialog(frame, "Exit?");
        if (confirm == JOptionPane.YES_OPTION) {
            System.exit(0);
        }
    }
});
```

**When used:** Save confirmation before closing, cleanup operations

---

## 6. ItemEvent (Checkbox, Radio Button)

```java
checkBox.addItemListener(e -> {
    if (e.getStateChange() == ItemEvent.SELECTED) {
        System.out.println("Checked");
    } else {
        System.out.println("Unchecked");
    }
});
```

**Methods:** `getItem()`, `getStateChange()` (SELECTED or DESELECTED)

---

## Complete Compact Example (Exam Ready)

```java
import javax.swing.*;
import java.awt.event.*;

public class EventDemo extends JFrame {
    
    public EventDemo() {
        setTitle("Event Demo");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(null);
        
        // Button - ActionEvent
        JButton btn = new JButton("Click");
        btn.setBounds(50, 50, 100, 30);
        btn.addActionListener(e -> System.out.println("Button clicked"));
        add(btn);
        
        // TextField - KeyEvent + FocusEvent
        JTextField tf = new JTextField();
        tf.setBounds(50, 100, 150, 30);
        tf.addKeyListener(new KeyAdapter() {
            public void keyPressed(KeyEvent e) {
                if (e.getKeyCode() == KeyEvent.VK_ENTER)
                    System.out.println("Enter: " + tf.getText());
            }
        });
        tf.addFocusListener(new FocusAdapter() {
            public void focusGained(FocusEvent e) {
                tf.setBackground(Color.YELLOW);
            }
            public void focusLost(FocusEvent e) {
                tf.setBackground(Color.WHITE);
            }
        });
        add(tf);
        
        // CheckBox - ItemEvent
        JCheckBox chk = new JCheckBox("Accept Terms");
        chk.setBounds(50, 150, 150, 30);
        chk.addItemListener(e -> {
            System.out.println(e.getStateChange() == ItemEvent.SELECTED ? 
                               "Selected" : "Deselected");
        });
        add(chk);
        
        // Panel - MouseEvent
        JPanel panel = new JPanel();
        panel.setBounds(50, 200, 150, 50);
        panel.setBackground(Color.LIGHT_GRAY);
        panel.addMouseListener(new MouseAdapter() {
            public void mouseEntered(MouseEvent e) {
                panel.setBackground(Color.CYAN);
            }
            public void mouseExited(MouseEvent e) {
                panel.setBackground(Color.LIGHT_GRAY);
            }
        });
        add(panel);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new EventDemo();
    }
}
```

---

## Quick Comparison Table (For Exams)

| Event | Listener | Method | When |
|-------|----------|--------|------|
| Action | ActionListener | `actionPerformed(ActionEvent e)` | Button click |
| Key | KeyListener | `keyPressed(KeyEvent e)` | Key press |
| Focus | FocusListener | `focusGained(FocusEvent e)` | Field active |
| Mouse | MouseListener | `mouseClicked(MouseEvent e)` | Mouse click |
| Window | WindowListener | `windowClosing(WindowEvent e)` | Window close |
| Item | ItemListener | `itemStateChanged(ItemEvent e)` | Checkbox toggle |

---

## Key Points for Exams

1. **Adapter classes** (`MouseAdapter`, `KeyAdapter`, `WindowAdapter`) let you override only needed methods (useful for interfaces with multiple methods)

2. **Action Command** - String identifier for component: `button.setActionCommand("SAVE")`

3. **Lambda expressions** simplify single-method listeners: `e -> method()`

4. **`e.getSource()`** returns the component that triggered the event

5. **`e.consume()`** prevents default behavior (like typing invalid characters)