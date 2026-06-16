## [[Web Containers]]

"Servlet handles the interaction between front end and backend"

web container is backend packaged
```
┌─────────────────────────────────────────────────────────────┐
│                    WEB CONTAINER                            │
│                   (BACKEND PACKAGED)                        │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Servlets (Java logic)                              │   │
│  │  JSPs (templates)                                   │   │
│  │  Session Management                                 │   │
│  │  Database Connections                               │   │
│  │  Security                                           │   │
│  │  Request/Response Handling                          │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  ALL BACKEND STUFF INSIDE ONE PACKAGE!                      │
└─────────────────────────────────────────────────────────────┘
```

---
## [[Servlet and lifecycle (get request ko example nicha )]]

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

## [[Types of Servlet]]
## [[Handling Request and Response code]]
---
## [[Servlet API]]

"A servlet is a part of servlet API and API as a whole is a system that uses servlets for request and response between the client and backend"

---
## [[Processing Fourms in Servlet (Post request in servlet ko example yeai lekhda huncha)]]

---
## [[Database access in servlets]]

![[Pasted image 20260608121448.png]]

---
## [[Cookie and Sessions]]

![[Pasted image 20260608123923.png]]
Note: "Cookie and sessions are limited under the Cookie and HttpSession class"

---
## [[Servlet vs JSP (Java Server Pages)]]
note: [[JSP file converts into Servlet pages and is processed]]
note: [[JSP and servlet work together not alternatives]]



> **Servlets are for processing (Controller). JSP are for displaying (View). Use Servlets for Java logic, database, form handling. Use JSP for HTML, CSS, JavaScript, and displaying data. Never mix them - keep logic in Servlets, presentation in JSP.**

**Memory trick:**
```
Servlet = Logic (Controller)
JSP = Look (View)

Servlet does the thinking
JSP does the showing

Together they make dynamic web applications
```



![[Pasted image 20260608125403.png|525]]
![[Pasted image 20260608125416.png|528]]

---
## [[What is JSP]]
---
## [[JSP Syntax]]
| Element          | Syntax                     | When to Use               |
| ---------------- | -------------------------- | ------------------------- |
| **Directive**    | `<%@ page import="..." %>` | Page setup, imports       |
| **Declaration**  | `<%! int count = 0; %>`    | Shared variables, methods |
| **Expression**   | `<%= variable %>`          | Display values            |
| **Scriptlet**    | `<% if(x>0){ %>`           | Business logic            |
| **JSP Comment**  | `<%-- note --%>`           | Developer notes           |
| **HTML Comment** | `<!-- note -->`            | Client notes              |
| **Java Comment** | `// note`                  | Inside scriptlets         |
note:  A JSP **directive** (like `<%@ page ... %>`, `<%@ include ... %>`, or `<%@ taglib ... %>`) is only evaluated and processed during the **translation phase** when the JSP container converts the `.jsp` file into a Java servlet (`.java`).

---
## [[JSP implicit objects]]
![[Pasted image 20260608133212.png]]

---
## [[Object Scope in JSP]]

![[Pasted image 20260608135303.png]]

---
## [[Processing Forms in JSP]]

![[Pasted image 20260608140109.png|489]]
![[Pasted image 20260608140122.png|502]]

---
## [[Database Access with JSP]]
Easy 5 step Process
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
## [[Introductino to java web frameworks]]
