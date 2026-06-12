
**What are Adapter Classes?** Classes that provide empty implementations of listener interfaces.

| Problem | Solution |
|---------|----------|
| Listener interfaces have multiple methods | Adapter classes implement all methods with empty bodies |
| You only need 1 or 2 methods | Extend adapter and override only what you need |

### Problem: Without Adapter (Need all methods)

```java
// MouseListener has 5 methods - must implement ALL!
button.addMouseListener(new MouseListener() {
    @Override
    public void mouseClicked(MouseEvent e) { }
    
    @Override
    public void mousePressed(MouseEvent e) { }
    
    @Override
    public void mouseReleased(MouseEvent e) { }
    
    @Override
    public void mouseEntered(MouseEvent e) {
        // Only this one matters to me
        button.setBackground(Color.YELLOW);
    }
    
    @Override
    public void mouseExited(MouseEvent e) { }
});
// So much empty code! 😓
```

### Solution: With Adapter (Override only what you need)

```java
// MouseAdapter implements all 5 methods with empty bodies
button.addMouseListener(new MouseAdapter() {
    @Override
    public void mouseEntered(MouseEvent e) {
        button.setBackground(Color.YELLOW);  // Only override this one
    }
});
// Clean and simple! 😊
```

### Available Adapter Classes

| Listener Interface    | Adapter Class        | Methods in Adapter |
| --------------------- | -------------------- | ------------------ |
| `MouseListener`       | `MouseAdapter`       | 5 empty methods    |
| `MouseMotionListener` | `MouseMotionAdapter` | 2 empty methods    |
| `KeyListener`         | `KeyAdapter`         | 3 empty methods    |
| `FocusListener`       | `FocusAdapter`       | 2 empty methods    |
| `WindowListener`      | `WindowAdapter`      | 7 empty methods    |
| `ContainerListener`   | `ContainerAdapter`   | 2 empty methods    |

### Example: WindowAdapter (Closing window)

```java
// Without adapter (need all 7 methods!)
frame.addWindowListener(new WindowListener() {
    public void windowOpened(WindowEvent e) { }
    public void windowClosing(WindowEvent e) { System.exit(0); }
    public void windowClosed(WindowEvent e) { }
    public void windowIconified(WindowEvent e) { }
    public void windowDeiconified(WindowEvent e) { }
    public void windowActivated(WindowEvent e) { }
    public void windowDeactivated(WindowEvent e) { }
});

// With adapter (only what you need)
frame.addWindowListener(new WindowAdapter() {
    @Override
    public void windowClosing(WindowEvent e) {
        System.exit(0);
    }
});
```

### Example: KeyAdapter (Only need key pressed)

```java
JTextField textField = new JTextField(20);

// Without adapter (need 3 methods)
textField.addKeyListener(new KeyListener() {
    public void keyTyped(KeyEvent e) { }
    public void keyPressed(KeyEvent e) {
        if (e.getKeyCode() == KeyEvent.VK_ENTER) {
            System.out.println("Enter pressed!");
        }
    }
    public void keyReleased(KeyEvent e) { }
});

// With adapter (only keyPressed)
textField.addKeyListener(new KeyAdapter() {
    @Override
    public void keyPressed(KeyEvent e) {
        if (e.getKeyCode() == KeyEvent.VK_ENTER) {
            System.out.println("Enter pressed!");
        }
    }
});
```

### Example: FocusAdapter (Focus lost)

```java
JTextField field1 = new JTextField(10);
JTextField field2 = new JTextField(10);

field1.addFocusListener(new FocusAdapter() {
    @Override
    public void focusLost(FocusEvent e) {
        // Validate input when user leaves the field
        if (field1.getText().isEmpty()) {
            field1.setBackground(Color.PINK);
        } else {
            field1.setBackground(Color.WHITE);
        }
    }
});
```
