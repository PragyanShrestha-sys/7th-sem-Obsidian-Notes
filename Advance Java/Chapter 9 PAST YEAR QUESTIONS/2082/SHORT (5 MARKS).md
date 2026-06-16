## Q1.  Write a program to insert an icon in the frame and when the user presses the up arrow, it will move upward. (Swing and Event handling)

```JAVA
import javax.swing.*;
import java.awt.event.*;

public class MoveIcon {
    public static void main(String[] args) {
        JFrame frame = new JFrame();
        JLabel icon = new JLabel(new ImageIcon("icon.png"));
        int y = 200;
        
        frame.setLayout(null);
        icon.setBounds(175, y, 50, 50);
        
        icon.addMouseListener(new MouseAdapter() {
            public void mouseClicked(MouseEvent e) {
                System.out.println("Clicked");
            }
        });
        
        frame.addKeyListener(new KeyAdapter() {
            public void keyPressed(KeyEvent e) {
                if (e.getKeyCode() == KeyEvent.VK_UP) {
                    y -= 10;
                    icon.setLocation(175, y);
                }
            }
        });
        
        frame.add(icon);
        frame.setSize(400, 400);
        frame.setFocusable(true);
        frame.setVisible(true);
    }
}
```
[[2082 q1 explanation]]

---

## How do you handle HTTP req and res in JSP with exmaple

[[Servlet vs JSP (Java Server Pages)]]

### JSP (request and response )
```jsp
<%-- This is messy for complex logic --%>
<%
<%@ page contentType="text/html" %>
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <form method="post">
        Name: <input name="username"><br>
        Pass: <input name="password" type="password"><br>
        <input type="submit" value="Login">
    </form>

    <%-- Login logic --%>
    <%
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        
        if (username != null && password != null) {
            if ("admin".equals(username) && "123".equals(password)) {
                session.setAttribute("user", username);
                response.sendRedirect("welcome.jsp");
            } else {
                out.print("<p style='color:red'>Invalid!</p>");
            }
        }
    %>
</body>
</html>
%>
```


---
## Q3. Life Cycle of Servlet


```
Container starts
      │
      ▼
┌─────────────────────────────────────────────────────────────┐
│ 1. LOAD: Container loads servlet class                      │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. INSTANTIATE: Container creates instance (once)           │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. INITIALIZE: Container calls init() (once)                │
│    - Load resources, database connections                   │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. SERVICE: Container calls service() for EACH request      │
│    - doGet() for GET requests                               │
│    - doPost() for POST requests                             │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. DESTROY: Container calls destroy() (once)                │
│    - Cleanup resources                                      │
└─────────────────────────────────────────────────────────────┘
```

[[GET AND POST REQUEST OF SERVELT CODE EXAMPLE]]

---
## Q4. ACCEPT ONLY "CSIT" AND REJECT OTEHRS ERORR HANDLINNG

```JAVA 
import java.util.Scanner;

class InvalidFacultyException extends Exception {
    public InvalidFacultyException(String message) {
        super(message);
    }
}

public class FacultyCheck {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Enter faculty name: ");
        String faculty = sc.nextLine();
        
        try {
            if (!faculty.equals("CSIT")) {
                throw new InvalidFacultyException("Error: Only CSIT faculty is allowed!");
            }
            System.out.println("Valid faculty: " + faculty);
        } catch (InvalidFacultyException e) {
            System.out.println(e.getMessage());
        }
        
        sc.close();
    }
}
```

---

## Q5. CALCULATOR WITH JAVA FX
```JAVA
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.stage.Stage;

public class CalculatorLayout extends Application {
    @Override
    public void start(Stage stage) {
        // Display
        TextField display = new TextField();
        display.setEditable(false);
        
        // Buttons
        String[] btns = {"7","8","9","+","4","5","6","-","1","2","3","*","0","C","=","/"};
        GridPane grid = new GridPane();
        
        int idx = 0;
        for (int row = 0; row < 4; row++) {
            for (int col = 0; col < 4; col++) {
                grid.add(new Button(btns[idx++]), col, row);
            }
        }
        
        // Layout
        VBox root = new VBox(10, display, grid);
        
        stage.setScene(new Scene(root, 250, 300));
        stage.setTitle("Calculator");
        stage.show();
    }
    
    public static void main(String[] args) {
        launch(args);
    }
}
```

USING SWING

```JAVA
import javax.swing.*;
import java.awt.*;

public class CalculatorLayout {
    public static void main(String[] args) {
        // Create JFrame object (not extend)
        JFrame frame = new JFrame();
        frame.setTitle("Calculator");
        frame.setSize(250, 300);
        frame.setLayout(new BorderLayout());
        // Display
        JTextField display = new JTextField();
        display.setEditable(false);
        frame.add(display, BorderLayout.NORTH);
        
        // Buttons
        String[] btns = {"7","8","9","+","4","5","6","-","1","2","3","*","0","C","=","/"};
        JPanel panel = new JPanel(new GridLayout(4, 4));
        
        for (String btn : btns) {
            panel.add(new JButton(btn));
        }
        
        frame.add(panel);
        
        // Make visible
        frame.setVisible(true);
    }
}
```

## Q. Packages Method overloading and overriding

## What is a Package?

A **package** in programming (particularly in Java-like languages) is a namespace that organizes a set of related classes and interfaces. Think of it as a folder in your file system that groups related files together.

### Key purposes of packages:
1. **Prevent naming conflicts** - Two classes can have the same name if they're in different packages
2. **Control access** - Package-private visibility allows members to be accessed only within the same package
3. **Organize code** - Group related functionality together (e.g., `java.util`, `java.io`)
4. **Facilitate maintenance** - Easier to locate and manage classes

---

## Method Overloading vs. Method Overriding

| Feature                | **Overloading**                                                                            | **Overriding**                                                                                  |
| ---------------------- | ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| **Definition**         | Multiple methods in the **same class** with the **same name** but **different parameters** | Subclass provides a **specific implementation** of a method already defined in its parent class |
| **Relationship**       | Within the same class or between parent/child classes                                      | Between parent and child classes (inheritance)                                                  |
| **Parameters**         | **Must differ** (number, type, or order)                                                   | **Must be identical**                                                                           |
| **Return type**        | Can be different                                                                           | Must be the same or covariant (subtype)                                                         |
| **Checked exceptions** | Can declare different exceptions                                                           | Cannot declare new/broader checked exceptions                                                   |
| **Binding**            | **Compile-time** (static binding)                                                          | **Runtime** (dynamic binding)                                                                   |
| **Keyword**            | No special keyword                                                                         | `@Override` annotation (optional but recommended)                                               |


### Examples:

**Overloading:**
```java
public class Calculator {
    // Same name, different parameters
    public int add(int a, int b) { return a + b; }
    public int add(int a, int b, int c) { return a + b + c; }
    public double add(double a, double b) { return a + b; }
}
```

**Overriding:**
```java
public class Animal {
    public void sound() {
        System.out.println("Animal makes sound");
    }
}

public class Dog extends Animal {
    @Override
    public void sound() {  // Same signature as parent
        System.out.println("Dog barks");
    }
}
```

### Key Insight:
- **Overloading** = Same method name, different parameters (compile-time polymorphism)
- **Overriding** = Same method signature, different implementation (runtime polymorphism)
---
## Q. Java applet and Swing hierarchy

applets were designed to be **embedded directly within HTML web pages** using the `<applet>` tag.
No, we do not need Java applets anymore, as the technology is completely obsolete and has been entirely removed from modern Java
==**Yes, exactly.**== Java applets were Java source code compiled into bytecode (`.class` files) that ran directly inside a web browser using the HTML `<applet>` tag

![[Pasted image 20260604075823.png]]

```
Level 1: Object (root of ALL Java classes)
    │
    ↓
Level 2: Component (anything drawable on screen)
    │
    ↓
Level 3: Container (anything that can HOLD other components)
    │
    ↓
Level 4: Window (top-level window without decorations)
    │
    ↓
Level 5: Frame (basic window with title bar) ← This is java.awt.Frame
    │
    ↓
Level 6: JComponent (base for ALL Swing components) ← Swing starts HERE!
    │
    ├──────────────────────────────────────────────────┐
    │                                                  │
    ↓                                                  ↓
AbstractButton                                    JLabel
    │                                                  │
    ├──────────┬──────────┬──────────┐                │
    ↓          ↓          ↓          ↓                │
JButton   JMenuItem  JToggleButton  (others)          │
              │           │                           │
              ↓           ├───────────┐               │
         JMenu           ↓           ↓               │
                   JCheckBox    JRadioButton         │
                   (through (through                  │
                   JToggle)  JToggle)                │
                                                      ↓
                                              JComboBox, JList,
                                              JTabbedPane, JTable,
                                              JTableHeader, JTree,
                                              JScrollBar, JScrollPane,
                                              JSlider, JSplitPane,
                                              JTextComponent
                                                  │
                                                  ↓
                                              (JTextField, JTextArea)
```
