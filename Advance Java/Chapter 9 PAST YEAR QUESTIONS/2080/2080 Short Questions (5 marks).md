## List the steps to create a RMI application. Differentiate between RMI and CORBA

[[RMI Code Short]]

library funcitons used 
import javax.rmi
import javax.rmi.naming
iport javax.rmi.registry.LocateRegistry
Interface decalre
define interface ()
register interface(server side) (LocateRegistry.CreateRegistry and naming.rebind)
Call interface(client side) (Naming.Lookup)

---
![[Pasted image 20260616194956.png]]


---
![[Pasted image 20260617062742.png]]
```java
import java.sql.*;

public class MovieDB {
    public static void main(String[] args) throws Exception {
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "root", "password");
        
        // Insert 3 records in one line
        conn.createStatement().executeUpdate("INSERT INTO MOVIE VALUES(1,'Jatra','Drama'),(2,'Chha','Horror'),(3,'Kabhaddi','Action')");
        
        // Update genre using prepared statement
        PreparedStatement ps = conn.prepareStatement("UPDATE MOVIE SET genre=? WHERE title=?");
        ps.setString(1, "Comedy");//1 bhaneko first '?'
        ps.setString(2, "Jatra"); // 2 bhaneko second '?'
        ps.executeUpdate();
        
        conn.close();
    }
}
```


---
## Tables 
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


![[Pasted image 20260617063850.png]]

## Complete Code: Sending a Plain Text Email

JSP implicit objects are ==predefined Java objects created automatically by the web container during the translation of a JSP page into a Servlet==. You can use them directly in your code without having to declare or instantiate them first. 

| Object        | Type                  | Description                     |
| ------------- | --------------------- | ------------------------------- |
| `out`         | `JspWriter`           | Sends output to browser         |
| `request`     | `HttpServletRequest`  | Client request data             |
| `response`    | `HttpServletResponse` | Server response                 |
| `session`     | `HttpSession`         | User session data               |
| `application` | `ServletContext`      | Application-wide data           |
| `config`      | `ServletConfig`       | Servlet configuration           |
| `pageContext` | `PageContext`         | Page-scoped data and utilities  |
| `page`        | `Object`              | Current servlet instance        |
| `exception`   | `Throwable`           | Error object (error pages only) |

```java
import java.util.Properties;           // For setting configuration properties
import javax.mail.*;                   // Main JavaMail classes
import javax.mail.internet.*;          // Internet-specific email classes (MIME)

public class EmailSender {
    
    public static void main(String[] args) {
        
        // ========== CONFIGURATION ==========
        
        // 1. Set up mail server properties
        // Properties object holds configuration parameters for the mail session
        Properties props = new Properties();
        // Enable authentication (server requires username/password)
        props.put("mail.smtp.auth", "true"); 
        // SMTP server address (for Gmail: smtp.gmail.com)
        props.put("mail.smtp.host", "smtp.gmail.com");
        
        // SMTP server port (587 is standard TLS port)
        props.put("mail.smtp.port", "587");
        

        //This creates a **mail session** - a connection factory that holds all your email configuration and can create messages.
        Session session = Session.getInstance(props);
        
        
        
        try {
            // ========== CREATE MESSAGE ==========
            
            // 3. Create a MimeMessage object (represents the email)
            MimeMessage message = new MimeMessage(session);
            
            // 4. Set the sender's email address
            // InternetAddress validates and formats email addresses
            message.setFrom(new InternetAddress("your-email@gmail.com"));
            
            // 5. Set the recipient(s)
            // RecipientType.TO = primary recipient
            // Other types: CC (carbon copy), BCC (blind carbon copy)
            message.setRecipients(Message.RecipientType.TO, 
                InternetAddress.parse("recipient@example.com"));
            
            // 6. Set the email subject
            message.setSubject("Test Email from Java");
            
            // 7. Set the email body (plain text)
            // Use setText() for plain text, setContent() for HTML
            message.setText("Hello! This is a test email sent from Java using JavaMail API.");
            
            // ========== SEND MESSAGE ==========
            
            // 8. Send the email
            // Transport.send() is a static convenience method
            // It gets the transport from the session and sends the message
            Transport.send(message);
            
            System.out.println("Email sent successfully!");
            
        } catch (MessagingException e) {
            // MessagingException is the parent of all JavaMail errors
            System.out.println("Failed to send email: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```


main methods yad garna parne 
```java 
   Properties props = new Properties();
        props.put("mail.smtp.auth", "true"); 
        props.put("mail.smtp.host", "smtp.gmail.com");
        props.put("mail.smtp.port", "587");

        Session session = Session.getInstance(props);

            MimeMessage message = new MimeMessage(session);

            message.setFrom(new InternetAddress("your-email@gmail.com"));
            message.setRecipients(Message.RecipientType.TO, 
                InternetAddress.parse("recipient@example.com"));
            message.setSubject("Test Email from Java");
			message.setText("Hello! This is a test email sent from Java using JavaMail API.");

            Transport.send(message);

            
```

----
![[Pasted image 20260617071851.png]]

## Role of Result Sets

A **ResultSet** in JDBC serves as a **data container** that holds the results of a SQL query. Its key roles are:

1. **Data Storage**: Stores tabular data returned from database queries
2. **Data Navigation**: Provides cursor-based navigation through rows
3. **Data Retrieval**: Allows reading column values using various getter methods
4. **Data Update** (optional): Can update rows in the result set (if scrollable/updatable)
5. **Metadata Access**: Provides information about column names, types, and properties

## Issues in Your Code

```java
public class Point {
   int p;

   public void setP(int p) {
      p = p;
   }
}
```

### Problems:
1. **Variable Shadowing**: The parameter `p` has the same name as the instance variable `p`
2. **No `this` Reference**: The assignment `p = p` assigns the parameter to itself, not the instance variable
3. **Missing Getter**: No method to retrieve the value
4. **No Constructor**: Could benefit from a constructor for initialization


### Fixed Code:


```java

## Complete Example with Usage

```java
public class Point {
    private int p;  // Made private for encapsulation

    // Option 1: Use 'this' to distinguish instance variable
    public void setP(int p) {
        this.p = p;  // 'this.p' refers to instance variable, 'p' is parameter
    }
    
    // Option 2: Rename parameter (alternative)
    public void setP(int newP) {
        p = newP;  // No confusion now
    }
    
}
```

## The Rule to Remember

> **When a method parameter has the same name as an instance variable, use `this.variableName` to refer to the instance variable.**

---
![[Pasted image 20260617073825.png]]

[[tcp client and server returing greatest number among other numbers]]

---
![[Pasted image 20260617075348.png]]

```java
import javafx.application.*;
import javafx.scene.*;
import javafx.scene.control.*;
import javafx.stage.*;

public class Menu extends Application {
    public void start(Stage s) {
        // Create menu items separately
        MenuItem newItem = new MenuItem("New");
        MenuItem saveItem = new MenuItem("Save");
        MenuItem exitItem = new MenuItem("Exit");
        
        // Create menu and add items
        Menu file = new Menu("File");
        file.getItems().addAll(newItem, saveItem, exitItem);
        
        // Create menu bar and add menu
        MenuBar mb = new MenuBar();
        mb.getMenus().add(file);
        
        // Set scene and show
        s.setScene(new Scene(new VBox(mb), 300, 200));
        s.show();
    }
    public static void main(String[] args) { launch(args); }
}
```

----
Question refrences: https://hamrocsit.com/semester/seventh/advanced-java//question-bank/2080