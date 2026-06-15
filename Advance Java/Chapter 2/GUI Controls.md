Here's a **complete theoretical explanation** of all the GUI controls you listed.

---

## What are GUI Controls?

**GUI Controls** (also called components or widgets) are the interactive elements that users see and interact with in a graphical user interface.

```
┌─────────────────────────────────────────────────────────────┐
│                        MY FORM                              │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ Name: [_______________]  ← Text Field               │   │
│  │                                                     │   │
│  │ Password: [**********]  ← Password Field           │   │
│  │                                                     │   │
│  │ Description: ┌─────────────────────────────────┐   │   │
│  │              │                                 │   │   │
│  │              │    Text Area                    │   │   │
│  │              │                                 │   │   │
│  │              └─────────────────────────────────┘   │   │
│  │                                                     │   │
│  │ ☑ Checkbox 1    ☑ Checkbox 2    ← Check Boxes      │   │
│  │                                                     │   │
│  │ ○ Option 1     ● Option 2       ← Radio Buttons    │   │
│  │                                                     │   │
│  │ [▼ Select Item]                 ← Combo Box        │   │
│  │                                                     │   │
│  │ ├─────┼─────┤                   ← Slider           │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

---

## 1. Labels (JLabel)

**What it is:** A non-editable text or image display.

| Aspect             | Description                                |
| ------------------ | ------------------------------------------ |
| **Purpose**        | Display static text or images              |
| **User can edit?** | ❌ No (display only)                        |
| **Common uses**    | Field labels, titles, instructions, images |

```java
// Basic label
JLabel label = new JLabel("Enter your name:");

// Label with icon
JLabel imageLabel = new JLabel(new ImageIcon("icon.png"));

// Label with alignment
JLabel centerLabel = new JLabel("Centered", SwingConstants.CENTER);
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ Enter your name:                        │ ← Label
│ [________________________]              │
│                                         │
│ ┌─────┐                                 │
│ │Icon │ Label with image                │ ← Label with icon
│ └─────┘                                 │
└─────────────────────────────────────────┘
```

---

## 2. Text Fields (JTextField)

**What it is:** A single-line text input area.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Get single-line text input from user |
| **User can edit?** | ✅ Yes |
| **Common uses** | Name, email, address, single values |

```java
// Basic text field (20 columns wide)
JTextField textField = new JTextField(20);

// With initial text
JTextField nameField = new JTextField("Enter name here", 20);

// Get text from field
String text = textField.getText();

// Set text
textField.setText("New value");
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ Name: [________________________]        │
│        ↑                                │
│        └─ Text Field (single line)      │
└─────────────────────────────────────────┘
```

---

## 3. Password Fields (JPasswordField)

**What it is:** A text field that hides the input (shows dots or asterisks).

| Aspect | Description |
|--------|-------------|
| **Purpose** | Securely get password input |
| **User can edit?** | ✅ Yes |
| **Visibility** | Characters are masked (• or *) |
| **Common uses** | Passwords, PIN codes, sensitive data |

```java
// Password field
JPasswordField passwordField = new JPasswordField(20);

// Get password (returns char array for security)
char[] password = passwordField.getPassword();

// Get password as string (less secure)
String passwordStr = new String(passwordField.getPassword());
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ Password: [•••••••••••••]               │
│            ↑                            │
│            └─ Masked characters         │
└─────────────────────────────────────────┘
```

**Why char array vs String?** Security - you can clear char array immediately after use.

---

## 4. Text Areas (JTextArea)

**What it is:** A multi-line text input area.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Get multiple lines of text input |
| **User can edit?** | ✅ Yes |
| **Lines** | Multiple (wraps automatically) |
| **Common uses** | Comments, descriptions, notes, logs |

```java
// Text area (rows, columns)
JTextArea textArea = new JTextArea(10, 40);

// Enable line wrapping
textArea.setLineWrap(true);
textArea.setWrapStyleWord(true);

// Get text
String text = textArea.getText();

// Set text
textArea.setText("New content\nMultiple lines");
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ Description:                            │
│ ┌─────────────────────────────────────┐ │
│ │ This is a multi-line                │ │
│ │ text area that can hold             │ │
│ │ many lines of text.                 │ │
│ │                                     │ │
│ │ Users can type long descriptions    │ │
│ │ here.                               │ │
│ └─────────────────────────────────────┘ │
└─────────────────────────────────────────┘
```

---

## 5. Scroll Panes (JScrollPane)

**What it is:** A container that adds scrolling ability to another component.

| Aspect               | Description                                  |
| -------------------- | -------------------------------------------- |
| **Purpose**          | Add scroll bars to components                |
| **What it contains** | One component (usually a text area or table) |
| **Common uses**      | Large text areas, tables, lists, images      |


```java
// Create text area
JTextArea textArea = new JTextArea(20, 50);

// Wrap in scroll pane (adds scroll bars)
JScrollPane scrollPane = new JScrollPane(textArea);

// Control scroll bar visibility
scrollPane.setHorizontalScrollBarPolicy(JScrollPane.HORIZONTAL_SCROLLBAR_AS_NEEDED);
scrollPane.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ ┌─────────────────────────────────────┐ │
│ │                                     │ │
│ │                                     │ │
│ │        Large Content Area           │ │
│ │                                     │ │
│ │                                     │ │
│ │                                     │ │
│ └─────────────────────────────────────┘ │
│ ◄─────────── Scroll Bar ────────────►  │
└─────────────────────────────────────────┘
```

**Important:** JScrollPane wraps around ONE component to make it scrollable.

---

## 6. Check Boxes (JCheckBox)

**What it is:** A component that can be checked (on) or unchecked (off).

| Aspect | Description |
|--------|-------------|
| **Purpose** | Select/deselect an option |
| **States** | Selected (true) or deselected (false) |
| **Selection rule** | Multiple checkboxes can be selected independently |
| **Common uses** | Preferences, features, options, agreements |

```java
// Create checkbox
JCheckBox checkBox = new JCheckBox("Enable Feature");

// Initially selected
JCheckBox defaultChecked = new JCheckBox("Subscribe", true);

// Check state
boolean isSelected = checkBox.isSelected();

// Set state
checkBox.setSelected(true);

// Add action listener
checkBox.addActionListener(e -> {
    if (checkBox.isSelected()) {
        System.out.println("Checked");
    }
});
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ ☑ Enable notifications                   │ ← Checked
│ ☐ Remember me                           │ ← Unchecked
│ ☑ Agree to terms                        │ ← Checked
└─────────────────────────────────────────┘

☑ = Selected (true)
☐ = Deselected (false)
```

---

## 7. Radio Buttons (JRadioButton)

**What it is:** Buttons that work in groups where only ONE can be selected at a time.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Choose one option from a group |
| **Selection rule** | Only ONE in the group can be selected |
| **Common uses** | Gender selection, payment method, yes/no options |

```java
// Create radio buttons
JRadioButton option1 = new JRadioButton("Option 1");
JRadioButton option2 = new JRadioButton("Option 2");
JRadioButton option3 = new JRadioButton("Option 3");

// Group them (only one can be selected)
ButtonGroup group = new ButtonGroup();
group.add(option1);
group.add(option2);
group.add(option3);

// Default selection
option1.setSelected(true);

// Get selected
if (option1.isSelected()) {
    System.out.println("Option 1 chosen");
}
```

**Visual:**
```
┌─────────────────────────────────────────┐
│ Payment Method:                         │
│ ○ Credit Card                           │
│ ● PayPal        ← Selected (only one)   │
│ ○ Bank Transfer                         │
└─────────────────────────────────────────┘

○ = Not selected
● = Selected
Only ONE can be ● at a time!
```

**Important:** ButtonGroup only controls logical grouping. You still need to add radio buttons to the panel separately.

---

## 8. Borders (Border)

**What it is:** A decorative edge around a component.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Visually group components, add spacing, decorate |
| **Applies to** | Any JComponent (JPanel, JLabel, JButton, etc.) |

```java
import javax.swing.border.*;

// Types of borders
JPanel panel = new JPanel();

// 1. Line border (simple colored line)
panel.setBorder(BorderFactory.createLineBorder(Color.BLACK));

// 2. Titled border (with title text)
panel.setBorder(BorderFactory.createTitledBorder("User Information"));

// 3. Etched border (3D effect)
panel.setBorder(BorderFactory.createEtchedBorder());

// 4. Bevel border (raised or lowered)
panel.setBorder(BorderFactory.createRaisedBevelBorder());

// 5. Empty border (just spacing)
panel.setBorder(BorderFactory.createEmptyBorder(10, 10, 10, 10));

// 6. Compound border (multiple borders combined)
Border line = BorderFactory.createLineBorder(Color.GRAY);
Border titled = BorderFactory.createTitledBorder(line, "Details");
panel.setBorder(titled);
```

**Visual:**
```
Without Border:              With Titled Border:
┌─────────────────┐          ┌─────────────────────────────────┐
│ Name: [_____]   │          │ User Information               │
│ Age:  [_____]   │          ├─────────────────────────────────┤
└─────────────────┘          │ Name: [_____]  Age: [_____]     │
                             └─────────────────────────────────┘

Line Border:                  Etched Border:
┌─────────────────┐          ┌─────────────────────────────────┐
│ Name: [_____]   │          │ ┌─────────────────────────────┐ │
│ Age:  [_____]   │          │ │ Name: [_____]  Age: [_____] │ │
└─────────────────┘          │ └─────────────────────────────┘ │
(thin line around)           └─────────────────────────────────┘
                             (3D sunken effect)
```

---

## 9. Combo Boxes (JComboBox)

**What it is:** A dropdown list where users can select one option.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Select one option from a list |
| **Appearance** | Shows one item, dropdown shows all |
| **Editable** | Can allow custom input (optional) |
| **Common uses** | Country selection, category picker, quantity |

```java
// Create combo box with items
String[] items = {"Option 1", "Option 2", "Option 3"};
JComboBox<String> comboBox = new JComboBox<>(items);

// Add items dynamically
comboBox.addItem("Option 4");
comboBox.removeItem("Option 2");

// Get selected item
String selected = (String) comboBox.getSelectedItem();

// Get selected index
int index = comboBox.getSelectedIndex();

// Editable combo box (user can type)
comboBox.setEditable(true);
```

**Visual:**
```
Normal state:                 Dropdown open:
┌─────────────────┐          ┌─────────────────┐
│ Option 2      ▼│          │ Option 1        │
└─────────────────┘          │ Option 2 ◄───── │ Selected
                             │ Option 3        │
                             └─────────────────┘

After selection:              Editable combo box:
┌─────────────────┐          ┌─────────────────┐
│ Option 3      ▼│          │ Custom text   ▼│
└─────────────────┘          └─────────────────┘
```

---

## 10. Sliders (JSlider)

**What it is:** A component that lets users select a value by dragging a knob along a track.

| Aspect | Description |
|--------|-------------|
| **Purpose** | Select a value from a continuous range |
| **Orientation** | Horizontal or vertical |
| **Common uses** | Volume control, brightness, price range, zoom level |

```java
// Horizontal slider (min, max, initial)
JSlider slider = new JSlider(0, 100, 50);

// Vertical slider
JSlider verticalSlider = new JSlider(JSlider.VERTICAL, 0, 100, 50);

// Show tick marks
slider.setMajorTickSpacing(20);   // Major ticks every 20
slider.setMinorTickSpacing(5);    // Minor ticks every 5
slider.setPaintTicks(true);       // Show tick marks
slider.setPaintLabels(true);      // Show numeric labels

// Get value
int value = slider.getValue();

// Add change listener
slider.addChangeListener(e -> {
    int val = slider.getValue();
    System.out.println("Slider value: " + val);
});
```

**Visual:**
```
Horizontal Slider:
├─────┼─────┼─────┼─────┼─────┤
0     20    40    60    80    100
      ↑
    Knob at 40

Vertical Slider:
    100
     │
    80
     │
    60
─────●─────  ← Knob at 60
    40
     │
    20
     │
     0

With Labels:
├───┼───┼───┼───┼───┤
0   25  50  75  100
```

---

## Quick Reference Table

| Control | Class | Purpose | Editable? |
|---------|-------|---------|-----------|
| Label | `JLabel` | Display text/image | ❌ No |
| Text Field | `JTextField` | Single line input | ✅ Yes |
| Password Field | `JPasswordField` | Password input (masked) | ✅ Yes |
| Text Area | `JTextArea` | Multi-line input | ✅ Yes |
| Scroll Pane | `JScrollPane` | Add scrolling | Container |
| Check Box | `JCheckBox` | Yes/no selection | ✅ Yes |
| Radio Button | `JRadioButton` | One of many selection | ✅ Yes |
| Border | `Border` | Decorate component | N/A |
| Combo Box | `JComboBox` | Dropdown selection | ✅ Optional |
| Slider | `JSlider` | Range selection | ✅ Yes |

---

## Complete Example: Registration Form

```java
import javax.swing.*;
import javax.swing.border.*;
import java.awt.*;

public class RegistrationForm extends JFrame {
    
    public RegistrationForm() {
        setTitle("User Registration");
        setSize(500, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Main panel with border layout
        JPanel mainPanel = new JPanel(new BorderLayout(10, 10));
        mainPanel.setBorder(BorderFactory.createEmptyBorder(10, 10, 10, 10));
        
        // Form panel with GridBagLayout
        JPanel formPanel = new JPanel(new GridBagLayout());
        formPanel.setBorder(BorderFactory.createTitledBorder("Personal Information"));
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5);
        gbc.anchor = GridBagConstraints.WEST;
        
        // Labels and Text Fields
        gbc.gridx = 0; gbc.gridy = 0;
        formPanel.add(new JLabel("Name:"), gbc);
        gbc.gridx = 1;
        formPanel.add(new JTextField(20), gbc);
        
        gbc.gridx = 0; gbc.gridy = 1;
        formPanel.add(new JLabel("Email:"), gbc);
        gbc.gridx = 1;
        formPanel.add(new JTextField(20), gbc);
        
        gbc.gridx = 0; gbc.gridy = 2;
        formPanel.add(new JLabel("Password:"), gbc);
        gbc.gridx = 1;
        formPanel.add(new JPasswordField(20), gbc);
        
        // Radio Buttons for Gender
        gbc.gridx = 0; gbc.gridy = 3;
        formPanel.add(new JLabel("Gender:"), gbc);
        gbc.gridx = 1;
        JPanel genderPanel = new JPanel(new FlowLayout(FlowLayout.LEFT));
        JRadioButton male = new JRadioButton("Male");
        JRadioButton female = new JRadioButton("Female");
        ButtonGroup genderGroup = new ButtonGroup();
        genderGroup.add(male);
        genderGroup.add(female);
        genderPanel.add(male);
        genderPanel.add(female);
        formPanel.add(genderPanel, gbc);
        
        // Check Boxes for Interests
        gbc.gridx = 0; gbc.gridy = 4;
        formPanel.add(new JLabel("Interests:"), gbc);
        gbc.gridx = 1;
        JPanel interestPanel = new JPanel(new FlowLayout(FlowLayout.LEFT));
        interestPanel.add(new JCheckBox("Reading"));
        interestPanel.add(new JCheckBox("Music"));
        interestPanel.add(new JCheckBox("Sports"));
        formPanel.add(interestPanel, gbc);
        
        // Combo Box for Country
        gbc.gridx = 0; gbc.gridy = 5;
        formPanel.add(new JLabel("Country:"), gbc);
        gbc.gridx = 1;
        String[] countries = {"Select Country", "USA", "UK", "Canada", "Australia"};
        JComboBox<String> countryCombo = new JComboBox<>(countries);
        formPanel.add(countryCombo, gbc);
        
        // Slider for Age
        gbc.gridx = 0; gbc.gridy = 6;
        formPanel.add(new JLabel("Age:"), gbc);
        gbc.gridx = 1;
        JSlider ageSlider = new JSlider(0, 100, 25);
        ageSlider.setMajorTickSpacing(25);
        ageSlider.setMinorTickSpacing(5);
        ageSlider.setPaintTicks(true);
        ageSlider.setPaintLabels(true);
        formPanel.add(ageSlider, gbc);
        
        // Text Area with Scroll Pane
        gbc.gridx = 0; gbc.gridy = 7;
        formPanel.add(new JLabel("Bio:"), gbc);
        gbc.gridx = 1;
        JTextArea bioArea = new JTextArea(5, 20);
        bioArea.setLineWrap(true);
        JScrollPane scrollPane = new JScrollPane(bioArea);
        formPanel.add(scrollPane, gbc);
        
        // Button Panel
        JPanel buttonPanel = new JPanel(new FlowLayout());
        buttonPanel.setBorder(BorderFactory.createEtchedBorder());
        buttonPanel.add(new JButton("Submit"));
        buttonPanel.add(new JButton("Reset"));
        buttonPanel.add(new JButton("Cancel"));
        
        // Add panels to main panel
        mainPanel.add(formPanel, BorderLayout.CENTER);
        mainPanel.add(buttonPanel, BorderLayout.SOUTH);
        
        add(mainPanel);
        setVisible(true);
    }
    
    public static void main(String[] args) {
        new RegistrationForm();
    }
}
```

---

## The Golden Rule

> **GUI controls are the building blocks of user interfaces. Labels display text, Text Fields get single-line input, Password Fields mask sensitive input, Text Areas get multi-line input, Scroll Panes add scrolling, Check Boxes toggle options, Radio Buttons select one from a group, Borders decorate panels, Combo Boxes provide dropdown selection, and Sliders select from a range.**

**Memory trick:**
```
Text input: JTextField (single line), JTextArea (multi-line), JPasswordField (masked)
Selection: JCheckBox (multiple), JRadioButton (one), JComboBox (dropdown)
Range: JSlider
Display: JLabel
Scroll: JScrollPane
Decoration: Border
```

Would you like me to explain **event handling** (how to respond to button clicks, text changes, etc.) next?