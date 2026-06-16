```java
// Basic label
JFrame frame = new JFrame();  // Fixed: JFrame not Jframe
JLabel label = new JLabel("Enter your name:");

// Label with icon
JLabel imageLabel = new JLabel(new ImageIcon("icon.png"));  // Removed extra quote

// Solution 1: Use FlowLayout
frame.setLayout(new FlowLayout());
frame.add(label);
frame.add(imageLabel);

// Solution 2: Specify BorderLayout positions
frame.add(label, BorderLayout.NORTH);
frame.add(imageLabel, BorderLayout.CENTER);

// Don't forget these:
frame.setSize(300, 200);
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setVisible(true);
```
