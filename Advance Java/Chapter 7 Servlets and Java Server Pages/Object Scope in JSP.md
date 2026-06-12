# JSP Object Scope - Complete Explanation

Here's a **complete explanation** of Object Scope in JSP.

---

## What is Object Scope?

**Object scope** defines how long an object lives and who can access it.

```
┌─────────────────────────────────────────────────────────────┐
│                     SCOPES (smallest to largest)            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   PAGE SCOPE     → Lives only in current JSP               │
│        ↓                                                   │
│   REQUEST SCOPE  → Lives for one HTTP request              │
│        ↓                                                   │
│   SESSION SCOPE  → Lives for one user's entire visit       │
│        ↓                                                   │
│   APPLICATION SCOPE → Lives for entire application         │
│                         (all users share)                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Analogy:** Like different types of storage:
- **Page** = Post-it note (throw away after reading)
- **Request** = Envelope (discard after delivering)
- **Session** = Locker (keep for your visit)
- **Application** = Bulletin board (everyone sees)

---

## The 4 Scopes Comparison Table

| Scope | Lifetime | Who can access | When destroyed | Methods |
|-------|----------|----------------|----------------|---------|
| **Page** | Current JSP only | Current page only | After page finishes rendering | `pageContext.setAttribute()` |
| **Request** | One HTTP request | Forwarded/included pages | After response sent | `request.setAttribute()` |
| **Session** | User's entire visit | All pages user visits | Session timeout or logout | `session.setAttribute()` |
| **Application** | Server lifetime | ALL users, ALL pages | Server shutdown | `application.setAttribute()` |

---

## 1. Page Scope (Smallest)

### What it is:
Data exists ONLY on the current JSP page. Lost when page finishes.

### How to use:
```jsp
<%
    // Store data in page scope
    pageContext.setAttribute("tempData", "Only this page sees me");
    pageContext.setAttribute("counter", 100);
%>

<p>Value: <%= pageContext.getAttribute("tempData") %></p>

<%-- Forward to another page --%>
<jsp:forward page="next.jsp" />
```

### What happens in next.jsp:
```jsp
<%
    // This will be NULL! Page scope data is gone.
    String data = (String) pageContext.getAttribute("tempData");
%>
<p>Data from previous page: <%= data %>  <%-- null --%></p>
```

### When to use:
- Temporary variables
- Loop counters
- Data needed only on current page

---

## 2. Request Scope

### What it is:
Data lives for ONE HTTP request. Survives forwards (but not redirects).

### How to use:
```jsp
<%-- Page1.jsp --%>
<%
    // Store data in request scope
    request.setAttribute("userName", "John");
    request.setAttribute("age", 25);
%>

<%-- Forward to another page (data survives) --%>
<jsp:forward page="Page2.jsp" />
```

```jsp
<%-- Page2.jsp (receives the data) --%>
<%
    String name = (String) request.getAttribute("userName");
    Integer age = (Integer) request.getAttribute("age");
%>
<p>Name: <%= name %></p>   <%-- John --%>
<p>Age: <%= age %></p>     <%-- 25 --%>
```

### Forward vs Redirect (Important!)

```jsp
<%-- FORWARD - request scope data SURVIVES --%>
<jsp:forward page="next.jsp" %>
<%-- OR --%>
<%
    request.getRequestDispatcher("next.jsp").forward(request, response);
%>

<%-- REDIRECT - request scope data is LOST --%>
<%
    response.sendRedirect("next.jsp");
%>
```

### When to use:
- Passing data between servlet and JSP
- Form validation errors to be displayed
- Search results to display page

---

## 3. Session Scope

### What it is:
Data lives for entire user session (across multiple requests/pages).

### How to use:
```jsp
<%-- login.jsp --%>
<%
    String username = request.getParameter("username");
    
    // Store in session (remember for entire visit)
    session.setAttribute("loggedInUser", username);
    session.setAttribute("cart", new ArrayList());
%>
```

```jsp
<%-- anyPage.jsp (any page user visits) --%>
<%
    String user = (String) session.getAttribute("loggedInUser");
    if (user != null) {
%>
    <p>Welcome back, <%= user %>!</p>
<%
    }
%>
```

### Session Methods:
```jsp
<%
    // Store
    session.setAttribute("key", value);
    
    // Retrieve
    Object value = session.getAttribute("key");
    
    // Remove
    session.removeAttribute("key");
    
    // Get all attribute names
    java.util.Enumeration names = session.getAttributeNames();
    
    // Session info
    String id = session.getId();
    boolean isNew = session.isNew();
    long created = session.getCreationTime();
    long lastAccess = session.getLastAccessedTime();
    
    // Set timeout (30 minutes)
    session.setMaxInactiveInterval(30 * 60);
    
    // Destroy session (logout)
    session.invalidate();
%>
```

### Complete Login Example:
```jsp
<%-- login.jsp --%>
<%
    String user = request.getParameter("user");
    String pass = request.getParameter("pass");
    
    if ("admin".equals(user) && "123".equals(pass)) {
        session.setAttribute("user", user);
        session.setAttribute("loginTime", new java.util.Date());
        response.sendRedirect("dashboard.jsp");
    } else {
        out.println("Invalid login!");
    }
%>

<%-- dashboard.jsp --%>
<%
    String user = (String) session.getAttribute("user");
    if (user == null) {
        response.sendRedirect("login.html");
        return;
    }
%>
<h2>Welcome, <%= user %>!</h2>

<%-- logout.jsp --%>
<%
    session.invalidate();
    response.sendRedirect("login.html");
%>
```

### When to use:
- User login status
- Shopping cart
- User preferences
- Any data needed across multiple pages

---

## 4. Application Scope (Largest)

### What it is:
Data lives for entire application lifetime. SHARED by ALL users.

### How to use:
```jsp
<%
    // Store application-wide data
    application.setAttribute("totalVisitors", 1000);
    application.setAttribute("appName", "My Web App");
    application.setAttribute("adminEmail", "admin@example.com");
%>
```

### Real Example: Visitor Counter
```jsp
<%-- Any page in the application --%>
<%
    Integer count = (Integer) application.getAttribute("visitCount");
    if (count == null) {
        count = 0;
    }
    count++;
    application.setAttribute("visitCount", count);
%>
<p>Total visitors (all users): <%= count %></p>
```

### Another Example: Online Users Count
```jsp
<%-- When user logs in --%>
<%
    Integer online = (Integer) application.getAttribute("onlineUsers");
    if (online == null) online = 0;
    online++;
    application.setAttribute("onlineUsers", online);
%>

<%-- When user logs out --%>
<%
    Integer online = (Integer) application.getAttribute("onlineUsers");
    if (online != null && online > 0) {
        online--;
        application.setAttribute("onlineUsers", online);
    }
%>
```

### Application Initialization Parameters
```xml
<!-- web.xml -->
<context-param>
    <param-name>adminEmail</param-name>
    <param-value>admin@myapp.com</param-value>
</context-param>
<context-param>
    <param-name>appVersion</param-name>
    <param-value>2.0</param-value>
</context-param>
```

```jsp
<%
    String adminEmail = application.getInitParameter("adminEmail");
    String version = application.getInitParameter("appVersion");
%>
<p>Contact: <%= adminEmail %></p>
<p>Version: <%= version %></p>
```

### When to use:
- Visitor counters
- Application configuration
- Global settings
- Shared resources (caches, connection pools)

---

## Complete Example - All 4 Scopes

```jsp
<%@ page import="java.util.*" %>
<html>
<body>

<%
    // 1. PAGE SCOPE - only this page
    pageContext.setAttribute("pageData", "Only page1 sees this");
    
    // 2. REQUEST SCOPE - survives forward
    request.setAttribute("requestData", "Survives forward");
    
    // 3. SESSION SCOPE - user specific
    session.setAttribute("sessionData", "User specific data");
    
    // 4. APPLICATION SCOPE - all users
    application.setAttribute("appData", "All users see this");
%>

<h3>Current page (page1.jsp)</h3>
<p>Page scope: <%= pageContext.getAttribute("pageData") %></p>
<p>Request scope: <%= request.getAttribute("requestData") %></p>
<p>Session scope: <%= session.getAttribute("sessionData") %></p>
<p>Application scope: <%= application.getAttribute("appData") %></p>

<%-- Forward to another page to see what survives --%>
<jsp:forward page="page2.jsp" />

</body>
</html>
```

```jsp
<%-- page2.jsp --%>
<html>
<body>
<h3>Forwarded page (page2.jsp)</h3>

<%
    // Try to access data set in page1.jsp
    String pageData = (String) pageContext.getAttribute("pageData");
    String requestData = (String) request.getAttribute("requestData");
    String sessionData = (String) session.getAttribute("sessionData");
    String appData = (String) application.getAttribute("appData");
%>

<p>Page scope (from page1): <%= pageData %> - <%-- NULL! Lost --%></p>
<p>Request scope (from page1): <%= requestData %> - <%-- WORKS! --%></p>
<p>Session scope (from page1): <%= sessionData %> - <%-- WORKS! --%></p>
<p>Application scope (from page1): <%= appData %> - <%-- WORKS! --%></p>

</body>
</html>
```

---

## Scope Hierarchy - Finding Attributes

```jsp
<%
    // Sets data in different scopes with SAME key
    pageContext.setAttribute("key", "PAGE VALUE");
    request.setAttribute("key", "REQUEST VALUE");
    session.setAttribute("key", "SESSION VALUE");
    application.setAttribute("key", "APPLICATION VALUE");
    
    // findAttribute searches in order: Page → Request → Session → Application
    Object found = pageContext.findAttribute("key");
    // Returns "PAGE VALUE" (first found)
%>

<p>Found: <%= found %></p>

<%
    // To get specific scope
    String pageVal = (String) pageContext.getAttribute("key", PageContext.PAGE_SCOPE);
    String reqVal = (String) pageContext.getAttribute("key", PageContext.REQUEST_SCOPE);
    String sessVal = (String) pageContext.getAttribute("key", PageContext.SESSION_SCOPE);
    String appVal = (String) pageContext.getAttribute("key", PageContext.APPLICATION_SCOPE);
%>
```

---

## Quick Reference Table

| Scope | Set Method | Get Method | Lifetime |
|-------|-----------|-----------|----------|
| Page | `pageContext.setAttribute("k", v)` | `pageContext.getAttribute("k")` | Current page |
| Request | `request.setAttribute("k", v)` | `request.getAttribute("k")` | One request |
| Session | `session.setAttribute("k", v)` | `session.getAttribute("k")` | User session |
| Application | `application.setAttribute("k", v)` | `application.getAttribute("k")` | Server lifetime |

---

## When to Use Which Scope

| What you need | Scope to use |
|---------------|--------------|
| Loop counter, temporary variable | **Page** |
| Data from one page to next (forward) | **Request** |
| User login status | **Session** |
| Shopping cart | **Session** |
| User preferences | **Session** |
| Global visitor count | **Application** |
| Application configuration | **Application** |
| Form validation errors | **Request** |
| Search results | **Request** |

---

## The Golden Rule

> **Page scope = only this page. Request scope = one request (survives forward). Session scope = one user (survives multiple pages). Application scope = all users (entire application). Choose the smallest scope that works - don't use session if request is enough!**

**Memory trick:**
```
P - Page = "Private to this page"
R - Request = "Round trip only"
S - Session = "Stays with user"
A - Application = "All users share"

"PRSA" - Page, Request, Session, Application (from smallest to largest)
```