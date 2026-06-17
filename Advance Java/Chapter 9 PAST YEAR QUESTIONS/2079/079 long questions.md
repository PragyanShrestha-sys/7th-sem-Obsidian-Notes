![[Pasted image 20260617193259.png]]

## HTML Form + Processing JSP

### 1. HTML Form (`index.html`)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Full Name</title>
</head>
<body>
    <h2>Enter Your Name</h2>
    <form action="display.jsp" method="post">
        First Name: <input type="text" name="firstName"><br><br>
        Last Name: <input type="text" name="lastName"><br><br>
        <input type="submit" value="Submit">
    </form>
</body>
</html>
```

### 2. Processing JSP (`display.jsp`)

```jsp
<!DOCTYPE html>
<html>
<head>
    <title>Full Name</title>
</head>
<body>
    <h2>Your Full Name</h2>
    <%
        String f = request.getParameter("firstName");
        String l = request.getParameter("lastName");
        if (f != null && l != null) {
            out.println("<h3>Hello, " + f + " " + l + "!</h3>");
        } else {
            out.println("<h3>No data received!</h3>");
        }
    %>
    <a href="index.html">Go Back</a>
</body>
</html>
```

---
![[Pasted image 20260617193603.png]]
[[79 short question no 2 ans]]
