Here's a **complete theoretical explanation** of all the advanced Swing components you listed.

---

## What are Dialogs and Advanced Components?

These are special windows and components that extend basic GUI functionality:

```
┌─────────────────────────────────────────────────────────────┐
│                    MAIN APPLICATION (JFrame)                │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                  INTERNAL FRAME                       │   │
│  │  ┌─────────────┐  ┌─────────────┐                    │   │
│  │  │   Table     │  │    Tree     │                    │   │
│  │  └─────────────┘  └─────────────┘                    │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  When user clicks:                                         │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │
│  │ OptionDialog│  │ FileChooser │  │ ColorChooser│        │
│  └─────────────┘  └─────────────┘  └─────────────┘        │
└─────────────────────────────────────────────────────────────┘
```

---

## 1. Option Dialogs (JOptionPane)

**What it is:** Pre-built popup dialogs for common tasks like messages, confirmations, and input.

| Aspect          | Description                                  |
| --------------- | -------------------------------------------- |
| **Purpose**     | Quick popup windows for user interaction     |
| **Advantage**   | No need to create custom dialog windows      |
| **Common uses** | Error messages, confirmations, input prompts |

### Types of Option Dialogs

```java
import javax.swing.JOptionPane;

// 1. MESSAGE DIALOG (show information)
JOptionPane.showMessageDialog(frame, "File saved successfully!");
JOptionPane.showMessageDialog(frame, "Error occurred!", "Error", JOptionPane.ERROR_MESSAGE);
JOptionPane.showMessageDialog(frame, "Operation complete", "Info", JOptionPane.INFORMATION_MESSAGE);

// 2. CONFIRMATION DIALOG (yes/no/cancel)
int result = JOptionPane.showConfirmDialog(frame, "Do you want to save?", "Save File", 
                                           JOptionPane.YES_NO_CANCEL_OPTION);
if (result == JOptionPane.YES_OPTION) {
    // Save file
} else if (result == JOptionPane.NO_OPTION) {
    // Don't save
}

// 3. INPUT DIALOG (get text from user)
String name = JOptionPane.showInputDialog(frame, "Enter your name:");
if (name != null && !name.trim().isEmpty()) {
    System.out.println("Hello, " + name);
}

// 4. OPTION DIALOG (custom buttons)
Object[] options = {"Red", "Green", "Blue"};
int choice = JOptionPane.showOptionDialog(frame, "Choose a color", "Color Picker",
                                          JOptionPane.DEFAULT_OPTION, JOptionPane.QUESTION_MESSAGE,
                                          null, options, options[0]);
```

### Message Types

| Message Type | Icon | Use |
|--------------|------|-----|
| `ERROR_MESSAGE` | ❌ Red circle | Errors |
| `INFORMATION_MESSAGE` | ℹ️ Blue i | Information |
| `WARNING_MESSAGE` | ⚠️ Yellow triangle | Warnings |
| `QUESTION_MESSAGE` | ❓ Green question | Questions |
| `PLAIN_MESSAGE` | No icon | Simple messages |

**Visual:**
```
┌─────────────────────────────────────────┐
│  Error                             [X]  │
├─────────────────────────────────────────┤
│  ❌ File not found!                     │
│                                         │
│                    [ OK ]               │
└─────────────────────────────────────────┘
```

---

## 2. Creating Dialogs (JDialog)

**What it is:** Custom popup windows you create yourself for complex interactions.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Create custom popup windows |
| **Vs JOptionPane** | More flexible, more complex |
| **Common uses** | Preferences dialog, search dialog, custom forms |

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class CustomDialog extends JDialog {
    
    public CustomDialog(JFrame parent) {
        super(parent, "Custom Dialog", true);  // true = modal (blocks parent)
        
        setSize(300, 200);
        
        // Add components
        JPanel panel = new JPanel();
        panel.add(new JLabel("Enter value:"));
        panel.add(new JTextField(15));
        
        JButton okButton = new JButton("OK");
        okButton.addActionListener(e -> dispose());  // Close dialog
        
        panel.add(okButton);
        add(panel);
    }
    
    // Usage:
    // CustomDialog dialog = new CustomDialog(frame);
    // dialog.setVisible(true);
}
```

### Modal vs Modeless

| Type | Description |
|------|-------------|
| **Modal** | Blocks parent window until closed (user must respond) |
| **Modeless** | Parent window remains active (floating palette) |

```java
// Modal dialog (most common)
JDialog dialog = new JDialog(frame, "Modal", true);

// Modeless dialog (rare)
JDialog dialog = new JDialog(frame, "Modeless", false);
```

---

## 3. File Choosers (JFileChooser)

**What it is:** A dialog for selecting files or directories from the file system.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Browse and select files/folders |
| **Common uses** | Open file, Save file, Choose directory |

```java
import javax.swing.JFileChooser;
import javax.swing.filechooser.FileNameExtensionFilter;

// Create file chooser
JFileChooser chooser = new JFileChooser();

// Set initial directory
chooser.setCurrentDirectory(new File("C:\\Users"));

// OPEN FILE DIALOG
int result = chooser.showOpenDialog(frame);
if (result == JFileChooser.APPROVE_OPTION) {
    File selectedFile = chooser.getSelectedFile();
    String filePath = selectedFile.getAbsolutePath();
    System.out.println("Opened: " + filePath);
}

// SAVE FILE DIALOG
int result = chooser.showSaveDialog(frame);
if (result == JFileChooser.APPROVE_OPTION) {
    File fileToSave = chooser.getSelectedFile();
    System.out.println("Save to: " + fileToSave);
}

// DIRECTORY CHOOSER
chooser.setFileSelectionMode(JFileChooser.DIRECTORIES_ONLY);
int result = chooser.showOpenDialog(frame);
if (result == JFileChooser.APPROVE_OPTION) {
    File selectedDir = chooser.getSelectedFile();
}

File[] files = chooser.getSelectedFiles();

```

**Visual:**
```
┌─────────────────────────────────────────────────────────────┐
│  Open                                    [X]                │
├─────────────────────────────────────────────────────────────┤
│  Look in:  Documents                   [向上]              │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────┐   │
│  │  MyProjects/                                        │   │
│  │  report.txt                                         │   │
│  │  data.csv                                           │   │
│  │  image.png                                          │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  File name: [report.txt              ]                     │
│  Files of type: [All Files (*.*)     ▼]                     │
│                                                             │
│                              [Open]  [Cancel]               │
└─────────────────────────────────────────────────────────────┘
```

---

## 4. Color Choosers (JColorChooser)

**What it is:** A dialog for selecting colors.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Pick colors from a palette |
| **Common uses** | Font color, background color, drawing tools |

```java
import javax.swing.JColorChooser;
import java.awt.Color;

// Basic color chooser
Color selectedColor = JColorChooser.showDialog(frame, "Choose a Color", Color.RED);

if (selectedColor != null) {
    System.out.println("Selected: " + selectedColor);
    component.setBackground(selectedColor);
}

// With initial color
Color initialColor = Color.BLUE;
Color newColor = JColorChooser.showDialog(frame, "Pick Color", initialColor);

// Embedded color chooser (in a panel)
JColorChooser colorChooser = new JColorChooser();
JPanel colorPanel = colorChooser.getPreviewPanel();
```

**Visual:**
```
┌─────────────────────────────────────────────────────────────┐
│  Choose a Color                        [X]                  │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Swatches  HSV  HSL  RGB                           │   │
│  │  ┌─────┬─────┬─────┬─────┬─────┐                   │   │
│  │  │ ■  │ ■  │ ■  │ ■  │ ■  │                   │   │
│  │  ├─────┼─────┼─────┼─────┼─────┤                   │   │
│  │  │ ■  │ ■  │ ■  │ ■  │ ■  │                   │   │
│  │  └─────┴─────┴─────┴─────┴─────┘                   │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  Preview:  [████████████████████]                           │
│                                                             │
│                              [OK]  [Cancel]                 │
└─────────────────────────────────────────────────────────────┘
```

---

## 5. Frames (JFrame)

**What it is:** The main application window.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Main window of application |
| **Features** | Title bar, minimize/maximize/close buttons |

```java
// Create frame
JFrame frame = new JFrame("My Application");

// Set size
frame.setSize(800, 600);

// Set position
frame.setLocationRelativeTo(null);  // Center on screen

// Set close operation (critical!)
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  // Exit app
// Or
frame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE); // Close window only

// Set icon
frame.setIconImage(new ImageIcon("icon.png").getImage());

// Make visible (MUST be last!)
frame.setVisible(true);

// Maximize
frame.setExtendedState(JFrame.MAXIMIZED_BOTH);

// Prevent resizing
frame.setResizable(false);
```

### Frame vs Dialog

| Aspect | JFrame | JDialog |
|--------|--------|---------|
| **Purpose** | Main application window | Popup/child window |
| **Close button** | X (can exit app) | X (close dialog) |
| **Task bar** | Shows | Doesn't show |
| **Parent** | None | Usually has parent frame |

---

## 6. Internal Frames (JInternalFrame)

**What it is:** A frame that lives INSIDE another frame (MDI - Multiple Document Interface).

| Aspect | Description |
|--------|-------------|
| **Purpose** | Multiple document windows inside main window |
| **Example** | Photoshop, Eclipse, NetBeans |

```java
import javax.swing.*;
import java.awt.*;

public class InternalFrameDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("MDI Application");
        frame.setSize(800, 600);
        
        JDesktopPane desktop = new JDesktopPane();
        frame.setContentPane(desktop);
        
        // Frame 1
        JInternalFrame doc1 = new JInternalFrame("Document 1", true, true, true, true);
        doc1.add(new JScrollPane(new JTextArea()));
        doc1.setBounds(0, 0, 300, 200);
        doc1.setVisible(true);
        desktop.add(doc1);
        
        // Frame 2
        JInternalFrame doc2 = new JInternalFrame("Document 2", true, true, true, true);
        doc2.add(new JScrollPane(new JTextArea()));
        doc2.setBounds(100, 100, 300, 200);
        doc2.setVisible(true);
        desktop.add(doc2);
        
        frame.setVisible(true);
    }
}
```

**Visual:**
```
┌─────────────────────────────────────────────────────────────┐
│ File  Edit  View  Window                          [X][□][-] │
├─────────────────────────────────────────────────────────────┤
│  ┌───────────────────┐  ┌───────────────────┐              │
│  │ Document 1   [X]  │  │ Document 2   [X]  │              │
│  ├───────────────────┤  ├───────────────────┤              │
│  │                   │  │                   │              │
│  │  Text here...     │  │  Text here...     │              │
│  │                   │  │                   │              │
│  └───────────────────┘  └───────────────────┘              │
│                                                             │
│  ┌───────────────────┐                                     │
│  │ Document 3   [X]  │                                     │
│  ├───────────────────┤                                     │
│  │  Text here...     │                                     │
│  └───────────────────┘                                     │
└─────────────────────────────────────────────────────────────┘
```

---

## 7. Tables (JTable)

**What it is:** A component to display data in rows and columns (spreadsheet-like).

| Aspect | Description |
|--------|-------------|
| **Purpose** | Display and edit tabular data |
| **Common uses** | Spreadsheets, database results, reports |

```java
import javax.swing.*;
import javax.swing.table.*;

// Create table with data
String[] columns = {"ID", "Name", "Age", "Department"};
Object[][] data = {
    {1, "Alice", 25, "Engineering"},
    {2, "Bob", 30, "Sales"},
    {3, "Charlie", 28, "Marketing"},
    {4, "Diana", 35, "HR"}
};

JTable table = new JTable(data, columns);

// Add to scroll pane (important!)
JScrollPane scrollPane = new JScrollPane(table);
frame.add(scrollPane);

// Customize table
//table.setRowHeight(25);
//table.setShowGrid(true);
//table.setGridColor(Color.GRAY);

// Selection modes
// 1. SINGLE_SELECTION - Only ONE row at a time
table.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
//or
// 2. SINGLE_INTERVAL_SELECTION - Contiguous block of rows (shift+click)
table.setSelectionMode(ListSelectionModel.SINGLE_INTERVAL_SELECTION);
//or
// 3. MULTIPLE_INTERVAL_SELECTION - Any combination (default, ctrl+click)
table.setSelectionMode(ListSelectionModel.MULTIPLE_INTERVAL_SELECTION);

// Get selected data
int selectedRow = table.getSelectedRow();     // Get selected row
int selectedCol = table.getSelectedColumn();  // Get selected column
if (selectedRow != -1) {
    String name = (String) table.getValueAt(selectedRow, selectedCol);
//     ↑         ↑        ↑                      ↑       ↑
//     |         |        |                      |       |
//  Variable   Cast    Table                  Row index   Column index
//  to store   to      object                              (0-based)
//  the value  String
    System.out.println("Selected: " + name);
}

// Add row
model.addRow(new Object[]{6, "Frank", 32, "Finance"});

// Remove row
model.removeRow(0);
```

**Visual:**
```
┌─────────────────────────────────────────────────────────────┐
│ ┌─────┬─────────┬─────┬─────────────┐                       │
│ │ ID  │ Name    │ Age │ Department  │                       │
│ ├─────┼─────────┼─────┼─────────────┤                       │
│ │ 1   │ Alice   │ 25  │ Engineering │                       │
│ │ 2   │ Bob     │ 30  │ Sales       │                       │
│ │ 3   │ Charlie │ 28  │ Marketing   │ ← Selected row        │
│ │ 4   │ Diana   │ 35  │ HR          │                       │
│ └─────┴─────────┴─────┴─────────────┘                       │
│ ◄─────────────── Scroll Pane ────────────────►              │
└─────────────────────────────────────────────────────────────┘
```

---

## 8. Trees (JTree)

**What it is:** A component to display hierarchical data (parent-child relationships).

| Aspect | Description |
|--------|-------------|
| **Purpose** | Display hierarchical data |
| **Common uses** | File explorer, organization chart, menu structure |

```java
import javax.swing.*;
import javax.swing.tree.*;

// Create tree with data
DefaultMutableTreeNode root = new DefaultMutableTreeNode("Root");

// Create nodes
DefaultMutableTreeNode fruits = new DefaultMutableTreeNode("Fruits");
DefaultMutableTreeNode vegetables = new DefaultMutableTreeNode("Vegetables");

// Add child nodes
fruits.add(new DefaultMutableTreeNode("Apple"));
fruits.add(new DefaultMutableTreeNode("Banana"));
fruits.add(new DefaultMutableTreeNode("Orange"));

vegetables.add(new DefaultMutableTreeNode("Carrot"));
vegetables.add(new DefaultMutableTreeNode("Broccoli"));

// Build tree
root.add(fruits);
root.add(vegetables);

// Create tree
JTree tree = new JTree(root);

// Add to scroll pane
JScrollPane scrollPane = new JScrollPane(tree);
frame.add(scrollPane);

// Expand all nodes
for (int i = 0; i < tree.getRowCount(); i++) {
    tree.expandRow(i);
}

// Handle selection
tree.addTreeSelectionListener(e -> {
    DefaultMutableTreeNode node = (DefaultMutableTreeNode) 
        tree.getLastSelectedPathComponent();
    if (node != null) {
        System.out.println("Selected: " + node.getUserObject());
    }
});

// Customize tree
tree.setRootVisible(true);  // Show root
tree.setShowsRootHandles(true);  // Show handles (+/-)

// Create tree from array
String[] data = {"Parent", "Child 1", "Child 2", "Grandchild"};
// ... more complex tree building
```

**Visual:**
```
┌─────────────────────────────────────────────────────────────┐
│  ┌─────────────────────────────────────────────────────┐   │
│  │ ▼ Root                                              │   │
│  │   ▼ Fruits                                          │   │
│  │     ├── Apple                                       │   │
│  │     ├── Banana                                      │   │
│  │     └── Orange                                      │   │
│  │   ▶ Vegetables                                      │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  ◄─────────────── Scroll Pane ────────────────►            │
└─────────────────────────────────────────────────────────────┘
```

---

## Quick Reference Table

| Component      | Class            | Purpose                    |
| -------------- | ---------------- | -------------------------- |
| Option Dialog  | `JOptionPane`    | Quick popup messages/input |
| Custom Dialog  | `JDialog`        | Custom popup windows       |
| File Chooser   | `JFileChooser`   | Browse files               |
| Color Chooser  | `JColorChooser`  | Pick colors                |
| Frame          | `JFrame`         | Main window                |
| Internal Frame | `JInternalFrame` | Child window inside frame  |
| Table          | `JTable`         | Spreadsheet data           |
| Tree           | `JTree`          | Hierarchical data          |

---

## The Golden Rule

> **Use JOptionPane for simple popups (messages, confirmations, input). Use JDialog for complex custom dialogs. Use JFileChooser for file selection and JColorChooser for color selection. Use JInternalFrame for MDI applications (multiple windows inside one main window). Use JTable for tabular data and JTree for hierarchical data.**

**Memory trick:**
```
OptionDialog = Quick popup
JDialog = Custom popup
JFileChooser = Browse files
JColorChooser = Pick colors
JFrame = Main window
JInternalFrame = Window inside window
JTable = Rows and columns
JTree = Parent and children
```

Would you like me to explain **event handling** (how to respond to button clicks, menu selections, etc.) next?

---

## Q. Movie question with implementation of COM.DAT

```java
import java.io.*;

class MOVIE implements Serializable {
    String name, genre;
    MOVIE(String n, String g) { name = n; genre = g; }
}

public class Main {
    public static void main(String[] args) throws Exception {
        ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("COM.DAT"));
        
        MOVIE[] movies = {
            new MOVIE("The Hangover", "comedy"),
            new MOVIE("Inception", "sci-fi"),
            new MOVIE("Dumb & Dumber", "comedy"),
            new MOVIE("The Matrix", "action")
        };
        
        for (MOVIE m : movies)
            if (m.genre.equalsIgnoreCase("comedy"))
                out.writeObject(m);
        
        out.close();
    }
}
```

**Key Points:**
- `Serializable` allows objects to be written to file
- `ObjectOutputStream` writes objects to binary file `COM.DAT`
- Only movies with genre "comedy" are saved
- `equalsIgnoreCase()` handles case-insensitive comparison
## What is COM.DAT?

**COM.DAT** is just a **custom filename** you chose for your data file. It's not a special or standard file type - it's a name you made up.

```
Your Program
     ↓ (has MOVIE objects)
ObjectOutputStream  ← "Convert object to bytes"
     ↓ (sends bytes)
FileOutputStream    ← "Write bytes to file"
     ↓
COM.DAT File (created on disk)
```