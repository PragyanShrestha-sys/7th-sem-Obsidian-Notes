

**What is a Listener Interface?** An interface that declares methods for handling specific events.

| Listener Interface | Methods                                                                                  | When called                   |
| ------------------ | ---------------------------------------------------------------------------------------- | ----------------------------- |
| `ActionListener`   | `actionPerformed(ActionEvent e)`                                                         | Button clicked, menu selected |
| `MouseListener`    | `mouseClicked()`, `mousePressed()`, `mouseReleased()`, `mouseEntered()`, `mouseExited()` | Mouse actions                 |
| `KeyListener`      | `keyPressed()`, `keyReleased()`, `keyTyped()`                                            | Keyboard actions              |
| `ItemListener`     | `itemStateChanged(ItemEvent e)`                                                          | Checkbox toggled              |
| `FocusListener`    | `focusGained()`, `focusLost()`                                                           | Focus changes                 |
Note: 
`FocusListener` activates only when a component gains or loses **keyboard focus**—typically through:
- Tab key navigation
- Clicking on a focusable component (e.g., `JTextField`, `JButton`)
- Programmatically calling `requestFocus()`
### Example: ActionListener

```java
import javax.swing.*;
import java.awt.event.*;

public class ListenerExample {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Listener Demo");
        JButton button = new JButton("Click Me");
        
        // Implementing ActionListener as anonymous class
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("Button clicked!");
            }
        });
        
        frame.add(button);
        frame.setSize(300, 200);
        frame.setVisible(true);
    }
}
```

### Example: Multiple Listeners (Same component can have multiple listeners)

```java
JButton button = new JButton("Save");

// Listener 1: Save to file
button.addActionListener(e -> saveToFile());

// Listener 2: Update status bar
button.addActionListener(e -> updateStatus("Saved!"));

// Listener 3: Play sound
button.addActionListener(e -> playSound());

// All three run when button is clicked!
```

### Example: Different Event Types

```java
JButton button = new JButton("Hover Me");

// Action listener (click)
button.addActionListener(e -> System.out.println("Clicked!"));

// Mouse listener (hover, enter, exit)
button.addMouseListener(new MouseAdapter() {
    public void mouseEntered(MouseEvent e) {
        button.setBackground(Color.YELLOW);
    }
    public void mouseExited(MouseEvent e) {
        button.setBackground(null);
    }
});
```

---
