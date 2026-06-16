## Part 5: Simple Servlet Example GET REQ

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
    // Called once when servlet is unloaded
    @Override
    public void destroy() {
        System.out.println("Servlet destroyed");
    }
}
```

---
## Step 2: Servlet POST REQUST

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet("/login")  // URL that matches form action
public class LoginServlet extends HttpServlet {
    
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        
        // 1. READ form data
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        
        // 2. PROCESS data (validate)
        resp.setContentType("text/html");
        PrintWriter out = resp.getWriter();
        
        if ("admin".equals(username) && "123".equals(password)) {
            // Success - show welcome page
            out.println("<html><body>");
            out.println("<h1>Welcome " + username + "!</h1>");
            out.println("</body></html>");
        } else {
            // Failure - show error
            out.println("<html><body>");
            out.println("<h3>Invalid username or password!</h3>");
            out.println("<a href='login.html'>Try again</a>");
            out.println("</body></html>");
        }
    }
}
```

main part yo matra ho 

        String username = req.getParameter("username");
        String password = req.getParameter("password");
getting the parameters from the fourm 

---
