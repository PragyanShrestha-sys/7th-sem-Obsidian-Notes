Here's a **complete theoretical explanation** of all the event types you listed. 

## note: maile ni yo ramrari hereko chaina sir ko slides ma ni herda ta huncha concept chai bujhye tara need to practice 

[[shorter version (Have not checked)]]

![[Pasted image 20260615154910.png]]

---

## What is Event Handling? (Quick Recap)

**Event Handling** is the mechanism that makes GUI programs respond to user actions.

```
User does something → Java creates an Event object → Event is sent to Listener → Listener runs your code
```

**Without event handling:** Buttons don't click, keys don't type, windows don't close.

---

## Why Different Event Types?

**Different user actions create different kinds of events.**

| User Action          | Event Type  | Listener       |
| -------------------- | ----------- | -------------- |
| Clicking a button    | ActionEvent | ActionListener |
| Pressing a key       | KeyEvent    | KeyListener    |
| Clicking a mouse     | MouseEvent  | MouseListener  |
| Closing a window     | WindowEvent | WindowListener |
| Selecting a checkbox | ItemEvent   | ItemListener   |
| Focusing on a field  | FocusEvent  | FocusListener  |

---

## 1. Action Events (ActionEvent)

**What it is:** The most common event - occurs when user performs an "action" on a component.

| When does it occur?            | Components that trigger it |
| ------------------------------ | -------------------------- |
| Button clicked                 | JButton                    |
| Menu item selected             | JMenuItem                  |
| Checkbox/radio button selected | JCheckBox, JRadioButton    |
| Enter pressed in text field    | JTextField                 |

### Example: ActionEvent

```java
import javax.swing.*;
import java.awt.event.*;

public class ActionEventDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("ActionEvent Demo");
        JPanel panel = new JPanel();
        
        // Button click
        JButton button = new JButton("Click Me");
        button.addActionListener(e -> {
            System.out.println("Button clicked!");
            System.out.println("Action command: " + e.getActionCommand());
        });
        
        // Text field with Enter key
        JTextField textField = new JTextField(15);
        textField.addActionListener(e -> {
            System.out.println("Enter pressed! Text: " + textField.getText());
        });
        
        // Radio button
        JRadioButton radio = new JRadioButton("Select Me");
        radio.addActionListener(e -> {
            System.out.println("Radio button selected: " + radio.isSelected());
        });
        
        panel.add(button);
        panel.add(textField);
        panel.add(radio);
        
        frame.add(panel);
        frame.setSize(400, 200);
        frame.setVisible(true);
    }
}
```

**Useful ActionEvent methods:**

| Method | What it returns |
|--------|-----------------|
| `getSource()` | The component that triggered the event |
| `getActionCommand()` | The command string associated with the component |
| `getModifiers()` | Modifier keys (Shift, Ctrl, Alt) pressed |
| `getWhen()` | Timestamp of the event |

---

## 2. Key Events (KeyEvent)

**What it is:** Occurs when user presses, releases, or types a key on the keyboard.

| When does it occur?                 | Method in KeyListener     |
| ----------------------------------- | ------------------------- |
| Key is pressed down                 | `keyPressed(KeyEvent e)`  |
| Key is released                     | `keyReleased(KeyEvent e)` |
| Key is typed (pressed and released) | `keyTyped(KeyEvent e)`    |

### Key Codes vs Key Characters

| Concept           | What it is                                | Example                     |
| ----------------- | ----------------------------------------- | --------------------------- |
| **Key Code**      | Physical key on keyboard (VK_A, VK_ENTER) | Same for 'A' and 'a'        |
| **Key Character** | Actual character typed                    | 'A' vs 'a' depends on Shift |

### Example: KeyEvent

```java
import javax.swing.*;
import java.awt.event.*;

public class KeyEventDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("KeyEvent Demo");
        JTextArea textArea = new JTextArea(10, 30);
        
        textArea.addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                System.out.println("Key pressed: " + KeyEvent.getKeyText(e.getKeyCode()));
                
                // Check for modifier keys note: VK = "Virtual Keys"
                if (e.isControlDown() && e.getKeyCode() == KeyEvent.VK_S) {
                    System.out.println("Ctrl+S pressed - Save action!");
                    e.consume(); // Prevent default behavior
                }
                
                // Check for function keys
                if (e.getKeyCode() == KeyEvent.VK_F1) {
                    System.out.println("F1 - Help!");
                }
            }
            
            @Override
            public void keyTyped(KeyEvent e) {
                System.out.println("Character typed: " + e.getKeyChar());
                
                // Allow only digits
                if (!Character.isDigit(e.getKeyChar())) {
                    e.consume(); // Discard non-digit characters
                }
            }
        });
        
        frame.add(new JScrollPane(textArea));
        frame.setSize(400, 300);
        frame.setVisible(true);
    }
}
```

### Useful KeyEvent Methods

| Method | What it does |
|--------|--------------|
| `getKeyCode()` | Returns integer code of the key (VK_A, VK_ENTER) |
| `getKeyChar()` | Returns the character typed (for keyTyped) |
| `getKeyText()` | Returns readable name of the key |
| `isShiftDown()` | Checks if Shift is pressed |
| `isControlDown()` | Checks if Ctrl is pressed |
| `isAltDown()` | Checks if Alt is pressed |
| `consume()` | Prevents default behavior |

### Common Key Codes

| Key Code             | Description   |
| -------------------- | ------------- |
| `VK_ENTER`           | Enter key     |
| `VK_SPACE`           | Space bar     |
| `VK_ESCAPE`          | Escape key    |
| `VK_BACK_SPACE`      | Backspace     |
| `VK_TAB`             | Tab key       |
| `VK_A` ... `VK_Z`    | Letter keys   |
| `VK_F1` ... `VK_F12` | Function keys |

---

## 3. Focus Events (FocusEvent)

**What it is:** Occurs when a component gains or loses keyboard focus.

| When does it occur? | Method in FocusListener |
|---------------------|------------------------|
| Component receives focus | `focusGained(FocusEvent e)` |
| Component loses focus | `focusLost(FocusEvent e)` |

### Example: FocusEvent

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class FocusEventDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("FocusEvent Demo");
        JTextField field1 = new JTextField("Field 1", 15);
        JTextField field2 = new JTextField("Field 2", 15);
        
        // FocusListener example
        field1.addFocusListener(new FocusAdapter() {
            @Override
            public void focusGained(FocusEvent e) {
                field1.setBackground(Color.YELLOW);
                System.out.println("Field 1 - Gained focus");
            }
            
            @Override
            public void focusLost(FocusEvent e) {
                field1.setBackground(Color.WHITE);
                System.out.println("Field 1 - Lost focus");
            }
        });
        
        field2.setName("Field 2");
        field2.addFocusListener(new FocusAdapter() {
            @Override
            public void focusGained(FocusEvent e) {
                field2.setBackground(Color.CYAN);
                System.out.println("Field 2 - Gained focus");
            }
        });
        
        frame.setLayout(new FlowLayout());
        frame.add(field1);
        frame.add(field2);
        frame.setSize(300, 100);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
}
```

### Useful FocusEvent Methods

| Method | What it returns |
|--------|-----------------|
| `isTemporary()` | True if focus loss is temporary (popup, scroll) |
| `getOppositeComponent()` | The component getting/losing focus |

### Common Uses for Focus Events

| Use Case | How it helps |
|----------|--------------|
| **Form validation** | Validate when user leaves a field |
| **Highlighting** | Highlight active field (yellow background) |
| **Error indication** | Show error when user forgets to fill |
| **Auto-format** | Format input (phone, date) when focus lost |

---

## 4. Mouse Events (MouseEvent)

**What it is:** Occurs when user interacts with mouse on a component.

| When does it occur?             | Method in MouseListener       | MouseMotionListener          |
| ------------------------------- | ----------------------------- | ---------------------------- |
| Mouse clicked (press + release) | `mouseClicked(MouseEvent e)`  |                              |
| Mouse button pressed            | `mousePressed(MouseEvent e)`  |                              |
| Mouse button released           | `mouseReleased(MouseEvent e)` |                              |
| Mouse enters component          | `mouseEntered(MouseEvent e)`  |                              |
| Mouse exits component           | `mouseExited(MouseEvent e)`   |                              |
| Mouse moves (no button)         |                               | `mouseMoved(MouseEvent e)`   |
| Mouse drags (button pressed)    |                               | `mouseDragged(MouseEvent e)` |

### Example: MouseEvent

```java
import javax.swing.*;
import java.awt.event.*;

public class MouseEventDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("MouseEvent Demo");
        JPanel panel = new JPanel();
        
        panel.addMouseListener(new MouseAdapter() {
            public void mouseClicked(MouseEvent e) {
                System.out.println("Clicked at: " + e.getX() + ", " + e.getY());
                System.out.println("Clicks: " + e.getClickCount());
            }
            
            public void mouseEntered(MouseEvent e) {
                panel.setBackground(java.awt.Color.YELLOW);
            }
            
            public void mouseExited(MouseEvent e) {
                panel.setBackground(null);
            }
        });
        
        panel.addMouseMotionListener(new MouseMotionAdapter() {
            public void mouseMoved(MouseEvent e) {
                System.out.println("Mouse at: " + e.getX() + ", " + e.getY());
            }
        });
        
        frame.add(panel);
        frame.setSize(300, 200);
        frame.setVisible(true);
    }
}
```

### Useful MouseEvent Methods

| Method                                 | What it returns                             |
| -------------------------------------- | ------------------------------------------- |
| `getX()`, `getY()`                     | Mouse coordinates relative to component     |
| `getClickCount()`                      | Number of clicks (1 = single, 2 = double)   |
| `isPopupTrigger()`                     | Whether this event should show a popup menu |
| `SwingUtilities.isLeftMouseButton(e)`  | Checks if left button                       |
| `SwingUtilities.isRightMouseButton(e)` | Checks if right button                      |

---

## 5. Window Events (WindowEvent)

**What it is:** Occurs when user interacts with a window (frame, dialog).

| When does it occur? | Method in WindowListener |
|---------------------|-------------------------|
| Window opened | `windowOpened(WindowEvent e)` |
| Window closing (user clicked X) | `windowClosing(WindowEvent e)` |
| Window closed | `windowClosed(WindowEvent e)` |
| Window iconified (minimized) | `windowIconified(WindowEvent e)` |
| Window deiconified (restored) | `windowDeiconified(WindowEvent e)` |
| Window activated (gains focus) | `windowActivated(WindowEvent e)` |
| Window deactivated (loses focus) | `windowDeactivated(WindowEvent e)` |

### Example: WindowEvent

```java
import javax.swing.*;
import java.awt.event.*;

public class WindowEventDemo {
    public static void main(String[] args) {
        // Create frame
        JFrame frame = new JFrame("Window Event Demo");
        frame.setSize(300, 200);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Add window listener with all events
        frame.addWindowListener(new WindowAdapter() {
            public void windowOpened(WindowEvent e) {
                System.out.println("Window opened");
            }
            public void windowClosed(WindowEvent e) {
                System.out.println("Window closed");
            }
        });
        
        // Show frame
        frame.setVisible(true);
    }
}
```

### WindowClosing vs WindowClosed

| Event | When it happens |
|-------|-----------------|
| `windowClosing` | User clicks X button (before window closes) |
| `windowClosed` | After window is actually closed |

**Important:** `windowClosed` only happens if you call `dispose()` or `System.exit()`.

---

## 6. Item Events (ItemEvent)

**What it is:** Occurs when item's state changes (checkbox, radio button, combo box).

| When does it occur? | Components |
|---------------------|------------|
| Checkbox selected/deselected | JCheckBox |
| Radio button selected/deselected | JRadioButton |
| Combo box item selected | JComboBox |
| List item selected | JList |

### Example: ItemEvent

```java
import javax.swing.*;
import java.awt.event.*;

public class ItemEventDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("ItemEvent Demo");
        
        JCheckBox checkBox = new JCheckBox("Check me");
        JRadioButton radio = new JRadioButton("Radio me");
        
        // Single listener demonstrating all ItemEvent features
        ItemListener listener = e -> {
            System.out.println("Item: " + e.getItem());
            System.out.println("State: " + (e.getStateChange() == ItemEvent.SELECTED ? "SELECTED" : "DESELECTED"));
            System.out.println("---");
        };
        
        checkBox.addItemListener(listener);
        radio.addItemListener(listener);
        combo.addItemListener(listener);
        
        // Group radio button to behave properly
        ButtonGroup group = new ButtonGroup();
        group.add(radio);
        
        frame.setLayout(new BoxLayout(frame.getContentPane(), BoxLayout.Y_AXIS));
        frame.add(checkBox);
        frame.add(radio);
        frame.add(combo);
        frame.setSize(250, 150);
        frame.setVisible(true);
    }
}
```

### Useful ItemEvent Methods

| Method | What it returns |
|--------|-----------------|
| `getItem()` | The item that was selected/deselected |
| `getStateChange()` | `ItemEvent.SELECTED` or `ItemEvent.DESELECTED` |

---

## Quick Reference Table

| Event Type | Listener | When it occurs | Common Use |
|------------|----------|----------------|-------------|
| **ActionEvent** | ActionListener | Button click, menu select, Enter in text field | Form submission, commands |
| **KeyEvent** | KeyListener | Key press, release, type | Input validation, shortcuts |
| **FocusEvent** | FocusListener | Component gains/loses focus | Form validation, highlighting |
| **MouseEvent** | MouseListener, MouseMotionListener | Mouse click, move, drag, enter, exit | Drawing, popup menus, hover effects |
| **WindowEvent** | WindowListener | Window open, close, minimize, activate | Save on close, cleanup |
| **ItemEvent** | ItemListener | Checkbox/radio/combo selection | Toggle settings, selections |

---

## The Golden Rule

> **Different user actions create different event types. ActionEvent is for "action" components (buttons, menus). KeyEvent handles keyboard input. FocusEvent tracks which component is active. MouseEvent handles all mouse interactions. WindowEvent manages window lifecycle. ItemEvent tracks selection state changes. Choose the right event type for the user interaction you need to handle.**

**Memory trick:**
```
Action = "I did something" (click button)
Key = "I pressed a key" (type text)
Focus = "I'm active now" (click into field)
Mouse = "I moved/clicked mouse" (hover, drag)
Window = "I changed window" (minimize, close)
Item = "I selected something" (check box, radio)
```

Would you like me to explain **how to handle multiple event types together** or **event propagation** next?