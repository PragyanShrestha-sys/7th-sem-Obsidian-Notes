# Handling Cookies and Sessions in Servlets - Simple Examples with Comments

---

## Part 1: Cookies (with Comments)

### Set Cookie - Send cookie to browser

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/setCookie")  // URL pattern: /setCookie
public class SetCookieServlet extends HttpServlet {
    
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Step 1: Create a cookie object (name, value)
        // This cookie will store username="john"
        Cookie cookie = new Cookie("username", "john");
        
        // Step 2: Set how long cookie should live (60 seconds * 60 minutes = 1 hour)
        // After 1 hour, browser will delete this cookie automatically
        cookie.setMaxAge(60 * 60);
        
        // Step 3: Add cookie to response
        // This sends the cookie to browser for storage
        resp.addCookie(cookie);
        
        // Step 4: Send confirmation to user
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        out.println("<h3>Cookie has been set on your browser!</h3>");
        out.println("<a href='getCookie'>Click here to read the cookie</a>");
    }
}
```

### Get Cookie - Read cookie from browser

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/getCookie")  // URL pattern: /getCookie
public class GetCookieServlet extends HttpServlet {
    
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Step 1: Get all cookies sent by browser
        // Browser automatically sends all cookies for this website
        Cookie[] cookies = req.getCookies();
        
        // Step 2: Variable to store the value we're looking for
        String username = null;
        
        // Step 3: Loop through all cookies to find our cookie
        if (cookies != null) {
            for (Cookie c : cookies) {
                // Check if cookie name is "username"
                if (c.getName().equals("username")) {
                    // Get the value stored in this cookie
                    username = c.getValue();
                    break;  // Found it, stop searching
                }
            }
        }
        
        // Step 4: Display the result
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        
        if (username != null) {
            out.println("<h3>Cookie found!</h3>");
            out.println("Username stored in cookie: " + username);
        } else {
            out.println("<h3>No cookie found!</h3>");
            out.println("Please set cookie first using /setCookie");
        }
        
        out.println("<br><a href='setCookie'>Set Cookie</a> | ");
        out.println("<a href='deleteCookie'>Delete Cookie</a>");
    }
}
```

## Part 2: Sessions (with Comments)

### Login Servlet - Create Session

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/login")  // URL pattern: /login
public class LoginServlet extends HttpServlet {
    
    // Handle form submission (POST request)
    protected void doPost(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Step 1: Get username from HTML form
        // HTML form has input field with name="username"
        String username = req.getParameter("username");
        
        // Step 2: Get or create a session for this user
        // true = create new session if one doesn't exist
        HttpSession session = req.getSession(true);
        
        // Step 3: Store user data in session
        // This data will be available across ALL pages
        session.setAttribute("user", username);
        
        // Step 4: Set session timeout (optional)
        // User will be logged out after 30 minutes of inactivity
        session.setMaxInactiveInterval(30 * 60);  // 30 minutes in seconds
        
        // Step 5: Redirect user to welcome page
        resp.sendRedirect("welcome");
    }
    
    // Handle direct access to /login (GET request)
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Show login form if user types /login directly
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        out.println("<html><body>");
        out.println("<h3>Login Form</h3>");
        out.println("<form method='post'>");
        out.println("Username: <input name='username'>");
        out.println("<input type='submit' value='Login'>");
        out.println("</form>");
        out.println("</body></html>");
    }
}
```

### Welcome Servlet - Read Session Data

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/welcome")  // URL pattern: /welcome
public class WelcomeServlet extends HttpServlet {
    
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Step 1: Get existing session (do NOT create new one)
        // false = don't create session if it doesn't exist
        HttpSession session = req.getSession(false);
        
        // Step 2: Prepare to send HTML response
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        
        // Step 3: Check if user is logged in
        if (session != null) {
            // Get user data from session
            String username = (String) session.getAttribute("user");
            
            if (username != null) {
                // USER IS LOGGED IN
                out.println("<html><body>");
                out.println("<h2>Welcome, " + username + "!</h2>");
                out.println("<p>You are logged in!</p>");
                out.println("<p>Session ID: " + session.getId() + "</p>");
                out.println("<a href='logout'>Click here to logout</a>");
                out.println("</body></html>");
            } else {
                // SESSION EXISTS BUT NO USER DATA (shouldn't happen normally)
                out.println("<h3>Please login first!</h3>");
                out.println("<a href='login'>Go to Login</a>");
            }
        } else {
            // NO SESSION FOUND - USER NOT LOGGED IN
            out.println("<h3>Please login first!</h3>");
            out.println("<a href='login'>Go to Login</a>");
        }
    }
}
```



---
## Quick Reference

| Operation | Code |
|-----------|------|
| **Create cookie** | `Cookie c = new Cookie("name","value"); resp.addCookie(c);` |
| **Read cookie** | `Cookie[] cookies = req.getCookies();` |
| **Delete cookie** | `c.setMaxAge(0); resp.addCookie(c);` |
| **Create session** | `HttpSession s = req.getSession();` |
| **Store in session** | `s.setAttribute("key", value);` |
| **Read from session** | `Object value = s.getAttribute("key");` |
| **Delete session** | `s.invalidate();` |

---

## The Golden Rule

> **Cookies: Create → addCookie → Browser stores → getCookies → Loop to find. Sessions: getSession → setAttribute → Later getAttribute → invalidate to destroy.**

**Memory trick:**
```
Cookie: new → addCookie → getCookies → loop
Session: getSession → setAttribute → getAttribute → invalidate
```


[[Complete Mini Application (All in One sessions and cookies)]]
