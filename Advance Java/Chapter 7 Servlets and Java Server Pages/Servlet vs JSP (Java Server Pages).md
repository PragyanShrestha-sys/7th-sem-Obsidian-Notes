# Servlets vs JSP - Complete Comparison

---

## What is the Difference?

**Servlets** are Java classes that write HTML inside Java code.  
**JSP** are HTML pages that contain Java code inside them.

```
Servlet (Java with HTML inside)          JSP (HTML with Java inside)
┌─────────────────────────┐             ┌─────────────────────────┐
│ public class Hello {    │             │ <html>                   │
│   out.println("<html>");│             │   <body>                 │
│   out.println("<body>");│             │   <% String name="John"; %>
│   out.println("Hello"); │             │   Hello <%= name %>      │
│   out.println("</body>");│            │   </body>                │
│   out.println("</html>");│            │ </html>                  │
│ }                       │             │                          │
└─────────────────────────┘             └─────────────────────────┘
```

**Analogy:** 
- **Servlet** = Writing a letter by hand (you control every character)
- **JSP** = Using a template with fill-in-the-blanks (easier for formatting)

---

## Complete Difference Table

| Feature | Servlet | JSP |
|---------|---------|-----|
| **Definition** | Java class that generates HTML | HTML page with embedded Java |
| **Extension** | `.java` file | `.jsp` file |
| **Translation** | Compiled directly to .class | Translated to servlet first, then compiled |
| **Writing HTML** | Hard (must use out.println() for each line) | Easy (write HTML naturally) |
| **Writing Java** | Easy (write Java code naturally) | Messy (need special tags: `<% %>`) |
| **Role in MVC** | Controller (handles logic, request processing) | View (handles presentation, display) |
| **Best for** | Business logic, form processing, database operations | Displaying data, HTML layout, UI components |
| **Modifications** | Need recompilation and server restart | Auto-reload (can see changes without restart) |
| **Code readability** | Poor for HTML (lots of strings) | Good for HTML, poor for Java |
| **Separation of concerns** | Java and HTML mixed together | Still mixed but cleaner |
| **Tag libraries** | No (must write all HTML manually) | Yes (JSTL, custom tags) |
| **Expression Language (EL)** | No (${} syntax not available) | Yes (${} for easy data access) |
| **Learning curve** | Steeper (need Java + HTTP knowledge) | Easier (HTML developers can learn) |
| **Compilation time** | Compiles once | First request slower (translation + compile) |

---

## Code Comparison - Same Output

### Servlet Version (Hello World)
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        
        out.println("<!DOCTYPE html>");
        out.println("<html>");
        out.println("<head>");
        out.println("<title>Hello Servlet</title>");
        out.println("</head>");
        out.println("<body>");
        out.println("<h1>Hello from Servlet!</h1>");
        out.println("<p>Current time: " + new java.util.Date() + "</p>");
        out.println("</body>");
        out.println("</html>");
    }
}
```

### JSP Version (Same Output)
```jsp
<!DOCTYPE html>
<html>
<head>
    <title>Hello JSP</title>
</head>
<body>
    <h1>Hello from JSP!</h1>
    <p>Current time: <%= new java.util.Date() %></p>
</body>
</html>
```

**Notice:** JSP is much cleaner and easier to write for HTML!

---

## Code Comparison - Form Processing

### Servlet (Better for Logic)
```java
@WebServlet("/login")
public class LoginServlet extends HttpServlet {
    
    protected void doPost(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Java code is natural here
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        
        if ("admin".equals(username) && "123".equals(password)) {
            HttpSession session = req.getSession();
            session.setAttribute("user", username);
            resp.sendRedirect("welcome");
        } else {
            resp.sendRedirect("login.html?error=1");
        }
    }
}
```

### JSP (Messy for Logic)
```jsp
<%-- This is messy for complex logic --%>
<%
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    
    if ("admin".equals(username) && "123".equals(password)) {
        session.setAttribute("user", username);
        response.sendRedirect("welcome");
    } else {
        response.sendRedirect("login.html?error=1");
    }
%>
```

---

## When to Use Which

| Scenario | Use | Why |
|----------|-----|-----|
| **Processing form data** | Servlet | Clean Java code, easy parameter access |
| **Database operations** | Servlet | Business logic belongs here |
| **Displaying data** | JSP | Easy HTML formatting |
| **User interface** | JSP | HTML designers can work on it |
| **Redirect logic** | Servlet | Control flow is logic |
| **Login validation** | Servlet | Authentication is business logic |
| **Showing product list** | JSP | Presentation of data |
| **Sending email** | Servlet | Backend operation |
| **Dashboard page** | JSP | Display with some dynamic content |

---

## The MVC Pattern (How They Work Together)

```
┌─────────────────────────────────────────────────────────────┐
│                      MVC ARCHITECTURE                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   Browser                                                   │
│      │                                                      │
│      │ Request                                              │
│      ▼                                                      │
│   ┌─────────────────────────────────────────────────────┐  │
│   │              SERVLET (Controller)                    │  │
│   │                                                      │  │
│   │  - Receives request                                 │  │
│   │  - Processes parameters                             │  │
│   │  - Calls database                                   │  │
│   │  - Stores data in request/session                   │  │
│   │  - Forwards to JSP                                  │  │
│   └─────────────────────────┬───────────────────────────┘  │
│                             │                              │
│                             │ Forward                       │
│                             ▼                              │
│   ┌─────────────────────────────────────────────────────┐  │
│   │                 JSP (View)                          │  │
│   │                                                      │  │
│   │  - Displays data                                    │  │
│   │  - Formats HTML                                     │  │
│   │  - Uses Expression Language ${}                     │  │
│   │  - No complex logic                                 │  │
│   └─────────────────────────────────────────────────────┘  │
│      │                                                      │
│      │ Response (HTML)                                     │
│      ▼                                                      │
│   Browser                                                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Complete MVC Example

**Servlet (Controller)**
```java
@WebServlet("/products")
public class ProductController extends HttpServlet {
    
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Logic: Get data from database
        List<String> products = Arrays.asList("Laptop", "Mouse", "Keyboard");
        
        // Store data in request
        req.setAttribute("productList", products);
        
        // Forward to JSP for display
        req.getRequestDispatcher("/WEB-INF/products.jsp").forward(req, resp);
    }
}
```

**JSP (View)**
```jsp
<!-- products.jsp -->
<html>
<body>
    <h2>Product List</h2>
    <ul>
        <%-- Use JSTL or scriptlet to loop --%>
        <c:forEach items="${productList}" var="product">
            <li>${product}</li>
        </c:forEach>
    </ul>
</body>
</html>
```

---

## Lifecycle Comparison

| Phase | Servlet | JSP |
|-------|---------|-----|
| **Load** | Container loads servlet class | Container translates JSP to servlet |
| **Compile** | Compiles .java to .class | Compiles generated servlet |
| **Initialize** | `init()` method | `jspInit()` method |
| **Execute** | `service()` method | `_jspService()` method |
| **Destroy** | `destroy()` method | `jspDestroy()` method |

---

## JSP Translation Process

```
JSP File (hello.jsp)
        │
        ▼ (Container translates)
        │
Servlet Java File (hello_jsp.java)
        │
        ▼ (Container compiles)
        │
Servlet Class (hello_jsp.class)
        │
        ▼ (Container executes)
        │
HTML Response
```

---

## Key Takeaways

| Point | Explanation |
|-------|-------------|
| **Servlets = Java with HTML** | Good for logic, bad for HTML |
| **JSP = HTML with Java** | Good for display, bad for logic |
| **Together = MVC** | Servlet = Controller, JSP = View |
| **Never write HTML in Servlet** | Use JSP for display |
| **Never write complex logic in JSP** | Use Servlet for business logic |

---

## The Golden Rule

> **Servlets are for processing (Controller). JSP are for displaying (View). Use Servlets for Java logic, database, form handling. Use JSP for HTML, CSS, JavaScript, and displaying data. Never mix them - keep logic in Servlets, presentation in JSP.**

**Memory trick:**
```
Servlet = Logic (Controller)
JSP = Look (View)

Servlet does the thinking
JSP does the showing

Together they make dynamic web applications
```