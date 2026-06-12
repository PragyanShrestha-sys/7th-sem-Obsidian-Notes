# Handling Cookies and Sessions in Servlets - Complete Guide

Here's a **complete explanation** of handling cookies and sessions in servlets.

[[smaller code explanation]]

---

## Part 1: What are Cookies?

**Cookies** are small text files stored on the user's computer by the browser. They persist between browser sessions.

```
Browser (User's Computer)              Server
        │                                  │
        │  1. First request                │
        ├─────────────────────────────────→│
        │                                  │
        │  2. Response + Set-Cookie        │
        │←─────────────────────────────────┤
        │                                  │
        │  3. Next request + Cookie        │
        ├─────────────────────────────────→│
        │                                  │
```

**Analogy:** Cookies are like a **library card** - the server gives it to you, you keep it, and show it on each visit.

---

## Part 2: What are Sessions?

**Sessions** store user data on the server side, identified by a unique session ID (usually stored in a cookie).

```
┌─────────────────────────────────────────────────────────────┐
│                      WEB SERVER                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                    SESSIONS                          │   │
│  │                                                      │   │
│  │  Session ID: ABC123 → {user: "john", cart: [...]}   │   │
│  │  Session ID: XYZ789 → {user: "jane", cart: [...]}   │   │
│  │  Session ID: DEF456 → {user: "bob", cart: [...]}    │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

**Analogy:** Sessions are like a **locker at a gym** - you get a key (session ID), the server keeps your stuff in the locker.

---

## Part 3: Cookies vs Sessions

| Aspect | Cookie | Session |
|--------|--------|---------|
| **Storage location** | Browser (client side) | Server side |
| **Data size limit** | ~4KB | Much larger |
| **Security** | Less secure (user can see) | More secure |
| **Persistence** | Can be permanent | Usually temporary |
| **Best for** | Preferences, tracking | Login status, shopping cart |

---

## Part 4: Working with Cookies

### Creating and Sending Cookies

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/setCookie")
public class SetCookieServlet extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Create a cookie
        Cookie cookie = new Cookie("username", "john_doe");
        
        // Set cookie properties
        cookie.setMaxAge(60 * 60 * 24);  // 1 day in seconds
        cookie.setPath("/");              // Available for whole app
        cookie.setHttpOnly(true);         // Can't be accessed by JavaScript
        cookie.setSecure(true);           // Only sent over HTTPS
        
        // Add cookie to response
        resp.addCookie(cookie);
        
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        out.println("<html><body>");
        out.println("<h2>Cookie has been set!</h2>");
        out.println("<a href='getCookie'>Read Cookie</a>");
        out.println("</body></html>");
    }
}
```

### Reading Cookies

```java
@WebServlet("/getCookie")
public class GetCookieServlet extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        
        out.println("<html><body>");
        out.println("<h2>Reading Cookies</h2>");
        
        // Get all cookies from request
        Cookie[] cookies = req.getCookies();
        
        if (cookies != null) {
            for (Cookie cookie : cookies) {
                out.println("Cookie Name: " + cookie.getName() + "<br>");
                out.println("Cookie Value: " + cookie.getValue() + "<br>");
                out.println("Max Age: " + cookie.getMaxAge() + "<br>");
                out.println("Path: " + cookie.getPath() + "<br>");
                out.println("------------------------<br>");
            }
        } else {
            out.println("No cookies found!<br>");
        }
        
        out.println("<a href='setCookie'>Set Another Cookie</a><br>");
        out.println("<a href='deleteCookie'>Delete Cookie</a>");
        out.println("</body></html>");
    }
}
```

### Deleting Cookies

```java
@WebServlet("/deleteCookie")
public class DeleteCookieServlet extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Get the cookie to delete
        Cookie[] cookies = req.getCookies();
        
        if (cookies != null) {
            for (Cookie cookie : cookies) {
                if (cookie.getName().equals("username")) {
                    // Set max age to 0 to delete
                    cookie.setMaxAge(0);
                    resp.addCookie(cookie);
                    break;
                }
            }
        }
        
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        out.println("<html><body>");
        out.println("<h2>Cookie deleted!</h2>");
        out.println("<a href='getCookie'>Check Cookies Again</a>");
        out.println("</body></html>");
    }
}
```

---

## Part 5: Working with Sessions

### Creating and Using Sessions

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/login")
public class LoginServlet extends HttpServlet {
    
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        
        // Validate user (simplified)
        if ("admin".equals(username) && "123".equals(password)) {
            
            // Get or create session
            HttpSession session = req.getSession();
            
            // Store user data in session
            session.setAttribute("username", username);
            session.setAttribute("loginTime", new java.util.Date());
            
            // Set session timeout (30 minutes)
            session.setMaxInactiveInterval(30 * 60);
            
            // Redirect to welcome page
            resp.sendRedirect("welcome");
            
        } else {
            resp.sendRedirect("login.html?error=invalid");
        }
    }
}
```

### Reading Session Data

```java
@WebServlet("/welcome")
public class WelcomeServlet extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Get session (don't create new one)
        HttpSession session = req.getSession(false);
        
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        
        out.println("<html><body>");
        
        if (session != null) {
            String username = (String) session.getAttribute("username");
            java.util.Date loginTime = (java.util.Date) session.getAttribute("loginTime");
            
            if (username != null) {
                out.println("<h2>Welcome, " + username + "!</h2>");
                out.println("Logged in at: " + loginTime + "<br>");
                out.println("Session ID: " + session.getId() + "<br>");
                out.println("Session is new: " + session.isNew() + "<br>");
                out.println("<a href='profile'>View Profile</a><br>");
                out.println("<a href='logout'>Logout</a>");
            } else {
                out.println("<h2>Please log in first!</h2>");
                out.println("<a href='login.html'>Login</a>");
            }
        } else {
            out.println("<h2>No session found! Please login.</h2>");
            out.println("<a href='login.html'>Login</a>");
        }
        
        out.println("</body></html>");
    }
}
```


## Part 8: Session Attributes (Common Uses)

| Attribute Type | Example | Best for |
|----------------|---------|----------|
| **User info** | `session.setAttribute("user", userObject)` | Login status |
| **Shopping cart** | `session.setAttribute("cart", cartItems)` | E-commerce |
| **Preferences** | `session.setAttribute("theme", "dark")` | User settings |
| **Temp data** | `session.setAttribute("message", "Saved")` | One-time messages |

---


## Quick Reference

### Cookie Methods

| Method | Purpose |
|--------|---------|
| `new Cookie(name, value)` | Create cookie |
| `cookie.setMaxAge(seconds)` | Set lifetime (0 = delete) |
| `cookie.setPath("/")` | Set URL scope |
| `resp.addCookie(cookie)` | Send to browser |
| `req.getCookies()` | Get all cookies |

### Session Methods

| Method | Purpose |
|--------|---------|
| `req.getSession()` | Get or create session |
| `req.getSession(false)` | Get session (don't create) |
| `session.setAttribute(name, value)` | Store data |
| `session.getAttribute(name)` | Get data |
| `session.removeAttribute(name)` | Remove data |
| `session.invalidate()` | Destroy session |
| `session.setMaxInactiveInterval(sec)` | Set timeout |

---

## The Golden Rule

> **Use sessions for server-side data storage (login, cart). Use cookies for client-side preferences (theme, language). Sessions are more secure but temporary. Cookies persist but have size limits. Always call `req.getSession(false)` before assuming a session exists.**

**Memory trick:**
```
Cookies = Client storage (small, persistent)
Sessions = Server storage (large, temporary)

Cookie = "I remember your preference"
Session = "I remember YOU"

setAttribute() = Store in session
getAttribute() = Read from session
invalidate() = End session
```