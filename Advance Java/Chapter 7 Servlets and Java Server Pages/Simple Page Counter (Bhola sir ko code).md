## JSP Syntax in Action: A Simple Page Counter

```
<%@ page import="java.util.Date" %> <%-- Directive: Import the Date class --%>

<html>

<head><title>JSP Syntax Example</title></head>

<body>

    <%! int pageVisits = 0; %> <%-- Declaration: A variable for the whole page --%>

    <%

        // Scriptlet: Java code to increment the counter

        pageVisits++;

        String message = "Welcome!";

    %>

    <h1><%= message %></h1> <%-- Expression: Print the message --%>

    <p>You are visitor number: <%= pageVisits %></p>

    <p>Page generated at: <%= new Date() %></p>

</body>

</html>
```