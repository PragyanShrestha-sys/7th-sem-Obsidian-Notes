Here's a **complete theoretical explanation** of all the event types you listed. 

## note: maile ni yo ramrari hereko chaina sir ko slides ma ni herda ta huncha concept chai bujhye tara need to practice 

[[shorter version (Have not checked)]]



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

| User Action | Event Type | Listener |
|-------------|------------|----------|
| Clicking a button | ActionEvent | ActionListener |
| Pressing a key | KeyEvent | KeyListener |
| Clicking a mouse | MouseEvent | MouseListener |
| Closing a window | WindowEvent | WindowListener |
| Selecting a checkbox | ItemEvent | ItemListener |
| Focusing on a field | FocusEvent | FocusListener |

---

## 1. Action Events (ActionEvent)

**What it is:** The most common event - occurs when user performs an "action" on a component.

| When does it occur? | Components that trigger it |
|---------------------|---------------------------|
| Button clicked | JButton |
| Menu item selected | JMenuItem |
| Checkbox/radio button selected | JCheckBox, JRadioButton |
| Enter pressed in text field | JTextField |

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
                
                // Check for modifier keys
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

| Key Code | Description |
|----------|-------------|
| `VK_ENTER` | Enter key |
| `VK_SPACE` | Space bar |
| `VK_ESCAPE` | Escape key |
| `VK_BACK_SPACE` | Backspace |
| `VK_TAB` | Tab key |
| `VK_A` ... `VK_Z` | Letter keys |
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
        JPanel panel = new JPanel(new GridLayout(3, 2, 10, 10));
        
        JLabel nameLabel = new JLabel("Name:");
        JTextField nameField = new JTextField(15);
        
        JLabel emailLabel = new JLabel("Email:");
        JTextField emailField = new JTextField(15);
        
        JLabel ageLabel = new JLabel("Age:");
        JTextField ageField = new JTextField(5);
        
        // Add focus listeners
        nameField.addFocusListener(new FocusAdapter() {
            @Override
            public void focusGained(FocusEvent e) {
                nameField.setBackground(Color.YELLOW);
                System.out.println("Name field focused");
            }
            
            @Override
            public void focusLost(FocusEvent e) {
                nameField.setBackground(Color.WHITE);
                if (nameField.getText().isEmpty()) {
                    nameField.setBackground(Color.PINK);
                    System.out.println("Name is required!");
                }
            }
        });
        
        emailField.addFocusListener(new FocusAdapter() {
            @Override
            public void focusGained(FocusEvent e) {
                emailField.setBackground(Color.YELLOW);
            }
            
            @Override
            public void focusLost(FocusEvent e) {
                emailField.setBackground(Color.WHITE);
                String email = emailField.getText();
                if (!email.contains("@")) {
                    emailField.setBackground(Color.PINK);
                    System.out.println("Invalid email!");
                }
            }
        });
        
        // Temporary focus (opposite component)
        ageField.addFocusListener(new FocusAdapter() {
            @Override
            public void focusLost(FocusEvent e) {
                // Check if focus is moving to another component
                if (e.isTemporary()) {
                    System.out.println("Temporary focus loss");
                } else {
                    System.out.println("Permanent focus loss");
                }
            }
        });
        
        panel.add(nameLabel);
        panel.add(nameField);
        panel.add(emailLabel);
        panel.add(emailField);
        panel.add(ageLabel);
        panel.add(ageField);
        
        frame.add(panel);
        frame.setSize(400, 200);
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

| When does it occur? | Method in MouseListener | MouseMotionListener |
|---------------------|------------------------|---------------------|
| Mouse clicked (press + release) | `mouseClicked(MouseEvent e)` | |
| Mouse button pressed | `mousePressed(MouseEvent e)` | |
| Mouse button released | `mouseReleased(MouseEvent e)` | |
| Mouse enters component | `mouseEntered(MouseEvent e)` | |
| Mouse exits component | `mouseExited(MouseEvent e)` | |
| Mouse moves (no button) | | `mouseMoved(MouseEvent e)` |
| Mouse drags (button pressed) | | `mouseDragged(MouseEvent e)` |

### Example: MouseEvent

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class MouseEventDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("MouseEvent Demo");
        
        JPanel panel = new JPanel();
        panel.setPreferredSize(new Dimension(400, 300));
        panel.setBackground(Color.LIGHT_GRAY);
        
        JLabel statusLabel = new JLabel("Move mouse over panel");
        
        // MouseListener for clicks, enter, exit
        panel.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                int clicks = e.getClickCount();
                if (clicks == 2) {
                    statusLabel.setText("Double-click at (" + e.getX() + ", " + e.getY() + ")");
                } else {
                    statusLabel.setText("Click at (" + e.getX() + ", " + e.getY() + ")");
                }
                
                // Check which button was clicked
                if (SwingUtilities.isLeftMouseButton(e)) {
                    System.out.println("Left button");
                } else if (SwingUtilities.isRightMouseButton(e)) {
                    System.out.println("Right button - popup menu");
                }
            }
            
            @Override
            public void mouseEntered(MouseEvent e) {
                panel.setBackground(Color.CYAN);
                statusLabel.setText("Mouse entered panel");
            }
            
            @Override
            public void mouseExited(MouseEvent e) {
                panel.setBackground(Color.LIGHT_GRAY);
                statusLabel.setText("Mouse exited panel");
            }
        });
        
        // MouseMotionListener for move and drag
        panel.addMouseMotionListener(new MouseMotionAdapter() {
            @Override
            public void mouseMoved(MouseEvent e) {
                statusLabel.setText("Position: (" + e.getX() + ", " + e.getY() + ")");
            }
            
            @Override
            public void mouseDragged(MouseEvent e) {
                statusLabel.setText("Dragging at (" + e.getX() + ", " + e.getY() + ")");
                panel.setBackground(Color.ORANGE);
            }
        });
        
        frame.setLayout(new BorderLayout());
        frame.add(panel, BorderLayout.CENTER);
        frame.add(statusLabel, BorderLayout.SOUTH);
        
        frame.pack();
        frame.setVisible(true);
    }
}
```

### Useful MouseEvent Methods

| Method | What it returns |
|--------|-----------------|
| `getX()`, `getY()` | Mouse coordinates relative to component |
| `getClickCount()` | Number of clicks (1 = single, 2 = double) |
| `isPopupTrigger()` | Whether this event should show a popup menu |
| `SwingUtilities.isLeftMouseButton(e)` | Checks if left button |
| `SwingUtilities.isRightMouseButton(e)` | Checks if right button |

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

public class WindowEventDemo extends JFrame {
    
    private JTextArea logArea;
    
    public WindowEventDemo() {
        setTitle("WindowEvent Demo");
        setSize(500, 400);
        
        logArea = new JTextArea();
        logArea.setEditable(false);
        add(new JScrollPane(logArea));
        
        // Add window listener
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowOpened(WindowEvent e) {
                log("Window opened");
            }
            
            @Override
            public void windowClosing(WindowEvent e) {
                log("Window closing (user clicked X)");
                int confirm = JOptionPane.showConfirmDialog(WindowEventDemo.this,
                    "Do you want to save before closing?",
                    "Confirm Exit",
                    JOptionPane.YES_NO_CANCEL_OPTION);
                
                if (confirm == JOptionPane.YES_OPTION) {
                    log("Save and exit");
                    System.exit(0);
                } else if (confirm == JOptionPane.NO_OPTION) {
                    log("Exit without saving");
                    System.exit(0);
                }
                // Cancel - don't exit
            }
            
            @Override
            public void windowClosed(WindowEvent e) {
                log("Window closed");
            }
            
            @Override
            public void windowIconified(WindowEvent e) {
                log("Window minimized");
            }
            
            @Override
            public void windowDeiconified(WindowEvent e) {
                log("Window restored");
            }
            
            @Override
            public void windowActivated(WindowEvent e) {
                log("Window activated (gained focus)");
            }
            
            @Override
            public void windowDeactivated(WindowEvent e) {
                log("Window deactivated (lost focus)");
            }
        });
        
        setVisible(true);
    }
    
    private void log(String message) {
        logArea.append(message + "\n");
        System.out.println(message);
    }
    
    public static void main(String[] args) {
        new WindowEventDemo();
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
import java.awt.*;
import java.awt.event.*;

public class ItemEventDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("ItemEvent Demo");
        JPanel panel = new JPanel();
        panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS));
        
        JLabel statusLabel = new JLabel("Select options above");
        
        // Checkboxes
        JCheckBox boldCheck = new JCheckBox("Bold");
        JCheckBox italicCheck = new JCheckBox("Italic");
        
        // Radio buttons (in a group)
        JRadioButton redRadio = new JRadioButton("Red");
        JRadioButton greenRadio = new JRadioButton("Green");
        JRadioButton blueRadio = new JRadioButton("Blue");
        
        ButtonGroup colorGroup = new ButtonGroup();
        colorGroup.add(redRadio);
        colorGroup.add(greenRadio);
        colorGroup.add(blueRadio);
        
        // Combo box
        String[] sizes = {"Small", "Medium", "Large"};
        JComboBox<String> sizeCombo = new JComboBox<>(sizes);
        
        // ItemListener for checkboxes
        ItemListener checkListener = e -> {
            String item = (String) e.getItem();
            int state = e.getStateChange();
            
            if (state == ItemEvent.SELECTED) {
                statusLabel.setText(item + " selected");
            } else {
                statusLabel.setText(item + " deselected");
            }
        };
        
        boldCheck.addItemListener(checkListener);
        italicCheck.addItemListener(checkListener);
        
        // ItemListener for radio buttons
        ItemListener radioListener = e -> {
            if (e.getStateChange() == ItemEvent.SELECTED) {
                statusLabel.setText("Color changed to: " + e.getItem());
            }
        };
        
        redRadio.addItemListener(radioListener);
        greenRadio.addItemListener(radioListener);
        blueRadio.addItemListener(radioListener);
        
        // ItemListener for combo box
        sizeCombo.addItemListener(e -> {
            if (e.getStateChange() == ItemEvent.SELECTED) {
                statusLabel.setText("Size selected: " + e.getItem());
            }
        });
        
        // Add components to panel
        panel.add(new JLabel("Text Style:"));
        panel.add(boldCheck);
        panel.add(italicCheck);
        
        panel.add(Box.createVerticalStrut(10));
        panel.add(new JLabel("Text Color:"));
        panel.add(redRadio);
        panel.add(greenRadio);
        panel.add(blueRadio);
        
        panel.add(Box.createVerticalStrut(10));
        panel.add(new JLabel("Font Size:"));
        panel.add(sizeCombo);
        
        panel.add(Box.createVerticalStrut(20));
        panel.add(statusLabel);
        
        frame.add(panel);
        frame.setSize(300, 400);
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

## Complete Example: Form with All Event Types

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class CompleteEventDemo extends JFrame {
    
    private JTextArea logArea;
    private JTextField nameField;
    private JCheckBox subscribeCheck;
    private JRadioButton maleRadio, femaleRadio;
    private JComboBox<String> countryCombo;
    
    public CompleteEventDemo() {
        setTitle("Complete Event Handling Demo");
        setSize(600, 500);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Create main panel
        JPanel mainPanel = new JPanel(new BorderLayout(10, 10));
        mainPanel.setBorder(BorderFactory.createEmptyBorder(10, 10, 10, 10));
        
        // Form panel
        JPanel formPanel = new JPanel(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5);
        gbc.anchor = GridBagConstraints.WEST;
        
        // Name field with focus and key events
        gbc.gridx = 0; gbc.gridy = 0;
        formPanel.add(new JLabel("Name:"), gbc);
        gbc.gridx = 1;
        nameField = new JTextField(15);
        formPanel.add(nameField, gbc);
        
        nameField.addFocusListener(new FocusAdapter() {
            public void focusGained(FocusEvent e) {
                log("Focus gained: Name field");
                nameField.setBackground(Color.YELLOW);
            }
            public void focusLost(FocusEvent e) {
                log("Focus lost: Name field");
                nameField.setBackground(Color.WHITE);
                if (nameField.getText().isEmpty()) {
                    log("WARNING: Name is required!");
                }
            }
        });
        
        nameField.addKeyListener(new KeyAdapter() {
            public void keyPressed(KeyEvent e) {
                if (e.getKeyCode() == KeyEvent.VK_ENTER) {
                    log("Enter pressed in name field");
                }
            }
        });
        
        // Checkbox with item event
        gbc.gridx = 0; gbc.gridy = 1;
        formPanel.add(new JLabel("Subscribe:"), gbc);
        gbc.gridx = 1;
        subscribeCheck = new JCheckBox("Receive newsletter");
        formPanel.add(subscribeCheck, gbc);
        
        subscribeCheck.addItemListener(e -> {
            if (e.getStateChange() == ItemEvent.SELECTED) {
                log("Subscribed to newsletter");
            } else {
                log("Unsubscribed from newsletter");
            }
        });
        
        // Radio buttons with item event
        gbc.gridx = 0; gbc.gridy = 2;
        formPanel.add(new JLabel("Gender:"), gbc);
        gbc.gridx = 1;
        JPanel genderPanel = new JPanel(new FlowLayout(FlowLayout.LEFT));
        maleRadio = new JRadioButton("Male");
        femaleRadio = new JRadioButton("Female");
        ButtonGroup genderGroup = new ButtonGroup();
        genderGroup.add(maleRadio);
        genderGroup.add(femaleRadio);
        genderPanel.add(maleRadio);
        genderPanel.add(femaleRadio);
        formPanel.add(genderPanel, gbc);
        
        ItemListener genderListener = e -> {
            if (e.getStateChange() == ItemEvent.SELECTED) {
                log("Gender selected: " + e.getItem());
            }
        };
        maleRadio.addItemListener(genderListener);
        femaleRadio.addItemListener(genderListener);
        
        // Combo box with item and action events
        gbc.gridx = 0; gbc.gridy = 3;
        formPanel.add(new JLabel("Country:"), gbc);
        gbc.gridx = 1;
        String[] countries = {"Select Country", "USA", "UK", "Canada", "Australia"};
        countryCombo = new JComboBox<>(countries);
        formPanel.add(countryCombo, gbc);
        
        countryCombo.addItemListener(e -> {
            if (e.getStateChange() == ItemEvent.SELECTED && 
                countryCombo.getSelectedIndex() > 0) {
                log("Country selected: " + e.getItem());
            }
        });
        
        // Buttons with action events
        JPanel buttonPanel = new JPanel(new FlowLayout());
        JButton submitButton = new JButton("Submit");
        JButton clearButton = new JButton("Clear");
        JButton closeButton = new JButton("Close");
        
        submitButton.addActionListener(e -> {
            log("SUBMIT clicked");
            validateAndSubmit();
        });
        
        clearButton.addActionListener(e -> {
            log("CLEAR clicked");
            clearForm();
        });
        
        closeButton.addActionListener(e -> {
            log("CLOSE clicked");
            System.exit(0);
        });
        
        buttonPanel.add(submitButton);
        buttonPanel.add(clearButton);
        buttonPanel.add(closeButton);
        
        // Log area
        logArea = new JTextArea(10, 40);
        logArea.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(logArea);
        scrollPane.setBorder(BorderFactory.createTitledBorder("Event Log"));
        
        // Mouse events on log area
        logArea.addMouseListener(new MouseAdapter() {
            public void mouseEntered(MouseEvent e) {
                logArea.setBackground(Color.CYAN);
            }
            public void mouseExited(MouseEvent e) {
                logArea.setBackground(Color.WHITE);
            }
        });
        
        // Assemble
        mainPanel.add(formPanel, BorderLayout.NORTH);
        mainPanel.add(buttonPanel, BorderLayout.CENTER);
        mainPanel.add(scrollPane, BorderLayout.SOUTH);
        
        add(mainPanel);
        setVisible(true);
    }
    
    private void log(String message) {
        java.text.SimpleDateFormat sdf = new java.text.SimpleDateFormat("HH:mm:ss");
        String timestamp = sdf.format(new java.util.Date());
        logArea.append("[" + timestamp + "] " + message + "\n");
        System.out.println(message);
    }
    
    private void validateAndSubmit() {
        StringBuilder errors = new StringBuilder();
        
        if (nameField.getText().trim().isEmpty()) {
            errors.append("- Name is required\n");
        }
        
        if (!maleRadio.isSelected() && !femaleRadio.isSelected()) {
            errors.append("- Gender must be selected\n");
        }
        
        if (countryCombo.getSelectedIndex() == 0) {
            errors.append("- Country must be selected\n");
        }
        
        if (errors.length() > 0) {
            log("VALIDATION FAILED:\n" + errors.toString());
            JOptionPane.showMessageDialog(this, errors.toString(), 
                "Validation Error", JOptionPane.ERROR_MESSAGE);
        } else {
            log("VALIDATION SUCCESS! Form submitted.");
            JOptionPane.showMessageDialog(this, "Form submitted successfully!");
        }
    }
    
    private void clearForm() {
        nameField.setText("");
        subscribeCheck.setSelected(false);
        maleRadio.setSelected(false);
        femaleRadio.setSelected(false);
        countryCombo.setSelectedIndex(0);
        log("Form cleared");
    }
    
    public static void main(String[] args) {
        new CompleteEventDemo();
    }
}
```

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