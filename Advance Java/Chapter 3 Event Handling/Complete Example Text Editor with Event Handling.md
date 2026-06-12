```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.io.*;

public class EventHandlingDemo extends JFrame {
    
    private JTextArea textArea;
    private JLabel statusLabel;
    
    public EventHandlingDemo() {
        setTitle("Text Editor - Event Handling Demo");
        setSize(600, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        // Create text area
        textArea = new JTextArea();
        add(new JScrollPane(textArea), BorderLayout.CENTER);
        
        // Status bar
        statusLabel = new JLabel("Ready");
        add(statusLabel, BorderLayout.SOUTH);
        
        // Create menu bar
        JMenuBar menuBar = new JMenuBar();
        JMenu fileMenu = new JMenu("File");
        
        // Menu items with action commands
        JMenuItem newItem = new JMenuItem("New");
        newItem.setActionCommand("NEW");
        newItem.addActionListener(menuListener);
        fileMenu.add(newItem);
        
        JMenuItem openItem = new JMenuItem("Open");
        openItem.setActionCommand("OPEN");
        openItem.addActionListener(menuListener);
        fileMenu.add(openItem);
        
        JMenuItem saveItem = new JMenuItem("Save");
        saveItem.setActionCommand("SAVE");
        saveItem.addActionListener(menuListener);
        fileMenu.add(saveItem);
        
        fileMenu.addSeparator();
        
        JMenuItem exitItem = new JMenuItem("Exit");
        exitItem.setActionCommand("EXIT");
        exitItem.addActionListener(menuListener);
        fileMenu.add(exitItem);
        
        menuBar.add(fileMenu);
        setJMenuBar(menuBar);
        
        // Create buttons panel
        JPanel buttonPanel = new JPanel();
        
        JButton clearButton = new JButton("Clear");
        clearButton.setActionCommand("CLEAR");
        clearButton.addActionListener(buttonListener);
        buttonPanel.add(clearButton);
        
        JButton countButton = new JButton("Count");
        countButton.setActionCommand("COUNT");
        countButton.addActionListener(buttonListener);
        buttonPanel.add(countButton);
        
        add(buttonPanel, BorderLayout.NORTH);
        
        // Mouse listener (adapter) for right-click popup
        textArea.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseReleased(MouseEvent e) {
                if (e.isPopupTrigger()) {
                    showPopupMenu(e.getX(), e.getY());
                }
            }
        });
        
        // Key listener (adapter) for Ctrl+S shortcut
        textArea.addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                if (e.isControlDown() && e.getKeyCode() == KeyEvent.VK_S) {
                    saveToFile();
                }
            }
        });
        
        // Focus listener (adapter) for text area
        textArea.addFocusListener(new FocusAdapter() {
            @Override
            public void focusGained(FocusEvent e) {
                statusLabel.setText("Text area focused");
            }
            
            @Override
            public void focusLost(FocusEvent e) {
                statusLabel.setText("Text area lost focus");
            }
        });
        
        setVisible(true);
    }
    
    // Single listener for all menu items (using action commands)
    ActionListener menuListener = new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            String command = e.getActionCommand();
            
            switch (command) {
                case "NEW":
                    textArea.setText("");
                    statusLabel.setText("New file created");
                    break;
                case "OPEN":
                    openFile();
                    break;
                case "SAVE":
                    saveToFile();
                    break;
                case "EXIT":
                    System.exit(0);
                    break;
            }
        }
    };
    
    // Single listener for all buttons
    ActionListener buttonListener = new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            String command = e.getActionCommand();
            
            if (command.equals("CLEAR")) {
                textArea.setText("");
                statusLabel.setText("Text cleared");
            } else if (command.equals("COUNT")) {
                String text = textArea.getText();
                int chars = text.length();
                int words = text.trim().isEmpty() ? 0 : text.trim().split("\\s+").length;
                JOptionPane.showMessageDialog(null, 
                    "Words: " + words + "\nCharacters: " + chars,
                    "Count", JOptionPane.INFORMATION_MESSAGE);
            }
        }
    };
    
    private void showPopupMenu(int x, int y) {
        JPopupMenu popup = new JPopupMenu();
        
        JMenuItem cutItem = new JMenuItem("Cut");
        cutItem.addActionListener(e -> textArea.cut());
        popup.add(cutItem);
        
        JMenuItem copyItem = new JMenuItem("Copy");
        copyItem.addActionListener(e -> textArea.copy());
        popup.add(copyItem);
        
        JMenuItem pasteItem = new JMenuItem("Paste");
        pasteItem.addActionListener(e -> textArea.paste());
        popup.add(pasteItem);
        
        popup.show(textArea, x, y);
    }
    
    private void openFile() {
        JFileChooser chooser = new JFileChooser();
        if (chooser.showOpenDialog(this) == JFileChooser.APPROVE_OPTION) {
            try (BufferedReader reader = new BufferedReader(
                    new FileReader(chooser.getSelectedFile()))) {
                textArea.read(reader, null);
                statusLabel.setText("Opened: " + chooser.getSelectedFile().getName());
            } catch (IOException ex) {
                JOptionPane.showMessageDialog(this, "Error opening file");
            }
        }
    }
    
    private void saveToFile() {
        JFileChooser chooser = new JFileChooser();
        if (chooser.showSaveDialog(this) == JFileChooser.APPROVE_OPTION) {
            try (PrintWriter writer = new PrintWriter(chooser.getSelectedFile())) {
                writer.print(textArea.getText());
                statusLabel.setText("Saved: " + chooser.getSelectedFile().getName());
            } catch (IOException ex) {
                JOptionPane.showMessageDialog(this, "Error saving file");
            }
        }
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new EventHandlingDemo());
    }
}
```
