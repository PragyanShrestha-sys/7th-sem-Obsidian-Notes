```java 
import javax.swing.*;
import java.awt.event.*;

public class MoveIcon {
    public static void main(String[] args) {
        // Create the main window (JFrame)
        JFrame frame = new JFrame();
        
        // Create a label that will hold our icon/image
        JLabel icon = new JLabel(new ImageIcon("icon.png"));
        
        // Variable to track the vertical position (Y coordinate)
        int y = 200;
        
        // Set layout to null so we can manually position the icon
        frame.setLayout(null);
        
        // Set initial position and size of icon (x, y, width, height)
        icon.setBounds(175, y, 50, 50);
        
        // Add mouse click listener to the icon
        icon.addMouseListener(new MouseAdapter() {
            public void mouseClicked(MouseEvent e) {
                System.out.println("Clicked");  // Print when user clicks the icon
            }
        });
        
        // Add keyboard listener to the frame
        frame.addKeyListener(new KeyAdapter() {
            public void keyPressed(KeyEvent e) {
                // Check if the pressed key is the UP arrow
                if (e.getKeyCode() == KeyEvent.VK_UP) {
                    y -= 10;                    // Decrease Y coordinate (move up)
                    icon.setLocation(175, y);   // Update icon position
                }
            }
        });
        
        // Add the icon label to the frame
        frame.add(icon);
        
        // Set window size to 400x400 pixels
        frame.setSize(400, 400);
        
        // Make frame focusable so it can receive keyboard events
        frame.setFocusable(true);
        
        // Make the window visible on screen
        frame.setVisible(true);
    }
}
```

