**What is an Action Command?** A string that identifies the action, useful when multiple components share the same listener.

| Aspect       | Description                                  |
| ------------ | -------------------------------------------- |
| **Purpose**  | Identify which component triggered the event |
| **Default**  | Button's text (if not set)                   |
| **Use case** | Multiple buttons with one listener           |

### Example: [[Without Action Command (Hard to identify)]]


### Example: With Action Command (Cleaner)

```java
JButton saveButton = new JButton("Save");
JButton loadButton = new JButton("Load");
JButton deleteButton = new JButton("Delete");

// Set action commands
saveButton.setActionCommand("SAVE");
loadButton.setActionCommand("LOAD");
deleteButton.setActionCommand("DELETE");

// ONE listener uses action command to identify
ActionListener listener = new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        String command = e.getActionCommand();
        
        switch (command) {
            case "SAVE": save(); break;
            case "LOAD": load(); break;
            case "DELETE": delete(); break;
        }
    }
};

saveButton.addActionListener(listener);
loadButton.addActionListener(listener);
deleteButton.addActionListener(listener);
```

### Why Use Action Commands?

| Without Action Command                 | With Action Command                 |
| -------------------------------------- | ----------------------------------- |
| Compare `e.getSource()` to each button | Compare string (`"SAVE"`, `"LOAD"`) |
| Need references to all buttons         | No references needed                |
| Code is longer and messier             | Code is cleaner                     |
| Harder to test                         | Easier to test                      |

### Real-World Example: Calculator Buttons

```java
// All calculator buttons share ONE listener!
ActionListener calcListener = e -> {
    String cmd = e.getActionCommand();
    switch (cmd) {
        case "0": case "1": case "2": case "3": case "4":
        case "5": case "6": case "7": case "8": case "9":
            appendDigit(cmd);
            break;
        case "+": setOperation("ADD"); break;
        case "-": setOperation("SUBTRACT"); break;
        case "=": calculate(); break;
        case "C": clear(); break;
    }
};

// Create all buttons with action commands
String[] buttons = {"7","8","9","+","4","5","6","-","1","2","3","*","0","C","=","/"};
for (String text : buttons) {
    JButton btn = new JButton(text);
    btn.setActionCommand(text);
    btn.addActionListener(calcListener);
    panel.add(btn);
}
```
