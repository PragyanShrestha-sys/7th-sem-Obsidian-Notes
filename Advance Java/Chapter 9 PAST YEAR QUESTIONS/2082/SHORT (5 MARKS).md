## Q1.  Write a program to insert an icon in the frame and when the user presses the up arrow, it will move upward. (Swing and Event handling)

```JAVA
import javax.swing.*;
import java.awt.event.*;

public class MoveIcon {
    public static void main(String[] args) {
        JFrame frame = new JFrame();
        JLabel icon = new JLabel(new ImageIcon("icon.png"));
        int y = 200;
        
        frame.setLayout(null);
        icon.setBounds(175, y, 50, 50);
        
        icon.addMouseListener(new MouseAdapter() {
            public void mouseClicked(MouseEvent e) {
                System.out.println("Clicked");
            }
        });
        
        frame.addKeyListener(new KeyAdapter() {
            public void keyPressed(KeyEvent e) {
                if (e.getKeyCode() == KeyEvent.VK_UP) {
                    y -= 10;
                    icon.setLocation(175, y);
                }
            }
        });
        
        frame.add(icon);
        frame.setSize(400, 400);
        frame.setFocusable(true);
        frame.setVisible(true);
    }
}
```
[[2082 q1 explanation]]

---

## How do you handle HTTP req and res in JSP with exmaple

[[Servlet vs JSP (Java Server Pages)]]

### JSP (request and response )
```jsp
<%-- This is messy for complex logic --%>
<%
<%@ page contentType="text/html" %>
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <form method="post">
        Name: <input name="username"><br>
        Pass: <input name="password" type="password"><br>
        <input type="submit" value="Login">
    </form>

    <%-- Login logic --%>
    <%
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        
        if (username != null && password != null) {
            if ("admin".equals(username) && "123".equals(password)) {
                session.setAttribute("user", username);
                response.sendRedirect("welcome.jsp");
            } else {
                out.print("<p style='color:red'>Invalid!</p>");
            }
        }
    %>
</body>
</html>
%>
```
