Here's a **complete theoretical explanation** of all the menu-related topics you listed.

---

## What are Menus in Java Swing?

**Menus** are drop-down lists of commands or options that appear at the top of a window.

```
┌─────────────────────────────────────────────────────────────┐
│ File    Edit    View    Help                    ← Menu Bar  │
│ ┌─────┐                                                   │
│ │ New │ ← Menu Item                                       │
│ │ Open│                                                   │
│ │ Save│                                                   │
│ │ ────│ ← Separator                                       │
│ │ Exit│                                                   │
│ └─────┘                                                   │
└─────────────────────────────────────────────────────────────┘
```

---

## The Menu Hierarchy

```
JMenuBar (Menu Bar - holds all menus)
    │
    ├── JMenu (File)
    │       ├── JMenuItem (New)
    │       ├── JMenuItem (Open)
    │       ├── JSeparator (line)
    │       └── JMenuItem (Exit)
    │
    ├── JMenu (Edit)
    │       ├── JMenuItem (Cut)
    │       ├── JMenuItem (Copy)
    │       └── JMenuItem (Paste)
    │
    └── JMenu (Help)
            └── JMenuItem (About)
```

---

## 1. Menu Bar (JMenuBar)

**What it is:** The container that holds all menus at the top of the window.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Holds all menu items |
| **Position** | Top of the frame |
| **How to add** | `frame.setJMenuBar(menuBar)` |

```java
// Create menu bar
JMenuBar menuBar = new JMenuBar();

// Add to frame
frame.setJMenuBar(menuBar);
```

---

## 2. Menu (JMenu)

**What it is:** A drop-down menu on the menu bar (like File, Edit, View).

| Aspect | Description |
|--------|-------------|
| **Purpose** | Groups related menu items |
| **Appearance** | Clickable word on menu bar |
| **Contains** | Menu items, sub-menus, separators |

```java
// Create menus
JMenu fileMenu = new JMenu("File");
JMenu editMenu = new JMenu("Edit");
JMenu viewMenu = new JMenu("View");
JMenu helpMenu = new JMenu("Help");

// Add menus to menu bar
menuBar.add(fileMenu);
menuBar.add(editMenu);
menuBar.add(viewMenu);
menuBar.add(helpMenu);
```

---

## 3. Menu Item (JMenuItem)

**What it is:** A single clickable command inside a menu.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Represents an action (New, Open, Save, Exit) |
| **What happens** | ActionListener triggers when clicked |

```java
// Create menu items
JMenuItem newItem = new JMenuItem("New");
JMenuItem openItem = new JMenuItem("Open");
JMenuItem saveItem = new JMenuItem("Save");
JMenuItem exitItem = new JMenuItem("Exit");

// Add to menu
fileMenu.add(newItem);
fileMenu.add(openItem);
fileMenu.add(saveItem);
fileMenu.addSeparator();  // Adds a line
fileMenu.add(exitItem);

// Add action listener
exitItem.addActionListener(e -> System.exit(0));
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ File    Edit    View    Help            │
│ ┌─────┐                                 │
│ │ New │ ← JMenuItem                     │
│ │ Open│ ← JMenuItem                     │
│ │ Save│ ← JMenuItem                     │
│ ├─────┤ ← JSeparator                    │
│ │ Exit│ ← JMenuItem                     │
│ └─────┘                                 │
└─────────────────────────────────────────┘
```

---

## 4. Icons in Menu Items

**What it is:** Adding small images next to menu item text.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Visual cue for menu actions |
| **File format** | PNG, GIF, JPEG (usually 16x16 pixels) |

```java
// Load icon
ImageIcon newIcon = new ImageIcon("new.png");
ImageIcon openIcon = new ImageIcon("open.png");
ImageIcon saveIcon = new ImageIcon("save.png");

// Create menu items with icons
JMenuItem newItem = new JMenuItem("New", newIcon);
JMenuItem openItem = new JMenuItem("Open", openIcon);
JMenuItem saveItem = new JMenuItem("Save", saveIcon);

// Alternative: Set icon after creation
JMenuItem exitItem = new JMenuItem("Exit");
exitItem.setIcon(new ImageIcon("exit.png"));
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ File                                    │
│ ┌─────────────────────────────────────┐ │
│ │ 📄 New                              │ │ ← Icon + text
│ │ 📂 Open                             │ │
│ │ 💾 Save                             │ │
│ ├─────────────────────────────────────┤ │
│ │ ❌ Exit                             │ │
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘
```

---

## 5. Check Box and Radio Buttons in Menu Items

### CheckBox Menu Item (JCheckBoxMenuItem)

**What it is:** A menu item with a check box that toggles on/off.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Toggle a setting (View Toolbar, Show Status Bar) |
| **State** | Checked or unchecked |

```java
// Create check box menu items
JCheckBoxMenuItem showToolbar = new JCheckBoxMenuItem("Show Toolbar");
JCheckBoxMenuItem showStatusBar = new JCheckBoxMenuItem("Show Status Bar");
JCheckBoxMenuItem wrapText = new JCheckBoxMenuItem("Wrap Text");

// Initially checked
showToolbar.setSelected(true);

// Add to View menu
viewMenu.add(showToolbar);
viewMenu.add(showStatusBar);
viewMenu.add(wrapText);

// Check state
boolean isSelected = showToolbar.isSelected();
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ View                                    │
│ ┌─────────────────────────────────────┐ │
│ │ ☑ Show Toolbar                      │ │ ← Checked
│ │ ☐ Show Status Bar                   │ │ ← Unchecked
│ │ ☑ Wrap Text                         │ │ ← Checked
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘
```

### Radio Button Menu Item (JRadioButtonMenuItem)

**What it is:** Menu items where only one in a group can be selected.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Choose one option from multiple (View as Icons, List, Details) |

```java
// Create radio button menu items
JRadioButtonMenuItem iconView = new JRadioButtonMenuItem("Icons");
JRadioButtonMenuItem listView = new JRadioButtonMenuItem("List");
JRadioButtonMenuItem detailView = new JRadioButtonMenuItem("Details");

// Group them (only one can be selected)
ButtonGroup viewGroup = new ButtonGroup();
viewGroup.add(iconView);
viewGroup.add(listView);
viewGroup.add(detailView);

// Default selection
iconView.setSelected(true);

// Add to View menu
viewMenu.addSeparator();
viewMenu.add(iconView);
viewMenu.add(listView);
viewMenu.add(detailView);
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ View                                    │
│ ┌─────────────────────────────────────┐ │
│ │ ☑ Icons                             │ │ ← Selected
│ │ ○ List                              │ │ ← Not selected
│ │ ○ Details                           │ │ ← Not selected
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘

Only ONE can be selected (like radio buttons)!
```

---

## 6. Pop-up Menus (JPopupMenu)

**What it is:** A menu that appears when right-clicking (context menu).

| Aspect | Description |
|--------|-------------|
| **Purpose** | Show context-sensitive commands |
| **Trigger** | Usually right-click (mouse event) |

```java
// Create popup menu
JPopupMenu popupMenu = new JPopupMenu();

// Add items
JMenuItem cutItem = new JMenuItem("Cut");
JMenuItem copyItem = new JMenuItem("Copy");
JMenuItem pasteItem = new JMenuItem("Paste");

popupMenu.add(cutItem);
popupMenu.add(copyItem);
popupMenu.add(pasteItem);

// Add mouse listener to component
component.addMouseListener(new MouseAdapter() {
    @Override
    public void mouseReleased(MouseEvent e) {
        if (e.isPopupTrigger()) {
            popupMenu.show(component, e.getX(), e.getY());
        }
    }
});
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ My Document.txt                         │
│ Some selected text here                 │
│ ┌─────────┐                             │
│ │ Cut     │ ← Right-click popup menu    │
│ │ Copy    │                             │
│ │ Paste   │                             │
│ └─────────┘                             │
└─────────────────────────────────────────┘
```

---

## 7. Keyboard Mnemonics and Accelerators

### Mnemonics (Alt + Key)

**What it is:** Keyboard shortcut to open a menu using Alt+Letter.

| Aspect | Description |
|--------|-------------|
| **How it works** | Press Alt + underlined letter |
| **Appearance** | Underlined letter in menu text |
| **Scope** | Opens the menu (not executes command) |

```java
// Set mnemonic (Alt+F opens File menu)
JMenu fileMenu = new JMenu("File");
fileMenu.setMnemonic(KeyEvent.VK_F);  // 'F' underlined

// Mnemonic for menu item (Alt+N activates New)
JMenuItem newItem = new JMenuItem("New");
newItem.setMnemonic(KeyEvent.VK_N);   // 'N' underlined
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ File    Edit    View                    │
│   ↑                                     │
│   └─ 'F' underlined (Alt+F opens File)  │
│                                         │
│ When File is open:                      │
│ ┌─────────────────────────────────────┐ │
│ │ New                                 │ │
│ │  ↑                                  │ │
│ │  └─ 'N' underlined (Alt+N activates)│ │
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘
```

### Accelerators (Ctrl + Key)

**What it is:** Direct keyboard shortcut that executes a menu command without opening the menu.

| Aspect | Description |
|--------|-------------|
| **How it works** | Press Ctrl+Key directly |
| **Appearance** | Shows shortcut next to menu item |
| **Scope** | Executes the command immediately |

```java
// Set accelerator (Ctrl+N)
JMenuItem newItem = new JMenuItem("New");
newItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_N, 
                        InputEvent.CTRL_DOWN_MASK));

// Ctrl+S for Save
JMenuItem saveItem = new JMenuItem("Save");
saveItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_S, 
                        InputEvent.CTRL_DOWN_MASK));

// Ctrl+O for Open
JMenuItem openItem = new JMenuItem("Open");
openItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_O, 
                        InputEvent.CTRL_DOWN_MASK));
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ File                                    │
│ ┌─────────────────────────────────────┐ │
│ │ New        Ctrl+N                   │ │ ← Accelerator shown
│ │ Open       Ctrl+O                   │ │
│ │ Save       Ctrl+S                   │ │
│ ├─────────────────────────────────────┤ │
│ │ Exit                                 │ │
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘

Press Ctrl+N → New is created immediately!
```

### Mnemonic vs Accelerator

| Aspect | Mnemonic | Accelerator |
|--------|----------|-------------|
| **Keys** | Alt + Letter | Ctrl + Letter (usually) |
| **Opens menu?** | Yes | No (executes directly) |
| **Shows in menu?** | Underlined letter | Shown next to item |
| **Example** | Alt+F opens File | Ctrl+S saves |

---

## 8. Enabling and Disabling Menu Items

**What it is:** Making menu items grayed out (unclickable) when not available.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Prevent invalid actions (can't cut if nothing selected) |
| **Appearance** | Grayed out text |

```java
// Create menu items
JMenuItem cutItem = new JMenuItem("Cut");
JMenuItem copyItem = new JMenuItem("Copy");
JMenuItem pasteItem = new JMenuItem("Paste");

// Initially disabled (grayed out)
cutItem.setEnabled(false);
copyItem.setEnabled(false);

// Enable when text is selected
// ... in selection listener
if (textSelected) {
    cutItem.setEnabled(true);
    copyItem.setEnabled(true);
}

// Disable paste if clipboard is empty
if (clipboardEmpty) {
    pasteItem.setEnabled(false);
}

// Check state
boolean isEnabled = cutItem.isEnabled();
```

**Visual:**
```
Enabled:                        Disabled:
┌─────────────────────────────────────────┐
│ Edit                                    │
│ ┌─────────────────────────────────────┐ │
│ │ Cut                                 │ │
│ │ Copy                                │ │
│ │ Paste    (normal, clickable)        │ │
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ Edit                                    │
│ ┌─────────────────────────────────────┐ │
│ │ Cut           (grayed out)          │ │
│ │ Copy          (grayed out)          │ │
│ │ Paste                               │ │
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘
```

---

## 9. Toolbars (JToolBar)

**What it is:** A movable bar with buttons for quick access to common commands.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Quick access to frequently used commands |
| **Position** | Usually below menu bar |
| **Features** | Can be dragged to different locations |

```java
// Create toolbar
JToolBar toolBar = new JToolBar("Main Toolbar");

// Add buttons with icons
ImageIcon newIcon = new ImageIcon("new.png");
JButton newButton = new JButton(newIcon);
newButton.setToolTipText("New File");

ImageIcon openIcon = new ImageIcon("open.png");
JButton openButton = new JButton(openIcon);
openButton.setToolTipText("Open File");

ImageIcon saveIcon = new ImageIcon("save.png");
JButton saveButton = new JButton(saveIcon);
saveButton.setToolTipText("Save File");

// Add buttons to toolbar
toolBar.add(newButton);
toolBar.add(openButton);
toolBar.add(saveButton);
toolBar.addSeparator();  // Adds vertical line

// Add toolbar to frame
frame.add(toolBar, BorderLayout.NORTH);
```

**Visual:**
```
┌─────────────────────────────────────────────────────────────┐
│ [📄] [📂] [💾] │ [✂️] [📋] [📎]                      ← Toolbar │
├─────────────────────────────────────────────────────────────┤
│ File    Edit    View    Help                                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                     Main Content Area                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘

Toolbar can be dragged and dropped to different positions!
```

---

## 10. Tooltips

**What it is:** Small popup text that appears when mouse hovers over a component.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Provide hints about what a button/menu item does |
| **Appearance** | Small yellow box with text |
| **Delay** | Appears after ~1 second of hovering |

```java
// Tooltip for menu item
JMenuItem saveItem = new JMenuItem("Save");
saveItem.setToolTipText("Save the current file (Ctrl+S)");

// Tooltip for toolbar button
JButton saveButton = new JButton(saveIcon);
saveButton.setToolTipText("Save File");

// Tooltip for any component
JTextField textField = new JTextField();
textField.setToolTipText("Enter your name here");

// Tooltip with HTML formatting
JButton helpButton = new JButton("Help");
helpButton.setToolTipText("<html><b>Click here</b><br>for help</html>");
```

**Visual:**
```
┌─────────────────────────────────────────┐
│                                         │
│      [Save File]                        │
│       ┌──────────────┐                  │
│       │ Save the     │ ← Tooltip popup  │
│       │ file (Ctrl+S)│                  │
│       └──────────────┘                  │
│                                         │
└─────────────────────────────────────────┘

Appears when mouse hovers over Save button
```

---

## Complete Example: Text Editor Menu System

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class TextEditorMenu extends JFrame {
    
    private JTextArea textArea;
    private JToolBar toolBar;
    
    public TextEditorMenu() {
        setTitle("My Text Editor");
        setSize(600, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Create text area
        textArea = new JTextArea();
        JScrollPane scrollPane = new JScrollPane(textArea);
        add(scrollPane, BorderLayout.CENTER);
        
        // Create menu bar
        JMenuBar menuBar = new JMenuBar();
        
        // ========== FILE MENU ==========
        JMenu fileMenu = new JMenu("File");
        fileMenu.setMnemonic(KeyEvent.VK_F);
        
        // New (with icon, accelerator, tooltip)
        JMenuItem newItem = new JMenuItem("New", new ImageIcon("new.png"));
        newItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_N, InputEvent.CTRL_DOWN_MASK));
        newItem.setToolTipText("Create new file");
        newItem.addActionListener(e -> textArea.setText(""));
        fileMenu.add(newItem);
        
        // Open
        JMenuItem openItem = new JMenuItem("Open", new ImageIcon("open.png"));
        openItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_O, InputEvent.CTRL_DOWN_MASK));
        fileMenu.add(openItem);
        
        // Save
        JMenuItem saveItem = new JMenuItem("Save", new ImageIcon("save.png"));
        saveItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_S, InputEvent.CTRL_DOWN_MASK));
        fileMenu.add(saveItem);
        
        fileMenu.addSeparator();
        
        // Exit
        JMenuItem exitItem = new JMenuItem("Exit");
        exitItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_Q, InputEvent.CTRL_DOWN_MASK));
        exitItem.addActionListener(e -> System.exit(0));
        fileMenu.add(exitItem);
        
        menuBar.add(fileMenu);
        
        // ========== EDIT MENU ==========
        JMenu editMenu = new JMenu("Edit");
        editMenu.setMnemonic(KeyEvent.VK_E);
        
        JMenuItem cutItem = new JMenuItem("Cut");
        cutItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_X, InputEvent.CTRL_DOWN_MASK));
        cutItem.addActionListener(e -> textArea.cut());
        editMenu.add(cutItem);
        
        JMenuItem copyItem = new JMenuItem("Copy");
        copyItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_C, InputEvent.CTRL_DOWN_MASK));
        copyItem.addActionListener(e -> textArea.copy());
        editMenu.add(copyItem);
        
        JMenuItem pasteItem = new JMenuItem("Paste");
        pasteItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_V, InputEvent.CTRL_DOWN_MASK));
        pasteItem.addActionListener(e -> textArea.paste());
        editMenu.add(pasteItem);
        
        menuBar.add(editMenu);
        
        // ========== VIEW MENU ==========
        JMenu viewMenu = new JMenu("View");
        viewMenu.setMnemonic(KeyEvent.VK_V);
        
        // Check box menu items
        JCheckBoxMenuItem showToolbarItem = new JCheckBoxMenuItem("Show Toolbar");
        showToolbarItem.setSelected(true);
        showToolbarItem.addActionListener(e -> toolBar.setVisible(showToolbarItem.isSelected()));
        viewMenu.add(showToolbarItem);
        
        // Radio button menu items for zoom
        viewMenu.addSeparator();
        JRadioButtonMenuItem zoomIn = new JRadioButtonMenuItem("Zoom In");
        JRadioButtonMenuItem zoomNormal = new JRadioButtonMenuItem("Normal Zoom");
        JRadioButtonMenuItem zoomOut = new JRadioButtonMenuItem("Zoom Out");
        
        ButtonGroup zoomGroup = new ButtonGroup();
        zoomGroup.add(zoomIn);
        zoomGroup.add(zoomNormal);
        zoomGroup.add(zoomOut);
        zoomNormal.setSelected(true);
        
        viewMenu.add(zoomIn);
        viewMenu.add(zoomNormal);
        viewMenu.add(zoomOut);
        
        menuBar.add(viewMenu);
        
        // ========== HELP MENU ==========
        JMenu helpMenu = new JMenu("Help");
        JMenuItem aboutItem = new JMenuItem("About");
        aboutItem.addActionListener(e -> JOptionPane.showMessageDialog(this, 
                                        "Text Editor v1.0", "About", 
                                        JOptionPane.INFORMATION_MESSAGE));
        helpMenu.add(aboutItem);
        menuBar.add(helpMenu);
        
        setJMenuBar(menuBar);
        
        // ========== TOOLBAR ==========
        toolBar = new JToolBar();
        
        JButton newBtn = new JButton(new ImageIcon("new.png"));
        newBtn.setToolTipText("New File (Ctrl+N)");
        newBtn.addActionListener(e -> textArea.setText(""));
        toolBar.add(newBtn);
        
        JButton openBtn = new JButton(new ImageIcon("open.png"));
        openBtn.setToolTipText("Open File (Ctrl+O)");
        toolBar.add(openBtn);
        
        JButton saveBtn = new JButton(new ImageIcon("save.png"));
        saveBtn.setToolTipText("Save File (Ctrl+S)");
        toolBar.add(saveBtn);
        
        toolBar.addSeparator();
        
        JButton cutBtn = new JButton(new ImageIcon("cut.png"));
        cutBtn.setToolTipText("Cut (Ctrl+X)");
        cutBtn.addActionListener(e -> textArea.cut());
        toolBar.add(cutBtn);
        
        JButton copyBtn = new JButton(new ImageIcon("copy.png"));
        copyBtn.setToolTipText("Copy (Ctrl+C)");
        copyBtn.addActionListener(e -> textArea.copy());
        toolBar.add(copyBtn);
        
        JButton pasteBtn = new JButton(new ImageIcon("paste.png"));
        pasteBtn.setToolTipText("Paste (Ctrl+V)");
        pasteBtn.addActionListener(e -> textArea.paste());
        toolBar.add(pasteBtn);
        
        add(toolBar, BorderLayout.NORTH);
        
        // Popup menu (right-click)
        JPopupMenu popupMenu = new JPopupMenu();
        popupMenu.add(cutItem);
        popupMenu.add(copyItem);
        popupMenu.add(pasteItem);
        
        textArea.addMouseListener(new MouseAdapter() {
            public void mouseReleased(MouseEvent e) {
                if (e.isPopupTrigger()) {
                    popupMenu.show(textArea, e.getX(), e.getY());
                }
            }
        });
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new TextEditorMenu();
    }
}
```

---

## Quick Reference Table

| Concept | Class | Purpose |
|---------|-------|---------|
| Menu Bar | `JMenuBar` | Container for menus |
| Menu | `JMenu` | Drop-down menu (File, Edit) |
| Menu Item | `JMenuItem` | Clickable command |
| Checkbox Menu Item | `JCheckBoxMenuItem` | Toggle option |
| Radio Menu Item | `JRadioButtonMenuItem` | One of many selection |
| Popup Menu | `JPopupMenu` | Right-click context menu |
| Separator | `JSeparator` | Line between items |
| Mnemonic | `setMnemonic()` | Alt+Letter shortcut |
| Accelerator | `setAccelerator()` | Ctrl+Letter shortcut |
| Toolbar | `JToolBar` | Quick access buttons |
| Tooltip | `setToolTipText()` | Hover help text |

---

## The Golden Rule

> **JMenuBar holds JMenus, which hold JMenuItems. Use mnemonics (Alt+Letter) to open menus, accelerators (Ctrl+Letter) for direct shortcuts, tooltips for help text, and popup menus for right-click context. Toolbars provide quick button access to common commands.**

**Memory trick:**
```
Menu Bar = The shelf at top
Menu = The folder hanging on shelf
Menu Item = The command inside folder
Separator = Line between commands
Accelerator = Keyboard shortcut (Ctrl+S)
Mnemonic = Alt+Letter to open menu
Toolbar = Shortcut buttons below menu bar
Tooltip = Hover help text
Popup = Right-click menu
```

Would you like me to explain **event handling** (how to respond to menu clicks) next?