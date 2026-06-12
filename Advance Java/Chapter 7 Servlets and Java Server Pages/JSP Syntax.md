# JSP Syntax Elements - Complete Explanation

Here's a **complete explanation** of the 5 main JSP syntax elements.

---

## The 5 JSP Syntax Elements

| Element | Syntax | Purpose |
|---------|--------|---------|
| **Directive** | `<%@ ... %>` | Instructions to JSP container |
| **Declaration** | `<%! ... %>` | Declare variables/methods (class level) |
| **Expression** | `<%= ... %>` | Output value (converted to String) |
| **Scriptlet** | `<% ... %>` | Java code block (executed) |
| **Comment** | `<%-- ... --%>` | JSP comment (not sent to browser) |

---

## 1. Directives (`<%@ ... %>`)

**What it is:** Instructions to the JSP container about how to process the page.

 A JSP **directive** (like `<%@ page ... %>`, `<%@ include ... %>`, or `<%@ taglib ... %>`) is only evaluated and processed during the **translation phase** when the JSP container converts the `.jsp` file into a Java servlet (`.java`).

### Types of Directives

| Directive | Purpose                               | Example                              |
| --------- | ------------------------------------- | ------------------------------------ |
| `page`    | Page settings (imports, content type) | `<%@ page import="java.util.*" %>`   |
| `include` | Include another file                  | `<%@ include file="header.jsp" %>`   |
| `taglib`  | Use tag library (JSTL)                | `<%@ taglib uri="..." prefix="c" %>` |
|           |                                       |                                      |
note: **JSTL** (JavaServer Pages Standard Tag Library) is ==a collection of reusable JSP tags that replace embedded Java code (scriptlets)==.

![[Pasted image 20260608132311.png|697]]
### Page Directive Attributes

```jsp
<%@ page import="java.util.*, java.sql.*" %>
<%@ page contentType="text/html; charset=UTF-8" %>
<%@ page errorPage="error.jsp" %>
<%@ page isErrorPage="true" %>
<%@ page session="true" %>
<%@ page buffer="16kb" %>
<%@ page isThreadSafe="true" %>
```

**Analogy:** Directives are like **instructions to the chef** before cooking starts.

---

## 2. Declarations (`<%! ... %>`)

**What it is:** Declares variables or methods that become part of the servlet class (outside the service method).

### Declaration Examples

```jsp
<%! 
    // Class-level variable (shared across ALL requests)
    private int visitCount = 0;
    
    // Class-level method
    public String formatDate(java.util.Date d) {
        return d.toString();
    }
    
    // Static block (runs once when class loads)
    static {
        System.out.println("Class loaded");
    }
    
    // Constant
    public static final double PI = 3.14159;
%>
```

### Using the Declaration

```jsp
<% 
    visitCount++;  // Increment shared counter
%>
<p>Total visits: <%= visitCount %></p>
<p>PI value: <%= PI %></p>
<p>Formatted date: <%= formatDate(new java.util.Date()) %></p>
```

### Declaration vs Scriptlet (Important!)

| Declaration (`<%! %>`) | Scriptlet (`<% %>`) |
|------------------------|---------------------|
| Becomes class-level member | Goes inside `_jspService()` method |
| Executed ONCE when class loads | Executed for EVERY request |
| Can declare methods | Cannot declare methods |
| Shared across ALL users | Separate for each request |
| Use for constants, utilities | Use for request processing |

**Analogy:** Declaration = **Blueprint of the house** (created once). Scriptlet = **Living in the house** (happens every day).

---

## 3. Expression (`<%= ... %>`)

**What it is:** Outputs the result of a Java expression (automatically converted to String).

### Expression Examples

```jsp
<%-- Basic expressions --%>
Current time: <%= new java.util.Date() %>
User name: <%= request.getParameter("name") %>
Sum: <%= 10 + 20 %>

<%-- With variables --%>
<% int x = 100; %>
Value: <%= x %>

<%-- With method calls --%>
<%= formatDate(new Date()) %>

<%-- With ternary operator --%>
<%= (age >= 18) ? "Adult" : "Minor" %>
```

### What Happens Internally

```jsp
<%= expression %>
```
**Becomes in servlet:**
```java
out.print(expression);
```

### Expression vs Scriptlet

| Expression (`<%= %>`) | Scriptlet (`<% %>`) |
|----------------------|---------------------|
| Outputs value | Executes code (no output) |
| No semicolon needed | Semicolon needed |
| Cannot contain multiple statements | Can contain multiple statements |
| `out.print()` automatically | Must use `out.print()` manually |

**Analogy:** Expression = **Speaking out loud** (produces output). Scriptlet = **Thinking** (does action, no output).

---

## 4. Scriptlet (`<% ... %>`)

**What it is:** Any Java code that executes when the page is requested.

### Basic Scriptlet Examples

```jsp
<%-- Simple variable declaration --%>
<%
    String name = "John";
    int age = 25;
%>

<%-- If-else logic --%>
<%
    String user = request.getParameter("user");
    if (user == null) {
        user = "Guest";
    }
%>

<%-- Loop example --%>
<ul>
<%
    for (int i = 1; i <= 5; i++) {
%>
    <li>Item <%= i %></li>
<%
    }
%>
</ul>
```

### Scriptlet with HTML Mixed

```jsp
<%-- Conditionally display HTML --%>
<%
    String role = (String) session.getAttribute("role");
    if ("admin".equals(role)) {
%>
    <a href="admin.jsp">Admin Panel</a>
    <a href="users.jsp">Manage Users</a>
<%
    } else {
%>
    <a href="profile.jsp">My Profile</a>
<%
    }
%>
```

### Scriptlet with Database

```jsp
<%@ page import="java.sql.*" %>
<%
    Connection con = null;
    try {
        Class.forName("com.mysql.cj.jdbc.Driver");
        con = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "root", "password");
        
        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM users");
        
        while (rs.next()) {
%>
            <p>Name: <%= rs.getString("name") %></p>
<%
        }
        rs.close();
        stmt.close();
    } catch(Exception e) {
        out.println("Error: " + e.getMessage());
    } finally {
        if(con != null) con.close();
    }
%>
```

**Analogy:** Scriptlet = **Instructions for the robot** (what to do step by step).

---

## 5. Comments

### Three Types of Comments

| Type | Syntax | Visible in HTML Source? | Purpose |
|------|--------|------------------------|---------|
| **JSP Comment** | `<%-- comment --%>` | ❌ No | Document JSP code |
| **HTML Comment** | `<!-- comment -->` | ✅ Yes | Visible to users |
| **Java Comment** | `//` or `/* */` | ❌ No | Inside scriptlets |

### JSP Comment (Not visible in browser)

```jsp
<%-- This is a JSP comment --%>
<%-- It will NOT appear in HTML source --%>
<%-- Use for developer notes, explaining JSP logic --%>

<%-- 
    Multi-line JSP comment
    Can span multiple lines
    Safe for documenting JSP syntax
--%>
```

### HTML Comment (Visible in browser)

```jsp
<!-- This is an HTML comment -->
<!-- User can see this in View Source -->
<!-- Use for client-side notes -->
```

### Java Comment (Inside Scriptlets)

```jsp
<%
    // Single line Java comment (inside scriptlet)
    
    /* Multi-line
       Java comment */
    
    /* This comment style is useful for
       temporarily commenting out code */
%>
```

### Comment Comparison Example

```jsp
<html>
<body>
    <%-- JSP comment - not visible to user --%>
    
    <!-- HTML comment - visible in page source -->
    
    <%
        // Java comment - only in server code
        String name = "John";
        /* This explains the logic */
    %>
    
    Name: <%= name %>
</body>
</html>
```

---

## Complete Example - All Elements Together
## Code : [[Simple Page Counter (Bhola sir ko code)]]

```jsp
<%@ page language="java" contentType="text/html" %>
<%@ page import="java.util.*" %>
<%-- This is a JSP comment - not visible in browser --%>

<%! 
    // Declaration: Class-level variable
    private int counter = 0;
    
    // Declaration: Class-level method
    public String greet(String name) {
        return "Hello, " + name;
    }
%>

<html>
<head>
    <title>JSP Syntax Demo</title>
</head>
<body>
    <!-- HTML comment - visible in source -->
    
    <h1>JSP Syntax Elements Demo</h1>
    
    <%-- Scriptlet: Java code that executes --%>
    <%
        // Java comment inside scriptlet
        String user = request.getParameter("user");
        if (user == null) {
            user = "Guest";
        }
        counter++;
    %>
    
    <%-- Expression: Outputs value --%>
    <p>User: <%= user %></p>
    <p>Visit count: <%= counter %></p>
    <p>Greeting: <%= greet(user) %></p>
    <p>Current time: <%= new Date() %></p>
    
    <%-- Scriptlet with loop --%>
    <ul>
    <%
        for (int i = 1; i <= 3; i++) {
    %>
        <li>Item <%= i %></li>
    <%
        }
    %>
    </ul>
    
</body>
</html>
```

---

## Quick Reference Card

| Element          | Syntax                     | When to Use               |
| ---------------- | -------------------------- | ------------------------- |
| **Directive**    | `<%@ page import="..." %>` | Page setup, imports       |
| **Declaration**  | `<%! int count = 0; %>`    | Shared variables, methods |
| **Expression**   | `<%= variable %>`          | Display values            |
| **Scriptlet**    | `<% if(x>0){ %>`           | Business logic            |
| **JSP Comment**  | `<%-- note --%>`           | Developer notes           |
| **HTML Comment** | `<!-- note -->`            | Client notes              |
| **Java Comment** | `// note`                  | Inside scriptlets         |

---

## The Golden Rule

> **Use Directives for page configuration, Declarations for shared methods/variables, Expressions for output, Scriptlets for Java logic, and Comments for documentation. Remember: Scriptlets execute, Expressions output, Declarations define.**

**Memory trick:**
```
D = Directive = "Direct the page"
D = Declaration = "Declare the variables"
E = Expression = "Express the value"
S = Scriptlet = "Script the logic"
C = Comment = "Comment the code"

"DDESC" = JSP Syntax Elements
```