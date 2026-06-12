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

| Aspect | Description |
|--------|-------------|
| **Purpose** | Quick popup windows for user interaction |
| **Advantage** | No need to create custom dialog windows |
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
        setLocationRelativeTo(parent);
        
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

// FILE FILTERS (show only certain file types)
FileNameExtensionFilter filter = new FileNameExtensionFilter(
    "Text Files", "txt", "text");
chooser.setFileFilter(filter);

// Multiple file selection
chooser.setMultiSelectionEnabled(true);
File[] files = chooser.getSelectedFiles();

// Default directory
chooser.setCurrentDirectory(new File(System.getProperty("user.home")));
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

public class InternalFrameDemo extends JFrame {
    
    public InternalFrameDemo() {
        setTitle("MDI Application");
        setSize(800, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Create desktop pane (holds internal frames)
        JDesktopPane desktop = new JDesktopPane();
        setContentPane(desktop);
        
        // Create internal frame
        JInternalFrame internalFrame = new JInternalFrame("Document 1", 
                                          true,  // resizable
                                          true,  // closable
                                          true,  // maximizable
                                          true); // iconifiable (minimize)
        
        // Add content
        JTextArea textArea = new JTextArea();
        internalFrame.add(new JScrollPane(textArea));
        
        internalFrame.setSize(300, 200);
        internalFrame.setVisible(true);
        
        // Add to desktop
        desktop.add(internalFrame);
        
        // Create multiple internal frames
        JInternalFrame anotherFrame = new JInternalFrame("Document 2", true, true, true, true);
        anotherFrame.setSize(300, 200);
        anotherFrame.setLocation(100, 100);
        anotherFrame.setVisible(true);
        desktop.add(anotherFrame);
        
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new InternalFrameDemo();
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
table.setRowHeight(25);
table.setShowGrid(true);
table.setGridColor(Color.GRAY);

// Selection modes
table.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
// OR
table.setSelectionMode(ListSelectionModel.MULTIPLE_INTERVAL_SELECTION);

// Get selected data
int selectedRow = table.getSelectedRow();
if (selectedRow != -1) {
    String name = (String) table.getValueAt(selectedRow, 1);
    System.out.println("Selected: " + name);
}

// Create table model (better for dynamic data)
DefaultTableModel model = new DefaultTableModel(columns, 0);
model.addRow(new Object[]{5, "Eve", 29, "IT"});
table.setModel(model);

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

## Complete Example: Document Editor with All Components

```java
import javax.swing.*;
import javax.swing.tree.*;
import javax.swing.table.*;
import java.awt.*;
import java.awt.event.*;
import java.io.File;

public class AdvancedComponentsDemo extends JFrame {
    
    private JDesktopPane desktop;
    private JTable dataTable;
    private JTree fileTree;
    
    public AdvancedComponentsDemo() {
        setTitle("Advanced Components Demo");
        setSize(900, 700);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Create menu bar
        JMenuBar menuBar = new JMenuBar();
        
        // File menu
        JMenu fileMenu = new JMenu("File");
        JMenuItem openItem = new JMenuItem("Open");
        openItem.addActionListener(e -> showFileChooser());
        fileMenu.add(openItem);
        
        JMenuItem colorItem = new JMenuItem("Choose Color");
        colorItem.addActionListener(e -> showColorChooser());
        fileMenu.add(colorItem);
        
        JMenuItem dialogItem = new JMenuItem("Show Dialog");
        dialogItem.addActionListener(e -> showOptionDialog());
        fileMenu.add(dialogItem);
        
        JMenuItem newFrameItem = new JMenuItem("New Internal Frame");
        newFrameItem.addActionListener(e -> createInternalFrame());
        fileMenu.add(newFrameItem);
        
        fileMenu.addSeparator();
        JMenuItem exitItem = new JMenuItem("Exit");
        exitItem.addActionListener(e -> System.exit(0));
        fileMenu.add(exitItem);
        
        menuBar.add(fileMenu);
        setJMenuBar(menuBar);
        
        // Split pane for tree and table
        JSplitPane splitPane = new JSplitPane(JSplitPane.HORIZONTAL_SPLIT);
        
        // Create tree panel (left)
        JPanel treePanel = new JPanel(new BorderLayout());
        treePanel.setBorder(BorderFactory.createTitledBorder("File Explorer"));
        createFileTree();
        treePanel.add(new JScrollPane(fileTree), BorderLayout.CENTER);
        
        // Create table panel (right)
        JPanel tablePanel = new JPanel(new BorderLayout());
        tablePanel.setBorder(BorderFactory.createTitledBorder("Data Table"));
        createDataTable();
        tablePanel.add(new JScrollPane(dataTable), BorderLayout.CENTER);
        
        splitPane.setLeftComponent(treePanel);
        splitPane.setRightComponent(tablePanel);
        splitPane.setDividerLocation(250);
        
        // Desktop for internal frames
        desktop = new JDesktopPane();
        desktop.setBorder(BorderFactory.createTitledBorder("Internal Frames"));
        
        // Main content
        JSplitPane mainSplit = new JSplitPane(JSplitPane.VERTICAL_SPLIT);
        mainSplit.setTopComponent(splitPane);
        mainSplit.setBottomComponent(desktop);
        mainSplit.setDividerLocation(400);
        
        add(mainSplit);
        setVisible(true);
    }
    
    private void createFileTree() {
        DefaultMutableTreeNode root = new DefaultMutableTreeNode("My Computer");
        
        DefaultMutableTreeNode documents = new DefaultMutableTreeNode("Documents");
        documents.add(new DefaultMutableTreeNode("resume.txt"));
        documents.add(new DefaultMutableTreeNode("notes.txt"));
        
        DefaultMutableTreeNode pictures = new DefaultMutableTreeNode("Pictures");
        pictures.add(new DefaultMutableTreeNode("vacation.jpg"));
        pictures.add(new DefaultMutableTreeNode("family.png"));
        
        root.add(documents);
        root.add(pictures);
        
        fileTree = new JTree(root);
        fileTree.addTreeSelectionListener(e -> {
            DefaultMutableTreeNode node = (DefaultMutableTreeNode) 
                fileTree.getLastSelectedPathComponent();
            if (node != null && node.isLeaf()) {
                JOptionPane.showMessageDialog(this, 
                    "Opening: " + node.getUserObject(),
                    "File Selected", 
                    JOptionPane.INFORMATION_MESSAGE);
            }
        });
    }
    
    private void createDataTable() {
        String[] columns = {"ID", "Name", "Role", "Status"};
        Object[][] data = {
            {1, "Alice", "Developer", "Active"},
            {2, "Bob", "Designer", "Active"},
            {3, "Charlie", "Manager", "Inactive"},
            {4, "Diana", "Tester", "Active"}
        };
        dataTable = new JTable(data, columns);
        dataTable.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
    }
    
    private void showFileChooser() {
        JFileChooser chooser = new JFileChooser();
        int result = chooser.showOpenDialog(this);
        if (result == JFileChooser.APPROVE_OPTION) {
            File file = chooser.getSelectedFile();
            JOptionPane.showMessageDialog(this, 
                "Selected file: " + file.getName(),
                "File Chooser", 
                JOptionPane.INFORMATION_MESSAGE);
        }
    }
    
    private void showColorChooser() {
        Color color = JColorChooser.showDialog(this, "Pick a Color", Color.RED);
        if (color != null) {
            desktop.setBackground(color);
        }
    }
    
    private void showOptionDialog() {
        String[] options = {"Save", "Don't Save", "Cancel"};
        int result = JOptionPane.showOptionDialog(this, 
            "Do you want to save changes?", "Save File",
            JOptionPane.DEFAULT_OPTION, JOptionPane.QUESTION_MESSAGE,
            null, options, options[0]);
        
        if (result == 0) {
            JOptionPane.showMessageDialog(this, "File saved!");
        } else if (result == 1) {
            JOptionPane.showMessageDialog(this, "Changes discarded");
        }
    }
    
    private void createInternalFrame() {
        int count = desktop.getAllFrames().length + 1;
        JInternalFrame frame = new JInternalFrame("Document " + count, 
            true, true, true, true);
        
        JTextArea textArea = new JTextArea();
        textArea.setLineWrap(true);
        frame.add(new JScrollPane(textArea));
        
        frame.setSize(300, 200);
        frame.setLocation(count * 30, count * 30);
        frame.setVisible(true);
        desktop.add(frame);
        
        try {
            frame.setSelected(true);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new AdvancedComponentsDemo());
    }
}
```

---

## Quick Reference Table

| Component | Class | Purpose |
|-----------|-------|---------|
| Option Dialog | `JOptionPane` | Quick popup messages/input |
| Custom Dialog | `JDialog` | Custom popup windows |
| File Chooser | `JFileChooser` | Browse files |
| Color Chooser | `JColorChooser` | Pick colors |
| Frame | `JFrame` | Main window |
| Internal Frame | `JInternalFrame` | Child window inside frame |
| Table | `JTable` | Spreadsheet data |
| Tree | `JTree` | Hierarchical data |

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