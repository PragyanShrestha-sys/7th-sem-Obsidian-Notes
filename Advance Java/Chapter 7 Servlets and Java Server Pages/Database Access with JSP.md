## [[Bhola Sir ko Notes(Database access with JSP)]]

# Database Access with JSP - Short Explanation

## What is Database Access in JSP?

**Database access** means reading data from or writing data to a database (like MySQL) directly from a JSP page.

```
JSP Page → Connect to Database → Execute SQL → Display Results
```

---

## Simple Example: Display Users from Database

### Complete JSP Code
```jsp
<%@ page import="java.sql.*" %>

<html>
<body>
    <h2>User List</h2>
    <table border="1">
        <tr><th>ID</th><th>Name</th><th>Email</th></tr>
        
        <%
            try {
                // 1. Load driver
                Class.forName("com.mysql.cj.jdbc.Driver");
                
                // 2. Connect to database
                Connection con = DriverManager.getConnection(
                    "jdbc:mysql://localhost:3306/mydb", "root", "password");
                
                // 3. Execute query
                Statement stmt = con.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT * FROM users");
                
                // 4. Display results
                while (rs.next()) {
        %>
                    <tr>
                        <td><%= rs.getInt("id") %></td>
                        <td><%= rs.getString("name") %></td>
                        <td><%= rs.getString("email") %></td>
                    </tr>
        <%
                }
                
                // 5. Close connections
                rs.close();
                stmt.close();
                con.close();
                
            } catch (Exception e) {
                out.println("Error: " + e.getMessage());
            }
        %>
    </table>
</body>
</html>
```

### What User Sees
```
User List

┌─────┬───────────┬──────────────────┐
│ ID  │ Name      │ Email            │
├─────┼───────────┼──────────────────┤
│ 1   │ Alice     │ alice@email.com  │
│ 2   │ Bob       │ bob@email.com    │
└─────┴───────────┴──────────────────┘
```

---

## Insert Data into Database

### HTML Form (addUser.html)
```html
<form action="insert.jsp" method="post">
    Name: <input name="name"><br>
    Email: <input name="email"><br>
    <input type="submit" value="Add User">
</form>
```

### JSP Processor (insert.jsp)
```jsp
<%@ page import="java.sql.*" %>

<%
    String name = request.getParameter("name");
    String email = request.getParameter("email");
    
    try {
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/mydb", "root", "password");
        
        PreparedStatement pstmt = con.prepareStatement(
            "INSERT INTO users (name, email) VALUES (?, ?)");
        pstmt.setString(1, name);
        pstmt.setString(2, email);
        
        pstmt.executeUpdate();
        
        pstmt.close();
        con.close();
        
        out.println("<h3>User added successfully!</h3>");
        
    } catch (Exception e) {
        out.println("Error: " + e.getMessage());
    }
%>

<a href="users.jsp">View All Users</a>
```

---

## Delete Data from Database

### JSP Page (delete.jsp)
```jsp
<%@ page import="java.sql.*" %>

<%
    int id = Integer.parseInt(request.getParameter("id"));
    
    try {
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/mydb", "root", "password");
        
        PreparedStatement pstmt = con.prepareStatement(
            "DELETE FROM users WHERE id = ?");
        pstmt.setInt(1, id);
        pstmt.executeUpdate();
        
        pstmt.close();
        con.close();
        
        response.sendRedirect("users.jsp");
        
    } catch (Exception e) {
        out.println("Error: " + e.getMessage());
    }
%>
```

### In users.jsp (add delete link)
```jsp
<a href="delete.jsp?id=<%= rs.getInt("id") %>">Delete</a>
```

---

## [[Complete CRUD Example (Single Page)]]

---

## The 5 Steps (Always the Same)

```jsp
<%
    // 1. Load driver
    Class.forName("com.mysql.cj.jdbc.Driver");
    
    // 2. Connect
    Connection con = DriverManager.getConnection(url, user, pass);
    
    // 3. Create statement
    PreparedStatement pstmt = con.prepareStatement("SQL with ?");
    pstmt.setString(1, value);
    
    // 4. Execute
    pstmt.executeUpdate();  // For INSERT/UPDATE/DELETE
    // OR
    ResultSet rs = pstmt.executeQuery();  // For SELECT
    
    // 5. Close
    pstmt.close();
    con.close();
%>
```

---

## The Golden Rule

> **To access database in JSP: (1) Add `import="java.sql.*"` in page directive, (2) Load driver, (3) Connect, (4) Execute SQL, (5) Close connections. Always use `PreparedStatement` to prevent SQL injection.**

**Memory trick:**
```
Import → Load → Connect → Query → Close

(Every time, same pattern!)
```