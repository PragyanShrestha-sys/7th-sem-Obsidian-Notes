
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/app")
public class CompleteAppServlet extends HttpServlet {
    
    // Handle all GET requests (show appropriate page)
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        
        // Check if user is already logged in
        HttpSession session = req.getSession(false);
        
        if (session != null && session.getAttribute("user") != null) {
            // USER IS LOGGED IN - Show welcome page
            String user = (String) session.getAttribute("user");
            
            out.println("<html><body>");
            out.println("<h2>Welcome, " + user + "!</h2>");
            out.println("<a href='app?action=logout'>Logout</a>");
            out.println("</body></html>");
            
        } else {
            // USER NOT LOGGED IN - Show login form
            
            // Check for "action" parameter
            String action = req.getParameter("action");
            
            if ("logout".equals(action)) {
                out.println("<h3>You have been logged out!</h3>");
            }
            
            // Show login form
            out.println("<html><body>");
            out.println("<h3>Login</h3>");
            out.println("<form method='post'>");
            out.println("Username: <input name='username'>");
            out.println("<input type='submit' value='Login'>");
            out.println("</form>");
            out.println("</body></html>");
        }
    }
    
    // Handle POST request (login form submission)
    protected void doPost(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // Get username from form
        String username = req.getParameter("username");
        
        if (username != null && !username.trim().isEmpty()) {
            // Create session and store user
            HttpSession session = req.getSession();
            session.setAttribute("user", username);
        }
        
        // Go back to main page (which will show welcome screen)
        resp.sendRedirect("app");
    }
}
```
