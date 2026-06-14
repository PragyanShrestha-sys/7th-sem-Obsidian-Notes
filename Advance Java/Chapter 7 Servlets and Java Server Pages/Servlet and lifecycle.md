# Servlets - Complete Explanation

Here's a **complete explanation** of Servlets, what they are, why they're needed, and how they work.

---

## Part 1: What is a Servlet?

**A Servlet is a Java program that runs on a web server and handles client requests (usually from web browsers).**

```
Web Browser                    Web Server with Servlet
     │                                │
     │  HTTP Request (GET/POST)       │
     ├───────────────────────────────→│
     │                                │
     │                                ├── Servlet (Java Code)
     │                                │      │
     │                                │      ├── Process request
     │                                │      ├── Access database
     │                                │      ├── Generate HTML
     │                                │      │
     │  HTTP Response (HTML)          │      │
     │←───────────────────────────────┤      │
     │                                │      │
```

**Analogy:** Servlet is like a **cashier** at a store. Customer (browser) makes a request, cashier (servlet) processes it, and gives back a response.

---

## Part 2: Why are Servlets Needed?

| Problem               | Without Servlet  | With Servlet                           |
| --------------------- | ---------------- | -------------------------------------- |
| Serve dynamic content | Only static HTML | ✅ Dynamic HTML based on user/database  |
| Process form data     | Can't process    | ✅ Read form parameters                 |
| Handle user login     | No               | ✅ Validate credentials, create session |
| Access database       | No               | ✅ Connect to database, display data    |
| Track users           | No               | ✅ Session management                   |
|                       |                  |                                        |

**Without Servlets:** Web pages are static (same for everyone).
**With Servlets:** Web pages are dynamic (different for each user).

---

## Part 3: Servlet Lifecycle

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

---

## Part 4: Servlet Class Hierarchy

```
Object
    │
    └── Servlet (interface)
            │
            └── GenericServlet (abstract class)
                    │
                    └── HttpServlet (abstract class) ← Most common
                            │
                            └── Your Servlet (extends HttpServlet)
```

---

## Part 5: Simple Servlet Example

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class HelloServlet extends HttpServlet {
    
    // Called once when servlet is loaded
    @Override
    public void init() throws ServletException {
        System.out.println("Servlet initialized");
    }
    
    // Called for every GET request
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        
        // Set response content type
        response.setContentType("text/html");
        
        // Get parameter from URL (e.g., ?name=John)
  //      String name = request.getParameter("name");
  //      if (name == null) {
  //          name = "World";
  //      }
        
        // Generate HTML response
        PrintWriter out = response.getWriter();
        out.println("<html>");
        out.println("<body>");
        out.println("<h1>Hello, " + name + "!</h1>");
        out.println("</body>");
        out.println("</html>");
    }
    
    // Called for every POST request
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        
        // Usually call doGet or handle form submission
        doGet(request, response);
    }
    
    // Called once when servlet is unloaded
    @Override
    public void destroy() {
        System.out.println("Servlet destroyed");
    }
}
```

---

## Part 6: doGet() vs doPost()

| Method       | When used    | How data is sent | Use case                            |
| ------------ | ------------ | ---------------- | ----------------------------------- |
| **doGet()**  | GET request  | In URL (visible) | Search, view pages                  |
| **doPost()** | POST request | In body (hidden) | Login, form submission, file upload |

### URL with GET:
```
http://example.com/login?username=john&password=123
                              ↑ Data visible in URL
```

### POST (data not visible):
```
Browser ──→ Server
(Data in body, not visible in URL)
```

---

## Part 12: Servlet vs JSP vs HTML

| Aspect                   | HTML         | Servlet                 | JSP         |
| ------------------------ | ------------ | ----------------------- | ----------- |
| **Type**                 | Static       | Java class              | HTML + Java |
| **Dynamic content**      | ❌ No         | ✅ Yes                   | ✅ Yes       |
| **Ease of writing HTML** | Easy         | Hard (print statements) | Easy        |
| **Ease of writing Java** | N/A          | Easy                    | Mixed       |
| **Use for**              | Static pages | Logic/Processing        | Display     |

---

## Part 14: Servlet Best Practices

| Practice                              | Why                      |
| ------------------------------------- | ------------------------ |
| **Use doPost() for form submissions** | Data not visible in URL  |
| **Never trust user input**            | Validate all parameters  |
| **Use PreparedStatement**             | Prevent SQL injection    |
| **Close database connections**        | Avoid resource leaks     |
| **Use session for user state**        | Track logged-in users    |
| **Separate logic from display**       | Use JSP for presentation |

---

## The Golden Rule

> **A servlet is a Java class that handles HTTP requests, processes data, and generates dynamic responses. It runs in a web container, has a lifecycle (init, service, destroy), and is the backbone of Java web applications.**

**Memory trick:**
```
Servlet = Server + Applet
Server-side Java program that handles web requests

Servlet Lifecycle: Load → Create → init() → service() → destroy()

GET = Read data (visible in URL)
POST = Send data (hidden in body)

Servlet + JSP = Dynamic web application
```