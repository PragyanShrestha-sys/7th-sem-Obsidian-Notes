
```jsp
<%@ page import="java.sql.*" %>

<html>
<body>

<h2>Add New User</h2>
<form method="post">
    Name: <input name="name"><br>
    Email: <input name="email"><br>
    <input type="submit" value="Add">
</form>

<%
    // INSERT new user
    String name = request.getParameter("name");
    String email = request.getParameter("email");
    
    if (name != null && email != null) {
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
            
        } catch (Exception e) {
            out.println("Error: " + e.getMessage());
        }
    }
%>

<h2>User List</h2>
<table border="1">
    <tr><th>ID</th><th>Name</th><th>Email</th><th>Delete</th></tr>
    
<%
    try {
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/mydb", "root", "password");
        
        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM users");
        
        while (rs.next()) {
%>
            <tr>
                <td><%= rs.getInt("id") %></td>
                <td><%= rs.getString("name") %></td>
                <td><%= rs.getString("email") %></td>
                <td><a href="?delete=<%= rs.getInt("id") %>">Delete</a></td>
            </tr>
<%
        }
        
        rs.close();
        stmt.close();
        con.close();
        
    } catch (Exception e) {
        out.println("Error: " + e.getMessage());
    }
%>

</table>

<%
    // DELETE user
    String deleteId = request.getParameter("delete");
    if (deleteId != null) {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");
            
            PreparedStatement pstmt = con.prepareStatement(
                "DELETE FROM users WHERE id = ?");
            pstmt.setInt(1, Integer.parseInt(deleteId));
            pstmt.executeUpdate();
            
            pstmt.close();
            con.close();
            
            response.sendRedirect("crud.jsp");
            
        } catch (Exception e) {
            out.println("Error: " + e.getMessage());
        }
    }
%>

</body>
</html>
```
